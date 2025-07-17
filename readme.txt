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


---------------------------------------CLONE---------------------------------------
前面的步骤是我们先创建一个本地库，然后上传到远程库，但大多数时候是我们从已经存在的远程库clone到本地
git clone git@github.com:G-J-and-234/learngit.git


------------------------------------创建分支dev----------------------------------



------------------------------------创建分支dev----------------------------------


git checkout -b dev 。 git checkout 命令加上 -b 参数表示创建并切换，相当于 git branch dev  + git checkout dev 两条命令

git branch  命令查看当前分支

---------------------------------切换到dev分支----------------------------------------


---------------------------------切换到dev分支----------------------------------------


git branch                                                                    查看分支    git branch -a 查看所有分支

git merge dev                                                              分支合并，将 dev 分支合并到 master 上面

git branch dev                                                              创建分支
git branch -d dev                                                         删除分支，合并后就可以删除分支，分支相当于一个指针对于修改没有影响

git switch -c dev   |  git checkout -b dev                   创建并切换到分支dev   git checkout -b dev origin/dev  创建并切换到基于远程dev分支的dev分支

git switch master  |  git checkout master                  切换到 master 分支



解决合并分支的冲突：
	git switch -c feature1  创建并切换分支到 feature1， 在 feature1 分支上面对readme.txt 进行修改添加一行  add, commit
	git switch | checkout master  切换到master分支，  在master 分支上面对readme.txt 进行修改添加一行,  add, commit
	git merge feature1        合并master 分支和feature1 分支，git会主动标记出两个分支的冲突之处，
						我们在readme.txt 文件里面手动合并，之后再 add，commit


Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，我们修改如下后保存add, commit , 在master 的条件下git merge feature1 
合并之后使用 git branch -d feature1 删除分支



分支管理策略：
	通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
	如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。
	下面我们实战一下--no-ff方式的git merge：
	
	git switch -c dev  创建并切换到分支 dev,  git add readme.txt, git commit -m "---" 提交一个新的commit
	git switch master 切换到分支 master， 
	git merge --no-ff -m "merge with no-ff" dev, 将dev 合并到 master分支上面， 并且添加一个commit



Bug 分支：
	在软件开发中，bug就像家常便饭一样。我们通过对每个bug 新建一个临时分支来修复。修复后合并分支，然后将临时分支删除。
	
	当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它，但是，等等，当前正在dev上进行的工作还没有提交：
	
	并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须在两个小时内修复该bug，
	怎么办？幸好，Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作
	
	在master分支修复好bug 后，其实dev 是在修复bug 之前在master创建的分支，所以其实dev上面也存在这个bug ,
	所以我们采用在dev 分支上面使用 cherry-pick命令，让我们能复制一个特定的提交到当前分支，来修复dev分支上的 bug。
	git  cherry-pick  4c805e2 ( 在master分支上面的 commit 的编号 )


	git stash                                                  隐藏工作现场，待以后恢复现场继续工作，通常用在当前工作未提交，但需要创建新分支修改bug 的情况
	git stash list                                            查看隐藏未提交工作状态列表
        git stash apply | git stash apply @{0}    @后面是stash的标号，在stash list 查看。  恢复隐藏的工作状态，但是没有在stash list中删除隐藏记录
	git stash drop                                         删除在 stash list 列表中隐藏的工作记录
	git stash pop                                          恢复隐藏的工作状态，并删除 stash list 中隐藏的工作记录

	bug 分支只是用于在本地修复bug 使用，不需要推送给 origin


Feature 分支
	软件开发中，总有无穷无尽的新的功能要不断添加进来。
	添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，
	最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。


	现在，你终于接到了一个新任务：开发代号为Vulcan的新功能，该功能计划用于下一代星际飞船。

于是准备开发：

	git switch -c feature-vulcan      创建feature-vulcan 分支
	git add vulcan.py                       新功能文件 vulcan.py
        git commit -m "add feature vulcan"   
	git switch dev
	git merge --no-ff -m "添加 vulcan 功能" feature-vulcan,    将feature 分支合并到dev 分支上面

	如果项目取消了 Vulcan 功能使用 git branch -D feature-vilcan ,    使用 -D 强制删除 feature-vulcan 分支
	
	feature 分支是否推送到远程取决于开发伙伴是否需要改功能配合


多人协作：
	git remote                                                             查看远程库信息
	git remote -v                                                         查看详细的远程库信息

	git push origin master                                         推送 master 分支到远程仓库上，如果没有 master，系统会自动创建它
	git push origin dev                                               推送 dev 分支到远程的仓库上， 如果没有 dev，系统会自动创建它


	master分支是主分支，因此要时刻与远程同步；
	dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
	bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
	feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

	
	git clone git@github.com:michaelliao/learngit.git                只能看到本地的master分支
	git checkout -b dev origin/dev                                                  创建并切换到基于远程dev分支的dev分支
	然后在本地的 dev 分支上面进行修改
	git push origin dev                                                                      推送到远程的 dev 分支

	但是如果开发同伴也对于 dev 分支 进行了修改，那就会push 失败
	这时候我们想到 要先 pull , 然后在本地手动合并之后再 push
	但是这时候我们pull 也会失败， 因为本地 dev 分支没有和远程的 dev 分支建立链接
	git branch --set-upstream-to=origin/dev dev  | git branch -u origin/dev dev      两条都可以实现dev 分支之间的跟踪关系
	然后 git pull 
	然后手动合并冲突，然后 commit, 然后 git  push origin dev 	
	

因此，多人协作的工作模式通常是这样：

	首先，可以尝试用git push origin <branch-name>推送自己的修改；
	如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
	如果合并有冲突，则解决冲突，并在本地提交；
	没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
	如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，
	用命令git branch --set-upstream-to <branch-name> 	origin/<branch-name>。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。


标签管理：
	系统在某个 commit 的时候打上 tag,唯一确定了打标签时刻的版本。 
	
	git tag v1.0                                             在上次的 commit 上面创建标签
	git tag v1.1  f52c633(commit id)          在指定的 commit 上面创建标签
	git tag                                                     查看所有的标签
	
	标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。

	git tag -d v0.1                                         删除标签
	git push origin v1.0                                推送标签到远程
	git push origin --tags				  一次性推送全部尚未推送到远程的本地标签

	如果标签已经推送到远程，要删除远程标签就麻烦一点
	先从本地删除：git tag -d v0.9
	然后，从远程删除。删除命令也是push，但是格式如下：git push origin :refs/tags/v0.9
	要看看是否真的从远程库删除了标签，可以登陆GitHub查看。




idea 配置 git和github: https://blog.csdn.net/ITjavaxiaobai/article/details/122326046



git 配置云雀研发云：
	git config -l                                   查看git 全局配置信息
	git config --global user.email zhang.yi@iwhalecloud.com
	git config --global user.name "张易"
	











