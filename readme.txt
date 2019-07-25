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
master分支应该是非常稳定的，平时不在上面干活，干活都在dev分支，然后每个人都有自己的分支，再合并到dev分支，做好后dev再合并到master
1.创建与合并分支
  创建分支 git branch <name>
  切换分支 git checkout <name>
 （创建+切换）git checkout -b <name>
  查看分支 git branch
  合并某分支到当前分支 git merge <name>  （Fast forward）
  git merge --no-ff -m "message" <name>  （普通合并，可历史查看）
  删除分支 git branch -d <name>
  一般先合并再删除，强行删除-D
2.Bug分支
  适用于当前分支工作不想现在提交，又需要立马在另一分支工作，之后再返回操作
  git stash 隐藏当前工作现场
  git stash list 查看工作现场隐藏在哪
  恢复：
  a.先 git stash apply（可以选择apply哪一个，通过list查看），再删除git stash drop
  b.直接git stash pop
3.多人协作
  推送分支 git push origin master（origin，master可修改），一般master为主分支，dev是开发分支，这些需要推送
  抓取分支 git clone（一般只有master分支），使用git checkout -b dev origin/dev可以从远程origin的dev分支到本地
  当推送失败时，需要根据提示 git pull试图合并；如果合并冲突，则解决冲突（手动），并在本地提交，之后再推送
  如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to=origin/<branch> dev
五、标签管理  commit号和标签，类似IP与域名的关系
1.创建标签 
   git tag xxx  默认打到最新提交的commit上，也可以打到指定的commit上，后面加上指定id就可以
   git tag -a <tagname> -m "blablabla"  指定标签信息 
   git tag 查看所有标签
   git show <tagname> 查看标签内容
2.操作标签
   git tag -d xxx 本地删除  git push origin <tagname> 推送一个标签 git push origin --tags 所有
   git push origin :refs/tags/<tagname>  删除远程标签（先本地删除）
六、1.使用GitHub https://github.com
   先fork，再在自己的账号下clone，这样可以发起推送，pull request  
    2.使用码云https://gitee.com/ 
      先git remote rm origin，再关联GitHub远程库git remote add github git@github.com:xxx/xxx.git	
	  和码云的远程库git remote add gitee git@gitee.com:xxx/xxx.git
	之后推送要改成git push github master
七、自定义Git
   1.忽略特殊文件，比如密码的配置文件等
   在Git工作区的根目录下创建一个特殊的.gitignore文件，注意在Windows下无法创建，需要通过保存或另存为（因为没有文件名）
   只需要在里面添加想要忽略的文件名即可，最后提交到版本库
   























