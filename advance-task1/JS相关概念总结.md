## JS相关概念总结

### 简单介绍JavaScript的发展历史
JavaScript因互联网而生，回顾它的历史要从浏览器的历史讲起。
- 1990年底，欧洲核能研究组织科学家Tim Berners-Lee发明了万维网（World Wide Web），但只能在操作系统的终端里浏览和操作，非常不方便。
- 1992年底，美国国家超级电脑应用中心开发了人类历史上第一个浏览器Mosaic，从此网页可以在图形界面的窗口浏览。
- 1994年10月，NCSA的主要程序员Marc Andreessen联合风险投资家Jim Clark，成立了Mosaic通信公司，后改名为Netscape。这家公司的方向，就是在Mosaic的基础上，开发面向普通用户的新一代的浏览器Netscape Navigator。
- 1994年12月，Navigator发布了1.0版，该公司很快发现浏览器需要一种可嵌入网页的脚本语言来控制浏览器行为。
管理层对这种浏览器脚本语言的设想是：功能够用，语法简单，容易学习。当时就职于Netscape的Brendan Eich着手计划于1995年2月发布的Netscape Navigator2开发LiveScript脚本语言，那年正逢Sun公司的Java语言问世，市场推广活动非常成功，为赶在发布日期前完成LiveScript开发，Netscape公司与Sun公司建立了开发联盟。
- 1995年5月，Brendan Eich只用了10天，就设计完成了LiveScript第一版，所以这门语言比较随意。
- 1995年12月，Netscape公司与Sun公司达成协议，后者允许将这种语言叫做JavaScript，于是Netscape在二代浏览器问世前顺利蹭到了java的热度，场面一度十分火爆。
- 1996年3月，Navigator 2.0浏览器正式内置了JavaScript脚本语言。
- 1996年8月，微软模仿JavaScript开发了一种相近的语言，取名为JScript。
- 1996年11月，Netscape公司决定将JavaScript提交给国际标准化组织ECMA，希望JavaScript能够成为国际标准，以此抵抗微软。
- 1997年7月，ECMA组织发布262号标准文件（ECMA-262）的第一版，规定了浏览器脚本语言的标准，并将这种语言称为ECMAScript。这个版本就是ECMAScript 1.0版。ECMAScript和JavaScript的关系是，前者是后者的规格，后者是前者的一种实现。日常场合这两个词是可以互换的。
- 1998年6月，ECMAScript 2.0版发布。
- 1999年12月，ECMAScript 3.0版发布，成为JavaScript的通行标准，得到了广泛支持。
- 2007年10月，ECMAScript 4.0版草案发布，对3.0版做了大幅升级，预计次年8月发布正式版本。
- 2008年7月，由于对于下一个版本应该包括哪些功能，各方分歧太大，争论过于激进，ECMA开会决定，中止ECMAScript 4.0的开发（即废除了这个版本），将其中涉及现有功能改善的一小部分，发布为ECMAScript 3.1，而将其他激进的设想扩大范围，放入以后的版本，由于会议的气氛，该版本的项目代号起名为Harmony（和谐）。会后不久，ECMAScript 3.1就改名为ECMAScript 5。
- 2009年12月，ECMAScript 5.0版正式发布。
- 2011年6月，ECMAscript 5.1版发布，并且成为ISO国际标准（ISO/IEC 16262:2011）。到了2012年底，所有主要浏览器都支持ECMAScript 5.1版的全部功能。
- 2013年3月，ECMAScript 6草案冻结，不再添加新功能。
- 2013年12月，ECMAScript 6草案发布。
- 2015年6月，ECMAScript 6正式发布，并且更名为“ECMAScript 2015”。
- 2016年6月，《ECMAScript 2016标准》发布。

### 简述网页的渲染机制
1. 解析HTML标签，构建DOM树
2. 解析CSS标签，构建CSSOM树
3. 把DOM和CSSOM组合成渲染树
4. 在渲染树的基础上布局，计算每个节点的几何结构
5. 把每个节点绘制到屏幕上

### CSS和JS在网页中的放置顺序是怎样的？
1. css放入head中，link引入样式表和写在head內的style标签里都可以，也可以直接在元素中写入样式，但注意要放在js脚本之前。

2. js放置位置：
- 放入body底部，`</body>`之前。
- 放入head中同时使用defer或async来延迟或异步加载js。
- 使用creatElement动态生成但要注意加载顺序。
- 用ajax加载。

