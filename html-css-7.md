3/6/2017 12:33:03 PM  
#### html表单 ####
html表单用于收集用户输入，而<form>元素用于定义html表单。
```html
<!DOCTYPE html>
<html>
<head>
	<title></title>
	<style type="text/css">
	</style>
</head>
<body>
<form action="action_page.php" method="GET" target="_blank" accept-charset="UTF-8"
ectype="application/x-www-form-urlencoded" autocomplete="off" novalidate>

<fieldset>
<legend>Personal information:</legend>
First name:<br>
<input type="text" name="firstname" value="Mickey">
<br/>
Last name:<br>
<input type="text" name="lastname" value="Mouse">
<br>
</fieldset>
<br/>

<fieldset>
<legend>Sex:</legend>
<input type="radio" name="sex" value="female" checked="checked">female<br/>
<input type="radio" name="sex"value="male">male<br/>
</fieldset>
<br/>

<fieldset>
<legend>喜欢的车:</legend>
<select name="cars">
<option value="volvo">Volvo</option>
<option value="saab">Saab</option>
<option value="fiat" selected>Fiat</option>
<option value="audi">Audi</option>
</select>
</fieldset>
<br/>

<fieldset>
<legend>文本域:</legend>
<textarea name="message" rows="10" cols="30">
The cat was playing in the garden.
</textarea>
</fieldset>
<br/>

<fieldset>
<legend>您最喜欢的浏览器是:</legend>
<input list="browsers" name="browser">
<datalist id="browsers">
  <option value="Internet Explorer">
  <option value="Firefox">
  <option value="Chrome">
  <option value="Opera">
  <option value="Safari">
</datalist>
<input type="submit" value="确定">
</fieldset>
<br/>

<fieldset>
<legend>提交:</legend>
<input type="submit" value="Submit">
<button type="button" onclick="alert('Hello World!')">点击我！</button>
</fieldset>
<br/>

</form>
</body>
</html>
```
**form元素的属性**
- action属性制订了某个服务器脚本来处理被提交的表单，如果省略action属性，则action会被设置为当前页面。
- method属性规定了提交表单的http方法，默认GET，GET最适合少量数据的提交，使用GET时表单数据在页面地址栏中是可见的。可设置为POST，安全性更佳，因为在页面地址栏中被提交的数据是不可见的。
- target属性规定在哪里打开新页面，默认_self,一般设置为_blank。
- accept-charset属性规定被提交表单中使用的字符集，默认为页面字符集。
- enctype属性规定被提交数据的编码。
- autocomplete属性规定浏览器应自动完成表单，默认为开启“on”
- novalidate属性规定浏览器不验证表单。

**表单元素**
- `<fieldset>`用于组合表单数据，每个`<fieleset></fieleset>`是一组。
- `<legend>`元素为`<fieldset>`元素定义标题。
- `<input>`是最重要的表单元素，有很多不同的type属性，input元素需要定义type，name，value，或者checked，其中，每个输入字段必须设置一个name属性，checked属性用于设置按钮的预选项。
- `<select>`元素定义下拉列表，`<option>`元素定义下拉列表的选项，列表通常会把首个选项显示为被选选项，但可以通过selected定义预定义选项。
- `<textarea>`元素定义多行输入字段（文本域），【rows="10" cols="30"】的意思是定义一个30个字符宽，10行高的文本区。
- `<button>`元素定义可点击的按钮，请示中为按钮规定type属性。如果在HTML表单中使用button元素，不同的浏览器会提交不同的值。IE将提交`<button>`与`<button/>`之间的文本，而其他浏览器将提交value属性的内容。应用`<input>`元素创建按钮。
- `<datalist>`为`<input>`预定义选项列表，起到提示作用。用户会在他们输入数据时看到预定义选项的下拉列表。
**注意：**`<input>`元素的list属性值必须与`<datalist>`元素的id属性值相同。Safari或≤IE9不支持datalist标签。


