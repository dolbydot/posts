## 一、输入网址
如：**`baidu.com`**

----------
## 二、[DNS](https://zh.wikipedia.org/wiki/%E5%9F%9F%E5%90%8D%E7%B3%BB%E7%BB%9F)（Domain Name Server-域名服务器）解析
# 
互联网上设备通信都要遵循IP协议，它规定了每台设备都要有唯一的[IP地址](https://zh.wikipedia.org/wiki/IP%E5%9C%B0%E5%9D%80)，单纯数字的IP地址难以记忆，于是产生了用户更方便记忆的由字符构成的域名，为了方便性和可用性，DNS解析实现了域名到对应IP地址的转换，而DNS的本质就是一组键值对，键名就是域名，如www.baidu.com，值就是IP地址，如119.75.217.109。对于用户来说，DNS解析实际上就是寻找哪台机器上有你需要的资源的过程。
# 
> DNS查询有两种方式：递归和迭代。
DNS客户端设置使用的DNS服务器一般都是递归服务器，负责全权处理客户端的DNS查询请求，直到返回最终结果。
DNS服务器之间一般采用迭代查询方式。

我们只需要了解DNS递归查询。
# 
 1. 浏览器缓存：用户在浏览器输入www.baidu.com，如果之前访问过该主机且未超过浏览器的缓存时间，可直接使用浏览器缓存的DNS。
 2. 系统缓存：如果浏览器缓存里没有记录，浏览器会做系统调用，获取系统中的缓存记录。
 3. 路由器缓存：如果系统缓存中同样没有记录，需要继续查找路由器缓存。
 4. 互联网服务提供商（ISP）的缓存：路由器中未找到记录会继续查找ISP中的缓存。
 5. 若以上本地DNS中都没有缓存记录，那么就会开始DNS递归搜索。首先本地DNS向[根域名服务器](https://zh.wikipedia.org/wiki/%E6%A0%B9%E7%B6%B2%E5%9F%9F%E5%90%8D%E7%A8%B1%E4%BC%BA%E6%9C%8D%E5%99%A8)发出请求，无结果。*注意：**`www.baidu.com`**的**网址实际上是`www.baidu.com.`**，com后的**`.`**对应的就是根域名服务器，只是默认情况下所有网址最后一位都是**`.`**，为了方便用户通常都省略，浏览器请求DNS时会自动加上*。
 6. 本地DNS向**`com`**顶级域名服务器发出请求，无结果。
 7. 本地DNS向**`baidu.com`**权威域名服务器发出请求，无结果。
 8. 本地DNS向**`www.baidu.com`**域名服务器发出请求，www.baidu.com域名服务器查到了对应的IP地址119.75.217.109并将地址反馈给了本地DNS，本地DNS得到了这个IP地址，存入自身缓存并反馈给了浏览器。
# 
**注意**：

 - 网址的解析是一个从右向左的过程，看似步骤繁多，实际完成这一系列行为只需要几毫秒的时间。
 - DNS返回的IP地址并不是每次都一样，真实的互联网世界背后存在成千上万台服务器甚至更多，用户只需要服务器处理他的需求而并不在意是哪台机器完成了这一过程，所以DNS能做的就是返回一个合适的机器IP给用户以达到DNS负载均衡，又叫做重定向。
  
----------
## 三、浏览器与服务器通过三次握手（SYN,SYN/ACK,ACK）建立TCP连接
Q：**为什么是三次握手而不是两次握手或四次握手或更多呢？**
A：**三次握手更为稳妥**。
# 
故事一：
革命战争影片中，呼号为黄河的一方想找呼号叫长江的一方说事，于是观众会听到这么一段对话：

> “长江长江，我是黄河，听到请回答。”
“黄河黄河，我是长江，我听到了你，请回答。”
“长江长江，我是黄河，我听到了你，现在请你收报。”

 1. 第一次握手：黄河发起呼叫，长江收到了。这时长江可以确认的是，黄河的发信机和自己的收信机是好的，否则的话他收不到长江的呼叫；黄河能确认什么呢？他什么也不能确认，有可能自己的电台除了指示灯是好的，其它都是坏的，他在对着一台铁疙瘩发功。
 2. 第二次握手：长江回应，黄河收到了。这时黄河可以确认的是，自己和长江的收发信机都是好的，否则的话他收不到长江的回应信号。这时黄河可以说正事了吗？还不能，虽然长江发出了回应，但他并不能确认自己的发信机和黄河的收信机都是好的。
 3. 第三次握手：黄河对长江的回应进行回应。这时黄河很清楚，双方收发信机都是好的，自己的这次回应长江肯定能收到，这个回应的目的只是消除长江对黄河的收信机和长江自己的发信机的担心。然后，黄河不必等长江的再次回应就可以说正事。
# 
故事二：
> **战争态势：**驻扎在两个山头上的红1团和红2团分别有两个营，而在山谷的蓝团有三个营，若红1团和红2团孤军下山作战会失败，而两个团同时进攻就会胜利，对于红方来说，问题的关键是要同时发起进攻。
**战争准备过程：**红1团团长找了个传令兵，命令他跑到红2团，告诉红2团团长明早9时发起进攻。传令兵没有被蓝团俘虏，成功地跑到了红2团的山头，告诉红2团团长明早9时两个团同时进攻。红2团团长一边握着传令兵的手激动地说“太好了！我早就等着这个消息呢！”，一边心里暗自核计“虽然我知道了这个消息，但是红1团的团长并不知道我已经知道了，谁都知道传令兵有可能被俘，消息很有可能传不过来，若明天总攻前，红1团团长不知道我已经得到了消息，他一定不会贸然进攻的，换成我也不会”。于是，红2团团长对传令兵说“兄弟，你辛苦了，先抽袋烟吧，抽完后再辛苦你跑回去，告诉你们团长，说我已经得到消息了，明天按时进攻。”
传令兵又跑回到红1团，侥幸又没被蓝团俘获，他告诉红1团团长有关红2团团长已经获知明早进攻的消息，但红1团团长明早敢发起攻击吗？他不敢，因为他心里清楚，红2团团长并不知道他（红1团团长）已经知道了“红2团团长已获知明早9时发起攻击”这个消息，红1团团长继续想，如果是他本人是红2团团长，就不会贸然攻击，因为自己已经获知明早9时发起攻击这件事，对方未必知道，而有可能因为传令兵回团时被抓，敌人反而知道了，自己贸然攻击，有可能就会失败。于是，红1团团长对传令兵说“兄弟，你辛苦了，先抽袋烟吧，抽完后再辛苦你跑一趟红2团，告诉他们团长，就说我已经知道他已经知道了明早9点进攻这件事，让他放心地打吧。”
写到这里你已经猜到了，即使传令兵再次来到红2团，红2团团长也不敢开战，还是要传令兵再次回红1团报信，因为红2团团长担心红1团团长不知道他（红2团团长）已经知道了红1团团长知道他（红2团团长）知道明早9点发生攻击的事。

# 
回到三次握手问题上，红1团和红2团其实就是通信的双方，这场永远也达不成协议的战斗，说明了一个重要的通信道理：**世界上不存在完全可靠的通信协议。三次握手成功后，握手成功后的设备故障、干扰或话务员死亡等无数种可能性会导致通信失败，三次握手成功只说明了之前的通信条件和环境，而不能决定和预测之后的通信条件和环境，通信协议只能做到尽可能的可靠，而不能做到理论上的完全可靠。**
# 
言归正传：谢希仁版《计算机网络》中的例子是这样的，“已失效的连接请求报文段”的产生在这样一种情况下：client发出的第一个连接请求报文段并没有丢失，而是在某个网络结点长时间的滞留了，以致延误到连接释放以后的某个时间才到达server。本来这是一个早已失效的报文段。但server收到此失效的连接请求报文段后，就误认为是client再次发出的一个新的连接请求。于是就向client发出确认报文段，同意建立连接。假设不采用“三次握手”，那么只要server发出确认，新的连接就建立了。由于现在client并没有发出建立连接的请求，因此不会理睬server的确认，也不会向server发送数据。但server却以为新的运输连接已经建立，并一直等待client发来数据。这样，server的很多资源就白白浪费掉了。采用“三次握手”的办法可以防止上述现象发生。例如刚才那种情况，client不会向server的确认发出确认。server由于收不到确认，就知道client并没有要求建立连接。”这个例子很清晰的阐释了“三次握手”对于建立可靠连接的意义。

----------
## 四、浏览器向web服务器发送HTTP请求
发送HTTP请求的过程就是构建HTTP请求报文并通过TCP协议中发送到服务器指定端口(HTTP协议80/8080, HTTPS协议443)。
# 
**HTTP请求报文是由三部分组成: 请求行, 请求报头和请求正文。**

 - **请求行：**
格式：`Method Request-URL HTTP-Version CRLF`
例子：`GET index.html HTTP/1.1`
常用的方法有: GET, POST, PUT, DELETE, OPTIONS, HEAD, TRACE，一般的浏览器只能发起GET或POST请求。
（1）GET
当我们通过在浏览器的地址栏中直接输入网址的方式去访问网页的时候，浏览器默认采用的就是 GET 方法向服务器获取资源。但用GET方法提交的表单数据只经过了简单的编码，同时它将作为URL的一部分向服务器发送，而URL具有长度限制，即GET方式提交的数据大小有限制，如`<Http://localhost/login.php?username=aa&password=1234>`，很容易辨认出表单提交的内容，因此，如果使用GET方法来提交表单数据就存在着安全隐患。
（2）POST
是GET的一个替代方法，主要是向Web服务器提交表单数据，尤其是大批量的数据。POST方法克服了GET方法的一些缺点。通过POST方法提交表单数据时，数据不是作为URL请求的一部分而是作为标准数据放在HTTP的body中传送给Web服务器，这就克服了GET方法中的信息无法保密和数据量太小的缺点。因此，出于安全的考虑以及对用户隐私的尊重，通常表单提交时采用POST方法。
（3）HEAD
HEAD 方法与 GET 方法几乎是相同的，它们的区别在于 HEAD 方法只是请求消息报头，而不是完整的内容。对于 HEAD 请求的回应部分来说，它的 HTTP 头部中包含的信息与通过 GET 请求所得到的信息是相同的。利用这个方法，不必传输整个资源内容，就可以得到 Request-URI 所标识的资源的信息。这个方法通常被用于测试超链接的有效性，是否可以访问，以及最近是否更新。
**注意：**在 HTML 文档中，书写 get 和 post，大小写都可以，但在 HTTP 协议中的 GET 和 POST 只能是大写形式。
# 
 - **请求报头**：允许客户端向服务器传递请求的附加信息和客户端自身的信息。
客户端不一定特指浏览器，有时候也可使用Linux下的CURL命令以及HTTP客户端测试工具等。
常见的请求报头有:` Accept, Accept-Charset, Accept-Encoding, Accept-Language, Content-Type,Connection, Authorization, Cookie, User-Agent`等。Accept用于指定客户端用于接受哪些类型的信息，Accept-Encoding与Accept类似，它用于指定接受的编码方式。Connection设置为Keep-alive用于告诉客户端本次HTTP请求结束之后并不需要关闭TCP连接，这样可以使下次HTTP请求使用相同的TCP通道，节省TCP连接建立的时间，keep-alive不会永久保持连接，可在不同的服务器软件中设定这个时间。
# 
 - **请求正文：**当使用POST, PUT等方法时，通常需要客户端向服务器传递数据。这些数据就储存在请求正文中。在请求报头中有一些与请求正文相关的信息，例如: 现在的Web应用通常采用Rest架构，请求的数据格式一般为json。这时就需要设置`Content-Type: application/json`。

----------
## 五、服务器处理请求并返回HTTP报文
后端从在固定的端口接收到TCP报文开始，会对TCP连接进行处理，对HTTP协议进行解析，并按照报文格式进一步封装成HTTP Request对象，供上层使用。
# 
**HTTP响应报文是由三部分组成: 状态行, 响应报头和响应报文。**

 - **状态行**：包含协议版本、状态描述、状态代码。
格式：`HTTP-Version Status-Code Reason-Phrase CRLF`
示例：`HTTP/1.1 200 OK`
协议版本：使用http1.0还是其他版本
状态描述：给出了关于状态代码的简短的文字描述。比如状态代码为200时的描述为 ok
状态代码：由三位数组成，第一个数字定义了响应类别，且有五种可能取值。
 1XX：指示信息–表示请求已接收，继续处理。
 2xx：成功–表示请求已被成功接收、理解、接受。
 3xx：重定向–要完成请求必须进行更进一步的操作。
 4xx：客户端错误–请求有语法错误或请求无法实现。
 5xx：服务器端错误–服务器未能实现合法的请求。

**平时遇到比较常见的状态码有:200, 204, 301, 302, 304, 400, 401, 403, 404, 422, 500。**

其中：301表示永久重定向响应，这样浏览器就会访问 http://www.baidu.com 而不是http://baidu.com ，服务器一定要重定向而不是直接发送用户想看的网页内容的原因如下：
1、搜索引擎的排名——如果一个页面有两个地址，就像 http://www.yy.com 和 http://yy.com ，搜索引擎会认为它们是两个网站，结果造成每个搜索链接都减少从而降低排名。而搜索引擎知道301永久重定向是什么意思，这样就会把访问带 www 的和不带 www 的地址归到同一个网站排名下，同时让访客自动跳转到主站点。
2、缓存友好性——当一个页面有好几个名字时，它可能会在缓存里出现好几次，造成缓存友好性变差。
3、网站调整——如改变网页目录结构。
4、网站被移到一个新地址。
5、网页扩展名改变——如应用需要把.php改成.html或.shtml。
在3、4、5这三种情况下如果不做重定向，用户收藏夹或搜索引擎数据库中旧地址只能让访客得到一个404页面错误信息，流量白白丧失。
# 
**301和302的区别：**
301和302状态码都表示重定向。
共同点：
浏览器在拿到服务器返回的这个状态码后会自动跳转到一个新的 URL 地址，这个地址可以从响应的 Location 首部中获取（用户看到的效果就是他输入的地址 A 瞬间变成了另一个地址 B）。
不同点：
301：永久重定向——表示旧地址 A 的资源已经被永久移除（这个资源不可访问了），搜索引擎在抓取新内容的同时也将旧的网址交换为重定向之后的网址。使用301状态码进行页面跳转的大致场景如下：
（1）域名到期不想续费（或者发现了更适合网站的域名），想换个域名。
（2）在搜索引擎的搜索结果中出现了不带www的域名，而带www的域名却没有收录，这个时候可以用301重定向来告诉搜索引擎我们目标的域名是哪一个。
（3）空间服务器不稳定，换空间的时候。
302：临时重定向——表示旧地址 A 的资源还在（仍然可以访问），这个重定向只是临时地从旧地址 A 跳转到地址 B，搜索引擎会抓取新的内容而保存旧的网址。
此时浏览器知道了正确的访问地址，会向服务器发送另一个http请求。
# 
 - **响应报头**：由关键字：值对组成，每行一对。
HTTP最常见响应报头如下：
**1、Cache头域**
（1）Date：
作用：生成消息的具体时间和日期，即当前的GMT时间。
例如：`Date: Sun, 17 Mar 2013 08:12:54 GMT`
（2）Expires：
作用: 浏览器会在指定过期时间内使用本地缓存，指明应该在什么时候认为文档已经过期，从而不再缓存它。
例如: `Expires: Thu, 19 Nov 1981 08:52:00 GMT`　　
（3）Vary
作用：告诉缓存服务器按照Vary指定的头的内容分别缓存不同的版本，
例如: `Vary: Accept-Encoding`，根据Accept-Encoding头值的不同缓存不同的版本，Accept-Encoding的值也作为参数计算hash，如果客户端直接访问源服务器，Vary就没有意义了。
**2、Cookie/Login 头域**
（1）P3P
作用: 用于跨域设置Cookie, 这样可以解决iframe跨域访问cookie的问题
例如: `P3P: CP=CURa ADMa DEVa PSAo PSDo OUR BUS UNI PUR INT DEM STA PRE COM NAV OTC NOI DSP COR`
（2）Set-Cookie
作用： 非常重要的header, 用于把cookie 发送到客户端浏览器， 每一个写入cookie都会生成一个Set-Cookie.
例如: `Set-Cookie: PHPSESSID=c0huq7pdkmm5gg6osoe3mgjmm3; path=/`
**3、Entity实体头域：**
实体内容的属性，包括实体信息类型，长度，压缩方法，最后一次修改时间，数据有效性等。
（1）ETag：
作用: 和If-None-Match 配合使用。 （实例请看上节中If-None-Match的实例）
例如: `ETag: “03f2b33c0bfcc1:0”`
（2）Last-Modified：
作用： 用于指示资源的最后修改日期和时间。（实例请看上节的If-Modified-Since的实例）
例如: `Last-Modified: Wed, 21 Dec 2011 09:09:10 GMT`
（3）Content-Type：
作用：WEB服务器告诉浏览器自己响应的对象的类型和字符集,
例如:
`Content-Type: text/html; charset=utf-8
Content-Type:text/html;charset=GB2312
Content-Type: image/jpeg`
（4）Content-Length：
指明实体正文的长度，以字节方式存储的十进制数字来表示。在数据下行的过程中，Content-Length的方式要预先在服务器中缓存所有数据，然后所有数据再一股脑儿地发给客户端。
例如: `Content-Length: 19847`
（5）Content-Encoding：
作用：文档的编码（Encode）方法。一般是压缩方式。
WEB服务器表明自己使用了什么压缩方法（gzip，deflate）压缩响应中的对象。利用gzip压缩文档能够显著地减少HTML文档的下载时间。
例如：`Content-Encoding：gzip`
（6）Content-Language：
作用： WEB服务器告诉浏览器自己响应的对象的语言者
例如：`Content-Language:da`
**4、Miscellaneous 头域**
（1）Server：
作用：指明HTTP服务器的软件信息
例如: `Apache/2.2.8 (Win32) PHP/5.2.5`
（2）X-Powered-By：
作用：表示网站是用什么技术开发的
例如：`X-Powered-By: PHP/5.2.5`
**5、Transport头域**
（1）Connection：
例如：`Connection: keep-alive` 当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，如果客户端再次访问这个服务器上的网页，会继续使用这一条已经建立的连接
例如： `Connection: close` 代表一个Request完成后，客户端和服务器之间用于传输HTTP数据的TCP连接会关闭， 当客户端再次发送Request，需要重新建立TCP连接。
**6、Location头域**
（1）Location：
作用： 用于重定向一个新的位置， 包含新的URL地址
# 
 - **响应正文**：服务器返回给浏览器的文本信息，通常HTML，CSS，JS，图片等文件就放在这一部分。

----------
## 六、浏览器缓存、解析并渲染页面
**浏览器缓存**：包括页面html缓存和图片、js、css、flash等资源的缓存。
**解析和渲染**：显示页面是一个从上往下边解析边渲染的过程，首先浏览器解析HTML文件构建DOM树，先执行head标签里的内容，再执行body里的，一行行渲染下去，然后解析CSS文件构建规则树，解析完成后浏览器引擎会通过DOM树和CSS规则树来构造渲染树，等到渲染树构建完成，盒模型位置、大小、颜色、字体等确认下来后，浏览器开始布局渲染树并将其绘制到屏幕上。
# 
JS的解析是由浏览器中的JS解析引擎完成的，JS是单线程运行，同一个时间内只能做一件事，所有的任务都需要排队，前一个任务结束，后一个任务才能开始。但某些任务比较耗时，所以需要一种机制可以先执行排在后面的任务，这就是：同步任务和异步任务。JS的执行机制就可以看做是一个主线程加上一个任务队列。同步任务就是放在主线程上执行的任务，异步任务是放在任务队列中的任务。所有的同步任务在主线程上执行，形成一个执行栈;异步任务有了运行结果就会在任务队列中放置一个事件；脚本运行时先依次运行执行栈，然后会从任务队列里提取事件，运行任务队列中的任务，这个过程是不断重复的，所以又叫做事件循环。
# 
浏览器在解析过程中，如果遇到请求外部资源时，如图像、JS等。浏览器将下载该资源。请求过程是异步的，并不会影响HTML文档进行加载，但是当文档加载过程中遇到JS文件，HTML文档会挂起渲染过程，不仅要等到文档中JS文件加载完毕还要等待解析执行完毕，才会继续HTML的渲染过程。原因是因为JS有可能修改DOM结构，这就意味着JS执行完成前，后续所有资源的下载是没有必要的，这就是JS阻塞后续资源下载的根本原因，即无论当前JS代码是内嵌还是在外部文件中，页面的下载和渲染都必须停下来等待脚本执行完成，JS执行过程越久，浏览器等待响应用户输入的时间就越长，所以尽量把JS放在底部可以起到性能优化效果，除此之外还可通过设置script标签的defer或async属性、合并脚本等方法进行优化。
# 
CSS文件的加载不影响JS文件的加载，但是却影响JS文件的执行。JS代码执行前浏览器必须保证CSS文件已经下载并加载完毕。
# 
**注意：**以上整个解析和渲染过程中会涉及到reflows（回流）和repaints（重绘）的概念，就某些浏览器如Opera而言，大部分的reflow将导致页面重新渲染，其变化涉及到部分甚至是整个页面的布局，而repaint则导致浏览器必须验证DOM树上其他节点元素的可见性。reflow和repaint过程非常消耗性能，尤其在移动设备上，会破坏用户体验，造成页面卡顿，所以应尽可能减少reflow和repaint。

**导致回流的原因**：

 1. 调整窗口大小
 2. 改变字体
 3. 增加或移除样式表
 4. 内容变化，如在input框中输入文字
 5. 激活CSS伪类，如hover
 6. 操作class属性
 7. 脚本操作DOM
 8. 计算offsetWidth和offsetHeight属性
 9. 设置style属性的值

**如何避免回流或将它们对性能的影响降到最低：**

 1. 尽可能在DOM树最末端通过改变元素的class名的方式设定元素的样式：回流会顺行或逆行传递给周围的节点，在DOM树里改变class限制了回流的范围，使其影响尽可能少的节点。
 2. 避免设置多项内联样式：因为每个内联样式都会造成回流，样式应合并在一个外部类，这样当该元素的class属性被操控时只会产生一个回流。
 3. 应用元素的动画使用position属性的absolute或fixed值：这样设置不影响其他元素的布局，只会导致重绘而不是完整回流。
 4. 牺牲平滑度换取速度：你可能想每次1px移动一个动画，但是此动画及随后的回流使用了100%的CPU，动画看上去就会是跳动的，因为浏览器正在与更新回流做斗争。而动画元素每次移动3px，在非常快的机器上看起来平滑度低了，但它不会导致CPU在较慢的机器和移动设备中抖动。
 5. 避免使用table布局：table是个和罕见的可以影响在它们之前已经进入的DOM元素的显示的元素。想象一下，因为表格最后一个单元格的内容过宽而导致纵列大小完全改变。这就是为什么所有的浏览器都逐步地不支持table表格的渲染。另外一个原因说明表格布局很糟糕，根据Mozilla，一些小的变化将导致表格(table)中的所有其他节点回流。
 6. 避免使用CSS的JS表达式：因为他们每次都重新计算全部或部分文档而导致每秒产生成千上万次回流。
 7. 设置`box-sizing: border-box;`把标准盒模型转换为IE盒模型，告诉浏览器去理解你设置的边框和内边距的值是包含在width内的。设置后，即使padding或者border发生了改变，盒子宽高不会发生变化，只会重绘，不会回流。

----------

## 七、连接结束
以上是在浏览器中输入一个URL到页面展现的过程。
服务器发给浏览器的文件中会带有 Expires（有效期） 或 Cache-Control（缓存控制） 说明文件什么时候失效，有效期内浏览器直接使用本地文件,不发请求。服务器响应中会带有文件的最后修改时间或 Etag，浏览器发送重复请求会带上这些信息，服务器判断没有变化会发送304状态码，让浏览器使用本地缓存。

----------

*参考资料：*

 - [*从URL到页面加载发生了什么*](https://segmentfault.com/a/1190000006879700)
 - [*从URL到页面展现发生了什么*](http://blog.leanote.com/post/mr_jiangjun/%E4%BB%8EURI%E5%88%B0%E9%A1%B5%E9%9D%A2%E5%B1%95%E7%8E%B0%E5%8F%91%E7%94%9F%E4%BA%86%E4%BB%80%E4%B9%88)
 - [*维基百科-域名系统*](https://zh.wikipedia.org/wiki/%E5%9F%9F%E5%90%8D%E7%B3%BB%E7%BB%9F)
 - [*通信协议中三次握手的故事*](http://blog.sina.com.cn/s/blog_624f70600100he7u.html)
 - [*HTTP-请求、响应、缓存*](https://cnbin.github.io/blog/2016/02/20/http-qing-qiu-,-xiang-ying-,-huan-cun/)
 - [*张鑫旭-回流与重绘：CSS性能让JavaScript变慢？*](http://www.zhangxinxu.com/wordpress/2010/01/%E5%9B%9E%E6%B5%81%E4%B8%8E%E9%87%8D%E7%BB%98%EF%BC%9Acss%E6%80%A7%E8%83%BD%E8%AE%A9javascript%E5%8F%98%E6%85%A2%EF%BC%9F/)

# 
*推荐资料：*

 - [*HowDNS漫画*](https://howdns.works/episodes/)