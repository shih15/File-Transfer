# 暂存区与版本库

## 提交版本

- git中暂存区（stage）和版本仓库（Repository）的关系

  ![add和commit命令](.\image\0.jpg)

- 添加文件到

  ```shell
  git add <filename>
  ```

- 提交文件到版本仓库（Repository）

  ```shell
  git commit -m "add file"
  ```

- 修改作者姓名和邮箱地址，并以新作者的身份重新提交

  ```shell
  git config --global user.name "Your Name"
  git config --global user.email you@example.com
  git commit --amend --reset-author -m "add file"
  ```

- 未add的文件可以比较不同

  ```shell
  git diff
  
  # 比较工作区目前的文件和仓库中的文件的差别
  git diff HEAD -- readme.txt 
  ```

- 查看当前文件的提交状态

  ```shell
  git status
  ```

- 查看修改的日志文件

  ```shell
  git log
  git log --pretty=oneline # 每个log一行显示
  ```

## 版本管理

- 版本回退

  ```shell
  git reset --hard HEAD^ # 回退到上一个版本
  git reset --hard HEAD^ # 回退到上上个版本
  git reset --hard HEAD~100 # 回退到100个修改之前版本
  git reset --hard fe0133 # 用版本号回退
                         # 版本号没有必要写全，6位即可
  ```

- 查看每一次命令HEAD所对应的版本号

  ```shell
  git reflog
  ```

- 放弃未add的工作区文件的修改，让这个文件回到最近一次`git commit`或`git add`时的状态。

  ```shell
  git checkout -- <filename>
  ```

- 对于已提交到stage中的修改，可以用reset把暂存区的修改回退到工作区

  ```shell
  git reset HEAD <file>
  ```

- 想要删除一个文件

  ```shell
  rm <filename>
  git rm <filename>
  git commit -m "remove file"
  ```

# 远程仓库的关联

- 添加远程库并命名为origin

  ```shell
  git remote add origin git@github.com:shih15/File-Transfer.git
  ```
  
- 将当前的master分支推送到远程库中

  ```shell
  git push -u origin master
  # -u 用于第一次推送，将远程仓库origin中的master分支与本地的master分支建立关联，后续推送可以简化
  git push origin master
  ```

- 删除远程库

  ```shell
  git romote -v # 查看远程库的信息
  git remote rm origin # 解除和远程库的关系
  ```

# 分支管理

## 分支的创建、切换与合并

```shell
git branch <new branch name> # 创建一个新分支
git switch <branch name> # 切换分枝
git checkout <branch name> # 切换分支

#创建一个新分支并切换到该分支
git checkout -b <new branch name>
git switch -c <new branch name>

# 分支的合并
git switch master
git merge dev
git merge --no-ff dev
# 有冲突，修改冲突后，add+commit

# 分支的删除
git branch -d dev
git branch -D dev # 强行删除没有合并的分支

# 显示当前分支
git branch

# 让分支合并更加清晰的显示
git log --graph --pretty=oneline --abbrev-commit

```

## 分支保护现场

```shell
git stash # 现场快照
git stash list # 现场快照list
git stash apply stash@{0} # 恢复现场
git stash drop stash@{0} # 删除现场快照
git stash pop stash@{0} # 弹出栈顶快照
git cherry-pick 4c805e2 # 复制某次修改
```