----------
#### `<input type="">`专题 ####
**1、input元素-type属性值专题**
```html
<!DOCTYPE html>
<html>
<head>
	<title>input元素type常用属性值专题</title>
	<style type="text/css"></style>
</head>
<body>
<form action="">
	<fieldset>
		<legend>User message</legend>
		First name:
		<input type="text" name="firstname"><br/>
		Last name:
		<input type="text" name="lastname"><br/><br/>
		User password:
		<input type="password" name="password"><br/><br/>
		Sex:<br/>
		<input type="radio" name="sex" value="female">Female
		<input type="radio" name="sex" value="male" checked="checked">male<br/><br/>
		Yellow bean:<br/>
		<input type="checkbox" name="yellow" value="pen">
		I have a pen~<br/>
		<input type="checkbox" name="yellow" value="apple">
		I have an apple~<br/>
		<input type="checkbox" name="yellow" value="apple-pen">
		Boom!apple-pen!<br><br>
		<input type="button" onclick="alert('Hello Dolby!')" value="Click Me!"><br/><br/>
		<input type="submit" name="submit" value="submit"><br/>
	</fieldset>
</form>
</body>
</html>
```
**格式：<input type="">**
1. text:定义共文本输入的**单行字段**
2. password：定义密码字段，字段中的字符会做**掩码处理**，显示为星号或实心圈。
3. submit：**定义提交**表单数据至表单处理程序（即form元素的action属性值）的**按钮**。如果省略了提交按钮的value属性，那么该按钮将获得默认文本，一般是“提交”这两个字。
4. radio：定义单选按钮。
5. checkbox：定义复选框，即多选。
6. button：定义按钮。

**2、html5中新增的input元素-type属性值专题**
````html
<!DOCTYPE html>
<html>
<head>
	<title>html5中新增的input元素-type属性值专题</title>
	<style type="text/css"></style>
</head>
<body>

<form action="">
<p><b>number</b>-输入一个0≤number≤100的数值，默认值30，数值以10为单位增加或减少，输入不符合规定的数值提示不能提交！≤IE9不支持！</p>
  Quantity:
  <input type="number" name="points" min="0" max="100" step="10" value="30"><hr/>

<p><b>data</b>-输入给定条件内的日期，IE不支持！</p>
  Enter a date before 1980-01-01:<br>
  <input type="date" name="bday" max="1979-12-31"><br><br>
  Enter a date after 2000-01-01:<br>
  <input type="date" name="bday" min="2000-01-02"><hr/>

<p><b>color</b>-选择颜色，默认值红色，IE不支持！</p>
  Select your favorite color:
  <input type="color" name="favcolor" value="#ff0000"><hr/>

<p><b>range</b>-输入一个0≤number≤10的数值，默认值4，数值以2为单位增加或减少，≤IE9不支持！</p>
  <input type="range" name="points" min="0" max="10" step="2" value="4"><hr/>

<p><b>month</b>-输入年月，IE不支持！</p>
  Birthday (month and year):
  <input type="month" name="bdaymonth"><hr/>

<p><b>week</b>-输入周和年，IE不支持！</p>
  Select a week:
  <input type="week" name="year_week"><hr/>

<p><b>time</b>-输入时间-无时区，IE及Firefox不支持！</p>
  Select a time:
  <input type="time" name="usr_time"><hr/>

<p><b>datetime</b>-输入日期与时间-有时区，IE，Chroem及Firefox不支持！</p>
  Birthday (date and time):
  <input type="datetime" name="bdaytime"><hr/>

<p><b>datetime-local</b>-输入日期与时间-无时区，IE及Firefox不支持！</p>
  Birthday (date and time):
  <input type="datetime-local" name="bdaytime"><hr/>

<p><b>email</b>-输入邮箱地址，≤IE9不支持！</p>
  E-mail:
  <input type="email" name="email"><hr/>

<p><b>search</b>-用于搜索字段。</p>
  Search Google:
  <input type="search" name="googlesearch"><hr/>

<p><b>tel</b>-用于应该包含电话号码的输入字段，目前只有safari 8支持。</p>
  Telephone:
  <input type="tel" name="usrtel"><hr/>

<p><b>url</b>-用于应该包含URL地址的输入字段，≤IE9不支持！</p>
  Add your homepage:
  <input type="url" name="homepage"><hr/>
  
  <input type="submit"><hr/>
