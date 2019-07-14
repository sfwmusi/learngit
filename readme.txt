Git is a version control system.
入门：Git教程 廖雪峰https://www.liaoxuefeng.com/wiki/896043488029600

一、创建版本库
1.初始化一个Git仓库，使用 git init 命令（先创建一个空文件夹）
2.添加文件到Git仓库，分两步：
   a.使用命令git add <file>，注意，可反复多次使用，添加多个文件；
   b.使用命令git commit -m “<message>”，完成。
二、过去与未来
1.掌握工作区的状态，使用命令git status
  git diff 可以查看修改内容
  git log  可以查看历史记录
2.回到过去
  首先要知道回到哪个版本，HEAD表示当前，HEAD^表示上一个，HEAD^^上上个，HEAD~100，往上100个
  git reset --hard HEAD^   回到上一个版本
  从过去返回：git reset --hard ****（版本号，git log可查看，很长一串，写前几个即可）