原因：当文档加载过程中遇到JS文件，HTML文档会挂起渲染过程，不仅要等到文档中JS文件加载完毕还要等待解析执行完毕，才会继续HTML的渲染。原因是因为JS有可能修改DOM结构，这就意味着JS执行完成前，后续所有资源的下载是没有必要的，这就是JS阻塞后续资源下载的根本原因，即无论当前JS代码是内嵌还是在外部文件中，页面的下载和渲染都必须停下来等待脚本执行完成，JS执行过程越久，浏览器等待响应用户输入的时间就越长，所以尽量把JS放在底部、设置script标签的defer或async属性、合并脚本等方法可起到性能优化效果。

### 解释白屏和FOUC
1. 白屏：
- 对IE来说，把样式放在底部时，在某些场景下（如打开新窗口／刷新页面等）页面会出现白屏，而不是内容逐步展现。
- 如果使用@import标签，即使将CSS写入外部样式表由link引入并放在头部，也可能出现白屏。
- 把js文件放入页面顶部而未使用defer或async延迟或异步加载js文件，从而阻塞html与css的加载也会导致白屏。
- 另外：Chrome会同时加载html和css分别构建DOM树和CSSOM树，等到二者都构建完成后再绘制渲染树，然后显示出页面，当外部css样式表设置了延时或者加载的时间比较久时就会显示出白屏，与浏览器的渲染机制有关。
2. FOUC：
Flash of unsettled content：无样式内容闪烁。对IE来说，把样式放在底部时，在某些场景下（如点击链接、输入URL、使用书签进入等）页面会出现FOUC现象，具体表现为逐步加载无样式的内容，等CSS加载完成后页面突然展现样式；对Firefox来说会先显示已加载的html内容，再逐步加载无样式内容，等css全部加载完成后页面突然展现样式，所以Firefox会一直表现出FOUC。

### async和defer的作用是什么？有什么区别
async和defer用于异步或延迟加载脚本。
没有 defer 或 async，浏览器会立即加载并执行指定的脚本，“立即”指的是读到就加载并执行。也就是说脚本会阻塞其后内容的解析和执行。
1. 作用：
- async（异步）：定义了async属性的脚本相对于页面的其他部分异步执行（同时执行），作用是不让页面等待两个或以上的脚本下载和执行，从而异步加载页面的其他内容。
```
<!DOCTYPE html>
<head>
    <title>Example HTML Page</title>
    <script type="text/javascript" async src="example1.js"></script> 
    <script type="text/javascript" async src="example2.js"></script>
</head>
<body>
    <!-- 这里放内容 --> 
</body>
</html>
```
以上代码中evample2.js可能会在example1.js之前执行，所以确保二者之间互不依赖很重要。
- defer（延迟）：定义了defer属性的脚本会被延迟到整个页面都解析完毕后再执行。
```
<!DOCTYPE html>
<head>
    <title>Example HTML Page</title>
    <script type="text/javascript" defer src="example1.js"></script>
    <script type="text/javascript" defer src="example2.js"></script>
</head>
<body>
    <!-- 这里放内容 -->
</body>
</html>
```
以上代码中虽然我们把`<script>`放在了`<head>`中，但其中包含的脚本文件将延迟到浏览器遇到`</html>`后再执行。HTML5规范要求脚本按照它们出现的先后顺序执行，即第一个延迟脚本先于第二个延迟脚本执行，而这两个脚本会先于DOMContentLoaded事件执行，但**现实中**延迟脚本并不一定会按照顺序执行，也不一定会在DOMContentLoaded事件触发前执行，所以一个文档里最好只包含一个延迟脚本。

