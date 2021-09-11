# 本地仓库相关命令
+ 初始化新本地仓库：```git init <repository name>```
    - 此操作将在文件夹下建立新的隐藏文件夹".git"
    - ".git"文件夹所在目录为“工作区”
    - 会自动进入默认分支master
    - 此后，工作区内文件的新建、修改、删除将被git工具监视
+ 仓库设置：```git config```
    - 查看仓库设置：```git config --list```
    - 设置用户名：```git config --global user.name <name>```
    - 设置用户E-mail:```git config --global user.email <email address>```
    - 生成远程登录免密秘钥：ssh-keygen
+ 查看文件状态：```git status```
    - 会显示当前所在分支
    - 未被纳入版本管理的文件会被用红色标出，置于"Untracked files"下
    - 加入暂存区中的文件会被用绿色标出，置于"Changes to be committed"下
    - 加入暂存区后，又被修改，该文件会被用红色标出，出现在"Changes not staged for commit"下，此时可以进行回滚，见下
+ 将新文件纳入git版本管理、将被修改的文件放入暂存区：```git add <filename>```
    - 如果加入暂存区后又对文件进行了修改甚至删除，该文件会被用红色标出，置于"Changes not staged for commit"下
        + 该修改如果不需要，想要回到暂存区中的版本：```git restore <filename>```
        + 该修改是需要的，更新暂存区中的该文件快照：```git add <filename>```
+ 对于纳入git管理的文件进行删除：```git rm <filename>```
    - 对于```git add```命令不小心加入的不想被管理的文件，可以将其在暂存区内的快照删除，成为"Untracked files"：```git rm --cached <filename>```
    - 对于已经归档的文件，在下一版本中被删除，可以利用此命令将改动纳入暂存区：```git rm <filename>```
+ 将这一次改动整体进行提交：```git commit```
    -  提交版本信息：```git commit -m <"message">```
+ 查看之前的提交日志：```git log```
+ 查看之前的操作日志，比如回滚：```git reflog```
+ 版本回滚，即归档区回滚：```git reset [default: --mixed opt：--hard --soft] <version hash>```
    - <version hash>可以在git log后每一次提交的后面看到，是版本的标识，不需要完整输入，一般输入六位以上能够唯一确定一个版本就可以了，git会自动匹配
    - 回滚有三个选项
      + --mixed 回滚了归档区以及暂存区（default）
      + --soft  只回滚了归档区，但是暂存区和工作区没有任何变化，即改动仍在暂存区中
      + --hard  工作区、暂存区、归档区均被回滚
    - 可以仅对某一分支进行版本回滚
+ 删除某一次提交带来的影响：```git revert <version hash>```
+ 查看当前分支以及有哪些分支：```git branch```
    - 进一步查看分支的当前版本：```git branch -v```
+ 切换分支：```git checkout <branch name>```
    - 新建分支并切换：```git checkout -b <new branch name>```
+ 将某分支合并到当前分支：```git merge <branch name>```
+ 比较两个文件的不同：```git diff <file 1> <file 2>```
+ 比较两个版本的不同：```git diff <version hash 1> <version hash 2>```

# 远程仓库相关命令
+ 将远程仓库复制到本地:```git clone <repository address> [new name]```
+ 远程仓库：```git remote```
    - 查看本地仓库绑定的远程仓库等信息：```git remote -v```
    - 本地仓库绑定远程仓库：```git remote add <remote repository name> <remote repository url>```
        + <remote repository name>是指远程仓库在本地git中的别名，实际位置就是后面的URL，一般是origin，当你从远程仓库clone一份到本地时，远程仓库的默认别名也是origin
        + 修改绑定的远程仓库
            - 先移除原来绑定的那个远程仓库，<previous remote repository name>是你```git clone```时重命名的名字，或者是默认名"origin"：```git remote remove <previous remote repository name>```
            - 再次使用绑定远程仓库命令：```git remote add <remote repository name> <remote repository url>```
+ 设定本地分支对应的上层远程分支：```git branch --set-upstream-to=<remote repository name/branch name> <local branch name>```
+ 将本地仓库的内容提交至远程仓库：```git push <remote repository name> <the branch name you want to update>```
+ 将远程仓库的改变拉取到本地仓库：```git pull [remote repository name]```
    - 相当于以下两个指令([remote repository name]如果绑定的远程仓库唯一，则可略，否则一般是默认的origin)
        + ```git fetch  [remote repository name]```
        + ```git merge  [remote repository name/remote repository branch name]```

# 文件相关命令
+ 创建文件夹：```mkdir <directory name>```
+ 创建文件：```touch <file name>```
+ 删除(参数可以放一起 如rm -rf *)：```rm <file name>```
    - 删除空文件夹：```rm -d <directory name>```
    - 递归删除，即删除文件夹以及其中所有内容：```rm -r <file name>```
    - 强制删除，忽略不存在的文件和警告，从不请求：```rm -f <file name>```
    - 删除每个文件时请求: ```rm -i <file name>```
    - 当删除超过三个文件或递归删除时请求：```rm -I <file name>```
+ 打印目录中所有文件：```ls```
