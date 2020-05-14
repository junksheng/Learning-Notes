---
title: 廖雪峰Git教程第四章---分支管理
Date:  2020-05-14 17:34
summary:  创建与合并分支, 解决冲突, 分支管理策略, Bug分支, Feature分支, 多人协作, Rebase
---

### [分支管理](https://www.liaoxuefeng.com/wiki/896043488029600/896954848507552#0)

分支在实际中的作用:

​		假设你准备开发一个新功能, 但是需要两周才能完成, 第一周你写了50%的代码, 如果立刻提交, 由于代码还没写完, 不完整的代码库会导致别人不能干活了. 如果等代码全部写完再一次提交, 又存在丢失每天进度的巨大风险. 

​		现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来的分支上，这样，既安全，又不影响别人工作。

​		Git的分支是与众不同的，无论创建、切换和删除分支，Git在1秒钟之内就能完成！无论你的版本库是1个文件还是1万个文件。



#### [创建与合并分支](https://www.liaoxuefeng.com/wiki/896043488029600/900003767775424)

​		每次提交, Git都把它们串成一条时间线, 这条时间线就是一个分支. 截止到目前, 只有一条时间线, 这个分支叫主分支, 即`master`分支. `HEAD`严格来说不是指向提交, 而是指向`master`, `master`才是指向提交的, 所以, `HEAD`指向的就是当前分支. 

​		一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点: 

![image-20200514174745259](LiaoXueFengGitCourse_04_Git_ManageBranch/image-20200514174745259.png)

​		每次提交, `master`就会向前移动一步. 



​		当我们创建新分支, 例如`dev`时, Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上：

![image-20200514174951970](LiaoXueFengGitCourse_04_Git_ManageBranch/image-20200514174951970.png)

​		不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变：

![image-20200514175033631](LiaoXueFengGitCourse_04_Git_ManageBranch/image-20200514175033631.png)

​		假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并：

![image-20200514175316439](LiaoXueFengGitCourse_04_Git_ManageBranch/image-20200514175316439.png)



​		当然, 这只是理想情况下, 还是你一个人处理代码, 如果多人协作的话会造成贼复杂的冲突. 



下面开始理想情况的实战: 

1. 创建`dev`分支, 然后切换到`dev`分支: 

```shell
$ git checkout -b dev
Switched to a new branch 'dev'
```

​		`git checkout`命令加上`-b`参数表示创建并切换, 相当于以下两条命令: 

```shell
$ git branch dev
$ git checkout dev
Switched to branch 'dev'
```



2. 然后, `git branch`可以查看当前分支: 

```shell
$ git branch
* dev
  master
```

​		当前分支前面会标一个`*`号. 



3. 修改文件, 然后提交. 

```shell
$ git add readme.txt 
$ git commit -m "branch test"
[dev 4dc3a6b] branch test
 1 file changed, 31 insertions(+)
```



4. 切回`master`分支: 

```shell
$ git checkout master
Switched to branch 'master'
```

​	   切换回`master`分支后，再查看一个`readme.txt`文件，刚才添加的内容不见了！因为那个提交是在`dev`分支上，而`master`分支此刻的提交点并没有变：

![image-20200514200107487](LiaoXueFengGitCourse_04_Git_ManageBranch/image-20200514200107487.png)



5. 合并`dev`分支到`master`分支上: 

```shell
$ git merge dev
Updating 0d43254..7bd6a31
Fast-forward
 ...xx.md      | 41 +++++++++++++++++++++++++++++++++++++
 1 file changed, 41 insertions(+)
```

​		`git merge`命令用于合并指定分支到当前分支。合并后，再查看改动的内容，就可以看到，和`dev`分支的最新提交是完全一样的。



6. 合并后, 可以删除掉`dev`分支: 

```shell
$ git branch -d dev
Deleted branch dev (was b17d20e).
```



7. 使用`git branch`, 只剩`master`分支: 

```shell
$ git branch
* master
```

​		因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在`master`分支上工作效果是一样的，但过程更安全。



**switch**

我们注意到切换分支使用`git checkout `，而前面讲过的撤销修改则是`git checkout -- `，同一个命令，有两种作用，确实有点令人迷惑。

实际上，切换分支这个动作，用`switch`更科学。因此，最新版本的Git提供了新的`git switch`命令来切换分支：

创建并切换到新的`dev`分支，可以使用：

```shell
$ git switch -c dev
```

直接切换到已有的`master`分支，可以使用：

```shell
$ git switch master
```

使用新的`git switch`命令，比`git checkout`要更容易理解



##### 小结

Git鼓励大量使用分支：

查看分支：`git branch`

创建分支：`git branch <name> `

切换分支：`git checkout <name>`或者`git switch <name> `

创建+切换分支：`git checkout -b <name> `或者`git switch -c <name> `

合并某分支到当前分支：`git merge <name> `

删除分支：`git branch -d <name> `