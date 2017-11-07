### 基本类型和引用类型的赋值问题
```
function dolby(a, b, c) {
    a = 2;
    b.color = 'red';
    c = {
        color: 'black'
    }
    console.log(a); //2
    console.log(b); //{color:'red'}
    console.log(c); //{color:'black'}
}
var a = 1;
var b = {
    color: 'blue'
}
var c = {
    color: 'white'
}
dolby(a, b, c);
console.log(a); //1
console.log(b); //{color:'red'}
console.log(c); //{color:'white'}
```
上例很好地证明了：基本类型值按值传递，引用类型值按引用传递

### 同名变量和方法覆盖问题
```
var fn = 3;
function fn(){};
console.log(fn); // 3
```
```
function fn(){};
var fn = 3;
console.log(fn); // 3
```
```
console.log(fn); //ƒ fn(){}
function fn(){};
var fn = 3;

-----
以上代码可改写为：注意变量声明和函数声明都会提升，但值不会提升。
function fn(){};
var fn;
console.log(fn);
fn=3;
```
-----
```
//例一
function add1(i){
console.log("函数声明："+(i+1));
}
add1(1);

var add1=function(i){
console.log("函数声明："+(i+10));
}
add1(1);

function add1(i){
console.log("函数声明："+(i+100));
}
add1(1);

//函数声明：101 
//函数声明：11 
//函数声明：11 
```
例一中：
- 函数从上往下依次读取代码，首先调用第一个add1(1)，同名函数后面覆盖前面的，所以调用第一个add1(1)实际上读取的是后一个add(i)函数的值，即返回"函数声明：101"
- 代码接着往下执行，读到变量add1，调用第二个add1(1),执行变量add1后函数体中的代码，打印结果为"函数声明：11"
- 接着读到第二个add1函数，因变量add1与函数add1在同一作用域下，所以变量add1的值会覆盖函数add1的值，所以第三个打印结果为"函数声明：11"
```
//例二
var add1=function(i){
console.log("函数声明："+(i+10));
}
add1(1);

function add1(i){
console.log("函数声明："+(i+1));
}
add1(1);

function add1(i){
console.log("函数声明："+(i+100));
}
add1(1);
//函数声明：11
//函数声明：11
//函数声明：11
```
例二中：
- 函数从上往下依次读取代码，首先调用第一个add1(1)，执行变量add1后函数题中的代码，打印结果为函数声明：11，
- 代码接着往下执行，读到函数add1，调用第二个add1(1),因变量add1与函数add1在同一作用域下，所以变量add1的值会覆盖函数add1的值，所以第二个打印结果为函数声明：11
- 代码接着往下执行，读到函数add1，调用第三个add1(1),因变量add1与函数add1在同一作用域下，所以变量add1的值会覆盖函数add1的值，所以第三个打印结果为函数声明：11
```
//例三
function add1(i){
console.log("函数声明："+(i+1));
}
add1(1);

function add1(i){
console.log("函数声明："+(i+100));
}
add1(1);

var add1=function(i){
console.log("函数声明："+(i+10));
}
add1(1);
//101
//101
//11
```
例三中：
- 函数从上往下依次读取代码，首先调用第一个add1(1)，同名函数后面覆盖前面的，所以调用第一个add1(1)实际上读取的第二个add(i)函数的值，即返回函数声明：101，
- 接着调用第二个add1(1)，执行函数体代码得到打印值：函数声明：101
- 代码接着往下执行，读到变量add1，调用第三个add1(1),执行变量add1后函数题中的代码，打印结果为函数声明：11

总结：
代码从上往下依次执行，当在同一个作用域内定义了同名的变量和方法，同名函数之间后面的会覆盖前面的赋值，同名变量赋值会覆盖函数的赋值。注意变量声明和函数声明都会提升，但值不会提升。



3. js语言中花括号没有块级作用域的概念

4. 立即执行函数表达式可以是匿名函数，可以隔离作用域，方便不用取名字立刻使用
函数声明也是天然隔离作用域，内部声明的变量外部无法调用