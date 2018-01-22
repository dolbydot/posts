首先看一个客户端发起http请求到服务端返回响应结果的过程：

![图源网](http://upload-images.jianshu.io/upload_images/6851923-4aeb81279dc21667.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Node.js
##### 为什么要使用Node.js?
Node.js 的目的是实现动态网页，也就是说由服务器动态生成 HTML 页面。之所以要这么做，是因为静态 HTML  的可扩展性非常有限，无法与用户有效交互，同时如果有大量相似的内容，例如产品介绍页面，那么1000个产品就要1000个静态的 HTML 页面，维护这1000个页面简直是一场灾难，因此动态生成 HTML  页面的技术应运而生。

Node.js可跳过 HTTP 服务器，因为它本身就是，Node.js 提供了 http 模块，它是由C++  实现的，性能可靠，可以直接应用到生产环境。

Node.js 和其他的语言相比的另一个显著区别，在于它的原始封装程度较低。在 Node.js  中，很多工作需要你自己来做，而自己来做这些事情太过麻烦，而且也没有必要重复造轮子，所以需要第三方框架来帮助我们。

##### 安装 [Node.js](https://nodejs.org/)

##### 用Node.js创建一个应用
在没有Express的时候，我们要创建一个web应用，用Node.js怎样实现呢？
- 新建一个目录，进入此目录并初始化
```
$ mkdir myapp && cd myapp
$ npm init -y
```

![](http://upload-images.jianshu.io/upload_images/6851923-72a4ed422553d552.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 创建index.js文件
`$ touch index.js`

- 在index.js文件下添加如下代码用于引入http模块并创建一个服务器，监听3001端口。
```
const http = require('http')
const log = console.log
const err = console.error

http.createServer((req, res) => res.end('hello world!'))
    .listen(3001, () => log('server started'))
```
- 运行`node index.js`，终端显示'server started'，证明服务启动成功

![](http://upload-images.jianshu.io/upload_images/6851923-5f9d1dba01e83f70.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 在浏览器中打开`http://localhost:3001/`，页面显示`'hello world!'`，至此一切正常。
![](http://upload-images.jianshu.io/upload_images/6851923-47908ea8f8194660.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

但实际的应用开发中不可能只是让页面显示一句话这么简单，我们需要了解各种参数及其用法以应对更为复杂的使用场景。

上面的代码中，req是http.IncomingMessage的实例，代表的是服务器接收到的请求，res是http.ServerResponse的实例，代表服务器响应的结果。

req上常见的属性有：
> 1. url: `/` 、`/write`、 `/post`
> 2. method: `get` 、`post` 、`delete` 、`put` 、`options`
> 3. METHODS  支持的方法
> 4. STATUS_CODES 

res上的常见操作有：
> 1. res.end([data][,encoding][,callback])
> 2. res.getHeader(name)
> 3. getHeaders()
> 4. setHeader(name,value)
> 5. res.statusCode
> 6. res.write(chunk[,encoding][,callback])

以req.url为例：
```
http.createServer((req, res) => {
    if (req.url === '/') {
        res.end('hey index')
    } else if (req.url === '/write') {
        res.end('hey write')
    } else if (req.url === '/post') {
        res.end('hey post')
    }
}).listen(3000, e => {
    if (e) {
        err(e)
    } else {
        log('server started')
    }
})
```
重启node，打开浏览器，页面内容根据url值的变化而变化

![](http://upload-images.jianshu.io/upload_images/6851923-31786e962a965e32.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-18865338362b39c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-918c5c8509d617e8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

实际应用中大部分的url对应的不是简单的一句话，而是某一个文件，所以我们需要引入fs模块实现文件级操作。

在项目根目录下新建static文件夹，在static文件夹下新建a.js，b.js，内容如下
```
# a.js
console.log('I am a.js')
```
```
# b.js
console.log('I am b.js')
```

注释掉index.js之前的所有代码，现在的代码如下：
```
const http = require('http')
const fs = require('fs')
const log = console.log
const err = console.error

http.createServer((req, res) => {
    if (req.url === '/a.js') {
        fs.createReadStream('./static/a.js').pipe(res)
    } else if (req.url === '/b.js') {
        fs.createReadStream('./static/b.js').pipe(res)
    }
}).listen(3000, e => {
    if (e) {
        err(e)
    } else {
        log('server started')
    }
})
```
启动node，分别打开http://localhost:3000/a.js和http://localhost:3000/b.js

![](http://upload-images.jianshu.io/upload_images/6851923-51df9ee50654ef3e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-bc56539c091907ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以看到页面上显示出了a.js和b.js的内容，而不是在控制台打印出console.log里的内容，原因在于createReadStream()方法用于打开文本文件创建一个读取操作的数据流，实现原理是每次发送触发一个data事件，发送结束触发end事件，即文本中的内容会被装在res.end()中，原样显示到对应url的页面上。

### Express
##### 为什么要使用Express作为开发框架呢？
Express是基于 [Node.js](http://nodejs.org/) 平台，快速、开放、极简的 web 开发框架，它提供一系列强大的特性用来创建各种 Web 和移动设备应用，拥有丰富的 HTTP 快捷方法和任意排列组合的 Connect 中间件。

Express 不对 Node.js 已有的特性进行二次抽象，只是在它之上扩展了 Web 应用所需的基本功能，例如：
- 路由控制
- 路由处理器（中间件）
- 模板引擎
- 静态文件服务
- 错误处理
- 访问日志
- 缓存
- 动态视图
- 用户会话
- CSRF保护
- 插件支持

上述功能中我们用得比较多的是前6个。

需要说明的是Express只是一个轻量级的 Web   框架，多数功能只是对 HTTP  协议中常用操作的封装，更多的功能需要插件或者整合其他模块来完成。

用 Express 实现的网站实际上就是一个 Node.js 程序，因此可以直接运行。

##### 安装
`npm install express --save`

##### 路由
路由是指如何定义应用的端点（URIs）以及如何响应客户端的请求。

路由是由一个 URI、HTTP 请求（GET、POST等）和若干个句柄组成，它的结构如下： `app.METHOD(path, [callback...], callback)`， `app` 是 `express` 对象的一个实例， `METHOD` 是一个 [HTTP 请求方法](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)， `path` 是服务器上的路径， `callback` 是当路由匹配时要执行的回调函数。

- 基本的路由示例
```
# express-index.js
const express = require('express')
const app = express()
const log = console.log
const err = console.error

app.get('/',(req,res)=>res.send('hey dolby'))
app.listen(3000,()=>log('server listening at localhost:3000'))
```
运行`node express-index.js`启动程序

![](http://upload-images.jianshu.io/upload_images/6851923-fe5abc1c73e1fd31.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在浏览器中打开localhost:3000

![](http://upload-images.jianshu.io/upload_images/6851923-f1b456b497c60111.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 正则匹配
`app.get(/.*dot$/, (req, res) => res.send('.*dot'))`
匹配所有以dot结尾的字符串
重启服务器并打开localhost:3000/hellodot

![](http://upload-images.jianshu.io/upload_images/6851923-bef00edf91bbe7f8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 路由参数
```
app.get('/users/:userId/books/:bookId', (req, res) => res.send(req.params))
app.get('/users/:userId(\\d+)', (req, res) => res.send(req.params))
```

:userId只是一个占位符，代表users后的参数，其后的(\\d+)表示只接收整数参数，注意有两个`\`，第一个用于转义。生命不息，采坑不止。

![](http://upload-images.jianshu.io/upload_images/6851923-b0597c877f737f73.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-9d6f8fcd811b0d33.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-c9d1be5fa974778f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 中间件
1. **使用多个回调处理路由**，注意回调函数中多了参数next，也别忘了后面的next()
```
app.get('/eat/:eatSomething', (req, res, next) => {
    if (req.params.eatSomething === 'eatEverything') {
        res.end('Hey you eat too much')
    } else {
        next()
    }
}, function (req, res) {
    res.send('Hello')
})
```
重启node并修改url

![](http://upload-images.jianshu.io/upload_images/6851923-03d0d5d6707ada41.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-6ed5fe03c19edac7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. **使用回调函数数组处理路由**
```
var mw0 = (req, res, next) => {
    log('mw0')
    next()
}

var mw1 = (req, res, next) => {
    log('mw1')
    next()
}

var mw2 = (req, res, next) => {
    log('mw2')
    res.send('finish')
}

app.get('/example/mw', [mw0, mw1, mw2])
```
重启node并修改url为http://localhost:3000/example/mw

![](http://upload-images.jianshu.io/upload_images/6851923-1e360af7ac15f039.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-6d2a3dd71c457700.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

3. **混合使用回调函数数组和回调函数处理路由**
```
var mw0 = (req, res, next) => {
    log('mw0')
    next()
}

var mw1 = (req, res, next) => {
    log('mw1')
    next()
}

app.get('/example/mw', [mw0, mw1], (req, res, next) => {
    log('mw2')
    next()
}, (req, res) => {
    log('mw3')
    res.send('finish')
})
```
重启node并刷新浏览器页面

![](http://upload-images.jianshu.io/upload_images/6851923-4e2315fd57735456.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-6d2a3dd71c457700.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- route路由（这种基本用不到）
get方法接收的是一个回调函数
```
app.route('/book')
    .get((req, res) => {
        res.end('hello book')
    }).post(function (req, res) {
        res.send('Add a book');
    }).put(function (req, res) {
        res.send('Update the book');
    })
```
重启node并修改url为http://localhost:3000/book

![](http://upload-images.jianshu.io/upload_images/6851923-8bac2c58bd9282a3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- express.Router()类及app.use(挂载点,中间件)
使用 express.Router 类创建模块化、可挂载的路由句柄。Router 实例是一个完整的中间件和路由系统，因此常称其为一个 “mini-app”。
下面的实例程序创建了一个路由模块，并加载了一个中间件，定义了一些路由，并且将它们挂载至应用的路径上。

在根目录下新建food.js
```
# food.js
const express = require('express')
const app = express()
const router = express.Router()
const log = console.log
const err = console.error

// 该路由使用打印时间的中间件
// 没有挂载点的中间件，应用的每个请求都会执行该中间件
router.use(function timeLog(req, res, next) {
    log('Time: ', Date.now())
    next()
})

// 定义主页的路由
router.get('/', (req, res) => {
    res.send('Home')
})

// 定义about页面的路由
router.get('/about', (req, res) => {
    res.send('About food')
})

module.exports = router
```
修改express-index.js
```
const express = require('express')
const app = express()
const log = console.log
const err = console.error

app.listen(3000, () => log('server listening at localhost:3000'))

var food = require('./food.js')
// 挂载至 /food 的中间件，任何指向 /food 的请求都会执行它
app.use('/food', food)
```
重启node后修改url

![](http://upload-images.jianshu.io/upload_images/6851923-fb0076d8fceec35e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-b864b78bef432f29.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-ce67ec041bd11b62.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)















