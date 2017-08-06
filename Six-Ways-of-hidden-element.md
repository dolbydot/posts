> 这个内容较好理解，不上完整代码，不截图！
# 
### 1、最常用之——display: none;
给元素设置`display: none;`后，元素会从页面中彻底消失，它原本占据的空间会被其他元素占有，会造成浏览器的回流与重绘。

### 2、最常用之——visibility: hidden;
给元素设置`visibility: hidden;`后，元素会从页面中消失，它原本占据的空间会被保留，会造成浏览器的重绘，适用于希望元素隐藏又不影响页面布局的场景。

### 2、隐身大法——opacity: 0;
给元素设置`opacity: 0;`后，元素变成透明的我们肉眼就看不到了，所以原本占据的空间还在。

### 4、设置盒模型属性为0
将height、width、padding、border、margin等盒模型属性的值全设为0，如果元素內还有子元素或内容，还应overflow: hidden;来隐藏子元素。
```
.box1 {
        width: 0;
        height: 0;
        padding: 0;
        border: 0;
        margin: 0;
        overflow: hidden;
}
```

### 5、最鸡贼——设置元素绝对定位与top、right、bottom、left等将元素移出屏幕。
如：
```
.box1 {
        position: absolute;
        left: 100%;
}
```
或:
```
.box1 {
        position: absolute;
        top: 9999px;
}
```

### 6、设置元素的绝对定位与z-index，将z-index设置成尽量小的负数。
但z-index是相对而言的 ，用z-index就要设置其他元素的z-index值，且如果元素本身占据空间很大就不一定会被z-index值比它大的元素完全覆盖，所以不推荐这种方法。
如：
```
.box1 {
        position: absolute;
        z-index: -9999;
}
.box2 {
        position: absolute;
        z-index: 1;
}
```
