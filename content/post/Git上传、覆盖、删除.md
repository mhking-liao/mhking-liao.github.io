# Git上传、覆盖、删除

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