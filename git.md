#####  git常用命令 
    1.下载代码： git clone git@xxxxxx.git
    
    2.拉去代码： git pull
    
    3.从工作区添加到暂存区 git add .
    
    4.从暂存区提交到本地仓库： git commit -m "提交信息"
    
    5.从本地仓库推送远程仓库： git push
    
    6.查看当前代码的修改状态 git status
    
#####  git各阶段常用命令
    一、本地：
    初始化：
    1.全局变量(git config --global设置的全局变量会在.gitconfig文件内  user.name "xxx" 表示的是给配置文件中的user对象的name的value设置为"xxx")
      1)git config --global user.name "xxx"				设置提交人姓名
      2)git config --global user.email "xxx@163.com"	设置提交人邮箱
      3)git config --global color.ui true				设置颜色差异显示
      4)git config --global gui.Encoding utf-8			解决gitk中文显示乱码
      5)git config --global core.longpaths true			解决git文件名太长导致无法下载
      
    2.初始化新版本库
    git init	只在根目录下创建一个名文 .git 的文件夹
    
    3.添加新文件到版本库
      1)添加单个文件		git add xxx.txt
      2)添加所有txt文件		git add *.txt
      3)添加所有文件		git add .
      
    4.提交
    git commit -m "message"
    
    日常操作：
    1.提交
    1)git commit -m "message" -a		提交所有修改
    2)git commit -m "message" xxx.txt	提交单个文件
    3)git commit -C head -a --amend		增补提交(不会产生新的提交历史记录)
    
    2.查看修改
    git diff xxx.txt	查看difference,查看xxx.txt修改了什么
    
    3.撤销修改(撤销的是工作目录中还没提交到暂存区的修改)
    1)git checkout head xxx.txt xxx2.txt	撤销1、2个文件
    2)git checkout head *.txt 				撤销所有的txt文件
    3)git checkout head . 					撤销所有文件
    
    4.复位
    git reset head		取消暂存(取消的是从工作目录提交到暂存区的修改)
    
    5.分支
    git branch					列出本地分支
    git branch -a   			列出所有分支
    git branch branch.name 		基于当前分支创建新的分支
    git checkout branch.name 	切换分支
    git push --set-upsteam origin branch.name 	将本地分支在远程仓库上设置一个起源远程分支
    
    6.状态
    git status			当前状态
    git log				历史记录
    gitk				查看当前分支历史记录
    gitk branch.name 	查看指定分支历史记录
    gitk --all			查看所有分支历史记录
    git branch -v		查看每个分支最后的提交
    
    7.版本控制
    git log								查看历史记录以及每次提交的版本号
    git reset --hard 版本号的前几位		将版本指向该版本
    git reflog							查看操作记录(防止你回退版本之后想回到最新的版本找不到版本号)
    
    8.合并分支
    git checkout master		从其他分支切换到master分支
    git merge dev			将指定指定分支dev合并到当前分支(合并到的是分支的本地仓库,接着git push推送到远程仓库即可)
    
    合并分支没有完成就退出导致push失败的解决办法：
    git merge --abort	如果有冲突，不想解决（未commit），想还原合并之前的状态
    git reset --merge   回滚到合并pull下来之前的状态，并且不会删除你在工作空间修改但是没有提交的代码
    git pull            执行完上面两步重新拉取一次代码
    
    9.使用rebase更新代码(代替merge)
    假如有三个分支master  test1  test2, master为主干, test1为公用代码库, test2为个人分支, 想将test1公用代码库的代码更新到自己分支然后提交代码
    git checkout test1 	切换到公用test1分支
    git pull 	更新最新代码
    git checkout test2 	切换到个人代码库 
    git rebase test1 	将版本指向公用库
    (解决冲突)
    git push
    在远程git库merge
    
    (如果有冲突, 解决冲突)
    "<<<<<<<" 表示冲突代码开始
    "=======" 表示test2与test1冲突代码分隔符
    ">>>>>>>" 表示冲突代码的结束
    
    <<<<<<<  
    所以这一块区域为源代码库test2的代码
    
    =======  
    这一块区域为个人代码库test1的代码
    
    >>>>>>> 
    
    (解决完冲突, 输入指令)
    git add -u 
    git rebase --continue 
    
    (一键回退到rebase前)
    git rebase --abort
    
    10. 删除分支
    删除远程分支: git push origin --delete 分支名
    删除本地分支: git branch -d 分支名

    11. tag
    查询所有tag：git tag
    创建新的tag: git tag -a v1.0.0 -m "注释"
    发布指定tag: git push origin v1.0.0
    发布所有tag: git push origin --tags
    
    
    二、远程
    初始化：
    1.克隆
    git clone url		克隆版本库
    
    2.分支
    git remote  				查看远程仓库(仓库里面可以包括很多个分支)
    git remote -v				查看可以抓取和推送的origin地址(fetch可以抓取的origin地址,push可以推送的origin地址,如果没有推送权限，就看不到push的地址)
    git branch -r 				列出远程分支
    git remote prune origin		删除远程库中已经不存在的分支
    
    3.拉取(git pull相当于git fetch和git merge)
    git pull		等价于git pull origin	从远程仓库更新到本地
    
    4.推送
    git push        等价于git push origin   从本地仓库推送到远程仓库(远程仓库的分支为当前分支)
    git push origin master			推送到远程仓库(masetr分支是主分支,因此要时刻与远程同步)
    git push origin dev 			dev分支是开发分支,团队所有成员都需要在上面工作,所以也需要与远程同步
    git push origin bug   			bug分支只用于在本地修复bug,就没必要推到远程了,除非老板要看看你每周到底修复了几个bug
    git push origin feature			feature分支是否推到远程,取决于你是否和你的小伙伴合作在上面开发
    
    5.生成SSH Key(SSH Key用于让Git服务器识别推送的提交确实是你推送的，而不是别人冒充的,Git允许添加多个Key,这样你在每台电脑设置一个SSH Key就可以都提交了)
    1)启动Git Bash
    2)如果以前生成过SSH Key,要先备份	
    	cd ~/.ssh	(~/.ssh就是c:\Users\xxx\.ssh)
    	mkdir	key_backup
    	cp id_rsa* key_backup
    3)生成SSH Key
    ssh-keygen -t rsa -C "邮箱名"
    4)将SSH Key 添加到GitHub账户里
    将id_rsa.pub(公钥文件)里面的内容复制粘贴到GitHub 的 Settings 的 SSH Key文本框中


