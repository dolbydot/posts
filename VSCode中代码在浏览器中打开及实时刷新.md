#**open in browser**
在vscode扩展中搜索“view in browser”插件并点击安装，点击资源管理器选中当前文件右键选择“View In Browser”即可在默认浏览器中打开页面。
![](http://upload-images.jianshu.io/upload_images/6851923-70933a0c6bfe0f1c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----------

#**实时刷新方法一：livereload**
在项目目录下运行命令：

    browser-sync start --server --files "**/*.css,**/*.html,**/*.js"

**方法：**

 - “查看”中选择“集成终端”，命令行输入以上指令
![](http://upload-images.jianshu.io/upload_images/6851923-8ee1b5c5afeda1bb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

 - 本地文件右键选择“在终端中打开”，在终端命令行中输入指令
![](http://upload-images.jianshu.io/upload_images/6851923-082e5524c0a155a2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

以上两种方法实现的效果和原理相同，都可后台运行，按下快捷键“control+c”退出当前运行进程。

----------
#**实施刷新方法二：**
装Live HTML Previewer插件，点击页面左下角Preview Available。

----------
***注意：***有了livereload可以不需要装“view in browser”插件。