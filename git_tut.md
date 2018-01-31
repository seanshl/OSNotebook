### Cheat Sheet
1. ```git status```: 查看当前状态
2. ```git commit -m '<message>'```: 提交修改
3. ```git diff <file_name>```: 查看修改的内容
4. ```git diff HEAD -- <file_name>```: 查看工作区和版本库最新版本的区别
4. ```git log <file_name>```: 查看日志
5. ```git reset --hard HEAD^```: 返回上一个版本
6. ```git reflog```: 查看记录的每一次命令
7. ```git reset --hard 版本号前n位```: 设置到版本号
8. ```git checkout -- <filename>```:
	* 修改后没有stage,撤销到和版本库一样
	* stage后又做修改，撤销到stage状态
	* 回到最近一次```commit```或者```add```状态
    

### Knowledge!
1. ```commit id```不是数字，而是SHA1计算出来的特殊字符串. 
2. ```HEAD```表示当前版本, ```HEAD^```表示上一个版本， ```HEAD~100```
3. ```Working Directory```: 电脑里的目录
4. ```Repository```:  版本库， ```.git```. 
5. ```Stage```: 暂存区，工作区的变化在```add```之后进入stage, 之后```commit```将暂存区的内容统一提交到branch上
6. Git跟踪的是修改而不是文件
