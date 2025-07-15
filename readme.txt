git init                        初始化本地git仓库(工作区)
git add file                 添加修改到暂存区(Stage)
git commit -m ""      -m 后面添加  解释内容
git status                   查看git的当前状态
git diff                        查看git的上次修改
git log                        查看git的操作日志

git reset --hard HEAD^^    返回上上次提交的版本   HEAD^^ =  HEAD^2   ;
 --hard 返回到已提交的状态；--soft返回到未提交的状态；--mixed返回到已添加未提交的状态

git diff HEAD -- readme.txt         查看工作区和版本库里面最新版本的区别

git checkout -- file        丢弃工作区的修改,也可以用来对已经在工作区删除但是还在远程仓库的文件的恢复，本质还是丢弃对文件的修改
git checkout  branchName                                   可以切换分支

删除文件的步骤：
手动删除工作区的文件 ---> git rm fileName  --->  git commit -m ""

配置远程仓库：
	创建账号对应的密钥：id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，粘贴到GitHub里面。
	ssh-keygen -t rsa -C "youremail@example.com|2139991438@qq.com" 会在电脑user的.ssh文件夹生成 id_rsa 和 id_rsa.pub 两个文件
	
	登陆GitHub，打开“Account settings”，“SSH Keys”页面：点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：