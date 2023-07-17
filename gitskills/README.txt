初始化一个Git仓库:git init
将工作区的文件添加到暂存区:git add <name>
将暂存区的文件提交到本地仓库:git commit -m "message"
掌握工作区的状态:git status
查看修改内容:git diff <name>
回退当前工程的版本:git reset --hard commit_id/git reset --hard HEAD^
查看历史提交记录:git log
查看历史提交记录，将每个提交放在一行显示:git log --pretty=oneline
查看命令历史:git reflog
撤销工作区修改:git checkout <name>
撤销暂存区内容:git reset HEAD <name>
确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit;
删错了:git checkout -- <name>
