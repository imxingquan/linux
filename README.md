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
4. 将本地分支的更新，推送到远程主机
    git push <远程主机名> <本地分支名>:<远程分支名>
    git push origin
