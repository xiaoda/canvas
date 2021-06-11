# Canvas

## [Canvas 介绍](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API)
Canvas API 提供了一个通过 JavaScript 和 HTML 的 &lt;canvas&gt; 元素来绘制图形的方式。它可以用于动画、游戏画面、数据可视化、图片编辑以及实时视频处理等方面。

Canvas API 主要聚焦于 2D 图形。而同样使用 &lt;canvas&gt; 元素的 WebGL API 则用于绘制硬件加速的 2D 和 3D 图形。

在浏览器以外，小程序也具备 [Canvas 画布](https://developers.weixin.qq.com/miniprogram/dev/framework/ability/canvas.html)的组件和能力。

## Canvas 基础示例
### [【示例一】](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API#%E7%BB%93%E6%9E%9C)

``` javascript
const canvas = document.getElementById('canvas')
const ctx = canvas.getContext('2d')

ctx.fillStyle = 'green'
ctx.fillRect(10, 10, 150, 100)
```

### [【示例二】](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D#%E5%9F%BA%E7%A1%80%E7%A4%BA%E4%BE%8B)

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

## [Canvas 库](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API#resources)
1. [EaselJS](https://www.createjs.com/easeljs)
2. [Fabric.js](http://fabricjs.com/)
3. [Konva.js](https://konvajs.org/)
4. [p5.js](https://p5js.org/)
5. [heatmap.js](https://www.patrick-wied.at/static/heatmapjs/)（热力图）
6. [Phaser](https://phaser.io/)（游戏）

### 优点
1. 直观、易用的 API
2. 丰富、强大的功能

### 讨论
1. 底层和应用层 API 设计的差异
2. 使用库（封装好的高级 API） or 原生代码（自己撸）？以 jQuery / WebSocket 为例，聊聊如何选择适合的开发方式。

## [Canvas vs SVG](https://g2.antv.vision/zh/docs/manual/tutorial/renderers)
HTML5 提供了 Canvas 和 SVG 两种绘图技术，也是多数 Web 图表库使用的渲染技术。Canvas 是基于脚本的，通过 JavaScript 指令来动态绘图。而 SVG 则是使用 XML 文档来描述矢量图。两者有不同的适用场景。

### 适用场景
- Canvas 提供的绘图能力更底层，适合做到像素级的图形处理，能动态渲染和绘制大数据量的图形。（适合游戏等）
- SVG 抽象层次更高，声明描述式的接口功能更丰富，内置了大量的图形、滤镜和动画等，方便进行文档元素的维护，也能导出为文件脱离浏览器环境使用。（适合网页、文档等）[【SVG 示例】](http://43.254.54.39:8103/)

### 性能差异
- 从底层来看，Canvas 的性能受画布尺寸影响更大。
- SVG 的性能受图形元素个数影响更大。

### 定制和交互
- SVG 做定制和交互更有优势，因为有类似 DOM 的结构，能快速应用浏览器底层的鼠标事件、CSS 样式、CSS3 动画等。
- 基于 Canvas 做上层封装后也能实现类似的定制和交互，并且自由度更高。

### 小结
- 小画布、大数据量的场景适合用 Canvas，譬如热力图、大数据量的散点图等。
- 如果画布非常大，有缩放、平移等高频的交互，或者移动端对内存占用量非常敏感等场景，可以使用 SVG 的方案。

## Canvas 应用
1. [刮刮卡](https://zhuanlan.zhihu.com/p/84020475)
2. [小程序生成海报](https://fe.anchnet.com/2020/%E5%BE%AE%E4%BF%A1%E5%B0%8F%E7%A8%8B%E5%BA%8F%E5%AE%9E%E8%B7%B5/)
3. [保存图片到本地](https://www.zhuyuntao.cn/canvas%E4%BF%9D%E5%AD%98%E5%9B%BE%E7%89%87%E5%88%B0%E6%9C%AC%E5%9C%B0)
4. [特殊的图片展示功能](https://openseadragon.github.io/)
5. 结合 Canvas 和 [OCR](https://cloud.tencent.com/product/ocr-catalog) 的能力，实现在图片上画框识字。

## [WebGL](https://developer.mozilla.org/zh-CN/docs/Web/API/WebGL_API)
WebGL（Web图形库）是一个 JavaScript API，可在任何兼容的 Web 浏览器中渲染高性能的交互式 3D 和 2D 图形，而无需使用插件。WebGL 通过引入一个与 OpenGL ES 2.0 非常一致的 API 来做到这一点，该 API 可以在 HTML5 &lt;canvas&gt; 元素中使用。这种一致性使 API 可以利用用户设备提供的硬件图形加速。

## WebGL 代码示例
``` javascript
// 从这里开始
function main() {
  const canvas = document.querySelector("#glcanvas");
  // 初始化WebGL上下文
  const gl = canvas.getContext("webgl");

  // 确认WebGL支持性
  if (!gl) {
    alert("无法初始化WebGL，你的浏览器、操作系统或硬件等可能不支持WebGL。");
    return;
  }

  // 使用完全不透明的黑色清除所有图像
  gl.clearColor(0.0, 0.0, 0.0, 1.0);
  // 用上面指定的颜色清除缓冲区
  gl.clear(gl.COLOR_BUFFER_BIT);
}
```

## [WebGL 库](https://developer.mozilla.org/zh-CN/docs/Web/API/WebGL_API#库)
- [three.js](https://threejs.org/)

## WebGL 应用
- [3D 小程序 POC](https://github.com/xiaoda/miniprogram-3d-poc)

<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/miniprogram-3d-poc.png" width="48%" />

## Canvas 的拓展性思考
1. &lt;canvas&gt; 与 &lt;audio&gt; &lt;video&gt; 等 HTML5 标签丰富、增强了浏览器前端的能力，可用于复杂的功能需求。

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

2. 浏览器本质上就是一个功能齐全、超级复杂的 Canvas。[【浏览器渲染流程】](https://juejin.cn/post/6844903565610188807)

## Canvas 进阶项目
1. [Flipboard/react-canvas](https://github.com/Flipboard/react-canvas)：在移动端页面使用支持硬件加速的 Canvas 代替性能较差的 DOM 的一次尝试
2. [html2canvas](https://html2canvas.hertzen.com/)：将页面上指定的 DOM 元素渲染到 canvas 并保存
3. [glfx.js](https://evanw.github.io/glfx.js/demo/)：Canvas 滤镜效果库

## [Canvas 进阶项目之设计稿生成代码](https://github.com/xiaoda/design2code)
### 前言
我们深知前端开发存在的问题，并期待进化。前端技术领域一直在不断发展和变革，短期不一定能发现明显的进步，但长期看就一定能看到。

就我个人而言，我觉得 [前后端联调](https://github.com/xiaoda/web-api-issues) 是开发流程中最复杂、耗时最长、问题最多的阶段，但这个阶段要想进行显著的改进是非常困难的。而前端开发流程中相对机械的工作：静态页面开发，可能是一个很好的切入点。

### 相关项目
1. [蓝湖](https://zhuanlan.zhihu.com/p/355970754)
2. [阿里 imgcook](https://www.imgcook.com/)

### [像素操作](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial/Pixel_manipulation_with_canvas)

事实上，你可以直接通过 ImageData 对象操纵像素数据，直接读取或将数据数组写入该对象中。

### 步骤
#### 设计稿
<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/design.png" width="48%" />

#### 边缘检测 & 实体检测
<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/detect-edge.png"  width="48%" />&nbsp;&nbsp;&nbsp;&nbsp;<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/highlight-stuff.png" width="48%" />

#### 实体数据
<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/stuff.png" />

#### 结构数据
<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/structure.png" />

#### HTML
<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/design.png" width="48%" align="top" />&nbsp;&nbsp;&nbsp;&nbsp;<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/code.png"  width="40%" align="top" />

#### 具体步骤
<img src="https://raw.githubusercontent.com/xiaoda/canvas/master/images/steps.png" />

#### TODO
1. CSS 样式及更多功能待开发
2. 算法需持续完善

## 广告
我们的[【前端最佳实践】](http://fe.anchnet.com)

## 写在最后
1. 在有更好的办法之前，不完善的办法总比没有强。
2. 想法付诸实践，不论成功或失败都有收获。
3. 面对困难始终保持积极的心态
