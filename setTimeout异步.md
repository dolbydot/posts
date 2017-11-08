### 简单解释单线程、任务队列的概念
单线程：JavaScript是一个单线程语言,浏览器只会分配一个js引擎线程来解析和执行js同步代码。即任务是串行的，后一个任务需要等待前一个任务的执行。

任务队列：所有同步任务都在主线程上执行，形成一个执行栈。主线程之外，还存在一个“任务队列”，指定过回调函数的事件发生时就会进入“任务队列”，等待主线程读取。线程把栈中任务做完之后，就会来看“任务队列”中的事件，“任务队列”是一个先进先出的数据结构，排在前面的事件优先被主线程读取。读取过程基本上是自动的，只要执行栈一清空，“任务队列”上第一位的事件就自动进入主线程。但是，如果包含“定时器”，主线程首先要检查一下执行时间，某些事件只有到了规定的时间，才能返回主线程。主线程从“任务队列”中读取事件，这个过程是循环不断的，所以整个的运行机制又称为“Event Loop”。

setTimeout：N毫秒之后执行某个函数，一次一个ID，实际延迟时间比N毫秒久，会在其他的运行完了以后最后来看setTimeout的内容，可想象为一个闹钟，设定了30秒后吃饭，30秒之后闹钟响了，但当时还在写作业，那么会等作业写完之后再来看闹钟的内容并去执行它。
setInterval：每隔N毫秒执行某个函数，只有一个ID

浏览器对定时器setTimeout很懈怠，当用户焦点离开该界面时，浏览器久变懒了，原本设置500ms做一件事情，但你没有看它，它可能就1000ms才去做一件事情。

异步：异步就是一个猴急的人不愿意等，于是叫了一个黄牛（回调函数）帮他等结果。
异步和回调一般同时出现。

比如排队取号，一个猴急的人不愿意等，但排队取号是不可能马上拿到号码的，因为他不可能拿到未来的东西。即用同步的方式无法拿到结果。
所以他派了一个黄牛（函数）帮他排队，他自己去干别的事情，等黄牛拿到了再把结果告诉他。
```
function 排队取号(黄牛) {
    setTimeout(function f2() {
        黄牛('你的号码是：233')
    }, 3000)
}
function 黄牛(result) {
    console.log(result)
}
排队取号(黄牛)
```
黄牛是我的，所以黄牛拿到的就是我拿到的，如果你不清楚为什么，那就改写一下代码：
```
function 排队取号(黄牛) {
    setTimeout(function f2() {
        黄牛('你的号码是：233')
    }, 3000)
}

//上面和下面分开看
var 我的号 = undefined
function 黄牛(result) {
    我的号 = result
    console.log(我的号)
}
排队取号(黄牛)
```

面试题：
```
for(var i=0;i<5;i++){
    console.log(i)//0,1,2,3,4
}
```
```
for (var i = 0; i < 5; i++) {
    (function (i) {//这一行的i是一个新的变量i，也可以叫j
        setTimeout(function () {
            console.log(i);//打印的i是新的变量i，这个i是全局中传递进来的，没有进行自增操作
        }, i * 1000);
    })(i);//把全局的i的值传递给函数中的i或者j
}//大约0s后打出0,大约1s后打出1，大约2s后打出2，大约3s后打出3，大约4s后打出4
```
```
for (var i = 0; i < 5; i++) {
    setTimeout((function (i) {
        console.log(i);
    })(i), i * 1000);
}

//首先改写代码
for (var i = 0; i < 5; i++) {
    var t1 = function (i) {
        console.log(i);//t1的返回值是undefined
    }
    var t2 = t1(i)//t2是调用t1的结果
    var t3 = i * 1000//0,1000,2000,3000,4000
    setTimeout(t2, t3);
}
//五次循环分别执行了五次setTimeout。分别是
//setTimeout(undefined,0)
//setTimeout(undefined,1000)
//setTimeout(undefined,2000)
//setTimeout(undefined,3000)
//setTimeout(undefined,4000)
//产生了undefined但并没有打印undefined，运行的5次打印了5次t1(i)，这个i是新建的局部变量i，不是全局中的，全局中的i值会赋值给局部变量的i
//最终结果是0,1,2,3,4，没有延时，因为setTimeout第一个参数为undefined，所以定时器什么也没做。
```
```
for(var i=0;i<5;i++){
    setTimeout(function(){
        console.log(i)
    },1000*i);
}//setTimeout是异步，js引擎在for循环结束后才会开始执行setTimeout的内容，也就是说console.log(i)之前for循环已经结束了，i变为5，所以结果是：大约0s后打出5,大约1s后打出5，大约2s后打出5，大约3s后打出5，大约4s后打出5
```
```
for (var i = 0; i < 5; i++) {
    (function () {
        setTimeout(function () {
            console.log(i);
        }, i * 1000);
    })(i);
}//结果是：大约0s后打出5,大约1s后打出5，大约2s后打出5，大约3s后打出5，大约4s后打出5

//如果觉得不好理解可以将一行拆分为多行，声明一个函数t，调用这个函数t
for (var i = 0; i < 5; i++) {
    function t() {
        setTimeout(function () {
            console.log(i);
        }, i * 1000);
    }
    t(i);
}
```

