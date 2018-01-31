### Cheat Sheet
1. ```git status```: 查看当前状态
2. ```git commit -m '<message>'```: 提交修改
3. ```git diff <file_name>```: 查看修改的内容
4. ```git diff HEAD -- <file_name>```: 查看工作区和版本库最新版本的区别
4. ```git log <file_name>```: 查看日志
5. ```git reset --hard HEAD^```: 返回上一个版本
6. ```git reset HEAD <file_name>```: 撤销掉暂存区的修改，重新放回工作区
6. ```git reflog```: 查看记录的每一次命令
7. ```git reset --hard 版本号前n位```: 设置到版本号
8. ```git checkout -- <filename>```:
	* 修改后没有stage,撤销到和版本库一样
	* stage后又做修改，撤销到stage状态
	* 回到最近一次```commit```或者```add```状态
9. ```git rm <file_name>```: 从版本库里删除某个文件
10. ```git remote add origin <git_url>```: 将本地版本库与远程库关联
11. ```git push -u origin master```: 只有第一次推送master分支时才加上-u参数，git不但会把本地master分支内容推送到远程新的master分支，还会把本地和远程的master分支关联起来，以后推送或拉取就可以简化命令. 
12. ```git clone <git_url>```: 从远程库克隆
13. ```git checkout -b <branch_name>```: 创建并切换到新的分支上.
14. ```git branch <branch_name>```: 创建branch
14. ```git branch <branch_name> origin/<branch_name>```: 创建远程origin的分支到本地
15. ```git checkout <branch_name>```: 切换到某分支
16. ```git branch```: 列出当前所有branch. 
17. ```git merge <branch_name>```: 将指定分支merge到当前分支上
18. ```git branch -d <branch_name>```: 删除某个branch
19. ```git log --graph --pretty=oneline --abbrev-commit```: 查看图形的分支合并情况
20. ```git merge --no-ff -m '<message>' <branch_name>```: 保留分支信息的merge
21. ```git stash```: 将当前工作现场储藏起来，等以后恢复现场后继续工作. 
22. ```git stash list```: 查看之前存好的工作现场. 
23. ```git stash apply```: 恢复现场，但不删除stash内容
24. ```git stash drop```: 删除stash内容
25. ```git stash pop```: 恢复的同时把stash内容删除
26. ```git remote```: 查看远程库信息
27. ```git remote -v ```: 远程库详细信息
### Knowledge!
1. ```commit id```不是数字，而是SHA1计算出来的特殊字符串. 
2. ```HEAD```表示当前版本, ```HEAD^```表示上一个版本， ```HEAD~100```
3. ```Working Directory```: 电脑里的目录
4. ```Repository```:  版本库， ```.git```. 
5. ```Stage```: 暂存区，工作区的变化在```add```之后进入stage, 之后```commit```将暂存区的内容统一提交到branch上
6. Git跟踪的是修改而不是文件
7. ```checkout```其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以一键还原
8. 找一台电脑充当服务器，24小时开机，其他人都从这个服务器克隆一份仓库到自己电脑上，并且各自把各自的提交推送到服务器仓库里，也从服务器仓库拉取别人的提交. ```origin```是远程库的名字，这是git默认的叫法， 也可以改成 origin别人一看就知道是远程库. 
9. ```git clone```从远程库直接克隆一个一模一样的版本库到本地. 
10. 所谓分支，就是每次提交串成的一条时间线. 一个版本库可以有多条平行的时间线. 
11. master是为主分支
12. ```HEAD```不是指向提交，而是指向```master```, ```master```才是指向提交的. 
13. 创建分支时例如叫dev， git新建了一个指针dev，指向与master相同的提交. 再把HEAD指向dev, 表示当前分支在dev上. 
14. git创建一个分支很快，只需要增加一个指针，然后改变HEAD的指向. 
15. 当dev线上进行提交以后，dev指针不断向前走，master此时不变. 
16. 当dev的工作上完成了，就把dev合并到master上. git只需要把master指向dev的当前提交就完成了合并. 
17. 真的形成分支后就不能快速合并了. 只能试图把各自的修改合并起来，但是可能会有冲突。 
18. 合并分支时，如果可能，git会使用```fast forward```模式，但是删除分支后就会丢掉分支信息
19. 最佳实践：master分支应该是非常稳定的，仅仅用来发布新版本，平时不能在上面干活
20. 确定哪个分支上修复bug,然后从该分支创建临时分支
21. 从远程仓库克隆时，git自动把本地的master分支和远程的master分支对应起来，远程仓库默认名称是```origin```.
21. ```fetch```是更新你的remote tracking branch. 
22. ```pull```=```fetch```+```merge```.bring a local branch up-to-date with its remote version, while also updating your other remote-tracking branches

