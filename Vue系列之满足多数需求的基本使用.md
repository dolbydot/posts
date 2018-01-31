### 首先创建一个简单的vue应用
```
# 全局安装 vue-cli
$ npm i -g vue-cli
# 创建一个简单的vue仓库
$ vue init webpack-simple learnvue
# 安装依赖
$ cd learnvue
$ npm I
$ npm run dev
```

### class绑定——动态地切换class
- 在:class上绑定一个对象
- 在:class上绑定一个对象名
- 在:class上绑定一个返回对象的计算属性
- 在:class上绑定一个数组，数组语法中也可以使用对象语法
- 三元表达式：根据条件切换列表中的class

注意：普通class和绑定class可以共存
```
<template>
  <div id="app">
    {{msg}}
    <!--  1.在在:class上绑定一个对象  -->
    <div :class="{active:isActive}" class="header">
      我是header，我有一个普通class和一个可能存在的class对象
    </div>
    <div :class="{bigger:isBigger,'text-danger':hasError}" class="main">
      我是main，我有一个普通class和一个可能存在的class对象
    </div>

    <!--  在:class上绑定一个对象名  -->
    <div :class="classObj1">
      我是小字，我有背景色
    </div>

    <!-- 在:class上绑定一个返回对象的计算属性 -->
    <div :class="classObj2">
      我是大字，没有背景色
    </div>

    <!--在:class上绑定一个数组，可使用三元表达式，数组语法中也可以使用对象语法  -->
    <div :class="['text-danger',classObj1]">我始终是红色字，可能是大字也可能是小字，有或者没有绿色背景</div>
    <div :class="[classObj2,{'text-danger':hasError}]">我现在是大字且为红色，没有背景色</div>
    <div :class="[isActive? '' :'text-danger']">我是红字</div>

  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      isActive: 0,
      isBigger: '',
      hasError: true,
      classObj1: {
        active: !this.isActive,
        bigger: this.isBigger
      }
    }
  },
  computed: {
    classObj2() {
      return {
        active: this.isActive && this.hasError,
        bigger: !this.isBigger && this.hasError
      }
    }
  }
}
</script>

<style>
.active {
  background: green;
}

.header {
  font-size: 2em;
}

.bigger {
  font-size: 4em;
}

.text-danger {
  color: red;
}

.main {
  font-style: italic;
}
</style>
```

