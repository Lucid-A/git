# git 的一些基本概念
我们经常在自己本地编程，也经常会写出一堆 bug ，有时候改 bug 改着改着发现还是原来好，有的时候做优化优化着优化着发现还是原来好，这个时候我们的代码可能已经和“原来”完全不同，面目全非，这个时候我们就需要使用版本管理工具来保存历史版本，git 就是其中常用的一个版本管理工具。
而国外的 github 和国内的 gitee 是两个比较常用的使用git工作流来做版本管理的网站，便于我们远程保存自己的个人项目和进行团队项目协作，处理代码中出现的问题。
github 等网站的作用是远程仓库，对于个人项目来说并不是必须的，git 软件本身可以在本地就完成你的个人仓库版本管理。
接下来先从个人本地仓库的管理开始介绍，首先我们要了解一些概念。

## 工作区域
git 划分了三个区域：工作区、暂存区、仓库区
在这里**区域**是个抽象的概念，并不一定特指某一个文件夹之类的东西，而更像是文件的一个**状态属性**
+ 工作区
    - 我们可以在此进行文件的新建、修改等操作
    - 通常指".git"隐藏文件夹所在的父目录
+ 暂存区
    - 我们可以在此暂时保存一些文件的快照。
    - 某一个改动可能涉及多个文件，我们希望一次性提交这些改动，成为同一个**修改版本**，暂存区就可以让我们先行暂存已经改好的一些文件，等待未改好的文件
    - 暂存区内的文件与工作区的同名文件毫无关联，这意味着如果暂存区中的文件对应的文件在工作区中被修改后，可以利用暂存区的快照进行回滚
+ 仓库区
    - 相当于一个档案馆，保存了我们过去的每一个版本。方便我们进行**版本回滚**工作，起到**保留历史数据**等一系列作用

## 分支
在 git 中，我们初始就有一个主分支 master (据说因为某事件，可能改名 main )，它相当于我们的树干，从树干上我们可以分出许多分支，名字可以由我们自己命名。
当建立分支时，分支上会有建立分支位置之前的分支(通常是 master )之前的所有文件的到目前为止的所有版本，实际结构如图所示。
我们可以在分支上进行修改而不影响原分支上的源文件。
修改完成之后我们可以提交审核申请，即所谓"pull request"，在经审核通过后即可 merge 到原分支上，一般情况下，git 可以自行完成 merge 操作。
然而有些时候，会发生版本冲突，比如，在 merge 回原分支之前，该分支建立时的依赖的原文件已经发生了改变，这时就需要我们手动进行合并。

## HEAD指针
这个指针指向我们当前分支的当前版本的位置，如果需要回滚到某一个版本，实际是将HEAD指针指向该版本，并衍生出另一条分支进行后续开发，原来被回滚的那部分代码**仍然存在**，可以使用查看过去操作的方式找到log中不再显示的版本并再次回滚，详细指令见 git_commands.md

## 远程 git 仓库
在团队协作中，远程仓库的作用十分巨大，相当于本地仓库的一个备份，同时也方便每个人的更改的最终合并，并对成员权限进行细分。
以下均以 github 为例
***待补充***

### ss h免密登录
使用ssh秘钥可以免去每次使用本地 git 软件时读写仓库内容时要输入 github 账户密码的麻烦
1. 运行 cmd，(git bash 也可以)
2. 输入```ssh-keygen```
3. 随后一直 Enter 直至回到命令行
4. 在将命令行的起始地址调整至```C:/Users/用户名/.ssh```，这个位置也出现在之前运行"ssh-keygen"的过程中
5. 随后```type id_rsa.pub```，将显示出来的内容整体拷贝出来
6. 为你自己的账户进行设置，在头像旁的小三角菜单里找到 setting
7. 找到"SSH and GPG keys"
8. 点进去，最上方有绿色按钮"New SSH key"
9. 将刚刚复制的内容整体粘帖进去并保存即可
10. 在 clone 仓库时使用 ssh 方式对应的 URL
