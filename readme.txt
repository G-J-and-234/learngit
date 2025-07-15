git init                        初始化本地git仓库(工作区)
git add file                 添加修改到暂存区(Stage)
git commit -m ""      -m 后面添加  解释内容
git status                   查看git的当前状态
git diff                        查看git的上次修改
git log                        查看git的操作日志

git reset --hard HEAD^^    返回上上次提交的版本   HEAD^^ =  HEAD^2   ;
 --hard 返回到已提交的状态；--soft返回到未提交的状态；--mixed返回到已添加未提交的状态
	
	git reset --soft HEAD~1      取消提交(commit)，回到暂存区状态(Stage)
	git reset --hard HEAD~1     彻底取消提交，并且回到未修改的状态，回到上一次提交的状态

git diff HEAD -- readme.txt         查看工作区和版本库里面最新版本的区别

git checkout -- file        丢弃工作区的修改,也可以用来对已经在工作区删除但是还在远程仓库的文件的恢复，本质还是丢弃对文件的修改
git checkout  branchName                                   可以切换分支

删除文件的步骤：
手动删除工作区的文件 ---> git rm fileName  --->  git commit -m ""

配置远程仓库：
	创建账号对应的密钥：id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，粘贴到GitHub里面。
	ssh-keygen -t rsa -C "youremail@example.com|2139991438@qq.com" 会在电脑user的.ssh文件夹生成 id_rsa 和 id_rsa.pub 两个文件
	
	登陆GitHub，打开“Account settings”，“SSH Keys”页面：点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

	连接远程仓库：git remote add origin git@github.com:G-J-and-234/learngit.git
					git remote(远程) add(添加) origin(仓库) git(仓库名)@github.com(远程服务器):G-J-and-234(用户名)/learngit.git(仓库名)

	首次推送：git push -u origin master      推送本地的master分支到远程库的master分支上。
	本地库和远程库建立绑定关系之后的首次推送需要添加 -u 实现建立跟踪关系，本地master和origin 的 master分支建立跟踪关系.
	后续推送使用 git push 即可, 建立跟踪关系之后 git push == git push origin master ; git pull == git pull origin master


SSH 警告： 初次使用 Git 的 clone或者 push时会出现SSH警告， 输入 yes即可

git remote -v                            查看远程库信息
git  remote rm origin              删除本地库和远程库的绑定关系

前面的步骤是我们先创建一个本地库，然后上传到远程库，但大多数时候是我们从已经存在的远程库clone到本地
git clone git@github.com:G-J-and-234/learngit.git


------------------------------------创建分支dev----------------------------------



------------------------------------创建分支dev----------------------------------


git merge dev                          分支合并，将 dev 分支合并到 master 上面

git branch -d dev                     删除分支，合并后就可以删除分支，分支相当于一个指针对于修改没有影响




















git checkout -b dev 。 git checkout 命令加上 -b 参数表示创建并切换，相当于 git branch dev  + git checkout dev 两条命令

git branch  命令查看当前分支

---------------------------------切换到dev分支----------------------------------------


---------------------------------切换到dev分支----------------------------------------















