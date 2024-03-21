---
title: git命令记忆
date: 2024-03-20
category: [Technology,Frontend]
toc_number: false
---

面试的时候被狠狠拷打了一番，发现git有些命令还是没有掌握的很好

## git reset

用于回退版本，遗弃不再需要的提交，通过移动HEAD头实现

- --mixed（默认）：默认的时候，只有暂存区变化

- --hard参数：如果使用 --hard 参数，那么工作区也会变化

- --soft：如果使用 --soft 参数，那么暂存区和工作区都不会变化

## git revert

在现有的版本后面新建一个提交来取消某一次提交，用于安全地取消某一次提交

revert撤销已经push（公开）的提交，reset用于工作区的修改

## git merge
将当前分支合并到给出的分支

## git rebase
将当前分支移植到指定分支或指定commit之上

## git stash
暂存一些代码修改
git stash

git stash save

git stash list

git stash pop

git stash apply

git stash show

git stash drop

git stash clear

【使用场景】

使用git pull拉去远程分支的代码到本地，与本地的修改发生冲突，但是并不想提交本地的修改，就需要用暂存命令保存

## git fetch & pull
从远程分支拉取最新代码到本地，git fetch不会自动merge，git pull会自动merge

## branch
【命名规则】

- 只能使用字母、数字、横线、下划线和句点。
- 分支名称不能以横线或句点开头或结尾。
- 不允许使用的特殊字符：空格，反斜杠、冒号、问号、星号、左右尖括号
