## Git仓库迁移

1、从原地址克隆一份裸版本库，比如原本托管于 GitHub。

```
git clone --bare http://github....(原始仓库地址)
```

2、进入克隆下来的目录

cd project.git（project即为你的项目名称）

 3、以镜像推送的方式上传代码到新的仓库地址。

git push --mirror http：//...(目标仓库地址)





问题1：Git本地没有push,本地仓库打了tag之后只把tag push了，远程仓库该tag下是最新的代

Git一共有四种类型的对象：数据对象（blobobject）、树对象（treeobject）、提交对象（commitobject）和标签对象（tagobject）。其中标签对象和提交对象非常类似，可以理解为是提交对象的一个引用。我们每次运行gitadd和gitcommit命令时，实际上是将被改写的文件保存为数据对象和树对象，并创建一个提交对象指向顶层的树对象，这些对象保存在.git/objects目录下。

其次，Git一共有三种类型的引用：HEAD引用、标签引用和远程引用，他们分别保存在refs/heads、refs/tags和refs/remotes三个目录下。HEAD引用代表你创建的代码分支，标签引用代表你创建的所有标签。你可以打开三个目录下的文件看看，实际上就是一个纯文本文件，里面记录着提交对象（或标签对象）的SHA-1哈希值，代表这个引用指向哪一次提交。

所以，当你推一个tag到远程仓库时，是在远程仓库的refs/tags目录下创建一个标签引用，它要指向一个提交对象，而这个对象由于你还没push，也会打包发送到服务器上。但是，由于HEAD引用并没有更新，所以随便checkout到哪个分支都看不到这次提交，只有checkout到指定的tag，才能看到这次提交。