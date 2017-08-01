# **status**
git status 需要经常用到的查看文件状态的命令

# **rm**
git rm file 删除了一个文件并将被删除的文件纳入到暂存区（stage, index）
rm file 被删除的文件不会被提交到暂存区，这是和 git rm的区别，同样的操作还有mv...

# **merge**
git merge xxx 将xxx分支的修改合并到当前分支

# **head**
head 指向当前分支,可以查看.git下的HEAD来查看当前分支

# **master** 
master指向最近提交的提交

# **reflog**
git reflot历史所操作的日志

# **commit**
git commit -m "comment" 将暂存区的修改提交到版本库
git commit --amend -m "comment"修改上一次提交的注释
git commit -am "xxx" 添加到暂存区并且提交

# **branch**
git branch 查看所有的分支，带*为当前的分支
git branch xxx  新建一个xxx分支
git branch -d xxx 删除xxx分支,如果被删除的分支有修改没有被merge，则会提示无法删除，改变参数 -D可以强制删除
git branch xxx commit_id 创建一个xxx分支，以一个给定的commit_id为基准（针对游离状态分支的一些提交）
git branch -m branch1 branch2 将brache1改名为branch2
git branch -a查看所有的分支，会额外查看到一个与远程关联的本地origin/master分支（本地的origin/master会和远程分支的状态相关联，每次push或者pull都会更新这个分支的状态，系统自动维护这个分支，我们无法去修改）


# **checkout **
git checkout xxx 切换到xxx分支
git checkout commit_id 进入到<font color=red>游离状态</font>的一个提交点，可以进行一些测试的修改，切换到其他分支，将会提示一个错误，需要提交游离的修改或者stash,如果是提交了修改，切换到其他分支的时候会被警告:
>you are leaving 1 commit behind, not connected to any of your branches: d40139f detached commit ,If you want to keep it by creating a new branch, this may be a good time to do so with: git branch new-branch-name d40139f

git checkout  -b xxx等同于，git branch xxx  ,  git checkout xxx
git checkout -b xxx yyy上一个命令默认基于master创建一个本地分支xxx，此命令基于一个本地已经关联的远程yyy分支（git branch -av remotes/origin/yyy）来创建一个分支
git checkout --track yyy 同上命令一样的功能，但是没有指定本地需要创建的分支的名字，默认是和本地的远程分支同名
git checkout  -- file 丢弃工作区指定文件的修改,<font color=red>使之返回到暂存区的状态</font>

# **reset**
git reset HEAD file <font color=red>将添加到暂存区的内容恢复到工作区</font>
git reset --hard HEAD^ 一个^代表往前一个版本回退
git reset --hard HEAD~1 数字代表往前多少个版本回退
git reset --hard commit_id 回退到确定的一个commitid上

# **stash**
git stash 将当前分支的修改临时保存起来，让当前分支可以切换到其他分支
git stash list 展示所有的stash列表
git stash save xxx 生成stash的同时有xxx注释
git stash apply stash@{x}  应用stash@{x}这个stash,默认应用最新的一个stash
git stash pop 在当前分支应用最新的一个stash并且删除这个stash
git stash drop stash@{x} 手动删除stash@{x}

# **tag**
标签属于一个静态的概念，一般都是用来记录某一个时期一个版本的快照
git tag 查看标签
git tag -l xxx 查看具体的标签，可以使用通配符
git tag xxx 创建一个轻量级标签
git tag -a xxx -m xxx 创建一个带有附注的标签
git tag -d xxx 删除标签

# **blame**
git blame xxx 查看文件的上一次提交的作者和修订

# **diff**
系统自带的diff(mac):
diff -u a b
```
--- a	2017-07-26 22:56:43.000000000 +0800
+++ b	2017-07-26 22:57:02.000000000 +0800
@@ -1,3 +1,3 @@
 hello world
-hello java
-hello ios
+hello python
+hello android
```

---代表源文件a,+++代表目标文件
-1，3表示源文件第一行到第三行来进行比较，+1，3目标文件从第一行到第三行被比较
-hello java表示删除这一行，+hello python表示加上这一行
之后a会得到b中一样的内容

git diff 表示暂存区与工作区的区别
git diff HEAD 表示本地版本库与工作区的区别
git diff commit_id 表示特定的一个版本与工作区比较
git diff --cached 【commit_id】 表示最新版本仓库与暂存区的比较

# **clone**

git clone url xxx: 克隆到本地以xxx命名

# **add**
git add xxx 
1. 将未追踪的文件纳入到缓存区中
2. 将工作区已经修改的文件纳入到缓存区中
3. 将解决完后的冲突文件标识为已经解决冲突

# **pull**
将远程仓库代码拉取到本地并merge。相当于git fetch , git merge (origin/master)

# **fetch**
将最新远程代码拉取到本地origin/master，这个操作一定会成功

# **push**
创建远程分支：
git push --set-upstream origin xxx:yyy  在远程分支创建一个yyy分支和本地的xxx分支关联（也可以写成git push -u origin xxx:yyy ），分支名可以只指定xxx，默认缺省会将远程和本地分支同名
推送到远程分支：
git push 默认会推送本地同名的分支到远程仓库
git push origin xxx:yyy: （完整写法）将本地的xxx分支推送到远程yyy分支，默认可以识别出远程分支和当前本地要推送的分支一样名字的分支
删除远程一个分支：
git push origin  :xxx ：删除一个远程的xxx分支（将一个空分支推送到远程xxx分支）
git push origin --delete xxx： 作用同上
