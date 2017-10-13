>最近做音乐播放器，基本功能已实现，准备再写一个循环播放功能，其中涉及列表循环、单曲循环、随机循环。实现这几个功能本质上就是维护一个列表，而列表可视为一个数组，要实现曲目随机循环，也就是实现数组项的随机重排。本文仅讨论实现随机循环的准备工作——即数组随机排序。

- **概念**
洗牌算法是一个形象术语，是一个用来将一个有限集合生成一个随机排列的算法（数组随机排序）。这个算法非常高效且生成的随机排列是等概率的。

- **举例说明**：
有如下数组，数组长度为9，数组内元素值分别为1~9

![](http://upload-images.jianshu.io/upload_images/6851923-9d36ff2aa55c80ba.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

从以上数组入手，我们要做的是打乱数组元素顺序，如：

![](http://upload-images.jianshu.io/upload_images/6851923-0b9e7c5e9369c807.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- **代码实现**：
```
Array.prototype.shuffle = function () {
    var arr = this
    for (var i = arr.length - 1; i >= 0; i--) {
        var randomIdx = Math.floor(Math.random() * (i + 1))
        var itemAtIdx = arr[randomIdx]
        arr[randomIdx] = arr[i]
        arr[i] = itemAtIdx
    }
    return arr
}
var tempArr = [1, 2, 3, 4, 5, 6, 7, 8, 9]
console.log(tempArr.shuffle())//[ 5, 9, 6, 8, 4, 7, 3, 1, 2 ]
```

以上代码中创建了一个shuffle方法，用于随机排列数组中的元素，我们将该方法挂在到Array对象的原型下，任何数组都可以调用该方法。如：
```
var tempArr=[1, 2, 3, 4, 5]
console.log(tempArr.shuffle())//[3, 2, 1, 4, 5]
```

- **工作原理**：
1. shuffle方法首先选中数组末项
2. 将数组第一项到上一步中选中的项（包括头尾）作为随机项的选择范围
3. 在此范围内随机挑选一项与选中项交换值
4. 交换完成后相当于完成了对数组末项的随机处理，接下来处理数组倒数第二项
5. shuffle方法选中数组倒数第二项
6. 重复2~3步，从后往前选中数组项，并与范围内的随机项交换值，直到所有项处理完成。

执行过程如下图：
![](http://upload-images.jianshu.io/upload_images/6851923-c9debad1b64c1005.jpeg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- **代码分析**：
```
1、Array.prototype.shuffle = function () {
2、    var arr = this
3、    for (var i = arr.length - 1; i >= 0; i--) {
4、        var randomIdx = Math.floor(Math.random() * (i + 1))
5、        var itemAtIdx = arr[randomIdx]
6、        arr[randomIdx] = arr[i]
7、        arr[i] = itemAtIdx
8、    }
9、    return arr
10、}
```
以下序号代表对应代码的行序
1. 自定义一个shuffle方法并将其挂在到Array原型之下，便于数组直接调用该函数
2. shuffle函数内部，this引用的就是调用shuffle函数的数组，定义一个变量arr引用this。
3. 定义一个for循环倒序遍历数组的每一项，数组长度为arr.length，而arr.length - 1得到的就是数组末项的索引。
4. 变量randomIdx存储了一个范围在0≤num≤i的随机数，randomIdx含义为随机索引。
5. 确定了随机索引之后，用变量itemAtIdx保存随机项arr[randomIdx]的值
6. 将选中的arr[i]的值赋给随机元素arr[randomIdx]
7. 将随机元素的值itemAtIdx赋给选中元素arr[i]。本质是互换两个元素的值的过程。循环内的逻辑介绍完了，剩下的都是重复操作
8. 至此for循环完成，遍历了数组内的所有元素，并进行随机交换
9. 返回随机重排后的新数组
10. shuffle函数执行完毕


-----
问题：
- 为什么要从后往前处理数组项？
便于确定随机选择的范围。

-----
参考资料：
- [*Fisher–Yates shuffle 洗牌算法*](https://gaohaoyang.github.io/2016/10/16/shuffle-algorithm/)
- *有兴趣可以看看这个*[*完美洗牌算法*](https://github.com/julycoding/The-Art-Of-Programming-By-July/blob/master/ebook/zh/02.09.md)
- [*洗牌算法动画演示*](https://codepen.io/haoyang/pen/jrvrQq)