</form>
</body>
</html>
```
1. number：用于应该包含数字值的输入字段，可自定义数字限制，详见教程。
2. data: 用于应该包含日期的输入字段,日期也可定义输入限制。
3. color：用于应该包含颜色的输入字段。
4. range：用于应该包含一定范围内的值的输入字段，可用min、max、step、value属性规定限制。
5. month：选择月份和年份。
6. week：选择周和年。
7. time：选择时间-无时区。
8. datatime：选择日期与时间-有时区。
9. datetime-local：选择日期和时间-无时区。
10. email：用于应该包含电子邮件地址的输入字段，若浏览器支持，能够在被提交时自动对电子邮件地址进行验证，某些智能手机会识别email类型，并在键盘增加".com" 以匹配电子邮件输入。
11. search：用于搜索字段（搜索字段的表现类似常规文本字段）。
12. tel：用于应该包含电话号码的输入字段，目前只有safari 8支持。
13. url：用于应该包含URL地址的输入字段，若浏览器支持，能够在提交时自动验证url字符，某些智能手机识别url类型，并向键盘添加".com"以匹配url输入。

----------
**3、input元素其他属性**
1. value:规定字段的初始值。
2. readonly：规定输入字段只读。`readonly="readonly"`
3. disabled:规定输入字段是禁用的，被禁用的元素是不可用不可点击并且不可提交。`disabled="disabled"`
4. **size**：规定输入字段的尺寸，如果size="5"，那么一行中可输入无数个字符但**一行中只有5个可见字符**。
5. **maxlength**：规定输入字段允许的最大长度。如果maxlength="5"，那么**一行中最多可输入5个字符**。


----------
**注意：以下属性都支持Opera Safari Chrome Firefox IE9+**

**4.html 5为form元素新增的属性**
```html
<!DOCTYPE html>
<html>
<head>
	<title>html 5为form元素新增的属性</title>
	<style type="text/css"></style>
</head>
<body>
<h1>html 5为form元素新增的属性</h1>
<p><b>autocomplete-规定表单或输入字段是否应该自动完成./novalidate-规定在提交表单时不对表单数据进行验证。</b></p>
<form action="" method="get" autocomplete="on" method="post" novalidate="novalidate">
  First name:<input type="text" name="fname" /><br/>
  Last name: <input type="text" name="lname" /><br/>
  E-mail: <input type="email" name="email" autocomplete="off" /><hr/>
  <input type="submit"><hr/>
</form>
</body>
</html>
```
1. autocomplete:规定表单或输入字段是否应该自动完成。当`<form action="action_page.php" autocomplete="on">`时，浏览器会基于用户之前的输入值自动填写值。
**注意：**
autocomplete属性也适用于`<form>`以及如下`<input>`类型：text、search、url、tel、email、password、datepickers、range 以及 color。
格式例如：
`E-mail: <input type="email" name="email" autocomplete="off">`
2. novalidate:如果设置`novalidate="novalidate"`，则novalidate规定在提交表单时不对表单数据进行验证。

**html 5为input元素新增的属性**
```html
<!DOCTYPE html>
<html>
<head>
	<title>html 5为input元素新增的属性</title>
	<style type="text/css"></style>
</head>
<body>
<h1>html 5为input元素新增的属性</h1>
<form action="/example/html5/demo_form.asp" method="get" id="form1">
<p><b>autocomplete</b>-规定表单或输入字段是否应该自动完成</p>
  E-mail: <input type="email" name="email" autocomplete="off" /><hr/>

<p><b>autofocus</b>-如果设置`autofocus="autofocus"`，则当页面加载时input元素应该自动获得焦点.</p>
  E-mail: <input type="email" name="email" autofocus="autofocus" /><hr/>

<p><b>form</b>-如果使用form属性，form属性的值必须是所属表单的id。</p>
  First name: <input type="text" name="fname" /><hr/>

<p><b>formaction</b>-formaction会覆盖`form`元素的action属性。</p>
First name: <input type="text" name="fname" /><br />
Last name: <input type="text" name="lname" /><hr/>

<input type="submit" value="提交" /><br />
<input type="submit" formaction="/example/html5/demo_admin.asp" value="以管理员身份提交" />
</form>

<p>下面的 "Last name" 字段位于form元素之外，但仍然是表单的一部分。</p>
Last name: <input type="text" name="lname" form="form1" />

</form>
</body>
</html>
```
1. autocomplete:html5为form和input都增加了这个属性，用法相同。
2. autofocus:布尔属性，如果设置`autofocus="autofocus"`，则当页面加载时`<input>`元素应该自动获得焦点（即打开页面时光标自动自动闪烁于输入框内）。
3. form：规定`<input>`元素所属的一个或多个表单。使用了form属性后，哪怕输入字段位于form表单之外但仍属表单。如需引用一个以上的表单，使用空格分隔的表单id列表。
**注意：**form属性的值必须是所属表单的id。
如上面代码中，输入First name:111，Last name:222，得到的结果如下：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-a5421ad50501ff89.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
4. formaction:适用于 type="submit" 以及 type="image"。规定当提交表单时处理该输入控件的文件的URL,formaction属性覆盖`form`元素的action属性。
如上面代码中，输入First name:111，Last name:222，并分别点击“提交”按钮和“以管理员身份提交”按钮，得到的2个结果如下：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-d04f5f97425168b8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-acc4fc34f67c66b3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


----------

---------------------------------------------**以下继续是html5中input新增属性**


1. formenctype：仅针对`<form method="post">`的表单，且只适用于`<input type="submit">`以及`<input type="image">`，规定当把表单数据（form-data）提交至服务器时如何对其进行编码。formenctype覆盖`form`元素的enctype属性。
```html
<!DOCTYPE HTML>
<html>
<body>
<form action="/example/html5/demo_post_enctype.asp" method="post" enctype="application/x-www-form-urlencoded">
  First name: <input type="text" name="fname" /><br />
