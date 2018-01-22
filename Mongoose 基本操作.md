### 前提
- 安装[Node](https://nodejs.org/dist/v9.4.0/node-v9.4.0.pkg)
- 新建一个单独的目录安装[MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-os-x/)并开启服务
- 新建项目目录，`npm init`初始化并安装mongoose包`npm i mongoose -S`
- 建议`npm i -g supervisor`安装[supervisor](https://www.npmjs.com/package/supervisor)，用于监听当前目录下 node 和 js 后缀的文件，当这些文件发生改动时，supervisor 会自动重启程序。
- 运行mongo连接数据库

-----

### 核心
**名词解释**
- Schema：以文件形式存储的数据库模型骨架，不具备操作数据库的能力
- Model：由Schema发布生成的模型，具有抽象属性和行为的数据库操作对
- Entity：由Model创建的实体，也可以对数据库进行操作

**三者关系**
Schema 生成 Model，Model 创造 Entity，Model 和 Entity 都可以对数据库进行操作，但 Model 比 Entity 更具操作性

-----

### 应用
首先要知道，数据库的所有操作都是异步的。
##### 基本操作
- 增：save()
- 删：remove()
- 查：find()，findOne()
- 改：update()，updateMany()

**结合代码使用**
```
# test.js
const mongoose = require('mongoose')
mongoose.Promise = global.Promise// 最好加上这句话
const Schema = mongoose.Schema
const log = console.log
const err = console.error

// 创建连接,因为数据库操作是异步的，使用then方法可保证连接之后才执行操作
const db = mongoose.connect('mongodb://localhost/test').then(() => {
    // Schema和Model变量名大写，entity变量名小写，集合名小写，如cats
    const CatSchema = Schema({ name: String }) // Schema

    const CatModel = mongoose.model('cats', CatSchema)  //Model

    const catEntity = new CatModel({ name: 'Dolb' })  //实体 entity
      
    //以下所有逻辑都在这里进行

})
```
- 增加一条数据
```
    // 增
    catEntity.save((e,res)=>{
        if(e){
            err(e)
        }else{
            log('save suc')
        }
    })
```
这里我运行`node test.js`保存成功后退出程序并再次`node test.js`

![运行两次node test.js](http://upload-images.jianshu.io/upload_images/6851923-dd844c445b3f7dc0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


得到的是几条数据呢？

![查看数据条目](http://upload-images.jianshu.io/upload_images/6851923-5dfcab3e8ea21abf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

得到了两条数据，结论是数据库的数据没有覆盖一说，哪怕内容相同，重复save只会重复添加。

为了方便后面的演示，将`const catEntity = new CatModel({ name: 'Dolb' })`中的name值分别改为`Miao`和`Mimi`，这样数据库下的cats集合里就有以下四条数据：

![当前数据](http://upload-images.jianshu.io/upload_images/6851923-437e3b3316160693.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

另外补充一下，使用Model来新增数据使用create方法，如：`CatModel.create({name: 'Dot'} , callback)`

- 删除一条数据
因为数据库的操作都是异步的，那么在保存和删除同时存在时我们不能保证代码的执行顺序，所以得到的很可能是我们不愿意看到的结果，假设代码是这个样子的：
```
    // 增
    catEntity.save((e, res) => {
        if (e) {
            err(e)
        } else {
            log('save suc')
        }
    })

    // 删除新增的Mimi的数据
    catEntity.remove({ name: 'Mimi' }, (e, res) => {
        if (e) {
            err(e)
        } else {
            log('remove Mimi suc')
        }
    })
```
# 
![运行node](http://upload-images.jianshu.io/upload_images/6851923-ba56cfe9265620b6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![结果](http://upload-images.jianshu.io/upload_images/6851923-953c945be97b3165.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

是不是和想象的完全不一样？那么怎样做到删除当前增加的条目呢？
```
    // 增
    catEntity.save((e, res) => {
        if (e) {
            err(e)
        } else {
            log('save suc')
            // 删除新增的Mimi的数据
            catEntity.remove({ name: 'Mimi' }, (e, res) => {
                if (e) {
                    err(e)
                } else {
                    log('remove Mimi suc')
                }
            })
        }
    })
```
将删除的代码放进增加的代码中，就可以保证删除在新增之后执行

![运行node](http://upload-images.jianshu.io/upload_images/6851923-152becd309ff54ed.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![数据](http://upload-images.jianshu.io/upload_images/6851923-405f4f3582c6fc48.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以看到仍是5条数据，说明新增的Mimi被删除了，事实上remove的第一个参数不写就可以做到删除当前条目了：
```
    // 增
    catEntity.save((e, res) => {
        if (e) {
            err(e)
        } else {
            log('save suc')
            // 删除新增的Mimi的数据
            catEntity.remove((e, res) => {
                if (e) {
                    err(e)
                } else {
                    log('remove Mimi suc')
                }
            })
        }
    })
```
# 
![数据](http://upload-images.jianshu.io/upload_images/6851923-405f4f3582c6fc48.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可是假设现在我们需要删除所有name为Dolb的数据，又该怎么做呢？这个时候就要用到Model了⬇️

- 删除所有符合条件的数据
首先我们将前面的代码注释掉，再添加以下代码
```
    // 删除所有符合name值为Dolb的数据
    CatModel.remove({ name: 'Dolb' }, (e, res) => {
        if (e) {
            err(e)
        } else {
            log('remove Dolb suc')
        }
    })
```

![数据](http://upload-images.jianshu.io/upload_images/6851923-42cce82be7e92857.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 删除所有数据
删除所有数据即去掉remove方法的第一个参数
```
    CatModel.remove((e, res) => {
        if (e) {
            err(e)
        } else {
            log('remove Dolb suc')
        }
    })
```
这里为了接下来的操作就不执行这段代码了

- 查找所有符合条件的数据
```
    CatModel.find({ name: 'Mimi' }, (e, res) => {
        if (e) {
            err(e)
        } else {
            log('find Mimi suc: There have ' + res)
        }
    })
```
- 查找所有数据
```
    CatModel.find((e, res) => {
        if (e) {
            err(e)
        } else {
            log('find all cats suc: There have ' + res)
        }
    })
```

![数据](http://upload-images.jianshu.io/upload_images/6851923-810e07d2bb951c8e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

到这里我误删了所有数据，所以重新新建的数据如下：

![现在的数据](http://upload-images.jianshu.io/upload_images/6851923-3e65bce3f73e9ce8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 修改
```
    CatModel.update({ name: 'Miao' }, { name: 'Miao2' }, (e, res) => {
        if (e) {
            err(e)
        } else {
            log('更新成功')
            // 只更新一个
            CatModel.updateOne({ name: 'Miao2' }, { name: 'Miao3' }, (e, res) => {
                if (e) {
                    err(e)
                } else {
                    log('更新第一个Miao成功')
                }
            })
        }
    })

    CatModel.updateMany({ name: 'Mimi' }, { name: 'Mimi2' }, (e, res) => {
        if (err) {
            err(err)
        } else {
            log('更新成功')
        }
    })
```

![加入updateOne前后，数据的变化](http://upload-images.jianshu.io/upload_images/6851923-f5d2f5b6efa62aca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

所以update和updateMany有什么区别呢？


-----

##### 进阶
- Middleware中间件，重点：next()，hook钩子。
- Plugin插件，用来更新Schema的功能，而全局Plugin用于更新全部Schema的功能，所以全局plugin最好放在靠前的位置。
- Validation验证器，验证存入数据库的数据
```
const mongoose = require('mongoose')
const Schema = mongoose.Schema
const log = console.log
const err = console.error

// Plugin插件，用来更新Schema的功能
// 全局Plugin，更新全部Schema的功能，全局plugin最好放在靠前的位置
// 以下代码为所有操作打上时间戳
function TimePlugin(schema, options) {
    const str = 'save time'
    schema.pre('save', next => {
        console.time(str)
        next()
    })
    schema.post('save', next => {
        console.timeEnd(str)
    })
}
mongoose.plugin(TimePlugin)

const PostSchema = new Schema({
    title: {
        type: String,
        // Validation  验证器 验证存入数据库的数据
        // 验证器，validate是放在Schema下的字段用来做字段限制的
        validate: {
            validator: v => v.length < 10,
            message: '文章标题长度必须小于10'
        }
    },
    author: {
        type: Schema.Types.ObjectId,
        ref: 'User'
    },
    rawContent: String,
    create_at: {
        type: Date,
        default: Date.now
    },
    update_at: {
        type: Date,
        default: Date.now
    },
    comments: {
        type: Array
    },
    votes: Number,
    downs: Number
})

const UserSchema = new Schema({
    name: String,
    sex: Number,
    avatar: String,
    mail: String,
    password: String
})

const CommentSchema = new Schema({
    author: {
        type: Schema.Types.ObjectId,
        required: true
    },
    content: {
        type: 'string',
        required: true
    },
    postId: {
        type: Schema.Types.ObjectId,
        required: true
    }
})

const PostModel = mongoose.model('Post', PostSchema)
const UserModel = mongoose.model('User', UserSchema)
const CommentModel = mongoose.model('Comment', CommentSchema)

const db = mongoose.connect('mongodb://localhost/dolb').then(() => {

    // 1. 插入文章
    function addPost(post) {
        const postEntity = new PostModel(post)
        postEntity.save((e, result) => {
            if (e) {
                err(e)
            } else {
                log('保存成功啦')
                //    getPostByTitle('hello world')// 插入之后才能查到文章，而操作都是异步的，不能保证顺序，所以调用getPostByTitle放在addPost里能保证查得到
            }
        })
    }
    addPost({
        title: 'hello wo'
    })

    // 2. 根据id删除文章
    function removePostById(postId) {
        PostModel.remove({ _id: postId }, (e, res) => {
            if (e) {
                err(e)
            } else {
                log('删除所有id为...成功啦')
            }
        })
    }
    // removePostById('5a609fba3906973fc61f640b')

    // 3. 根据文章标题查找文章
    function getPostByTitle(title) {
        PostModel.find({ title }, (e, res) => {
            if (e) {
                err(e)
            } else {
                log(res)
            }
        })
    }

    // 4.更新文章
    function updatePost(id, title) {
        PostModel.update({ _id: id }, { title }, (e, res) => {
            if (e) {
                err(e)
            } else {
                log(res)
            }
        })
    }
    // updatePost('5a60a17d951bc340519c0e95','hey dolby')
})

// middleware中间件
PostSchema.pre('save', next => {
    log('hey i am pre hook')
    next()
})
PostSchema.post('save', next => {
    log('hey i am post hook')
})
```
执行现有的代码，得到：
```
hey i am pre hook
save time: 9.787ms
hey i am post hook
保存成功啦
```
证明钩子优先级大于自身回调

-----

### 常见报错
- `*** is not a constructor`
解决办法：
如：`CatSchema is not a constructor`。说明调用了new CatSchema来生成实例，但是Schema是不能生成实例的，必须到Model才能生成实例，修改`new CatSchema`为`new CatModel`

- `Schema is not defined`
解决办法：
Schema需要引入，如`const Schema = require('mongoose').Schema`或者`const Schema = mongoose.Schema`

-----

### 实践结论
- 依赖于其他表时需要用到ObjectId
- hook钩子（pre，next）优先级大于自身回调
- populate用于处理关联表

-----

### [查询Mongoose API](http://devdocs.io/mongoose/api)

