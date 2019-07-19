Git is a version control system.
入门：Git教程 廖雪峰https://www.liaoxuefeng.com/wiki/896043488029600

一、创建版本库
1.初始化一个Git仓库，使用 git init 命令（先创建一个空文件夹）
2.添加文件到Git仓库，分两步：
   a.使用命令git add <file>，注意，可反复多次使用，添加多个文件；
   b.使用命令git commit -m “<message>”，完成。
二、过去与未来
1.掌握工作区的状态，使用命令git status
  git diff 可以查看修改内容 （没有提交的修改内容） （git diff HEAD -- <file>查看某个文件当前修改）
  git log  可以查看提交历史记录
2.回到过去
  首先要知道回到哪个版本，HEAD表示当前，HEAD^表示上一个，HEAD^^上上个，HEAD~100，往上100个
  git reset --hard HEAD^   回到上一个版本
  从过去返回：git reset --hard ****（版本号）
             （git log可查看，很长一串，写前几个即可）
  git reflog 可以查看命令历史记录（如果找不到新版本的id）
3.概念问题
  版本库即仓库，里面有很多内容，最重要的是称为stage的暂存区，还有Git为我们创建的第一个分支master，以及指针HEAD
  So，git add 是把文件添加到暂存区，而git commit是把暂存区所有文件提交到当前分支
  Git是跟踪的修改（暂存区）。理清楚才能明白一些命令
4.撤销修改
  a.丢弃工作区的修改 git checkout -- file 
  b.已经add到暂存区，先git reset HEAD <file>回到工作区，再用a
  c.已经commit到版本库，可以使用版本回退（前提没有提交到远程库） 
5.删除文件
  删除也是一种修改
  工作区删除 rm test.txt 
  a.确实删除  git rm 并且git commit
  b.删错了  git checkout -- file
三、远程仓库
1.创建SSH秘钥 ssh-keygen -t rsa -C "youremail@example.com"，可在用户主目录中找到id_rsa和id_rsa.pub两个文件
  登录GitHub Add SSH Key   填写任意Title，在Key中粘贴id_rsa.pub的内容
2.添加远程库，登录GitHub，创建一个新的仓库，填写一个名字，其他保持默认。根据提示操作，第二个，Push an existing repo……
  （本地作了提交，可以通过命令 git push origin master提交到GitHub）
3.从远程库克隆  先在GitHub创建一个新仓库，勾选Initialize……
  使用命令 git clone 地址（git@github.com:yourname/repo_name.git  or   https://）
四、分支管理  