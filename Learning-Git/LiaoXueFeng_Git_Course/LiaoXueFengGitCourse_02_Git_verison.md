---
title: LiaoXueFengGitCourse_01_Git_Basic.md
Date:  2020-05-11 19:54
summary: 廖雪峰Git教程 第二章	时光穿梭机
---



### [时光穿梭机](https://www.liaoxuefeng.com/wiki/896043488029600/896954074659008)

`git status`可以让我们时刻掌握仓库当前状态. 比如我更改了这个文件. 

```shell
$ git status
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        modified:   Learning-Git/LiaoXueFeng_Git_Course/LiaoXueFengGitCourse_02_Git_verison.md

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  (commit or discard the untracked or modified content in submodules)

        modified:   Blog/themes/hexo-theme-matery (modified content)
        modified:   Learning-Git/LiaoXueFeng_Git_Course/LiaoXueFengGitCourse_02_Git_verison.md

```

会提示这个文件已经被修改过了, 但是还没有准备提交的修改. 



`git diff`可以和上次提交相比较, 查看具体修改的内容. (可以加文件名, 也可以不加, 不加的话是全部修改过的文件)



然后用`git add`命令提交到缓冲区, 再使用`git commit`命令提交就好了. 



#### 小结

+ 要随时掌握工作区的状态, 使用`git status`命令. 
+ 如果`git status`告诉你有文件被修改过, 用`git diff`可以查看修改内容. 



### [版本回退](https://www.liaoxuefeng.com/wiki/896043488029600/897013573512192)



不断地对文件进行修改, 然后不断提交到版本库里, 就像游戏存档. 

随着时间地推移, 我们已经记不住我们修改地版本有哪些, 这时候可以使用`git log`命令查看. 

```shell
$ git log
commit adc1a90446a667785ab856e342e31506b90b285c (HEAD -> master)
Author: junksheng <junk.sheng@foxmail.com>
Date:   Mon May 11 20:14:17 2020 +0800

    Learn the Git about Liaoxvefeng in 版本回退

commit 16cbbfdbe70091fe011bac8970b00fb992151d14
Author: junksheng <junk.sheng@foxmail.com>
Date:   Mon May 11 20:05:10 2020 +0800

    Learn the Git about Liaoxvefeng

commit 2e4ba41d528c453cdd4883c5480d194cc6f92580
Author: junksheng <junk.sheng@foxmail.com>
Date:   Mon May 11 19:55:27 2020 +0800

    the git init
```

`git log` 命令显示从最近到最远的提交日志, 如果嫌输出信息太多, 看得眼花缭乱的, 可以试试加上`--pretty=oneline`参数: 

```shell
$ git log --pretty=oneline
adc1a90446a667785ab856e342e31506b90b285c (HEAD -> master) Learn the Git about Liaoxvefeng in 版本回退
16cbbfdbe70091fe011bac8970b00fb992151d14 Learn the Git about Liaoxvefeng
2e4ba41d528c453cdd4883c5480d194cc6f92580 the git init
```

会显示每一次的 `版本号+commit说明`. 



`$ git reset --hard HEAD^`回退到上一个版本

```shell
$ git add .

$ git commit -m "版本回退尝试"
[master d659bf7] 版本回退尝试
 1 file changed, 38 insertions(+), 1 deletion(-)
 
$ git add .

$ git commit -m "废弃的版本"
[master a037a10] 废弃的版本
 1 file changed, 2 insertions(+)
 
$ git reset --hard HEAD^
HEAD is now at d659bf7 版本回退尝试
```

使用命令`$ git reset --hard HEAD^`可以看到确实从 "废弃的版本" 回退到了 "回退版本尝试". 



运行`git log --pretty=oneline`发现废弃版本不见了.

```shell
$ git log --pretty=oneline
d659bf7378afc82532cf5474f8fa774bd2fdbdbb (HEAD -> master) 版本回退尝试
adc1a90446a667785ab856e342e31506b90b285c Learn the Git about Liaoxvefeng in 版本回退
16cbbfdbe70091fe011bac8970b00fb992151d14 Learn the Git about Liaoxvefeng
2e4ba41d528c453cdd4883c5480d194cc6f92580 the git init
```



"废弃的版本"找不到了, 当如果你没有关闭当前命令行, 你可以找到"废弃的版本"的版本号`commit id`, 使用`git reset --hard 1904a(commit id)`去恢复它, 版本号没必要写全, Git会自动去找. 



我特么, 提交了"废弃的版本"没有查看版本号...所以不能恢复了...

但我会就这样放弃吗? 不可能的.

通过命令`git reflog`可以看到你的`head`指针指过的版本号.

```shell
$ git reflog
d659bf7 (HEAD -> master) HEAD@{0}: reset: moving to HEAD^
a037a10 HEAD@{1}: commit: 废弃的版本
d659bf7 (HEAD -> master) HEAD@{2}: commit: 版本回退尝试
adc1a90 HEAD@{3}: commit: Learn the Git about Liaoxvefeng in 版本回退
16cbbfd HEAD@{4}: commit: Learn the Git about Liaoxvefeng
2e4ba41 HEAD@{5}: commit (initial): the git init
```

这不就有了吗??? 哈哈哈, 但我还是不想回退, 因为我记了笔记了, 麻烦...

