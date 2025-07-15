git init                        初始化本地git仓库(工作区)
git add file                 添加修改到暂存区(Stage)
git commit -m ""      -m 后面添加  解释内容
git status                   查看git的当前状态
git diff                        查看git的上次修改
git log                        查看git的操作日志

git reset --hard HEAD^^    返回上上次提交的版本   HEAD^^ =  HEAD^2   ;
 --hard 返回到已提交的状态；--soft返回到未提交的状态；--mixed返回到已添加未提交的状态

git diff HEAD -- readme.txt         查看工作区和版本库里面最新版本的区别