<input type="submit" value="提交" />
<input type="submit" formenctype="multipart/form-data" value="以 Multipart/form-data 编码提交" />
</form>
</body>
</html>
```
上例中，输入“world”，
form元素中enctype值（默认对字符编码）会被input元素中formenctype值（不进行编码）覆盖，点“提交”按钮效果如下：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-ae09236031b7b793.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)。
点“以 Multipart/form-data 编码提交” 按钮效果分别如下：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-da6f397b1ad47167.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3/7/2017 3:28:32 PM 
1. formmethod：适用于`<input type="submit">`以及`<input type="image">`，定义向action URL发送表单数据（form-data）的HTTP方法（get|post）。会覆盖 `<form>`元素的method属性。如下所示：
```html
<!DOCTYPE HTML>
<html>
<body>
<h1>html 5为input元素新增的属性formmethod</h1>
<form action="/example/html5/demo_form.asp" method="post">
  First name: <input type="text" name="fname" /><br />
  Last name: <input type="text" name="lname" /><br />
<input type="submit" value="提交" />
<input formaction="/example/html5/demo_form.asp" type="submit" formmethod="get" value="使用 POST 提交" />
</form>
</body>
</html>
```
在上面的代码中，分别输入First name:11，Last name:22，并分别点击“提交”按钮和“使用 POST 提交”按钮，得到的2个结果如下：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-a596c873557473e3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-4d14a46282e7c6fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
2. formnovalidate:用于`<input type="submit">`,布尔属性，和`<form>`元素的 novalidate 属性一样的功能，如果设置，规定在提交表单时不对input元素进行验证。formnovalidate属性覆盖`<form>`元素的 novalidate 属性。（即如果form元素中没有设置不验证，但input元素中设置了，则提交时不验证）
```html
<!DOCTYPE HTML>
<html>
<body>
<h1>html 5为input元素新增的属性formnovalidate</h1>
<form action="/example/html5/demo_form.asp" method="get">
E-mail: <input type="email" name="userid" /><br />
<input type="submit" value="提交" /><br />
<input type="submit" formnovalidate="formnovalidate" value="进行没有验证的提交" />
</form>
</body>
</html>
```
在上面的代码中，输入22222，并分别点击“提交”按钮和“进行没有验证的提交”按钮，得到的2个结果如下：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-c9199435516c3b68.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-3cca856a434a7151.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
3. formtarget:适用于`<input type="submit">`以及`<input type="image">`，指示在提交表单后在哪里打开页面。会覆盖 `<form>` 元素的 target 属性。
**说明：**若<form>元素中不设定target属性则默认值为_self,即在本页面中打开，此时在<input>元素中设定target="_blank",则点击提交按钮输入值会在新窗口中体现。
4. height和width：仅用于`<input type="image">`，用于规定input元素的高度和宽度，**始终要规定图像的尺寸**。
以下例子中将图片定义为提交按钮：
```html
<!DOCTYPE HTML>
<html>
<body>
<h1>html 5为input元素新增的属性height和width</h1>
<form action="/example/html5/demo_form.asp" method="get">
  First name: <input type="text" name="fname" /><br />
  Last name: <input type="text" name="lname" /><br />
  <input type="image" src="/i/eg_submit.jpg" alt="Submit" width="128" height="128"/>
