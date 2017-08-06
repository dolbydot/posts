## 1.动手
[form 表单](https://dolbydot.github.io/practice6/form-ele.html)
[table 表格](https://dolbydot.github.io/demos/table/table.html)

-----
## 2. `<form>`表单元素

 1） **简述**：
 `<form>`元素是块级元素,其开始标签和结束标签都不能省略，其中可以包含`<button>`, `<datalist>`, `<fieldset>`, `<input>`, `<keygen>`, `<label>`, `<legend>`, `<meter>`, `<menus>`, `<optgroup>`, `<option>`, `<output>`, `<progress>`, `<select>`, `<textarea>`等表单元素。
# 
其中：

 - `<fieldset>`用于组合表单数据，每个`<fieleset></fieleset>`是一组。
 - `<legend>`元素为`<fieldset>`元素定义标题。
 - `<input>`是最重要的表单元素，有很多不同的type属性，input元素需要定义type，name，value，或者checked，其中，每个输入字段必须设置一个name属性，checked属性用于设置按钮的预选项。
 - `<select>`元素定义下拉列表，`<option>`元素定义下拉列表的选项，列表通常会把首个选项显示为被选选项，但可以通过selected定义预定义选项。
 - `<textarea>`元素定义多行输入字段（文本域），【rows="10" cols="30"】的意思是定义一个30个字符宽，10行高的文本区。
 - `<button>`元素定义可点击的按钮，请示中为按钮规定type属性。如果在HTML表单中使用button元素，不同的浏览器会提交不同的值。IE将提交`<button>`与`<button/>`之间的文本，而其他浏览器将提交value属性的内容。应用`<input>`元素创建按钮。
 - `<datalist>`为`<input>`预定义选项列表，起到提示作用。用户会在他们输入数据时看到预定义选项的下拉列表。

**注意：**`<input>`元素的list属性值必须与`<datalist>`元素的id属性值相同。Safari或≤IE9不支持datalist标签。
# 
 2） **作用**：
 HTML`<form>`元素表示了文档中的一个区域，这个区域包含有交互控制元件，用来向web服务器提交信息。
#  
 3） **常用属性**：
 
 - `action`属性制订了某个服务器脚本来处理被提交的表单，如果省略action属性，则action会被设置为当前页面。
 - `method`属性规定了提交表单的http方法，默认GET，GET最适合少量数据且不需要保密的提交，使用GET时表单数据在页面地址栏中是可见的。设置为POST，安全性更佳，因为在页面地址栏中被提交的数据不可见。
 - `target`属性值是一个名字或关键字，规定在哪里打开新页面，默认_self,一般设置为_blank。
**_self**: 在当前HTML4或HTML5文档页面重新加载返回值。这个是默认值。译注：也就是说如果这个文档在一个frame中的话，self是在当前frame（document）中重新加载的，而不是整个页面（window）。
**_blank**: 以新的HTML4或HTML5文档窗口加载返回值。
**_parent**: 在父级的frame中以HTML4或HTML5文档形式加载返回值，如果没有父级的frame，行为和_self一致。
**_top**: 如果是HTML 4文档: 清空当前文档，加载返回内容；HTML5: 在当前文档的最高级内加载返回值，如果没有父级，和_self的行为一致。
**iframename**: 返回值在指定frame中加载。
在HTML5中这个值可以被 `<button>` 或者 `<input>` 元素中的 formtarget 属性重载（覆盖）。
 - `accept-charset`属性规定被提交表单中使用的字符集，默认为页面字符集。
 - `enctype`属性规定被提交数据的编码。
 - `autocomplete`属性规定浏览器应自动完成表单，默认为开启“on”。
 - `novalidate`属性规定浏览器不验证表单。

-----
## 3. input标签常用属性及作用
1）**简述**：
`<input>`标签用于搜集用户信息，根据不同的type属性值，输入字段拥有很多种形式，可以是文本字段、复选框、掩码后的文本控件、单选按钮等。
# 
2）**常用属性及作用**：

**type属性**：规定input元素的类型，可设置**值如下**：

 - text：定义共文本输入的单行字段，默认值。
 - password：定义密码字段，字段中的字符会做掩码处理，显示为星号或实心圈。
 - submit：定义提交表单数据至表单处理程序（即form元素的action属性值）的按钮。如果省略了提交按钮的value属性，那么该按钮将获得默认文本，一般是“提交”这两个字。
 - reset：定义重设按钮。
 - radio：定义单选按钮。
 - checkbox：定义复选框，即多选。
 - button：定义按钮。
 - hidden：定义隐藏输入字段。
 - number：用于应该包含数字值的输入字段，可自定义数字限制。
 - data: 用于应该包含日期的输入字段,日期也可定义输入限制。
 - color：用于应该包含颜色的输入字段。
 - range：用于应该包含一定范围内的值的输入字段，可用min、max、step、value属性规定限制。
 - month：选择月份和年份。
 - week：选择周和年。
 - time：选择时间-无时区。
 - datatime：选择日期与时间-有时区。
 - datetime-local：选择日期和时间-无时区。
 - email：用于应该包含电子邮件地址的输入字段，若浏览器支持，能够在被提交时自动对电子邮件地址进行验证，某些智能手机会识别email类型，并在键盘增加".com" 以匹配电子邮件输入。
 - search：用于搜索字段（搜索字段的表现类似常规文本字段）。
 - tel：用于应该包含电话号码的输入字段，目前只有safari 8支持。
 - url：用于应该包含URL地址的输入字段，若浏览器支持，能够在提交时自动验证url字符，某些智能手机识别url类型，并向键盘添加".com"以匹配url输入。

**name**：定义input元素的名称。

**value**：规定字段的初始值。

**readonly**：规定输入字段只读。readonly="readonly"。

**disabled**：规定输入字段是禁用的，被禁用的元素是不可用不可点击并且不可提交。disabled="disabled"。

**size**：规定输入字段的尺寸，如果size="5"，那么一行中可输入无数个字符但**一行中只有5个可见字符**。

**maxlength**：规定输入字段允许的最大长度。如果maxlength="5"，那么**一行中最多可输入5个字符**。

**placeholder**：规定帮助用户填写输入字段的提示（样本值或有关格式的简短描述），该提示会在用户输入值之前显示在输入字段中。

**list**：引用包含输入字段的与定义选项的datalist。

**src**：定义以提交按钮形式显示的图像的 URL。

**step**：规定`<input>`元素的合法数字间隔,如果step="3"，则合法数字应该是-3、0、3、6、等。只能是3的整数倍。可与max以及min属性一同使用，来创建合法值的范围。

-----
## 4. post和get方式的区别

 - **GET**
用GET方法提交的表单数据只经过了简单的编码，同时它将作为URL的一部分向服务器发送，URL具有长度限制，即GET方式提交的数据大小有限制，如`<Http://localhost/login.php?username=aa&password=1234>`，很容易辨认出表单提交的内容，因此，如果使用GET方法来提交表单数据就存在着安全隐患。
 - **POST**
是GET的一个替代方法，很适合提交表单数据，尤其是大批量的数据。POST方法克服了GET方法的一些缺点。通过POST方法提交表单数据时，数据不是作为URL请求的一部分而是作为标准数据放在HTTP的body中传送给Web服务器，这就克服了GET方法中的信息无法保密和数据量太小的缺点。因此，出于安全的考虑以及对用户隐私的尊重，通常表单提交时采用POST方法。
 - **比较**

||GET|POST|
|-----|-----|-----|
|后退刷新|无特殊事件|数据会被重新提交到服务器|
|书签收藏|可收藏|不可收藏|
|数据缓存|能被缓存|不能被缓存|
|编码类型|application/x-www-form-url|application/x-www-form-urlencoded或multipart/form-data|
|历史记录|参数保存在浏览器历史中|参数不会被保存在历史记录中|
|数据长度|受限于URL长度（最大2048个字符）|无限制|
|字符集|ASCII|无限制（允许二进制数据）|
|安全性|差|较好|

-----
## 5. input中name的作用
name属性规定input元素的名称，用于对提交到服务器后的表单数据进行标识，或是在客户端通过javascript引用表单数据。

**注意**：浏览器会根据name来设定发送到服务器的request，在表单的接收页面只接收有name的元素，即只有设置了name属性的表单元素才能在提交表单时传递它们的值，赋id的元素通过表单是接收不到值的。

-----
## 6. radio如何分组
`<input type="radio" />`定义单选按钮。radio使用name属性来分组，所有name属性相同的radio使用时其中只有一个会被选中。
```html
<input type="radio" value="male" name="sex"/>男
<input type="radio" value="female" name="sex"/>女
```
以上两个radio就是一组。

-----
## 7. placeholder属性的作用?
placeholder:规定用于描述输入字段预期值的提示（样本值或有关格式的简短描述）。该提示会在用户输入值之前显示在输入字段中。适用于如下输入类型：`<input type="text|search|url|tel|email|password">`。
```html
<!DOCTYPE HTML>
<html>
<body>
<h1>html 5为input元素新增的属性placeholder</h1>
<form action="/example/html5/demo_form.asp" method="get">
<input type="search" name="user_search" placeholder="Search W3School" />
<input type="submit" />
</form>
</body>
</html>
```
仅仅是提示值，至于是否按照提示写是另一回事。
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-5238541661156c22.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

-----
## 8. 举例说明type=hidden隐藏域的作用? 
`<input type="hidden" />`定义隐藏字段。隐藏字段对于用户是不可见的，通常会存储一个默认值，它们的值也可以由 JavaScript 进行修改。
作用：

 - 收集或发送信息以被处理表单的程序所使用，提交表单时隐藏域的信息也会被一起发送到服务器。
 - 所有浏览器都支持隐藏域，操作方便简单、对长度限制不大，且避免了用户禁用cookie的烦恼。
 - 一个网页有多个form，而多个form不能同时提交但他们确实相互作用，这种情况下我们可以在form中添加隐藏域使它们联系起来。

```html
<html>
    <body>
    <form action="/example/html/form_action.asp" method="get">
    Email: <input type="text" name="email" /><br />
    <input type="hidden" name="country" value="China" />
    <input type="submit" value="Submit" />
    </form>
    </body>
</html>
```
![](http://upload-images.jianshu.io/upload_images/6851923-34568e5a1b85c6d5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

输入email地址`dolby.dot@gmail.com`，单击Sumbit按钮，输入的内容会发送到服务器上名为form_action.asp的页面，服务器处理了我的输入并返回结果`"email=dolby.dot%40gmail.com&country=China"`。

-----
## 9. html5语义化新标签
- `<header>`：定义文档或节的页眉
- `<nav>`：定义导航链接的容器
- `<section>`：定义文档中的节
- `<article>`：定义独立的自包含文章
- `<aside>`：定义内容之外的内容（比如侧栏）
- `<footer>`：定义文档或节的页脚
- `<details>`：定义额外的细节
- `<summary>`：定义`details>` 的标题

-----
## 10. [CSRF攻击是什么，如何防范？](http://www.h3c.com.cn/MiniSite/Phone_Magazine/2012/07/IT/201212/766969_97665_0.htm)
简介：
CSRF（Cross-Site Request Forgery，跨站点伪造请求）是一种网络攻击方式，该攻击可以在受害者毫不知情的情况下以受害者名义伪造请求发送给受攻击站点，从而在未授权的情况下执行在权限保护之下的操作，具有很大的危害性。
可以这样理解CSRF攻击：攻击者盗用了你的身份，以你的名义发送恶意请求，对服务器来说这个请求是完全合法的，但是却完成了攻击者所期望的一个操作，比如以你的名义发送邮件、发消息，盗取你的账号，添加系统管理员，甚至于购买商品、虚拟货币转账等。
# 
原理：
SRF攻击原理如图所示。其中Web A为存在CSRF漏洞的网站，Web B为攻击者构建的恶意网站，User C为Web A网站的合法用户。
![](http://upload-images.jianshu.io/upload_images/6851923-101bcd8e6bd490e9.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 用户C打开浏览器，访问受信任网站A，输入用户名和密码请求登录网站A；
- 在用户信息通过验证后，网站A产生Cookie信息并返回给浏览器，此时用户登录网站A成功，可以正常发送请求到网站A；
- 用户未退出网站A之前，在同一浏览器中，打开一个TAB页访问网站B；
- 网站B接收到用户请求后，返回一些攻击性代码，并发出一个请求要求访问第三方站点A；
- 浏览器在接收到这些攻击性代码后，根据网站B的请求，在用户不知情的情况下携带Cookie信息，向网站A发出请求。网站A并不知道该请求其实是由B发起的，所以会根据用户C的Cookie信息以C的权限处理该请求，导致来自网站B的恶意代码被执行。
# 
防御手段：
养成良好上网习惯，不要轻易点击链接或图片，及时退出长时间不使用的已登录账户，安装防护软件并及时更新。
