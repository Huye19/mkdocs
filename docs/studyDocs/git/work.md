# git多人协作参考

### 基本操作有如下几个：

1. 查看当前分支 （git branch）

2. 创建分支 （git branch 分支名）

3.切换分支（git checkout 分支名）

4.分支上的常规操作

5.分支的合并 （git checkout master + git merge 分支名）

6.分支的删除（git branch -d 分支名）



### 1. **创建项目仓库：**

- 项目的创建者首先在版本控制系统中创建一个仓库。这可以是在远程仓库托管服务（如GitHub、GitLab、Bitbucket等）上创建，也可以是本地仓库。

### 2. **克隆仓库：**

- 其他团队成员通过 `git clone` 命令克隆远程仓库到本地，开始他们的开发工作。

  ```
  git clone <repository_url>
  ```

### 3. **创建分支：**

- 每位开发者在本地为自己的工作创建一个新分支，这样可以隔离各自的开发工作。

  ```
  git checkout -b feature-branch
  ```

### 4. **开发和提交：**

- 在各自的分支上进行开发工作，并通过 `git add` 和 `git commit` 提交更改。

  ```
  git add .
  git commit -m "Implement feature XYZ"
  ```

### 5. **拉取更新：**

- 在提交自己的更改之前，先拉取远程仓库的更新，以确保自己的分支是基于最新代码的。

  ```
  git pull origin main
  ```

### 6. **解决冲突（如果有）：**

- 如果多人在同一部分进行了修改，可能会发生冲突。在这种情况下，需要解决冲突，然后提交更改。

  ```
  git add .
  git commit -m "Merge remote-tracking branch 'origin/main'"
  ```

### 7. **推送分支：**

- 将本地分支推送到远程仓库，使其他人能够看到你的更改。

  ```
  git push origin feature-branch
  ```

### 8. **分支合并：**

分支合并一定要在主分支、只能在主分支合并其他分支

```
git merge hy
```

### 9. 删除分支

删除远程分支

```
git push origin --delete hy
```

删除本地分支

```
git branch -d hy
git branch -D hy (强制删除)
```



### 附加

切换至其他开发者的分支开发

```
git checkout -b fcl origin/fcl
```

设置当前分支与指定的远程分支相关联

```
git branch --set-upstream-to=origin/hyy hyy
```

