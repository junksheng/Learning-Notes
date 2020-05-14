---
title: 廖雪峰Git教程第三章---远程仓库
Date:  2020-05-13 16:10
summary:  添加远程库, 从远程库克隆
---

### [远程仓库](https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416#0)

这个世界上有一个叫做[Github](https://github.com/)的神奇网站, 提供者Git仓库的托管服务. 

由于你的本地Git仓库和Github仓库之间的传输是通过SSH加密的, 所以需要设置一下ssh. 

1. 创建SSH Key, 在你的电脑创建SSH Key: (非军事目的, 可以不设置密码)

   ```shell
   $ ssh-keygen -t rsa -C "youremail@example.com"
   ```

2. 找到用户主目录里的`.ssh`目录, 里面的`id_rsa`是私钥, 不能泄露出去, `id_ras.pub`是公钥, 需要交出去. 

3. 在GitHub的"Account settings", "SSH Keys"页面, 点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容. 



为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推送。

当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提交，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

最后友情提示，在GitHub上免费托管的公共Git仓库，任何人都可以看到喔（但只有你自己才能改）。所以，不要把敏感信息放进去。



### [添加远程库](https://www.liaoxuefeng.com/wiki/896043488029600/898732864121440)

现在是你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步. 



+ 首先需要在`Github`创建一个新的仓库. 这个直接在`Github`页面就能找到, 填上仓库名就行和选择public or private, 其他选项默认. 



+ 然后在本地你的仓库下运行命令: 

```shell
$ git remote add origin git@github.com:GithubName/RepoName.git
```

添加后，远程库的名字就是`origin`，这是Git默认的叫法，也可以改成别的，但是`origin`这个名字一看就知道是远程库。



+ 下一步，就可以把本地库的所有内容推送到远程库上：

```shell
$ git push -u origin master
Counting objects: 20, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (15/15), done.
Writing objects: 100% (20/20), 1.64 KiB | 560.00 KiB/s, done.
Total 20 (delta 5), reused 0 (delta 0)
remote: Resolving deltas: 100% (5/5), done.
To github.com:michaelliao/learngit.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.

```

把本地库的内容推送到远程，用`git push`命令，实际上是把当前分支`master`推送到远程。

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。



+ 推送成功后, 打开你的`Github`仓库, 可以发现你的远程库内容已经和本地一摸一样了. 
+ 从现在起, 只要本地作了提交, 就可以通过命令: 

```shell
$ git push origin master
```

把本地`master`分支的最新修改推送至GitHub，现在，你就拥有了真正的分布式版本库！



#### 小结

要关联一个远程库，使用命令`git remote add origin git@server-name:path/repo-name.git`；

关联后，使用命令`git push -u origin master`第一次推送master分支的所有内容；

此后，每次本地提交后，只要有必要，就可以使用命令`git push origin master`推送最新修改；

分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！





### [从远程库克隆](https://www.liaoxuefeng.com/wiki/896043488029600/898732792973664)

使用命令`git clone`克隆一个本地库:

```shell
$ git clone git@github.com:michaelliao/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 3
Receiving objects: 100% (3/3), done.
```

当然, 也可以使用`https`, 但速度比较慢, 而且每次推送都必须输入口令, 但是在某些只开放http端口的公司内部就无法使用`ssh`协议而只能用`https`。



#### 小结

要克隆一个仓库，首先必须知道仓库的地址，然后使用`git clone`命令克隆。

Git支持多种协议，包括`https`，但`ssh`协议速度最快。