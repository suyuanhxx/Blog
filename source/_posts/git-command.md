---
title: git command
date: 2017-01-07 12:17:28
tags:
---
# git常用命名汇总
## 1. First-Time Git Setup    
- `git config -l`      
- `git config --global user.name "your name"`     
- `git config --global user.email xxx@example.com`      
- `git config --global color.ui true`    
- `git config core.ignorecase false`   ##设置大小写敏感
<!--more-->
## 2. Generate SSH key    
- `ssh-keygen -t rsa -C "you@yourdomain.com"`    
- `cat ~/.ssh/id_rsa.pub`    
## 3. Initializing a Repository in an Existing Directory    
- `git init`    
- `git add .`    
- `git commit -m 'initial project'`    
- `git remote add <name> <url> `    
- `git push <name>`    
## 4. Cloning an Existing Repository
- `git clone [url]`
- 修改 `vim .git/config` 令： rebase = true (存在每个分支下)
- filemode = false （防止git将自己本身文件检测并显示）
## 5. Git Base Command
- `git status`
- `git add <file>`  					# 将工作文件修改提交到暂存区
- `git add .`  						# 将当前目录中所有修改过的工作文件提交暂存区
- `git rm <file>`  					# 将文件从仓库中移除，并且从当前目录中删除
- `git rm <file> --cached`  			# 将文件从仓库中移除，但仍然保留在当前目录中
- `git git clean -df <url>`
- `git mv FileName NewFileName`  	# 文件重命名
- `git commit -m "something" someFile`     # 提交指定文件
- `git commit -a -m "something"`                # 把所有已经跟踪过的文件暂存,并提交
- `git commit --amend`                      # 增补提交
- `git commit -C HEAD -a —amend`  # 复用HEAD留言，增补提交
- `git pull`                         # 抓取远程仓库所有分支更新并合并到本地
- `git fetch origin`           # 抓取远程仓库更新
- `git merge origin/master`     # 将远程主分支合并到本地当前分支
- `git merge <branch>`          # 将branch分支合并到当前分支
- `git push`                              # push所有分支   
- `git push origin master`       # 推到远程主分支   
- `git push -u origin master`   # 推到远程主分支(如无远程主分支则创建，用于初始化远程仓库)  
## 6. Undoing Unstaged File
- `git checkout  -- <file>`                    # 用暂存区中filename文件来覆盖工作区中的filename文件
- `git checkout <commit> -- <file>`  # 用<commit>所指向的提交中filename替换暂存区和工作区中相应的文件
- `git checkout -- .` 　　　　                # 或者git checkout . 用暂存区的所有文件直接覆盖本地文件
- `git checkout feature file-x`   #从feature分支检出相应文件
## 7. Undoing Staged/Commited File
- `git reset --mixed <commit>`    # (默认)更改引用的指向及重置暂存区，但是不改变工作区
- `git reset --hard <commit>`     # 替换引用的指向，替换暂存区，替换工作区
- `git reset --soft <commit>`     # 更改引用的指向(复位版本库)，不改变暂存区和工作区
- `git reset <file>`              # 将文件的改动撤出暂存区，相当于命令git add <file>的反射操作  
- `git reset --soft HEAD^`        # 工作区和暂存区不改变，但是引用向前回退一次，撤销最新的提交以便重新提交
- `git reset --hard HEAD^`        # 彻底撤销最近的提交（本地文件代码修改一并撤回）
## 8. Branch Related    
- `git checkout brname`          		# 切换分支
- `git checkout -b brname`         	# 创建并切换分支
- `git branch brname master/cid/tag`  # 基于某次提交、分支或标签创建新分支
- `git branch -r`   					# 显示远程分支
- `git branch -a`  					# 列出所有分支
- `git branch -m master mymaster`  	# 分支重命名 -M 大写M会覆盖同名的分支
- `git branch -d`  					# 删除分支
- `git br -D <branch>`  				# 强制删除某个分支 (未被合并的分支被删除的时候需要强制)
## 9. Diff Related
- `git diff`                          # 比较尚未暂存的文件
- `git diff <file>`               # 比较当前文件和暂存区文件差异   
- `git diff <commit1> <commit2>`  # 比较两次提交之间的差异   
- `git diff <branch1>..<branch2>`  # 在两个分支之间比较   
- `git diff --staged`     # 比较暂存区和版本库差异   
- `git diff --cached`    # 比较暂存区和版本库差异   
- `git diff --stat`         # 仅仅比较统计信息
## 10. Log Related
- `git log <--oneline>`
- `git log <file>`			# 查看该文件每次提交记录   
- `git log -p <file>`		# 查看每次详细修改内容的diff   
- `git log -p -2`			# 查看最近两次详细修改内容的diff   
- `git log --stat`			# 查看提交统计信息
## 11. stash
- `git stash`
- `git stash save "缓存记录名"`
- `git stash list 缓存列表`
- `git stash apply stash{0} 放出缓存为stash{0}的缓存`
## 12.
`git cherry-pick <commit>` 将另一个分支的提交提交到当前分支
Addition
rebase: [http://gitbook.liuhui998.com/4_2.html](http://gitbook.liuhui998.com/4_2.html)    
reset:  [http://www.cnblogs.com/craftor/archive/2012/11/04/2754140.html](http://www.cnblogs.com/craftor/archive/2012/11/04/2754140.html)
