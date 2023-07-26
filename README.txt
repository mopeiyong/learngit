git 仓库
	初始化一个Git仓库:git init
	在当前目录下创建:git init myGit.git 说明：myGit.git是创建的git目录，可以在里面添加项目文件

git 常用命令
	git add
		git add *:添加所有文件到暂存区
		git add <name>:将工作区的文件添加到暂存区
		git add <path>:添加目录到暂存区
		git add -u:添加改动过的文件到暂存区
	git status
		git status:掌握工作区的状态
		git status project:显示工作区project目录下的文件状态
	git log
		git log:查看历史提交记录
		git log -3:显示最近3次条日志
		git log --graph --oneline --all --decorate:分支图显示提交日志
		git log -p:显示日志的同时显示改动
		git log --stat:显示改动了哪些文件
		git log --pretty=oneline --abbrev-commit:查看历史提交记录，将每个提交放在一行显示
			-p：显示提交的补丁（具体更改内容）。
			--oneline：以简洁的一行格式显示提交信息。
			--graph：以图形化方式显示分支和合并历史。
			--decorate：显示分支和标签指向的提交。
			--author=<作者>：只显示特定作者的提交。
			--since=<时间>：只显示指定时间之后的提交。
			--until=<时间>：只显示指定时间之前的提交。
			--grep=<模式>：只显示包含指定模式的提交消息。
			--no-merges：不显示合并提交。
			--stat：显示简略统计信息，包括修改的文件和行数。
			--abbrev-commit：使用短提交哈希值。
			--pretty=<格式>：使用自定义的提交信息显示格式。
	git blame
		git blame <file>:以列表形式查看指定文件的历史修改记录
		git blame -L <起始行号>,<结束行号> <文件路径>:只显示指定行号范围内的代码注释
		git blame -C <文件路径>:对于重命名或拷贝的代码行进行溯源
		git blame -M <文件路径>:对于移动的代码行进行溯源
		git blame --show-stats <文件路径>:显示行数统计信息
		-C -C 或 -M -M：对于较多改动的代码行，进行更进一步的溯源
	git branch
		git branch:查看分支
		git branch <name>:创建分支
		git checkout <name>或者git switch <name>:切换分支
		git checkout -b <name>或者git switch -c <name>:创建+切换分支
		git merge <name>:合并某分支到当前分支
		git branch -d <name>:删除分支
		git branch -M <oldbranch> <newbranch>:重命名分支
		git branch <branchname> <start-point>:基于提交<start-point>创建分支
	将暂存区的文件提交到本地仓库:git commit -m "message"
	git diff
		git diff:对比当前工作区与暂存区的差异
		git diff --cached:对比暂存区与上个提交的差异
		git diff --<name>:查看具体某个文件 在工作区和暂存区之间的差异
		git diff <point_1> <point_2>:对比两次提交间的差异
		git diff <branch1> <branch2>:对比分支间的差异
	git show
		git show:显示当前HEAD指向的提交内容
		git show [point]:显示指定提交point的内容
		git show --stat:显示当前HEAD指向提交的相关文件信息
	git stash
		git stash:保存当前工作 进度，分别保存暂存区和工作区
		git stash list :显示进度列表
		git stash pop:恢复最新保存的工作进度，并删除该进度
		git stash apply [--index] [<stash>]:应用某个index进度，不删除该进度	
		git stash drop:删除stash进度
		修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
		当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop或（git stash apply恢复，再用git stash drop删除stash内容），回到工作现场；
		查看stash内容存储:git stash list在master分支上修复的bug，想要合并到当前dev分支，可以用git cherry-pick <commit>命令，把bug提交的修改“复制”到当前分支，避免重复劳动
	git cherry-pick
		对于多分支的代码库，将代码从一个分支转移到另一个分支是常见需求。
		这时分两种情况。一种情况是，你需要另一个分支的所有代码变动，那么就采用合并（git merge）。另一种情况是，你只需要部分代码变动（某几个提交），这时可以采用 Cherry pick。


	回退当前工程的版本:git reset --hard commit_id/git reset --hard HEAD^
	查看命令历史:git reflog
	撤销工作区修改:git checkout <name>
	撤销暂存区内容:git reset HEAD <name>
	确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit;
	删错了:git checkout -- <name>


上传:git push origin master

分支合并情况:git log --graph --pretty=oneline --abbrev-commit

禁用Fast forward，创建新的commit:git merge --no-ff -m "merge with no-ff" <name>

开发一个新feature，最好新建一个分支；
如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

多人协作的工作模式通常是这样：
1.首先，可以试图用git push origin <branch-name>推送自己的修改；
2.如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
3.如果合并有冲突，则解决冲突，并在本地提交；
4.没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！
如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。这就是多人协作的工作模式

查看远程库信息:git remote -v
本地新建的分支如果不推送到远程，对其他人就是不可见的；
从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；
从远程抓取分支，使用git pull，如果有冲突，要先处理冲突.

命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；
命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；
命令git tag可以查看所有标签。

命令git push origin <tagname>可以推送一个本地标签；
命令git push origin --tags可以推送全部未推送过的本地标签；
命令git tag -d <tagname>可以删除一个本地标签；
命令git push origin :refs/tags/<tagname>可以删除一个远程标签。

忽略某些文件时，需要编写.gitignore
例：	# 排除所有.开头的隐藏文件:
	.*
	# 排除所有.class文件:
	*.class
	# 不排除.gitignore和App.class:
	!.gitignore
	!App.class

	git submodule
	

Creating a new branch is quick and simple.
merge