做一个倒计时器
```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
</head>

<body>
  <select name="" id="mySelect" placeholder="选择一个时间">
    <option value="1" selected>1分钟</option>
    <option value="5">5分钟</option>
    <option value="10">10分钟</option>
    <option value="20">20分钟</option>
  </select>
  <button id="startButton">start</button>
  <button id="pauseButton" disabled>pause</button>
  <button id="resumeButton" disabled>resume</button>
  <div id="outputDiv">

  </div>
  <script>
    var timeLeft = 10
    let lastTimerID

    function showTime() {
      //通过id名可以直接获取到页面上的元素
      outputDiv.textContent = timeLeft + '秒';
      if (timeLeft === 0) return
      timeLeft -= 1
      lastTimerID = setTimeout(showTime, 1000)
    }

    startButton.onclick = function () {
      var valueNumber = parseInt(mySelect.value, 10)
      var seconds = valueNumber * 60
      timeLeft = seconds
      if (lastTimerID) {
        window.clearTimeout(lastTimerID)
      }
      showTime()
      pauseButton.disabled = false
    }

    pauseButton.onclick = function () {
      if (lastTimerID) {
        window.clearTimeout(lastTimerID)
        resumeButton.disabled = false
        pauseButton.disabled = true
      }
    }

    resumeButton.onclick = function () {
      showTime()
      pauseButton.disabled = false
      resumeButton.disabled = true
    }
  </script>
</body>

</html>
```
面试题
```
var startTime = +(new Date()),endTime;
setTimeout(function(){
    endTime = +(new Date());
    console.log(1);
    console.log(endTime - startTime);
    },3000);
setTimeout(function(){
    endTime = +(new Date());
    console.log(2);
    console.log(endTime - startTime);
    },2000);
while(+(new Date()) - startTime < 5000){}
console.log(+(new Date()) - startTime);
```
请问alert(1)和alert(2)的先后顺序和时间间隔。

5s钟的同步执行完之后，开始执行setTimeout异步代码，因为第二个插入的时间间隔早，先执行。

![](http://upload-images.jianshu.io/upload_images/6851923-e49b771d95a1b187.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

因为5s时间超过了3s，所以两个函数几乎同时执行。如果同步时间是1s，那就是第2s之后执行第二个函数，第3s后执行第一个函数，代码运行总时长3s多一点点

![](http://upload-images.jianshu.io/upload_images/6851923-c2c8769bb9a5f3c3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

setTimeout(..) 并没有把你的回调函数挂在事件循环队列中。它所做的是设 定一个定时器。
当定时器到时后,环境会把你的回调函数放在事件队列中,如果这时候事件循环中已经有 20 个项目了会怎样呢?你的回调就会等待,定时器只能确保你的回调函数不会在指定的 时间间隔之前运行,但可能会在那个时刻运行,也可能在那之后运行,要根据事件队列的 状态而定(PS: 这就是造成定时器不准确的缘由)。

setTimeout(..0)(hack)进行异步调度,基本上它的意思就是把这个函数插入到当前事件循环队列的结尾处。