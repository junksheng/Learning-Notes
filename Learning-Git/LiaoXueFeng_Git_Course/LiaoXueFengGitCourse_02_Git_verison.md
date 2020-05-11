---
title: LiaoXueFengGitCourse_01_Git_Basic.md
Date:  2020-05-11 19:54
summary: 廖雪峰Git教程 第二章	时光穿梭机
---



[时光穿梭机](https://www.liaoxuefeng.com/wiki/896043488029600/896954074659008)



### 时光机穿梭

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