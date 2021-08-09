# Video-Speed-Controller
效果：https://xl-z4869.github.io/Video-Speed-Controller/index.html
通过滑块控制视频播放的速度
### 一、知识点
#### 1.video.playbackRate
控制视频播放的速度
https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLMediaElement/playbackRate
#### 2.各种宽高
##### ①事件对象event
* clientX/clientY  获取鼠标基于浏览器窗口（可视区域的坐标位置）
* pageX/pageY 获取鼠标基于网页文本的坐标位置

##### ②元素element
* offsetLeft/offsetTop  获取基于offsetParent（当前元素的父级元素）相对的坐标值
* offsetWidth/offsetHeight 获取元素的实体范围的宽高 content+padding+border
* scrollLeft/offsetTop  获取元素滚动出去的距离
* scrollWidth/scrollHeight 滚动框里面的盒子（滚动元素） 大小 
* clientHeight/clientWidth 获取盒子的宽高，不包括滚动条


### 二、主要步骤
#### 1.获取元素
```
const video = document.querySelector('.flex')
const speed = document.querySelector(".speed")
const bar = document.querySelector('.speed-bar')
```
#### 2.监听鼠标移动事件
* 获得鼠标移动时占整个speed的长度
* 用video.playbackRate控制视频的播放速度
* 改变bar的样式
```
function speedHandler(e) {
    // console.log(e);
    const y = e.pageY - this.offsetTop
    const height = y / this.offsetHeight
    const percent = Math.round(height * 100) + "%"
        // console.log(height);
    const min = 0.5
    const max = 4
    const playbackRate = height * (max - min) + min
        // console.log(playbackRate);
    video.playbackRate = playbackRate
    bar.textContent = playbackRate.toFixed(2) + 'x'
    bar.style.height = percent
}
speed.addEventListener('mousemove', speedHandler)
```
