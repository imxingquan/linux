# Linux 学习笔记
## Git用法
1. 从远程主机Clone代码到本地
    git clone https://github.com/imxingquan/linux-study
2. 远程主机名
    git remote 显示远程主机名 默认显示 origin
    git clone -o <新的主机名> https://github.com/imxingquan/linux-study
    git remote show <主机名> 可以查看该主机的详细信息
3. 更新代码到本地
    git fetch <远程主机名> 
4. 取回远程主机某个分支的更新，再与本地的指定分支合并
    git pull
5. 将本地分支的更新，推送到远程主机
    git push <远程主机名> <本地分支名>:<远程分支名>
    git push origin master 将本地的master分支推送到origin主机的master

用法顺序
    本地修改代码 提交到服务器的git命令顺序  
    git add .  
    git commit -m 'my commit'  
    git push  

参考：http://gitref.org/zh

