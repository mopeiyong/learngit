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

上传:git push origin master

查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>或者git switch <name>
创建+切换分支：git checkout -b <name>或者git switch -c <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>

分支合并情况:git log --graph --pretty=oneline --abbrev-commit

禁用Fast forward，创建新的commit:git merge --no-ff -m "merge with no-ff" <name>

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
当手头工作没有完成时，先把工作现场git stash
一下，然后去修复bug，修复后，再
git stash pop或（git stash apply恢复，再用git stash drop删除stash内容）
，回到工作现场；
查看stash内容存储:git stash list


Creating a new branch is quick and simple.
merge
