# Git入门
1. Git是目前世界上最先进的分布式版本控制系统
2. 用Debian或Ubuntu Linux，通过一条`sudo apt-get install git`就可以直接完成Git的安装，非常简单。

# Git命令
**1. 创建git仓库**
假设现在linux的pwd显示当前路径为/users/ling/myGit,可以使用以下命令创建git仓库,创建完毕后会发现一个.git文件,目录一般为隐藏的,`ls-ah`可以查看
`git init`


**2. 添加文件到工作区**
`git add`

**3. 将工作区文件提交到仓库**
`git commit -m "xxx"`
其中xxx为这次提交的描述信息,只对add操作时的修改状态提交.
例如:
当你用git add命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，在工作区的第二次修改并没有放入暂存区，所以，git commit只负责把暂存区的修改提交了，也就是第一次的修改被提交了，第二次的修改不会被提交。

**4. 查看当前仓库状态**
`git status`

**5. 查看上次修改情况**
`git diff + 文件名`

**6. 查看修改历史**
`git log`
加入
`--pretty=oneline`
可以简化输出日志信息
```linux
e475afc93c209a690c39c13a46716e8fa000c366 add distributed
eaadf4e385e865d25c48e7ca9c8395c3f7dfaef0 wrote a readme file
```

==以上日志信息中,前方数字为版本号,后面为描述信息==

**7. 回退版本**
`git rest --hard HEAD^`
其中,`HEAD`表示当前版本,`HEAD^`表示上一版本,`HEAD^^`表示上上版本.`HEAD~+数字+`,表示返回上N个版本.

**8. 查看过去使用的命令**
`git reflog`,结合`git reset --hard`,通过查找过去版本ID,在reset命令后加入版本号即可

**9. 撤销修改**
`git checkout -- +文件名`
把该文件在工作区的修改全部撤销,有两种情况
*1*
`文件`自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
*2*
`文件`已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

**10. 删除文件**
`git rm +文件名`
如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，你只能恢复文件到最新版本，你会丢失**最近一次提交后你修改的内容**。

**11. 本地仓库关联远程仓库**
在本地仓库下执行
`git remote add origin git@github.com:+GitHub用户名+/本地仓库名字.git`

其中`origin`为远程仓库名字,这是Git默认的叫法，也可以改成别的

**12. 推送本地仓库关联到远程**
`git push -u origin master`

*master:git默认当前分支名字,新建仓库时自动设置*
把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支`master`推送到远程。
由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

**13. 普通推送**
`git push origin (master)`
括号中为本地分支名字
注意文件修改需要在本地提交到版本库中

**14. 从远程库克隆**
`git clone git@github.com:(github用户名)/(仓库名字).git`


**15. 创建合并分支**
==每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即`master`分支。`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支。==

>![[Pasted image 20231019150338.png]]

**16. 创建并切换分支**
旧版
`git checkout -b (dev)`
创建并切换分支
相当于以下两个语句
`git branch dev`
`git checkout dev`

新版
创建并切换
`git switch -c dev`
切换到已有
`git switch master`


**17. 列出所有分支**
`git branch`

**18. 快速合并分支**
`git merge`命令用于合并指定分支到当前分支


**19. 删除分支**
`git branch -d dev`

**20. 合并分支**
>![[Pasted image 20231020141342.png]]
对于以上情况,Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，我们可以对冲突文件修改后保存,然后再次提交即可,如图
>![[Pasted image 20231020141549.png]]

**21. 查看分支合并情况**
`git log --graph --pretty=oneline --abbrev-commit`

**22. 分支管理策略**
`git merge --no-ff -m "merge with no-ff" dev`
表示强制禁用`Fast forward`模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
>![[Pasted image 20231020142136.png]]



**23. 储存工作区**
`git stash`
**24. 查看存储工作区**
`git stash list`
**25. 恢复存储的工作区**
一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；
另一种方式是用`git stash pop`，恢复的同时把stash内容也删了


26. 为当前分支复制某一提交
用`git cherry-pick <commit>`命令，把某一提交的修改“复制”到当前分支，避免重复劳动。`<commit>`里面填写提交的id号

27. 