![async-VS-defer-图片来自文章最底部参考资料](http://upload-images.jianshu.io/upload_images/6851923-4b65d97fad9e74e8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上图的意思是：浏览器在解析HTML文件时，遇上没有设置defer或async属性的脚本，浏览器读到该脚本就加载并执行，脚本会阻塞其后内容的执行；
遇上设有async属性的脚本，会在HTML解析过程中下载该脚本，并在完成下载后暂停HTML的解析来执行这个异步脚本，直到执行完成后再继续HTML的解析；
遇上设有defer属性的脚本，会在HTML解析过程中下载该脚本，在HTML解析完成后才执行该文件。延迟脚本按照它们在文档中出现的顺序执行。

2. 共同点：
- 设置了async或defer属性的脚本不会阻塞页面渲染
- async和defer属性决定了js脚本的执行方式，内联脚本会忽略这两个属性
- 使用这两个属性的脚本中不能调用document.write
- 所有defer和async脚本执行完毕后，DOMContentLoaded和load事件都将触发

3. 区别：
- 异步脚本一定会在页面的load事件前执行，但可能在DOMContentLoaded事件触发之前或之后执行，所以可能出现无顺序加载js的情况；延迟脚本在文档完成解析后，执行理论上是有序的但现实中并不能保证顺序，也不一定会在DOMContentLoaded事件触发前执行。
（实际实验得到的结果是，在页面中有2个defer脚本，2个async脚本的情况下，这四个脚本的执行顺序是无序的，但单看defer或单看async，他们都是有序的，且这四个脚本文件都会在DOMContentLoaded事情之前执行完毕，load事件永远最后触发。）

4. 关联：
- async为true，脚本将在加载完成后立即执行
- async为false，defer为true，脚本将在页面全部解析完成后执行
- async和defer都为false，脚本将阻塞页面解析，即页面解析被挂起转而下载并立即执行脚本文件

5. 注意事项：
如果一个外部脚本依赖于另一外部脚本，请将它们标记为defer，并按它们被声明的顺序执行。
浏览器发起资源请求request的时间都比较接近，除非DOM树非常长，时间可能会有明显差别。但资源响应时间responsive的时间差别较大，浏览器会根据情况作出优化，图片字体等优先级较低，一般等到最后才加载完成（比js还久）。

### repaint 和 reflow
- 什么是repaint和reflow：
浏览器根据自己默认的或开发人员给出的样式表来计算DOM结构中的各个盒模型该出现的位置就是reflow；当各种盒子的位置、大小及其他属性，例如颜色、字体大小等都确定下来后，浏览器开始布局渲染树并将其绘制到屏幕上，这个过程就是repaint。


浏览器解析和渲染页面过程中会涉及到reflow（回流）和repaint（重绘），就某些浏览器如Opera而言，大部分的reflow将导致页面重新渲染，其变化涉及到部分甚至是整个页面的布局，而repaint则导致浏览器必须验证DOM树上其他节点元素的可见性。reflow和repaint过程非常消耗性能，尤其在移动设备上，会破坏用户体验，造成页面卡顿，所以应尽可能减少reflow和repaint。

- 导致回流的原因：
    - 调整窗口大小
    - 改变字体
    - 增加或移除样式表
    - 内容变化，如在input框中输入文字
    - 激活CSS伪类，如hover
    - 操作class属性
    - 脚本操作DOM
    - 计算offsetWidth和offsetHeight属性
    - 设置style属性的值

- 如何避免回流或将它们对性能的影响降到最低：
    - 尽可能在DOM树最末端通过改变元素的class名的方式设定元素的样式：回流会顺行或逆行传递给周围的节点，在DOM树里改变class限制了回流的范围，使其影响尽可能少的节点。
    - 避免设置多项内联样式：因为每个内联样式都会造成回流，样式应合并在一个外部类，这样当该元素的class属性被操控时只会产生一个回流。
    - 应用元素的动画使用position属性的absolute或fixed值：这样设置不影响其他元素的布局，只会导致重绘而不是完整回流。
    - 牺牲平滑度换取速度：你可能想每次1px移动一个动画，但是此动画及随后的回流使用了100%的CPU，动画看上去就会是跳动的，因为浏览器正在与更新回流做斗争。而动画元素每次移动3px，在非常快的机器上看起来平滑度低了，但它不会导致CPU在较慢的机器和移动设备中抖动。
    - 避免使用table布局：table是个和罕见的可以影响在它们之前已经进入的DOM元素的显示的元素。想象一下，因为表格最后一个单元格的内容过宽而导致纵列大小完全改变。这就是为什么所有的浏览器都逐步地不支持table表格的渲染。另外一个原因说明表格布局很糟糕，根据Mozilla，一些小的变化将导致表格(table)中的所有其他节点回流。
    - 避免使用CSS的JS表达式：因为他们每次都重新计算全部或部分文档而导致每秒产生成千上万次回流。
    - 设置`box-sizing: border-box;`把标准盒模型转换为IE盒模型，告诉浏览器去理解你设置的边框和内边距的值是包含在width内的。设置后，即使padding或者border发生了改变，盒子宽高不会发生变化，只会重绘，不会回流。

**关于浏览器渲染更详细内容可参考**[我的博客第六节](http://www.jianshu.com/p/1aa5d2d3a44a)

-----
**参考资料**
- [*async vs defer attributes*](http://www.growingwiththeweb.com/2014/02/async-vs-defer-attributes.html)