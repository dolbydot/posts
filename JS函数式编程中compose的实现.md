有以下需求：
创建一个compose函数,返回函数集 functions 组合后的复合函数, 也就是一个函数执行完之后把返回的结果再作为参数赋给下一个函数来执行. 以此类推. 在数学里, 把函数 f(), g(), 和 h() 组合起来可以得到复合函数 f(g(h()))。

![](http://upload-images.jianshu.io/upload_images/6851923-44fbf9aae43378b8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果只是为了完成这道题，可用以下做法
```
var greet = function(name){
  return 'hi:'+name
}
var exclaim = function(statement){
  return statement.toUpperCase()+'!' 
} 
var compose = function(greet,exclaim){
  return function(name){
    console.log(exclaim(greet(name)).replace(/(\w+:)/,function($1){
      return $1.toLowerCase() 
    }))  
  }  
} 

var welcome=compose(greet,exclaim)
welcome('dot')

//'hi: DOT!'
```
但上面的代码没有扩展性，如果嵌套的函数更多，该怎么解决呢？
我们可以定义两个方法，分别是compose()和pipe()（上面的题目我们用compose就可以实现，pipe是另行扩展的，不要有疑问），这两个方法接收的参数都是N个函数，返回的值都是一个函数。
- compose内的函数执行顺序为从右向左，即最右边的函数（最后一个参数）最先执行，执行完的结果作为参数传递给前一个函数（包裹它的函数），一直到整个函数执行完毕，return一个函数，所以compose内部实现的原理类似多米诺骨牌，层层递进的。
- pipe函数与compose函数十分相近，也是一个函数执行完毕后将结果作为参数传递给另一个函数，但它们的区别仅在于pipe函数的接收的函数参数，是从左向右执行的，即第一个参数（函数）执行完毕，将结果吐出来作为参数传递给第二个函数，也就是pipe的第二个参数，直到pipe所有参数作为函数都执行完毕，return出一个函数，才算执行完成。

compose和pipe的优点在于，哪怕再要增加或者删除一个参数（执行函数），只需增加或删除相应的参数和定义的函数即可，维护和扩展都十分方便。

代码实现如下：
```
function compose() {
    var fns = [].slice.call(arguments)
    return function (initialArg) {
        var res = initialArg
        for (var i = fns.length - 1; i > -1; i--) {
            res = fns[i](res)
        }
        return res
    }
}

function pipe() {
    var fns = [].slice.call(arguments)
    return function (initialAgr) {
        var res = initialAgr
        for (var i = 0; i < fns.length; i++) {
            res = fns[i](res)
        }
        return res
    }
}

var greet = function (name) { return 'hi:' + name }
var exclaim = function (statement) { return statement.toUpperCase() + '!' }
var transform = function (str) { return str.replace(/[dD]/, 'DDDDD') }
var welcome1 = compose(greet, exclaim, transform)
var welcome2 = pipe(greet, exclaim, transform)
console.log(welcome1('dot'))//hi:DDDDDOT!
console.log(welcome2('dolb'))//HI:DDDDDOLB!
```
根据前面说过的原理，分析一下以上代码：

出题人的意图是“把函数 f(), g(), 和 h() 组合起来得到复合函数 f(g(h()))”，我们首先就可以想到递归，函数从右至左依次执行，每执行完一个函数将其结果作为参数传递给它左边的函数（即包裹它的函数），我们可以很清楚地知道，compose接收的是N个函数参数，而其中每个参数作为函数在执行时接收的都是一个参数（前一个被执行的函数的结果）。

只看代码就可以发现，调用compose函数，将得到的结果赋值给welcome1变量，但这时我们并没有直接把welcome1打印出来，而是向welcome1里传入了参数，这就很像函数调用的格式有木有，那么我们可以做一个设想，其实compose返回的就是一个匿名函数，我们可以通过传递参数给这个匿名函数来得到某种结果，现在思路就很清晰了。

首先在页面上定义一个compose函数，但是不传递任何参数，因为参数的数量（即执行函数的个数）是不确定的，在compose函数内部return一个匿名函数，这个匿名函数接收一个形参initialAgr，函数执行过程中这个参数就是传递给welcome1的实参，也就是第一个被执行的函数接收的参数。
到这里完成了以下代码：
```
function compose() {
    return function (initialArg) {

    }
}
```
接下来干什么呢？
看到f(g(h()))这种形式的函数嵌套，我首先想到的就是递归，所以我们首先要取得调用compose函数时传递的参数，这个参数的形式如下：
```
arguments = {
    0: fn1,
    1: fn2,
    2: fn3,
    length: 3
}
```
为了实现递归，我们需要把这个形式的参数转换为数组，借用数组的slice方法可以实现这一点：
```
var fns = [].slice.call(arguments)
```
以上代码中，我们将传递给compose函数的参数转化为了一个数组并赋值给了fns，接下来我们用一个变量res将传递给welcome1的参数保存起来，定义一个for循环从右向左遍历fns中的每一项并执行它，在这段代码中函数的执行顺序是`transform=>exclaim=>greet`，其中，将res传递给第一个被执行的函数，并将值赋值给res，相当于每执行完一个函数，res的值就被重写一次。
for循环结束意味着复合函数已经执行完毕，我们要的无非就是res的值，所以在函数内部return res就可以达到我们预期的效果。

综上所述，compose函数定义如下：
```
function compose() {
    var fns = [].slice.call(arguments)
    return function (initialArg) {
        var res = initialArg
        for (var i = fns.length - 1; i > -1; i--) {
            res = fns[i](res)
        }
        return res
    }
}
```
这就是compose大致的使用，总结下来要注意的有以下几点：

- compose的参数是函数，返回的也是一个函数。
- 因为除了第一个函数的接受参数，其他函数的接受参数都是上一个函数的返回值，所以初始函数的参数是多元的（本题只讨论了一元参数的情况），而其他函数的接受值是一元的。
- compsoe函数可以接受任意的参数，所有的参数都是函数，且执行方向是自右向左的，初始函数一定放到参数的最右面。

pipe函数没有什么好说的，与compose的原理相同，只不过函数的执行顺序是从左至右，体现在以上代码中就是`greet=>exclaim=>transform`

可以看出，compose和pipe函数对相同执行函数的执行顺序不同，得到的结果也不同。

