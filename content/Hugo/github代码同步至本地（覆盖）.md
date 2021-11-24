---
title: "github"
date: 2021-11-24T11:57:03+08:00
categories:
- 广西贵港
- 家中
tags:
- 命令
keywords:
- tech
#thumbnailImage: //example.com/image.jpg



---
# 一、github代码同步至本地（覆盖）

(1) 更新远程仓库的代码为最新的
git fetch --all

(2) 让本地代码与origin/main完全相同
git reset --hard origin/main

(3) git pull origin main

# 二、github本地同步至仓库

1、（先进入项目文件夹）通过命令 git init 把这个目录变成git可以管理的仓库

```
git init
```

2、把文件添加到版本库中，使用命令 git add .添加到暂存区里面去，不要忘记后面的小数点“.”，意为添加文件夹下的所有文件

```
git add .
```

3、用命令 git commit告诉Git，把文件提交到仓库。引号内为提交说明

```
git commit -m 'first commit'
```

4、关联到远程库

```
git remote add origin 你的远程库地址
```

如：

```
git remote add origin https://github.com/cade8800/ionic-demo.git
```

5、获取远程库与本地同步合并（如果远程库不为空必须做这一步，否则后面的提交会失败）

```
git pull --rebase origin master
```

6、把本地库的内容推送到远程，使用 git push命令，实际上是把当前分支master推送到远程。执行此命令后会要求输入用户名、密码，验证通过后即开始上传。

```
git push -u origin master
```

*、状态查询命令

```
git status
```

# 三、Git上传、覆盖、删除

然后通过以下指令初始化，把这个项目所在目录变成Git可以管理的仓库。

```csharp
git init
```

成功后，复制仓库的ssh地址，并输入以下指令：

```csharp
 git remote add origin 仓库ssh地址
```

也可以用以下指令删除关联：

```bash
git remote rm origin
```

也可以通过以下指令更换仓库：

```python
git remote set-url origin 仓库ssh地址
```

更换后，可以用[查询](https://blog.csdn.net/m0_46419510/article/details/110499832#查询)查看是否更换成功。

 

## 添加上传

将全部内容添加，先输入以下指令：

```csharp
git add .
```

如果是指定目录，就改为以下指令：

```csharp
git add 目录
```

如果是指定文件，就改为以下指令：

```csharp
git add 文件.后缀
```

之后，再输入以下指令：

```sql
 git commit -m "把文件提交，这里是注释"
```

到这里，你的添加并没有上传到仓库，只是添加到了暂存区，上传到仓库还需要输入以下指令：

```perl
 git push -u origin main
```

最后，还会有个提示，输入 yes 即可。

## 删除

通过以下指令删除指定文件：

```css
git em 文件.后缀
```

通过以下指令可以删除指定文件夹：

```css
git em -r 文件夹
```

最后，必要通过以下指令提交修改：

```sql
git commit -m "注释"
```

 

## 查询

查看本地分支：

```undefined
git branch
```

查看关联仓库地址：

```undefined
git remote -v
```

待补充。
