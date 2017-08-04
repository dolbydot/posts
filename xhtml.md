3/5/2017 8:30:51 PM 
#### XHTML（EXtensible HyperText Markup Language：超文本标记语言） ####
- XHTML比起html4.01是更严格纯净的html版本，得到所有主流浏览器的支持。
- XHTML是以XML应用的方式定义的HTML，而XML是一种必须正确标记且格式良好的标记语言。

**和html的区别**
**1. 文档结构：**
- XHTML `<!DOCTYPE…>`是强制性的，即必须进行xhtml文档类型声明
- `<html>`中XML namespace属性(xmlns)是强制性的
- `<html>`、`<head>`、`<title>`以及`<body>`也是强制性的
 
**2. 元素语法：**
XHTML元素是以XML格式编写的HTML元素。
- XHTML 元素**必须正确嵌套**
- XHTML **元素必须始终关闭**
- XHTML **元素必须小写**
- XHTML 文档必须有一个根元素

**3. 属性语法：**
XHTML属性是以XML格式编写的HTML属性。
- XHTML 属性必须使用小写
- XHTML 属性值必须用引号包围
- XHTML 属性最小化也是禁止的，即禁止简写。
如：
错误的写法：`<input checked>`
正确的写法：`<input checked="checked" />`


下面的例子展示了带有最少的必需标签的XHTML文档：
```xhtml
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">

<head>
<title>Title of document</title>
</head>

<body>
......
</body>

</html>
```

**如何从 HTML 转换到 XHTML**
1. 向每张页面的第一行添加 `<!DOCTYPE>`，`<!DOCTYPE>`没有关闭标签。
2. 向每张页面的 html 元素添加xmlns属性
3. 把所有元素名改为小写
4. 关闭所有空元素，如`<br/>，<img/>,<hr/>,<input/>,<option/>`
5. 把所有属性名改为小写
6. 为所有属性值加引号

**注意：**
1. 在XHTML中只有这种lang属性的用法是正确的：
`<div lang="en" xml:lang="en">Hello World!</div>`
2. XHTML是一个web标准，HTML会被XHTML取代。
3. id属性可以代替a、applet、frame、iframe、img以及map的name属性。
4. XHTML中有Strict, Transitional, Frameset这三个DTD，其中Transitional最常用。
5. id属性值不能包含数字和“-”，可用字母和下划线。
