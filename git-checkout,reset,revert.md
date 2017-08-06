
### 撤销
1. git checkout -- HEAD <filename>  撤销本地未暂存的修改
2. git reset --hard <commitid>  **代码回滚**， 本地不保存<commitid>后的所有修改
3. git reset --soft <commitid>   **代码回滚**，本地编辑仓库保存<commitid>后的所有修改
4. git revert <commitid> 撤销**某次**提交历史

### 分支

### 标签


### ErrorLogs

1. fatal: refusing to merge unrelated histories
**解决方案**:自[git2.9.0](https://github.com/git/git/blob/master/Documentation/RelNotes/2.9.0.txt#L58-L68)后，git默认不再允许两个没有公共base的仓库进行直接合并，如果在远程GitHub分支创建时选择了README.md，**且在本地有自己的commit历史**，这个时候直接进行git pull(其实是git fetch 和git merge 的简写)在git看来是不合法的，因此，需要pull或者merge时添加--allow-unrelated-histories选项才可以完成合并
















### 获取git仓库
有两种取得git仓库的方法，第一种是在现有目录下导入所有文件到git中，另一种是从一个服务器克隆一个现有的git仓库。

##### 在现有目录中初始化仓库并与远程仓库连接
如下：
- 在当前目录下创建一个名为project的文件夹，在里面新建一个名为1.txt、内容为"hello"的文件，输入命令`git init`，目的是创建一个名为`.git`的子目录，这个子目录中含有初始化git仓库中的所有必须文件，不确定是否初始化了.git仓库可以`ls -la`查看一下。

![](http://upload-images.jianshu.io/upload_images/6851923-a0581ed82182fbd3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 本地仓库创建好了，下一步是本地git仓库与远程git仓库建立连接。首先在github上创建一个名为project的仓库。

![](http://upload-images.jianshu.io/upload_images/6851923-1c83255172efdcb4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

**注意： 千万不要勾选README.md选项**，多次验证表明勾选了这一项之后，后面会出bug，具体原因暂时不清楚。






创建完成后复制当前git仓库的url：
![](http://upload-images.jianshu.io/upload_images/6851923-883e200e25ab0194.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

在命令行输入`git remote add origin git@github.com:dolbydot/project.git
`，没有报错的话证明本地仓库与远程仓库已成功建立连接。

![](http://upload-images.jianshu.io/upload_images/6851923-35f118095a8bffaf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 此时的工作目录并不干净，`git status`查看一下目前状态，会提示当前工作目录下的文件没有添加到暂存区，命令行依次输入`git add .`，`git commit -am "aaa"`将文件添加到暂存区并将暂存区的更新提交到本地库。

![](http://upload-images.jianshu.io/upload_images/6851923-5a59610b40b13578.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 下一步就是将本地仓库中的文件push到远程master分支上，每次push之前pull一遍有利于养成良好的协同工作习惯和减少代码冲突，如图只有我一个人在编辑这个名为project的GitHub项目，在pull时显示当前分支没有被跟踪的文件，所以可以放心大胆地push。

![](http://upload-images.jianshu.io/upload_images/6851923-88a302a321232804.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

- 打开GitHub project仓库检查远程仓库与本地是同步的就可以了。

![](http://upload-images.jianshu.io/upload_images/6851923-6e5fb1374c5f1cec.png)

##### 克隆已有的仓库
如果想获得一份已经存在了的 Git 仓库的拷贝，比如说，你想为某个开源项目贡献自己的一份力，这时就要用到 `git clone` 命令。
Git 克隆的是该 Git 仓库服务器上的几乎所有数据，而不是仅仅复制完成你的工作所需要文件。 当你执行 git clone 命令的时候，默认配置下远程 Git 仓库中的每一个文件的每一个版本都将被拉取下来。 事实上，如果你的服务器的磁盘坏掉了，你通常可以使用任何一个克隆下来的用户端来重建服务器上的仓库（虽然可能会丢失某些服务器端的挂钩设置，但是所有版本的数据仍在)
克隆仓库的命令格式是 `git clone [url]`
 。 url为被克隆的仓库链接，比如要克隆上面的project仓库可以用下面的命令：

![](http://upload-images.jianshu.io/upload_images/6851923-2b20b3c4f3aa284b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

这会在当前目录下创建一个名为 “project” 的目录，并在这个目录下初始化一个 .git
 文件夹，从远程仓库拉取下所有数据放入 .git文件夹，然后从中读取最新版本的文件的拷贝。 如果你进入到这个新建的project文件夹，你会发现所有的项目文件已经在里面了，准备就绪等待后续的开发和使用。 如果你想在克隆远程仓库的时候，自定义本地仓库的名字，可以使用如下命令：
`git clone git@github.com:dolbydot/project.git project1`
这将执行与上一个命令相同的操作，不过在本地创建的仓库名字变为project1。

Git 支持多种数据传输协议。 上面的例子使用的是 https:// 协议，也可以使用 git://
 协议或者使用 SSH 传输协议。

-----

### git仓库的三个组成
工作目录，缓存区和提交历史。
![](http://upload-images.jianshu.io/upload_images/6851923-ef222367389a0fdb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 记录每次更新到仓库
现在我们手上有了一个真实项目的 Git 仓库，并从这个仓库中取出了所有文件的工作拷贝。 接下来对这些文件做些修改，在完成了一个阶段的目标之后，提交本次更新到仓库。
请记住，你工作目录下的每一个文件都是这两种状态：已跟踪或未跟踪。 已跟踪的文件是指被纳入了版本控制的文件，在上一次快照中有它们的记录，在工作一段时间后，它们的状态可能处于未修改，已修改或已放入暂存区。 工作目录中除已跟踪文件以外的所有其它文件都属于未跟踪文件，它们既不存在于上次快照的记录中，也没有放入暂存区。 初次克隆某个仓库的时候，工作目录中的所有文件都属于已跟踪文件，并处于未修改状态。
编辑过某些文件之后，由于自上次提交后你对它们做了修改，Git 将它们标记为已修改文件。 我们逐步将这些修改过的文件放入暂存区，然后提交所有暂存了的修改，如此反复。所以使用 Git 时文件的生命周期如下：

![](http://upload-images.jianshu.io/upload_images/6851923-b001ff197a70d3a2.png)

##### 检查当前文件状态
要查看哪些文件处于什么状态，可以用 `git status`命令。 克隆仓库后立即使用此命令，会看到这样的输出：

![](http://upload-images.jianshu.io/upload_images/6851923-03dd2b34e00e86b9.png)

这说明现在的工作目录相当干净，即所有已跟踪文件在上次提交后都未被更改过。 此外，上面的信息还表明，当前目录下没有出现任何处于未跟踪状态的新文件，否则 Git 会在这里列出来。 最后，该命令还显示了当前所在分支，并告诉你这个分支同远程服务器上对应的分支没有偏离。 现在，分支名是 “master”,这是默认的分支名。
现在我们在项目下新建一个README文件，使用`gt status`命令，会看到一个新的未跟踪的文件。

![](http://upload-images.jianshu.io/upload_images/6851923-81faa4f048ef5a03.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

状态报告中可以看到新建的README文件出现在 Untracked files 下面。未跟踪的文件意味着 Git 在之前的快照（提交）中没有这些文件；Git 不会自动将之纳入跟踪范围。

##### 跟踪新文件
使用命令 `git add` 开始跟踪一个文件。 所以，要跟踪 README 文件，运行如下代码：

![](http://upload-images.jianshu.io/upload_images/6851923-375325ae94163495.png)

从状态报告中可以看出README文件已被跟踪并处于暂存状态。`git add` 命令使用文件或目录的路径作为参数，如果参数是目录的路径，该命令将递归地跟踪该目录下的所有文件。

##### 暂存已修改文件
如果修改了上面的README文件，运行`git status`命令会看到如下内容：

![](http://upload-images.jianshu.io/upload_images/6851923-a8d13807662a302d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

状态报告说明一跟踪文件的内容发生了变化但还未放到暂存区，要暂存这次更新，需要运行 `git add`命令。 这是个多功能命令：可以用它开始跟踪新文件，或者把已跟踪的文件放到暂存区，还能用于合并时把有冲突的文件标记为已解决状态等。 将这个命令理解为“添加内容到下一次提交中”而不是“将一个文件添加到项目中”要更加合适。 现在运行 `git add`将"README"放到暂存区，再看 `git status`的输出。

![](http://upload-images.jianshu.io/upload_images/6851923-b7b2daf5c8397de4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

现在文件已暂存，并在下次提交时被记录到仓库，假设此时，你想要在 README里加一行内容， 重新编辑存盘后，再运行 `git status` 看看：

![](http://upload-images.jianshu.io/upload_images/6851923-7293812055476d0f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

又同时出现暂存区和非暂存区，是因为Git 只暂存了运行 `git add` 命令时的版本，运行了 git add 之后又作了修订的文件，需要重新运行 git add 把最新版本重新暂存起来：

![](http://upload-images.jianshu.io/upload_images/6851923-2905c56a087aeca1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 状态简览
`git status` 命令的输出十分详细，但其用语有些繁琐。 使用 `git status -s`命令或 `git status --short `命令，将得到一种更为紧凑的格式输出。 运行 `git status -s` ，状态报告输出如下：

![](http://upload-images.jianshu.io/upload_images/6851923-c7462b0d5dcfe53d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

上面的状态报告显示： README是新添加到暂存区的文件。
新添加的未跟踪文件前面有 ?? 标记，新添加到暂存区中的文件前面有 A 标记，修改过的文件前面有 M标记， M 有两个可以出现的位置，出现在右边的 M 表示该文件被修改了但是还没放入暂存区，出现在左边的 M 表示该文件被修改了并放入了暂存区。 

##### 移除文件
要从 Git 中移除某个文件，就必须要从暂存区中移除然后提交。 可以用 `git rm` 命令完成此项工作，并连带从工作目录中删除指定的文件，这样以后就不会出现在未跟踪文件清单中了。
如果只是简单地从工作目录中手工删除文件，运行 git status 时就会在 “Changes not staged for commit” 部分（也就是 未暂存清单）看到：

![](http://upload-images.jianshu.io/upload_images/6851923-f4ca4c3f5eecd62f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

再运行`git rm`记录此次移除文件的操作：

![](http://upload-images.jianshu.io/upload_images/6851923-743d14be7405595a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-44c9b3b6b2c157f4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

下一次提交时该文件就不再纳入版本管理。如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 `-f`（即 force 的首字母），这是一种安全特性，用于防止误删还没有添加到快照的数据，这样的数据不能被 Git 恢复，所以要谨慎使用。

##### 移动文件（重命名文件）
Git 并不显式跟踪文件移动操作。 如果在 Git 中重命名了某个文件，仓库中存储的元数据并不会体现出这是一次改名操作。 要在 Git 中对文件改名，可以这么做：

![](http://upload-images.jianshu.io/upload_images/6851923-16ccf6d622c665ca.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

运行`git mv`相当于运行了以下三条命令：
`mv 1.txt 2.txt`
`git rm 1.txt`
`git add 2.txt`
Git 会意识到这是一次改名，两种方式结果相同。 二者唯一的区别是，mv是一条命令而另一种方式需要三条命令，直接用 git mv 轻便得多。

-----

### 查看提交历史
在提交了若干更新或克隆某个项目后，想查看提交历史可以使用`git log`命令。
命令行输入`git log`结果如下：

![](http://upload-images.jianshu.io/upload_images/6851923-b8e96b0ab77088e3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

默认不用任何参数的话，`git log` 会按提交时间列出所有的更新，最近的更新排在最上面。 这个命令会列出每个提交的 SHA-1 校验和、作者的名字和电子邮件地址、提交时间以及提交说明。
git log 有许多选项可以搜寻所要找的提交，一个常用的选项是 -p，用来显示每次提交的内容差异。 也可以加上 -2 来仅显示最近两次提交，我先新增一个1.txt文件推送到远程仓库。
再执行`git log -p -2`命令：

![](http://upload-images.jianshu.io/upload_images/6851923-dcb4c8b5bbe4b8cf.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-dfc146545848773b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

除了显示基本信息之外，还附带了每次 commit 的变化。 当进行代码审查，或者快速浏览某个搭档提交的 commit 所带来的变化的时候，这个参数非常有用。

-----

### 撤销操作
**结论**:



任何一个阶段，你都有可能想要撤消某些操作，有的撤销操作是不可逆的，这是在使用 Git 的过程中因误操作而导致之前的工作丢失的少有的几个地方之一。
有时我们提交完了发现漏掉了几个文件没有添加，或者提交信息写错了。 此时，可以运行带有 `--amend` 选项的提交命令尝试重新提交。
`git commit --amend`
如下图所示，我创建了两个文件分别为5.txt、6.txt，但只commit了5.txt，之后没有做任何修改，那么快照会保持不变，修改的只是提交信息，文本编辑器vim启动后，可以看到之前的提交信息，编辑后保存会覆盖原来的提交信息，这里我没有做任何改动，

![](http://upload-images.jianshu.io/upload_images/6851923-6f54cac67ab6a351.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/6851923-77179dd67367ef5c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

`git log -s`一下可以看到，近期只有一个提交版本，说明操作生效了。

![](http://upload-images.jianshu.io/upload_images/6851923-47b70923e7ce93c1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

##### 取消暂存的文件`git reset`
已经修改了两个文件并想将它们作为两次独立的修改提交，但却意外地输入了 `git add *` 暂存了它们两个。 如何只取消暂存两个中的一个呢？ 

![](http://upload-images.jianshu.io/upload_images/6851923-846e7070e59e8b69.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

`git status` 命令提示了你，通过`git reset HEAD <file>... `来取消暂存：生效于当前分支。

![](http://upload-images.jianshu.io/upload_images/6851923-9ba7c0cd01e11454.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

如上图所示，命令生效了，8.txt回退到了未暂存的状态。
# 
提交层面上，reset 将一个分支的末端指向另一个提交。这可以用来移除当前分支的一些提交。比如，下面这两条命令让 1分支向后回退了两个提交。
`git checkout hotfix
git reset HEAD~2`
分支末端的两个提交现在变成了悬挂提交，下次 Git 执行垃圾回收的时候，这两个提交会被删除。

除了在当前分支上操作，还可以通过传入这些标记来修改你的缓存区或工作目录：

- soft – 缓存区和工作目录都不会被改变
- mixed – 默认选项。缓存区和你指定的提交同步，但工作目录不受影响
- hard – 缓存区和工作目录都同步到你指定的提交

##### 撤销对文件的修改`git checkout`
向project仓库中添加一个demo.md文件，代码如下所示：

![](http://upload-images.jianshu.io/upload_images/6851923-55924c6b1718075c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

向文件中写入字符“9999”提交到暂存区后，发现要修改为“change9999”，这时查看git状态，有提示用`git checkout -- <file>...`命令撤销修改，那么执行`git checkout -- demo.md`命令可以使文本回退到“9999”这个版本，如下图所示，命令生效了。

![](http://upload-images.jianshu.io/upload_images/6851923-70b1b77ff000df97.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

需要注意的是，当传入分支名时，可以切换到那个分支，如`git checkout 1`表示将HEAD移到一个新的分支，然后更新工作目录。因为这可能会覆盖本地的修改，Git 强制你提交或者缓存工作目录中的所有更改，不然在 checkout 的时候这些更改都会丢失。和 git reset 不一样的是，git checkout 没有移动这些分支。git checkout对于快速查看项目旧版本来说。但如果你当前的 HEAD 没有任何分支引用，那么这会造成 HEAD 分离。这是非常危险的，如果你接着添加新的提交，然后切换到别的分支之后就没办法回到之前添加的这些提交。因此，在为分离的 HEAD 添加新的提交的时候你应该创建一个新的分支。

##### 取消一个提交的同时创建一个新的提交`git revert`
这是一个安全的方法，因为它不会重写提交历史，因此，`git revert` 可以用在公共分支上，`git reset` 应该用在私有分支上。
你也可以把 `git revert` 当作撤销已经提交的更改，而 `git reset HEAD` 用来撤销没有提交的更改。
就像 `git checkout` 一样，`git revert` 也有可能会重写文件。所以，Git 会在你执行 revert 之前要求你提交或者缓存你工作目录中的更改。
revert是撤销某次操作，此次操作之前的commit都会被保留，而reset是撤销某次提交，此次之后的修改都会回退到暂存区。
如下图所示：

![](http://upload-images.jianshu.io/upload_images/6851923-e1975bbdc0a12c82.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

丢弃最近的三个commit，回退到最近的第四个commit，并且提交一个新的commit来记录这次改变。
# 
小结：下面这个表格总结了这些命令最常用的使用场景。

|命令|作用域|常用场景|
|-----|-----|-----|
|git reset|提交层面|在私有分支上舍弃一些没有提交的更改|
|git reset|文件层面|将文件从缓存区移除|
|git checkout|提交层面|切换分支或查看旧版本|
|git checkout|文件层面|舍弃工作目录中的更改|
|git revert|提交层面|在公共分支上回滚更改|
|git revert|文件层面|无|
-----


### 

*参考资料*：
- 微信公众号：git小助手
- [*代码回滚：Reset、Checkout、Revert 的选择*
](https://github.com/geeeeeeeeek/git-recipes/wiki/5.2-%E4%BB%A3%E7%A0%81%E5%9B%9E%E6%BB%9A%EF%BC%9AReset%E3%80%81Checkout%E3%80%81Revert-%E7%9A%84%E9%80%89%E6%8B%A9)