</form>
<p><b>注释：</b>默认地，image输入类型会发生点击图像按钮时的 X 和 Y 坐标。</p>
</body>
</html>
```
**注意：** `<input type="image">`定义图像形式的提交按钮。且点击图片后服务器的返回值中会带有x和y的坐标，根据点击的位置不同返回的坐标也不同，可点击的范围就是图片的长和宽组成的矩形区域，如下图所示：
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-f41eb97342c3f6fc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
5. list：list引用的`<datalist>`为`<input>`预定义选项列表，起到提示作用（如代码中编写有三行分别为web，work，world，则在输入框中输入wo底下会自动出现work和world）。用户会在他们输入数据时看到预定义选项的下拉列表。
**注意：**`<input>`元素的list属性值必须与`<datalist>`元素的id属性值相同。
前面已讲过，在此不重复做笔记。
6. min和max：规定input元素的最小值和最大值。适用于如下输入类型：`<input type="number|range|date|datetime|datetime-local|month|time|week">`
7. multiple:布尔属性，适用于`<input type="email|file">`,如果设置，则允许用户在输入框中输入一个以上的值。
```html
<!DOCTYPE HTML>
<html>
<body>
<form action="/example/html5/demo_form.asp" method="get">
选择图片：<input type="file" name="img" multiple="multiple" />
<input type="submit" />
</form>
<p>请尝试在浏览文件时选取一个以上的文件。</p>
</body>
</html>
```
按住ctrl键同时选取很多文件。
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-b65717a49e1b8de5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
8. pattern:规定用于检查input元素的正则表达式。适用于如下输入类型：`<input type="text|search|url|tel|email|password">`，使用全局的title属性对模式进行描述以帮助用户。
```html
<!DOCTYPE HTML>
<html>
<body>
<h1>html 5为input元素新增的属性pattern</h1>
<form action="/example/html5/demo_form.asp" method="get">
国家代码：<input type="text" name="country_code" pattern="[A-z]{3}"
title="三个字母的国家代码" />
<input type="submit" />
</form>
<p><strong>注意：</strong></p>
<ul>
<li>pattern="[A-z]{3}表示的是只能输入大写/小写字母中的任意三个</li>
<li>pattern="[a-z]{3}表示的是只能输入小写字母中的任意三个</li>
<li>pattern="[A-Z]{3}表示的是只能输入大写字母中的任意三个</li>
</ul>
</body>
</html>
```
9. placeholder:规定用于描述输入字段预期值的提示（样本值或有关格式的简短描述）。该提示会在用户输入值之前显示在输入字段中。适用于如下输入类型：`<input type="text|search|url|tel|email|password">`。
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
10. required：布尔属性，如果设置，则规定在提交表单之前必须填写输入字段。适用于如下输入类型：`<input type="text|search|url|tel|email|password|date pickers|number|checkbox|radio|file">`。
```html
<!DOCTYPE HTML>
<html>
<body>
<h1>html 5为input元素新增的属性placeholder</h1>
<form action="/example/html5/demo_form.asp" method="get">
Name: <input type="text" name="usr_name" required="required" />
<input type="submit" value="提交" />
</form>
</body>
</html>
```
![图片说明文字](http://upload-images.jianshu.io/upload_images/6851923-badd9f86ce74b552.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
11. step:规定`<input>`元素的合法数字间隔,如果step="3"，则合法数字应该是 -3、0、3、6、等。只能是3的整数倍。可与max以及min属性一同使用，来创建合法值的范围。适用于如下输入类型：`<input type="number|range|date|datetime|datetime-local|month|time|week">`.


#### 布尔属性专题 ####：
主要出现于表单元素上，是一种固有属性，在html中只要设置了布尔属性，不管写成`<input multiple>`还是`<input multiple="multiple">`,这两个意思相同，并且只要写了就认为其值为true。

- required:必须输入字段。
- multiple:允许多选，可按住ctrl选择。
- formnovalidate:规定在提交表单时不对input元素进行验证。
- autofocus:当页面加载时`<input>`元素应该自动获得焦点（即打开页面时光标自动自动闪烁于输入框内）。
- checked:预选中。所有表单元素都有这个属性弹只有radio和checkbox能在图形上表现出勾选的效果，其name和value属性就可以提交。
- selected:option的属性，一旦选上就呈现高亮状态，并将其name和value属性提交。
- readonly:只读。
- disabled:所有表单元素都支持disabled属性，让表单元素蒙上一个灰白色调，用户无法操作也不会提交其内容。
- hidden:效果等同于"display:no"优先级低于CSS，了解就行。
- contenteditable:应用于所有可见的非表单元素，让元素也像input一样编辑它里面的内容。
- noshade:用来表示无阴影，显现为纯色，多用于`<hr/>`。
- open:规定打开状态。
- controls:指定音视频控件的显示方式。提供添加播放、暂停和音量控件
- autoplay：指定音视频自动播放。
- loop：当媒介文件完成播放后再次开始播放。
- preload:如果出现该属性，则视频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。
- defer:只适用于.js外部脚本文件，表示告诉浏览器立即下载但脚本可**延迟到文档完全被解析**，即`</html>`之后再执行。
- async:只适用于.js外部脚本文件，表示告诉浏览器立即下载，表示不必等待其他脚本下载和执行，从而**异步加载页面其他内容**。
