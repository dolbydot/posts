- ** HTML、XML、XHTML 有什么区别？**
1、HTML：HyperText Markup Language / 超文本标记语言：被设计用来** 显示数据 **，不是一种编程语言，而是一种标记语言 (markup language)，标记语言是一套标记标签 (markup tag)。HTML 使用标记标签来描述网页。
2、XML: Extensible Markup Language / 可扩展标记语言：不会做任何事情，只用来** 传输和存储数据 **，XML 标签没有被预定义，你需要自行定义标签。XML被设计为具有自我描述性，是W3C推荐的标注。
3、[XHTML](http://www.jianshu.com/p/4d9c62223b80): Extensible Hypertext Markup Language / 可扩展超文本标记语言：是以XML应用的方式定义的HTML，比起html是更严格纯净的html版本，得到所有主流浏览器的支持，是一种** 必须正确标记且格式良好 **的标记语言。

-----
- ** 怎样理解 HTML 语义化。 **
1、用正确的标签做正确的事情，让页面的内容结构化，便于浏览器、搜索引擎解析
2、在没有CCS样式情况下也以一种文档格式显示且易读的。
3、搜索引擎的爬虫依赖于标记来确定上下文和各个关键字的权重，利于 SEO。
4、便于开发和维护。
5、使阅读源代码的人对网站更容易将网站分块，便于阅读维护理解。

-----
- ** 怎样理解内容与样式分离的原则 ？**
一个网页分为html——结构、css——表现、js——行为这三个部分，内容指html，样式指css，内容与样式分离指的是网页编码过程中html和css分开。
内容与样式分离的原则的实现依靠意识和经验。
1、初级开发人员思路及方法：div 层层嵌套；
2、中级开发人员思路及方法：去掉多余的 div ,进行简化；
3、高级开发人员思路及方法：最大化的简化 html 的结构，然后用 css 进行设置，减少 html 与 css 的契合度。
正确做法：写HTML的时候先不管样式，重点放在HTML的结构和语义化上，让HTML能提现页面结构或者内容，然后进行 css 样式设置，减少 HTML 与 CSS 契合度（即内容与样式分离），写JS的时候，尽量不要用JS去直接操作样式，而是通过给元素添加删除class来控制样式变化（即行为分离）。

-----
- ** 有哪些常见的meta标签？ **
meta元素的属性有：
1、content：对应值为some_text，定义与 http-equiv 或 name 属性相关的元信息，content 属性始终要和 name 属性或 http-equiv 属性一起使用。
2、http-equiv：对应值为content-type、expires、refresh、set-cookie，用于把content属性关联到 HTTP 头部。 
3、name：对应属性值为author、description、keywords、generator、revised、others，用于把 content 属性关联到一个名称，如果没有提供 name 属性，那么名称/值对中的名称会采用 http-equiv 属性的值。
4、scheme：对应属性值为some_text，用于定义翻译 content 属性值的格式。

-----
- ** 文档声明的作用?严格模式和混杂模式指什么?<!doctype html> 的作用? **
`<!DOCTYPE>` 声明必须是 HTML 文档的第一行，位于 `<html>` 标签之前。
（一）文档声明的作用：
1、`<!DOCTYPE>` 声明不是 HTML 标签，它是指示 web 浏览器关于页面使用哪个 HTML 版本进行编写的指令。
2、影响JS的功能。
（二）严格模式和混杂模式：
1、严格模式（标准模式）：浏览器以其支持的最高标准呈现页面
2、混杂模式（怪异／兼容模式）：页面以一种比较宽松的向后兼容的方式显示。混杂模式通常模拟老式浏览器的行为以防止老站点无法工作，可以理解为“没有DOCTYPE”意味着触发怪异模式，但包含了DOVTYPE却不一定是标准模式。
（三）`<!doctype html>` 的作用：按照标准模式（即W3C的标准）解析和渲染页面。

-----
- ** 浏览器乱码的原因是什么？如何解决 。**
原因：
1、浏览器对HTML网页的编码解释错误，HTML文件保存的编码与浏览器解释的编码不一致造成（一般多为中文)。
2、meta标签里没有设置编码字符集或meta字符集设置错误。
解决方法：
head元素內嵌套`<meta charset="UTF-8">`。

-----
- ** 常见的浏览器有哪些，什么内核 ？**
（一）常见浏览器：
Chrome，Safari，Opera，IE，Firefox。
（二）主要浏览器内核：
Chrome、Opera：blink；
Safari：webkit；
IE：trident，edgehtml；
Firefox：servo、gecko。

-----
- ** 列出常见的标签，并简单介绍这些标签用在什么场景 。**
`<!DOCTYPE>`：定义文档类型。
`<html>`：定义HTML文档。
`<head>`：定义文档的头部，它是所有头部元素的容器。
`<title>`：定义文档标题。
`<body>`：定义文档主体。
`<div>`：定义文档的分区或节。
`<h1>`-`<h6>`：定义一到六级标题。
`<p>`：定义段落。
`<br>`：定义折行。
`<!-- -->`：定义注释。
`<ul>`：定义无序列表。
`<ol>`：定义有序列表。
`<li>`：定义列表项。
`<table>`：定义表格。
`<form>`：定义表单
