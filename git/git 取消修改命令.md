## 取消对文件的修改。还原到最近的版本，废弃本地做的修改。
git checkout -- <file>

## 取消已经暂存的文件。即，撤销先前"git add"的操作
git reset HEAD <file>...

## 修改最后一次提交。用于修改上一次的提交信息，或漏提交文件等情况。
git commit --amend

## 回退所有内容到上一个版本
git reset HEAD^

## 回退a.py这个文件的版本到上一个版本  
git reset HEAD^ a.py  

## 向前回退到第3个版本  
git reset –soft HEAD~3  

## 将本地的状态回退到和远程的一样  
git reset –hard origin/master  

## 回退到某个版本  
git reset 057d  

## 回退到上一次提交的状态，按照某一次的commit完全反向的进行一次commit.(代码回滚到上个版本，并提交git)
git revert HEAD
