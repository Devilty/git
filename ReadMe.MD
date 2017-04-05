git 命令指南

1设置全局参数
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"

2在某个文件夹初始化 
git init

3添加到仓库 
git add <file> <file>

4提交
git commit -m <discrube>

5查看当前状态   可以查看当前有哪些文件被修改
git status 

6查看修改差异 (add 之前的差异)（add之后需要status才能看见？）
  如果git status告诉你有文件被修改过，用git diff可以查看修改内容。
git diff

7查看提交日志
git log 会显示最近三次commit的详情日志
git log --pretty=oneline 会精简化显示最近三次的commit日志

8回退 在Git中，用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。
git reset --hard HEAD^ 回退至上个版本
git reset --hard commit_id  回退某个版本

9查看修改日志的版本id
git reflog

10git回退
命令git checkout -- <file>
使用该命令会讲工作区的文件回退到暂存区 如果修改后还没放入暂存区则回退到版本库里面的状态
总之，就是让这个文件回到最近一次git commit或git add时的状态。
git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令
用命令git reset HEAD file可以把暂存区的修改撤销掉（unstage）

11删除文件
命令git rm删掉，并且git commit

12关联远程数据库
要关联一个远程库，
使用命令git remote add origin git@server-name:path/repo-name.git；
关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

13从远程仓库克隆
要克隆一个仓库，首先必须知道仓库的地址，然后使用git clone命令克隆。
Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

14git切换分支
git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：
$ git branch dev
$ git checkout dev
Switched to branch 'dev'

15查看分支
git branch命令会列出所有分支，当前分支前面会标一个*号。


16分支合并
git merge命令用于合并指定分支到当前分支。
合并完就可以删除dev分支了 
git branch -d dev
小结
Git鼓励大量使用分支：
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>
创建+切换分支：git checkout -b <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>

17解决冲突
Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，我们修改如下后保存：
git log --graph命令可以看到分支合并图。

18分支管理策略 
分支合并的话有可能Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
--no-ff可以禁用fast forwar
如$ git merge --no-ff -m "merge with no-ff" dev

19BUG分支
Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作
git stash 会保存当前现场（工作区 暂存区都会被储存）
git stash list 可以查看保存的现场 
git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除
git stash pop，恢复的同时把stash内容也删了：

20删除分支
git branch -D feature-vulcan 强制删除feature-vulcan分支
21 多人写作
22标签
git tag <name>

版本库介绍
一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；
第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
git diff HEAD -- readme.txt命令可以查看工作区和版本库里面最新版本的