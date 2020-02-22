# 新流程拉取远程代码
## pull远程代码：
* 执行：`git pull —rebase`或`git pull —rebase origin master` ，为了pull远程代码的时候不会生成merge commit，融合成线性提交。一次push只能有一个commit
  origin master可以不写，执行这条命令的时候必须保证本地分支是clean的，如果本地有untracted file则不影响，可以先`git stash`，或者先`git commit -am 'comit描述'`或`git commit —amend`一下
* 如`git pull —rebase`（或者`git stash pop`）之后有冲突，可以手动解决冲突之后执行`git rebase —continue`；也可以用`git rebase --abort`放弃本次rebase操作，但最好还是解决冲突，不然冲突一直存在也无法合入。


```
git stash
git pull --rebase
git push
git stash pop
// 如果有冲突，可以解决冲突后执行下面这个命令，然后正常提交
git commit --amend
```


## 如何获取 unmerged commit
（1）当前基于master进行开发，假设有插入需求，并且不想本地维护代码的话，请先push commit，这个时候会生成一个评审
（2）需要在之前的commit基础上继续进行开发的时候，找到之前的评审，左上方有一个“下载”按钮，点击之后，会显示fetch命令，譬如`git fetch ssh://liulangyu@icode.baidu.com:8235/baidu/ucop/ranking refs/changes/87/10909687/1 && git checkout FETCH_HEAD`，在master下执行该命令。注意这个fecth命令是执行了两个git 操作：a. fetch代码；b. 切换分支到FETCH_HEAD，也就是fetch的头指针指向的节点。
（3）本地新建一个分支，新的分支只存在于本地，而且会保有前面的commit，命令：`git checkout -b <new-branch-name>`，git流程规范要求新建一个分支再merge到master.
（4）切换到master: `git checkout master`
（5）合并前面的分支: `git merge <new-branch-name>`
 (6) 对于push的时候出现上一个commit的author不是自己的情况，有两种解决方案：
 方案一：修改最后一次commit的author: `git commit -amend --reset-author`
 方案二：`git log`查看上一个不是自己提交的commit，然后`git reset --soft '上一个不是自己提交的commit id'`
（7）修改代码，正常commit（`git commit --amend`或`git commit -am 'commitm描述'`）