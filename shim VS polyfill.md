在JavaScript中有两个词经常被提到：shim和polyfill。它们指的都是什么，又有什么区别?
##### shim
一个shim是一个库，它将一系列新的、标准的API引入到一个旧的环境中，而且仅靠旧环境中已有的手段实现旧版兼容。
例如我们经常听到的es5-shim，它是在es3的引擎上实现了es5的特性，但用到的都是es3的技术，而且在Node.js上和在浏览器上有完全相同的表现，所以它是shim。

##### polyfill
polyfill是解决跨浏览器API兼容性问题的shim，相当于一段代码。
我们通常的做法是先检查当前浏览器是否支持某个API，如果不支持的话就加载对应的polyfill，然后新旧浏览器就都可以使用这个API了。

-----

比较有趣的是，polyfill这个词源于英国的填强面料，中文俗称"腻子"”，把旧的浏览器想象成为一面有了裂缝的墙，而腻子可以把这面墙的裂缝抹平，还我们一个光滑的"浏览器"墙面。

Remy在自己2010年10月8日的博客中介绍了这个新词的来源：[What is a Polyfill?](http://remysharp.com/2010/10/08/what-is-a-polyfill/)。
他给出的定义是：
> A polyfill, or polyfiller, is a piece of code (or plugin) that provides the technology that you, the developer, expect the browser to provide natively. Flattening the API landscape if you will.（一段代码或插件，可以让开发人员使用应有的技术，就像浏览器原生提供该功能一样。换句话说，它能帮你抹平API之墙。）

文中也提到了[Paul](http://paulirish.com/)的定义：
> A shim that mimics a future API providing fallback functionality to older browsers.（一种模仿未来API并为旧浏览器提供后备功能的“衬垫”）

怎样区分polyfill和shim？
- 如果浏览器X支持标准规定的功能，那么polyfill可以让浏览器Y的行为与浏览器X一样。
- 而前面所说的es5-shim在es3的引擎上实现了es5的特性，但用到的都是es3的技术，而且在Node.js上和在浏览器上有完全相同的表现，所以它是shim。

比如，jQuery不是polyfill，但下面这段代码是：
```
// 首先包含jQuery
if (!document.querySelectorAll) {
  Element.prototype.querySelectorAll = function (q) {
    return $(this).find(q).get();
  };

  // document对象不是Element对象的后代，因此手工重写
  document.querySelectorAll = Element.prototype.querySelectorAll;
}
```


-----

**参考资料**：
- [*HTML5 Cross Browser Polyfills*](https://github.com/Modernizr/Modernizr/wiki/HTML5-Cross-browser-Polyfills)



