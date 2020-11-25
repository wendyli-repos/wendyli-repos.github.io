---
title: "Git Notes"
date: 2020-09-03
categories: Git 
---

# git command

[git clone](#git-clone)  
[git remote](#git-remote)  
[git init](#git-init)  
[git status](#git-status)  
[git add](#git-add)  
[git commit](#git-commit)  
[git reset](#git-reset)  
[git push](#git-push)  
[git fetch](#git-fetch)  
[git pull](#git-pull)  
[git branch](#git-branch)  
[git checkout](#git-checkout)  
[git stash](#git-stash)  
[git rebase](#git-rebase)  
[git squash](#git-squash)  
[git merge](#git-merge)  
[merge conflict](#merge-conflict)  
[git log](#git-log)  
[git diff](#git-diff)  
[git show](#git-show)  
[git reset](#git-reset)  
[git config](#git-config)  
[git rm](#git-rm)  
[git mv](#git-mv)  
[git Tips & Good Coding habits](#git-tips)

<a name="git-clone"></a> to clone a repository to local destination

```
git clone <github_repositary_address>
git clone <repo> <directory>
```

<a name="git-remote"></a>

```
git remote -v  #可以知道 origin 是哪个文件
```

<a name="git-init"></a>

```
git init
```

<a name="git-status"></a>

```
git status  #return current status of the repository
```

<a name="git-add"></a>to add file(s) to the staging area as tracked to be committed later

```
git add
git add .
git add <filename>
git add <filename1> <filename2>
git add -p  #-p means "patch", to confirm which patch of change to be added into staging
```

<a name="git-commit"></a>to commit

```
git commit  #first i, then add msg, then ctrl+c, then :wq to exit
git commit -m "try not to use only one line msg but edited in nano"
git commit -am "message"  #shortcut to combine add + commit
git commit --amend
```

Add this line to your ~/.vimrc to add spell checking and automatic wrapping at the recommended 72 columns to you commit messages.

```
autocmd Filetype gitcommit setlocal spell textwidth=72
```

<a name="git-reset"></a>to revert commit

```
git reset --hard <SHA1_key>  #reset to specific version LOCALLY. Github version is UNTOUCHED.
```

<a name="git-push"></a>to push changes to github

```
git push
```

to create file to local destination ONLY

```
touch file_name
```

<a name="git-fetch"></a>to retrieve the lastest updates from remotes or from all. It's more like just checking to see if there are any changes available.

```
git fetch
git fetch -all
gir fetch origin
git fetch upstream
```

<a name="git-pull"></a>to pull changes from the 'origin' remote, 'master' branch AND merge them to the local checked-out branch.

```
git pull origin master
git pull upstream master
```

git pull origin/master will pull changes from the locally stored branch origin/master and merge that to the local checked-out branch. The origin/master branch is essentially a "cached copy" of what was last pulled from origin, which is why it's called a remote branch in git parlance. This might be somewhat confusing.

```
git pull origin/master  #different from the first
```

<a name="git-branch"></a>to show and edit branches

```
git branch  #return all branches
git branch <new branch name>  #to create a branch
git branch -d <branch_name_to_delete>
git branch -d <branch_name1> <branch_name2>
git branch -D <branch name to delete>  #to delete a branch with uncommitted changes
```

<a name="git-checkout"></a>to revert to the snapshot before the most recent change  
to revert changes to modified files before they are staged.  
git checkout is effectively used to switch branches.  
git checkout can checkout both files and branches.

```
git checkout
```

to restore the file in your working directory to look exactly as it did when you last made a commit. 恢复上一个 commit 删除的文件

```
git checkout HEAD <filename>
```

```
git checkout <branch name to move to>
git checkout -b <newbranch>  #create a newbranch and switched to it
```

<a name="git-stash"></a>to stash the changes in a dirty working directory away

```
git stash
git stash list
git stash pop

```

<a name="git-rebase"></a>to delete all changes from one branch and only merge the last version to merge into the master
https://www.yiibai.com/git/git_rebase.html

```
git rebase origin/master
git rebase -i <SHA1_key> #to reword commit messages, combine, and remove commits

```

<a name="git-sqash"></a>

```

squash #to squash several commits into one

```

<a name="git-merge"></a>to merge into the master AND keep all commits happened in the edited branch  
fast-forward merge  
three-way merge

```

git merge <发生改动，需要 merge 进来的 branch>  #注意，此时必须在另外一个 branch 里运行这个 merge command
git merge upstream/master
git merge --abort  #stop merge and reset to previous

```

<a name="merge-conflict"></a>to solve merge conflicts is to delete whatever then save, then repeat push procedure  
merge conflict
如果在 2 个 branch 里对同一条语句进行修改，然后 merge，会出现 merge conflict。在 conflict 发生的文件里，git 会自动标记 conflict 出现的地方，如下  
如何解决 conflict：
选择希望保存的文件，然后删掉其他所有的 git 提示，比如<<<<<<< HEAD， =======， >>>>>>> fencing

```

<<<<<< HEAD
<your change>
=============
<other change>

> > > > > > conflicting commit

```

<a name="git-log"></a>history of all commits

```

git log
git log --stat
git log --graph
git log --oneline
git log --oneline decorate=no
git log --walk --reflogs
git log -p
git log -p -2  #return last two patches
git log -2  #show last two commits
git log --stat
git reflogs #show all reference logs
git help log

```

```

\$ git log

output:
commit 00a52122f86f0e20d9374079c8197d0eb2183b54
Author: codecademy <ccuser@codecademy.com>
Date: Fri May 8 11:41:11 2020 +0000

    First commit

    ////////////////////////////////////////
    A 40-character code, called a SHA1 hash numbers, that uniquely identifies the commit. This appears in orange text.
    The commit author (you!)
    The date and time of the commit
    The commit message
    //////////////////////////////////////
    press "q" to exit from git log

```

<a name="git-diff"></a>

```
git diff  #only shows unstaged changes
git diff file_name_1 file_name_2
git diff --stage  #to see changes staged but not committed yet
```

<a name="git-show"></a>

```
git show <SHA1_keys>
git show HEAD  #show last commit
```

<a name="git-reset"></a>to remove the file already in the staging area to untracked. It does not discard file changes from the working directory, it just removes them from the staging area.  
https://jwiegley.github.io/git-from-the-bottom-up/3-Reset/4-doing-a-hard-reset.html

```
git reset HEAD <filename>
git reset -p
```

通过 reset， 使 HEAD 指向之前的这个 commit

```
git reset <SHA_key>
```

<a name="git-config"></a>to check current config

```
git config -l
```

<a name="git-rm"></a>to remove files, changes are staged but not committed yet

```
git rm <filename>
```

<a name="git-mv"></a>to rename file, changes are staged but not committed yet

```
git mv <filename> <filename_renamed>
```

<a name="gitignore"></a>list of files to ignore

```
.gitignore
```

```
#some files in Mac OS system to ignore
https://gist.github.com/octocat/9257657
echo .DS_STORE > .gitignore
```

<a name="git-revert"></a>to rollback to version which was before the committ is happened; namely to cancel previous changes to a public repo
Good habit to add extra msg on why this rollback happened

```
git revert HEAD  #HEAD alias to represent the most recent commit in our history
```

# <a name="git-tips"></a>git Tips & Good Coding habits

1. Procedure to push local changes to github:
   1. "git add <filename>" after editing a file,
   2. "git commit -m "\$\$\$""
   3. "git push"
   4. check if version is updated on github
2. Procedure to create a branch locally then push to github:
   1. "git clone <url>"
   2. "git branch" to check there is only \*master branch
   3. "git branch <new branch name>" to create a new branch locally
   4. "git checkout <new branch name>" to be on the new branch
   5. follow "push local changes to github", after "git push"
   6. to solve, use "git push --set-upstream origin feature"
   7. check gitbub is a new branch is added