##### git分支(branch)和git标签(tag)的区别
  1. tag
    标签是一个点，代表项目的某个里程碑
    标签的位置是固定的，在给指定提交打好标签以后，它就固定于此位置。
    标签适用于记录某个固定版本

  2. branch 
    分支是一个条线，有生命周期
    分支的位置会不断变动的，随着分支的向前推移或者向后回滚，都在不断变化。
    分支适用于功能开发、bug修复等操作


##### git 分支管理
  master
    有质量保证的、可安全运行的分支
    禁止直接代码提交，避免被污染，仅用于代码合并和归集，在这个分支上的代码应该永远是可用的、稳定的。
    当需要拉一个特别的开发分支时，应该基于 master。


  release
    发布过程的分支
      包括开发转测(实际上我们认为这里的测试集成测试)、测试和BugFix以及发布上线的过程，
      当发布成功时要打一个发布beta Tag(如5.2.1-beta)，并将代码合并到 master 分支

  dev
    开发分支
    开发小组有信心转测时，就将代码合并到 release 分支，并要求打一个alpha级的Tag(如5.2.0-alpha)
    新功能开发分支在dev分支上拉新的对应分支进行开发迭代合并销毁

  hotfix 
    当出现线上Bug需要hotfix时，我们需要在上次上线的Tag处拉一个临时的 hotfix 分支进行修正
    或者在未被其他开发迭代污染的release分支上直接hotfix上线并合并到master和develop，然后打一个新的Tag(如5.2.2-beta）

  版本号v1.0.0

##### git相关资料
  http://roclinux.cn/?p=2129   (GIT分支管理是一门艺术)


##### git代码统计工具

https://blog.csdn.net/qq_37023538/article/details/53930200 

https://blog.csdn.net/fengyuansu656/article/details/72771178
    
    python  [gitstats.py路径] [git库路径] [输出结果路径]
    (环境变量设置在gitbash里面无效的时候, 需要在python的安装目录下C:\Python27, 在gitbash里面执行下面命令行, 在输出结果路径查看报告)
    例如:
    python C:/Users/Administrator/Desktop/gitstats/gitstats.py C:/Users/Administrator/Desktop/web-manage C:/Users/Administrator/Desktop/gitReport
    
##### git同步远程已删除的分支和删除本地多余的分支
```
  查看本地分支和远程分支情况
    git branch -a
  查看本地分支和追踪情况
    git remote show origin
  删除本地分支
    git branch -D 本地分支名
  同步远程已删除分支
    git remote prune origin
  
```

##### git查看本地分支和远程分支的关联
```
  git branch -vv
```