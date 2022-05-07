---
title: Git_learning
date: 2022-05-06 14:39:10
tags: 
 - Linux
 - Git
---

# Git_learning

# Git基本操作

记录目前已经用到过的git操作，后续如果有发生新的操作再进行修改

**创建仓库**

```bash
git init
git clone
```

**提交和修改**

```bash
git add
git status
git diff
git commit
```

**日志**

```bash
git log
#git blame <file>
```

**远程操作**

```bash
git remote
git fetch
git pull 
git push # -f为强制推送
```

**分支**

```bash
git branch -a -v -av -d -b
git checkout 
git merge
```

## Git子模块

### 问题

git add 时 出现warning 正在添加嵌入式 git 仓库

### 解决

1. 添加子模块

   ```bash
   #=删除仓库索引=======================================
   # 如果是文件
   git rm --cached themes/next
   # 如果是文件夹
   git rm -r --cached themes/next
   # 如果执行以上命令后提示：【 error: 如下文件其暂存的内容和工作区及 HEAD 中的都不一样：】 ，`-f`强制删除
   git rm -r -f --cached themes/next
   
   #=添加仓库索引=======================================
   # 创建子模块并添加 url 地址
   git submodule add <url> project
   # 例如：
   git submodule add https://****.git themes/next
   # 或者使用 ssh 地址
   git submodule add git@g****.git themes/next
   ```

   添加成功后会生成`.gitmodules`文件

2. 提交

   ```bash
   git add . 
   git commit -a
   git push
   ```

3. 拉取&更新

   ```bash
   git submodule update --init --recursive
   ```

# clone分支

 1. 克隆单分支

    ```bash
    git clone -b {分支名} https://***.git
    ```

2. 克隆所有分支

   ```bash
   git clone
   git branch -a
   * master
     remotes/origin/HEAD -> origin/master
     remotes/origin/main
     remotes/origin/master
   git checkout -b main origin/main 
   #作用是checkout远程仓库origin的分支main，在本地起名为main分支，并切换到本地的main分支 
   
   ```

# push

	1. git remote

    ```bash
    # 添加远程主机
    git remote add  <主机名> <网址>
    # 删除远程主机
    git remote rename <原主机名> <新主机名>
    
    ```

	2. git push

    ``` bash
    git push <远程主机名> <本地分支名>:<远程分支名>
    git push origin master
    git push --set-upstream origin main # 主机名 主机分支名
    ```

    