![](http://upload-images.jianshu.io/upload_images/6851923-b9f4b31c1af298b2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### style绑定——绑定内联样式
- 看着很像css内联样式，属性名可用驼峰式或用短横线分隔，短横线分隔要用单引号引起来
- 直接绑定到一个样式对象
- 结合计算属性使用
- 数组语法

当 `v-bind:style` 使用需要添加[浏览器引擎前缀](https://developer.mozilla.org/zh-CN/docs/Glossary/Vendor_Prefix)的 CSS 属性时，如 `transform`，Vue.js 会自动侦测并添加相应的前缀。

```
<template>
  <div id="app">
    {{msg}}
    <div :style="{color:activeColor,fontSize:fontSize+'px'}">
      hello world
    </div>

    <div :style="styleObj1">
      hello dot
    </div>

    <div :style="styleObj2">
      hello dolby
    </div>

    <div :style="[styleObj1,styleObj2]">
      hello dolby
    </div>

  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      activeColor: 'red',
      fontSize: 12,
      styleObj1: {
        background: 'yellow',
        color: 'pink'
      }
    }
  },
  computed: {
    styleObj2() {
      return {
        fontStyle: 'italic',
        fontWeight: 'bolder'
      }
    }
  }
}
</script>
```

![](http://upload-images.jianshu.io/upload_images/6851923-54eb893e565d532b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### vue不得不说的生命周期
当一个vue实例被创建时，它向 Vue 的响应式系统中加入了其 data 对象中能找到的所有的属性。当这些属性的值发生改变时，视图将会产生“响应”，即匹配更新为新的值。

看下图：

![图源Vue.js教程](http://upload-images.jianshu.io/upload_images/6851923-15570fdfc2f24566.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

一个实例的生命周期分为creat、mount、update、destroy四个阶段，它们的分工各有不同：

- create:创建
- mount:挂载DOM
- update:数据更新
- destroy:销毁（一般为手动清理事件和定时器）

同时在这些过程中也会运行一些叫做生命周期钩子的函数，这给了用户在不同阶段添加自己的代码的机会。对应生命周期来看，又有以下8个钩子：

beforeCreate、created、beforeMount、mounted、beforeUpdate、updated、beforeDestroy、destroyed。

看一个例子：
```
<template>
  <div id="app">
    {{msg}}
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
    }
  },
  beforeCreate() {
    console.log('beforeCreate')
  },
  created() {
    console.log('created')
    setTimeout(() => {
      this.msg = 'change msg'
    }, 1000);
  },
  beforeMount() {
    console.log('beforeMount')
  },
  mounted() {
    console.log('mounted')
  },
  beforeUpdate() {
    console.log('beforeUpdate')
  },
  updated() {
    console.log('updated')
  },
  beforeDestroy() {
    console.log('beforeDestroy')
  },
  destroyed() {
    console.log('destroyed')
  },
  methods: {
    clickBtn() {
      alert('hello')
    }
  },
  watch: {
    msg() {
      console.log('hello')
    }
  }
}
</script>
```
打开localhost:8080，页面显示初始msg内容，控制台打印beforeCreate、created、beforeMount、mounted

![](http://upload-images.jianshu.io/upload_images/6851923-cec952ddea6f7d5d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

大约1s之后，页面内容发生变化，紧接着watch生效，控制台一次打印出hello,beforeUpdate,updated，这里没有打印出beforeDestroy和destroyed是因为页面上没有事件。

![](http://upload-images.jianshu.io/upload_images/6851923-ab6c9c3bdeae9a03.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### v-model
##### 单行文本
 v-model 指令用于在表单 `<input>` 及 `<textarea>` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素，但 v-model 本质上不过是语法糖。它负责监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。
```
<template>
  <div id="app">
    <input type="text" placeholder="edit me" v-value="hello">
  </div>
</template>
```
以上代码的效果是页面上会出现一个input输入框且有初始值value

![](http://upload-images.jianshu.io/upload_images/6851923-eb33a5aa44604494.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

当我们在input中使用v-model用于绑定数据时，value值不生效
```
<template>
  <div id="app">
    <input type="text" placeholder="edit me" v-model="message" value="hello">
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      message: '',
    }
  },
}
</script>
```

![](http://upload-images.jianshu.io/upload_images/6851923-6b56b919b7959645.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

v-model 会忽略所有表单元素的 value、checked、selected 特性的初始值而总是将 Vue 实例的数据作为数据来源。如果有需要，我们应在组件的 data 选项中声明初始值。
```
<template>
  <div id="app">
    <input type="text" placeholder="edit me" v-model="value">
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      message: '',
      value: 'init',
    }
  },
}
</script>
```

![](http://upload-images.jianshu.io/upload_images/6851923-0b4d67ef1862b2c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

现在结合前面学到的看一段代码：
```
<template>
  <div id="app">
    <input type="text" placeholder="edit me" v-model="message">
    <button @click="clickBtn">Click me</button>
    <p :style="styleObj">Message is: {{message}}</p>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      message: '',
      isClick: ''
    }
  },
  computed: {
    styleObj() {
      return {
        color: this.isClick && this.message ? 'red' : '',
        background: this.isClick && this.message ? 'yellow' : ''
      }
    }
  },
  methods: {
    clickBtn() {
      if (this.message) {
        this.isClick = true
      }
    }
  },
}
</script>
```
我们为input定义了一个placeholder值为'edit me'并绑定了一个message属性

![](http://upload-images.jianshu.io/upload_images/6851923-f832b28803050692.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

首先看input里绑定的message和p中message之间的关系，前面说v-model双向绑定不过是语法糖，实际上还是单向绑定。
当input中的内容发生变化，也就是input中绑定的message——来自于data中的message属性值发生了变化，p中的message也会随之改变，所以数据改变是单向的从data中的message属性到页面上的message属性变换的过程。所以p中的文本会随着input中的内容改变而改变。

![](http://upload-images.jianshu.io/upload_images/6851923-44cf911bbdb29549.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们再来看看data中的另一个属性'isClick'，我们给它赋值为一个空的字符串，即布尔值false

继续看代码，在button按钮上定义了一个单击事件'clickBtn'，在p元素上绑定了一个内联样式'styleObj'，我们把样式对象放在computed中，这样就会返回计算后的属性对象。当用户点击按钮时，如果input中有输入，我们将'isClick'值设为true，反应在页面上就是输入不为空的情况下点击按钮之后p元素有了黄色背景，字色变为红色。

![](http://upload-images.jianshu.io/upload_images/6851923-903359540a522fe3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 多行文本
```
<template>
  <div id="app">
    <span>Multiline message is:</span>
    <p style="white-space: pre-line;">{{ message }}</p>
    <br>
    <textarea v-model="message" placeholder="add multiple lines"></textarea>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      message: '',
    }
  },
}
</script>
```

![](http://upload-images.jianshu.io/upload_images/6851923-cfe24502c7014c62.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-36fe26099f83ef52.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-3200271f45b9b106.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在文本区域插值 (`<textarea></textarea>`) 并不会生效，应用 v-model 来代替。

##### 复选框
- 单个复选框绑定到布尔值
```
<template>
  <div id="app">
    <input type="checkbox" v-model="checked">
    <label for="checkbox">{{checked}}</label>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      checked: false,
    }
  },
}
</script>
```

![](http://upload-images.jianshu.io/upload_images/6851923-2f4bf2c4f36da041.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-4e9900da9b42cb64.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 多个复选框绑定到同一数组
```
<template>
  <div id="app">
    <input type="checkbox" value="Jack" v-model="checkedArr">
    <label for="jack">Jack</label>
    <input type="checkbox" value="John" v-model="checkedArr">
    <label for="john">John</label>
    <input type="checkbox" value="Mike" v-model="checkedArr">
    <label for="mike">Mike</label>
    <br>
    <span>Checked names: {{ checkedArr }}</span>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      checkedArr: [],
    }
  },
}
</script>
```
绑定到checkedArr中的值是input中的value

![](http://upload-images.jianshu.io/upload_images/6851923-35fd4113bf905ff9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 单选按钮
```
<template>
  <div id="app">
    <input type="radio" value="Jack" v-model="picked">
    <label for="jack">Jack</label>
    <input type="radio" value="John" v-model="picked">
    <label for="john">John</label>
    <input type="radio" value="Mike" v-model="picked">
    <label for="mike">Mike</label>
    <br>
    <span>picked names: {{ picked }}</span>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      picked: '',
    }
  },
}
</script>
```

![](http://upload-images.jianshu.io/upload_images/6851923-72f59b40a18473c8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 选择框
- 单选时
```
<template>
  <div id="app">
    <select v-model="selected">
      <option disabled value="">请选择</option>
      <option>A</option>
      <option>B</option>
      <option>C</option>
    </select>
    <span>Selected: {{ selected }}</span>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      selected: '',
    }
  },
}
</script>
```

![](http://upload-images.jianshu.io/upload_images/6851923-fade29ba4382c87a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如果 v-model 表达式的初始值未能匹配任何选项，`<select>` 元素将被渲染为“未选中”状态。这种情况下iOS 不会触发 change 事件，这会使用户无法选择第一个选项。因此推荐像上面这样提供一个值为空的禁用选项。

- 多选时
```
<template>
  <div id="app">
    <select v-model="selectedArr" multiple >
      <option>A</option>
      <option>B</option>
      <option>C</option>
    </select>
    <span>SelectedArr: {{ selectedArr }}</span>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      selectedArr: [],
    }
  },
}
</script>
```

![](http://upload-images.jianshu.io/upload_images/6851923-a74825a8c17a2f51.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

用v-for渲染的动态项
```
<template>
  <div id="app">
    <select v-model="selected">
      <option v-for="option in options" :value="option.value">{{option.text}}</option>
    </select>
    <span>Selected: {{ selected }}</span>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      selected: 'A',
      options: [
        { value: 'A', text: 'One' },
        { value: 'B', text: 'Two' },
        { value: 'C', text: 'Three' },
      ]
    }
  }
}
```

![](http://upload-images.jianshu.io/upload_images/6851923-e063941088fd9a9e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### computed
接下来我们来说一个前面反复提到的计算属性对象computed，计算属性可以应用于各种复杂的逻辑，使代码更加轻便容易维护。
语法：`computed: {xxx: function () { return /*  */}}`
```
<template>
  <div id="app">
    <p>Original message: "{{ message }}"</p>
    <p>Computed reversed message: "{{ reversedMessage }}"</p>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      message: 'hello'
    }
  },
  computed: {
    reversedMessage() {
      return this.message.split('').reverse().join('')
    }
  },
}
```

![](http://upload-images.jianshu.io/upload_images/6851923-8ffdfd6f7c3c37d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以像绑定普通属性一样在模板中绑定计算属性。Vue 知道 reversedMessage 依赖于message，因此当 message 发生改变时，所有依赖 reversedMessage 的绑定也会更新。而且最妙的是用计算属性没有副作用，更易于测试和理解。

### methods
看了上面computed的例子你会发现，我们在methods中使用方法可达到同样的效果：
```
<template>
  <div id="app">
    <p>Original message: "{{ message }}"</p>
    <p>Methods reversed message: "{{ reversedMessage() }}"</p>
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      message: 'hello'
    }
  },
  methods: {
    reversedMessage() {
      return this.message.split('').reverse().join('')
    }
  },
}
```
我们可以将同一函数定义为一个方法而不是一个计算属性。两种方式的最终结果确实是完全相同的。不同的是计算属性是基于它们的依赖进行缓存的，只有在它的相关依赖发生改变时才会重新求值。这就意味着只要 message 还没有发生改变，多次访问 reversedMessage 计算属性会立即返回之前的计算结果，而不必再次执行函数。

这也同样意味着下面的计算属性将不再更新，因为 Date.now() 不是响应式依赖：
```
<template>
  <div id="app">
    <p>{{ now }}</p>
    <p>{{ now }}</p>
    <p>{{ now }}</p>
    <p>{{ now }}</p>
  </div>
</template>

<script>
export default {
  name: 'app',
  computed: {
    now() {
      return Date.now()
    }
  },
}
```

![](http://upload-images.jianshu.io/upload_images/6851923-1647bcfda1040f59.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

相比之下，每当触发重新渲染时，调用方法总会再次执行函数。

```
<template>
  <div id="app">
    <p>{{ now() }}</p>
    <p>{{ now() }}</p>
    <p>{{ now() }}</p>
    <p>{{ now() }}</p>
  </div>
</template>

<script>
export default {
  name: 'app',
  methods: {
    now() {
      return Date.now()
    }
  },
}
```

![](http://upload-images.jianshu.io/upload_images/6851923-7568cb693ae13d2a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

我们为什么需要缓存？假设我们有一个性能开销比较大的的计算属性 A，它需要遍历一个巨大的数组并做大量的计算。然后我们可能有其他的计算属性依赖于 A 。如果没有缓存，我们将不可避免的多次执行 A 的 getter函数，如果你不希望有缓存，请用方法来替代。

前面说过了computed计算属性与methods方法的比较，现在说说计算属性和侦听属性watch的比较。
```
<template>
  <div id="app">
    {{ fullName }}
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      firstName: 'Foo',
      lastName: 'Bar',
      fullName: 'Foo Bar'
    }
  },
  watch: {
    firstName: function(val) {
      this.fullName = val + ' ' + this.lastName
    },
    lastName: function(val) {
      this.fullName = this.firstName + ' ' + val
    }
  },
}
```
以上做法是命令式的watch回调，而且代码重复，也没办法做到响应式，没有任何意义。看computed如何实现
```
<template>
  <div id="app">
    {{ fullName }}
  </div>
</template>

<script>
export default {
  name: 'app',
  data() {
    return {
      firstName: 'Foo',
      lastName: 'Bar',
    }
  },
  computed: {
    fullName() {
      return this.firstName + ' ' + this.lastName
    }
  },
}
```
代码简洁直观，且当firstName或lastName改变时，fullName也会随之改变并反映到页面上。
虽然计算属性在大多数情况下更合适，但有时也需要一个自定义的侦听器，于是就有了watch。

### watch
当需要在数据变化时执行异步或开销较大的操作时，watch是最有用响应数据变化的方法,一般用于监听input等有输入操作的场景。
```
<template>
  <div id="app">
    {{msg}}
    <input v-model="question">
    <div>{{answer}}</div>
  </div>
</template>

<script>
export default {
  name: 'app',
  created() {
    console.log('')
    setTimeout(() => {
      this.msg = '12121212'
    }, 1000);
  },
  data() {
    return {
      msg: 'Welcome to Your Vue.js App',
      question: '',
      answer: 'I cannot give you an answei until you ask a question'
    }
  },
  watch: {
    question() {
      this.answer = 'Waiting for you to stop typing...'
    },
    msg() {
      alert('hello')
    }
  }
}
</script>
```
以上代码在http://localhost:8080/中打开后，页面正常显示数据，接着先弹出hello

![](http://upload-images.jianshu.io/upload_images/6851923-e6f7967219a9edc4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

点击确定后msg值变为setTimeout中的12121212

![](http://upload-images.jianshu.io/upload_images/6851923-5edf67ae752a56d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在输入框中输入任意内容，answer值变为我们设定的字符串

![](http://upload-images.jianshu.io/upload_images/6851923-0db89620fc607240.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
