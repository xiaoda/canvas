# Canvas

## [Intro](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API)
Canvas API 提供了一个通过 JavaScript 和 HTML 的 &lt;canvas&gt; 元素来绘制图形的方式。它可以用于动画、游戏画面、数据可视化、图片编辑以及实时视频处理等方面。

Canvas API 主要聚焦于 2D 图形。而同样使用 &lt;canvas&gt; 元素的 WebGL API 则用于绘制硬件加速的 2D 和 3D 图形。

## Demo
### [【Rectangle Demo】](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API#%E7%BB%93%E6%9E%9C)

``` javascript
const canvas = document.getElementById('canvas')
const ctx = canvas.getContext('2d')

ctx.fillStyle = 'green'
ctx.fillRect(10, 10, 150, 100)
```

### [【House Demo】](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D#%E5%9F%BA%E7%A1%80%E7%A4%BA%E4%BE%8B)

``` javascript
const canvas = document.getElementById('my-house')
const ctx = canvas.getContext('2d')

// Set line width
ctx.lineWidth = 10

// Wall
ctx.strokeRect(75, 140, 150, 110)

// Door
ctx.fillRect(130, 190, 40, 60)

// Roof
ctx.beginPath()
ctx.moveTo(50, 140)
ctx.lineTo(150, 60)
ctx.lineTo(250, 140)
ctx.closePath()
ctx.stroke()
```

## [Library](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API#resources)
1. [EaselJS](https://www.createjs.com/easeljs)
2. [Fabric.js](http://fabricjs.com/)
3. [Konva.js](https://konvajs.org/)
4. [p5.js](https://p5js.org/)
5. [heatmap.js](https://www.patrick-wied.at/static/heatmapjs/)（热力图）
6. [Phaser](https://phaser.io/)（游戏）

### Pros
1. 直观、易用的 API
2. 丰富、强大的功能
3. 性能优化

### P.S.
1. 底层和应用层 API 设计的差异
2. 使用库（面向百度编程） or 原生代码（自己撸）？以 jQuery / WebSocket 为例，聊聊如何选择适合的开发方式。

## [Canvas vs SVG](https://g2.antv.vision/zh/docs/manual/tutorial/renderers)
HTML5 提供了 Canvas 和 SVG 两种绘图技术，也是多数 Web 图表库使用的渲染技术。Canvas 是基于脚本的，通过 JavaScript 指令来动态绘图。而 SVG 则是使用 XML 文档来描述矢量图。两者有不同的适用场景。

### 适用场景
- Canvas 提供的绘图能力更底层，适合做到像素级的图形处理，能动态渲染和绘制大数据量的图形。（适合游戏等）
- SVG 抽象层次更高，声明描述式的接口功能更丰富，内置了大量的图形、滤镜和动画等，方便进行文档元素的维护，也能导出为文件脱离浏览器环境使用。（适合网页、文档等）[【SVG 示例】](http://43.254.54.39:8103/)[【情况类似的 CSS3 动画】](https://animate.style/)

### 性能差异
- 从底层来看，Canvas 的性能受画布尺寸影响更大。
- SVG 的性能受图形元素个数影响更大。

### 定制和交互
- SVG 做定制和交互更有优势，因为有类似 DOM 的结构，能快速应用浏览器底层的鼠标事件、CSS 样式、CSS3 动画等。
- 基于 Canvas 做上层封装后也能实现类似的定制和交互，并且自由度更高。

### 小结
- 小画布、大数据量的场景适合用 Canvas，譬如热力图、大数据量的散点图等。
- 如果画布非常大，有缩放、平移等高频的交互，或者移动端对内存占用量非常敏感等场景，可以使用 SVG 的方案。

## Application
1. [刮刮卡](https://zhuanlan.zhihu.com/p/84020475)
2. [小程序生成海报](https://fe.anchnet.com/2020/%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E5%AE%9E%E8%B7%B5/)
3. [保存图片到本地](https://www.zhuyuntao.cn/canvas%E4%BF%9D%E5%AD%98%E5%9B%BE%E7%89%87%E5%88%B0%E6%9C%AC%E5%9C%B0)
4. [特殊的图片展示功能](https://openseadragon.github.io/)

## Extension
1. 浏览器本质上就是一个功能齐全、超级复杂的 Canvas。
2. &lt;canvas&gt; 与 &lt;audio&gt; &lt;video&gt; 等标签丰富、增强了浏览器前端的能力，可用于复杂的功能需求。

### 【案例】录制视频，截取图片并上传 / 下载
``` html
<!DOCTYPE html>
<html>
<head>
  <meta name="viewport" content="width=device-width">
  <title>Demo</title>
  <style>
    .hide {display: none;}
  </style>
</head>
<body>
  <input id="upload" type="file" accept="video/*">
  <button id="load">Load</button>
  <video id="video" class="hide" controls></video>
  <canvas id="canvas" class="hide" width="200" height="200"></canvas>

  <script src="./jquery.js"></script>
  <script>
    const $upload = $('#upload')
    const $load = $('#load')
    const $video = $('#video')
    const video = $video.get(0)
    const $canvas = $('#canvas')
    const canvas = $canvas.get(0)
    const ctx = canvas.getContext('2d')

    $upload.on('change', function (event) {
      video.src = URL.createObjectURL(event.target.files[0])
    })
    $video.on('loadeddata', function () {
      video.currentTime = 1
    })
    $video.on('timeupdate', function () {
      ctx.drawImage(video, 0, 0, canvas.width, canvas.height)
      const dataUrl = canvas.toDataURL('image/jpeg')
      const link = document.createElement('a')
      link.href = dataUrl
      link.download = 'demo.jpg'
      link.click()
    })
    $load.on('click', function () {
      video.load()
    })
  </script>
</body>
</html>
```

## Project
1. [Flipboard/react-canvas](https://github.com/Flipboard/react-canvas)：在移动端页面使用支持硬件加速的 Canvas 代替性能较差的 DOM 的一次尝试

## [Design to Code](https://github.com/xiaoda/design2code)
### Preface
我们深知前端开发存在的问题，并期待进化。其实前端行业一直在不断发展和变革，短期看不一定能发现明显的进步，但长期看就一定能看到。

就我个人而言，我觉得前后端联调是开发流程中最复杂、耗时最长、问题最多的阶段，但这个阶段想要从前端单一方面进行改进是非常困难的。而前端开发流程中相对机械的工作：静态页面开发，可能是一个很好的切入点。

### Relavant Project
1. [蓝湖](https://zhuanlan.zhihu.com/p/355970754)
2. [阿里 imgcook](https://www.imgcook.com/)

### [Canvas Pixel](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial/Pixel_manipulation_with_canvas)

到目前为止，我们尚未深入了解 Canvas 画布真实像素的原理，事实上，你可以直接通过 ImageData 对象操纵像素数据，直接读取或将数据数组写入该对象中。

### Steps
#### 设计稿
<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/design.png" width="48%" />

#### 边缘检测 & 实体检测
<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/detect-edge.png"  width="48%" />&nbsp;&nbsp;&nbsp;&nbsp;<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/highlight-stuff.png" width="48%" />

#### 实体数据
<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/stuff.png" />

#### 结构数据
<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/structure.png" />

#### HTML
<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/design.png" width="48%" align="top" />&nbsp;&nbsp;&nbsp;&nbsp;<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/code.png"  width="48%" align="top" />

CSS 样式及更多功能待开发；算法需持续完善。

## Last but not Least
1. 在有更好的办法前，不完善的办法总比没有强。
2. 想法付诸实践，成功或失败都有收获。
3. 面对困难始终保持积极的心态
