# Git备忘录


# git操作备忘录

[TOC]

## 上传仓库

1. 初始化

   `git init`

2. 添加所有文件到暂存区

   `git add .`

3. 告诉git，把文件提交到仓库

   `git commit -m "frist commit"`

4. 关联远程仓库

   `git remote add origin 仓库地址`

5. 提交

   `git push`

## 删除分支

1. 　　我现在在master分支上，想删除master分支

2. 　　先切换到别的分支: git checkout main

3. 　　删除本地分支： git branch -d master

4. 　　如果删除不了可以强制删除，git branch -D master

5. 　　必要的情况下，删除远程分支**(慎用)**：git push origin --delete master

      　　注：上述操作是删除个人本地和个人远程分支，如果只删除个人本地，请忽略第5步

## 合并分支

1. 首先切换到主分支

   git checkout master

2. 使用git pull 把领先的主分支代码pull下来

   git pull

3. 切换到自己的分支

   git checkout xxx(自己的分支)

4. 把主分支的代码merge到自己的分支

   git merge master

   由于历史原因报错可加这个： --allow-unrelated-histories

5. git push推上去ok完成,现在 你自己分支的代码就和主分支的代码一样了

   git push

6. **注：有冲突先解决冲突再进行提交**

## 报错

### 由于网络

#### 错误代码：10051，443

#### 解决方法：

- 取消代理，都运行

  ```
  git config --global --unset http.proxy
  git config --global --unset https.proxy
  ```

- 换vpn

- 等等再说

### 编辑器问题

#### 错误代码

1. `hint: Waiting for your editor to close the file...`

#### 解决方法

1. 将编辑器更改为默认的`git config --global core.editor 'vim'`
