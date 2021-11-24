---
title: "Hugo to Github"
date: 2021-11-24T11:57:03+08:00
categories:
- 广西贵港
- 家中
tags:
- 博客
- 安装
keywords:
- tech
#thumbnailImage: //example.com/image.jpg

---

# Hugo安装

## 一、安装Git

```shell
sudo apt install git
```

### 配置ssh

```shell

```



## 二、hugo安装

https://github.com/gohugoio/hugo/releases

1. #### 下载最新的扩展版本 ( [hugo_extended_0.89.4_Linux-64bit.tar.gz](https://github.com/gohugoio/hugo/releases/download/v0.89.4/hugo_extended_0.89.4_Linux-64bit.tar.gz))。

2. #### 创建一个新目录：

   ```shell
   mkdir hugo
   ```

3. #### 将您下载的文件解压缩到`hugo`.

4. #### 切换到新目录：

   ```shell
   cd hugo
   ```

5. #### 安装雨果：

   ```shell
   sudo install hugo /usr/bin
   ```

6. #### 版本

   ```shell
   hugo version
   ```

## 三、配置本地站点

## 1.建立本地站点

```shell
# 在建立站点
mkdir ~/home_opt/blog
cd ~/home_opt/blog
hugo new site hugo_blog
cd hugo_blog
```

![截屏-20211123215327-691x86](https://photoline-1259169166.cos.ap-guangzhou.myqcloud.com/202111242056572.png)

```shell
cd ~/home_opt/blog/hugo_blog
git init	#将~/home_opt/blog/hugo_blog设置为空的初始化仓库,github默认仓库链接到hugo_blog
git status	#文件变动
git add .	#文件变动指定目录，.代表全部
git commit -m "first commit"	#文件变动提交至暂存区
```

## 2.添加博客主题，就是样式

https://themes.gohugo.io/

```shell
#推荐git submodule add theme-* themes/theme-*
#git clone（好多主题都不推荐的，写的是有些内容可能显示异常）
#一个主题对应一个作者的github仓库，submodule add将他人仓库链接到自己的仓库，主题更新时我们的网页主题同步更新

git submodule add https://github.com/kakawait/hugo-tranquilpeak-theme.git themes/hugo-tranquilpeak-theme themes/hugo-tranquilpeak-theme

#自己看主题配置，每个主题都不同，都需要修改一些配置。有些还要装插件
```

![截屏-20211123182529-2539x1050](https://photoline-1259169166.cos.ap-guangzhou.myqcloud.com/202111242056801.png)

![截屏-20211123182627-2254x1055](https://photoline-1259169166.cos.ap-guangzhou.myqcloud.com/202111242056216.png)

```shell
cd ~/home_opt/blog/hugo_blog
# 一般主题会有一个配置好的文件，在exampleSite下，替换站点根目录下的config.toml即可
rm -rf config.toml
cd /themes/hugo-theme-***
cp -rf /exampleSite/config.toml ~/home_opt/hugo_blog
```

## 3.添加一篇文章（markdown格式）

```shell
#网页文章一般以markdown格式写作，位置：content/post
hugo new content/post/test_post.md
gedit content/post/test_post.md		#hugo命令建立md，自动带模板
```

```makefile
---
title: "Test_post"
date: 2021-11-23T18:44:37+08:00
draft: true
---

# 有志者事竟成
### 人生的幸福，一半要争，一半要随。争，不是与他人，而是与困苦。没有唾手可得的幸福，发愤图强，主动争取才能一步步接近幸福。随，不是随波逐流，而是知止而后安。能力与条件的限制，很多人事只能随遇而安，随缘而止。争，人生少遗憾；随，知足者常乐。最怕该争时不争，该止时不止，总在纠结中痛苦着。
```

```bash
hugo server
```

![截屏-20211123185932-814x478](https://photoline-1259169166.cos.ap-guangzhou.myqcloud.com/202111242056793.png)

### 浏览器输入：http://localhost:1313/

## 四、上传Hugo至Github

```shell
git status
git add .
git commit -m "ready to upload"
git branch -M main	#命名分支为main
#github仓库为空，本地仓库添加github仓库地址
git remote add origin https://github.com/mhking-liao/mhking-liao.github.io.git
git push -u origin main	#改动文件上传至github
```

### 建立工作流，这是静态网页生成脚本，hugo官网有介绍，[Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/)

```shell
mkdir .github
cd .github
mkdir workflows
cd workflows
vim gh-pages.yml
```

```shell
#内容：
name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```

```shell
cd ~/home_opt/blog/hugo_blog
git status
git add .
git commit -m "deploy"
git push
```

```shell
#修改config.toml文件
baseURL = "github地址"
disqusShortname = "hugo-tranquilpeak-theme"
```

![截屏-20211123233301-1715x1034](https://photoline-1259169166.cos.ap-guangzhou.myqcloud.com/202111242056365.png)

```shell
git status
git add .
git commit -m "update toml"
git push
#自用样本，可自写sh脚本
git status
git add .
git commit -m "Article update 2021.11.24_11:45"
git push

```

### githut分支源默认改为gh-pages

------

## 总结：

### 虽说国内外教程挺多，但是一堆坑还不一定能弄完，有搞一半就没了，多多少少有缺斤少两的。（windows坑最多，hexo兼容最差，那个npm一言难尽，一堆过期包，修都要半天，主题都没法装）

### 最后两步骤，上传Hugo源码和静态文件的就没几个讲清楚的，整完主题不能显示的一堆.....themes没链接好，还是太小白，大神不大想讲

### 学好github的分布式开发吧。用官网的安装方式就行，个人向的水平参差不齐。

------

Hugo And Deploy To Github：https://www.youtube.com/watch?v=psyz4UPnGAA&amp;ab_channel=CodeNanshu 这是讲的最好的

------

Creating a Blog with Hugo and Github in 10 minutes：https://www.youtube.com/watch?v=LIFvgrRxdt4&amp;ab_channel=RyanSchachte 

使用Hugo和GitHub搭建博客： https://zhuanlan.zhihu.com/p/150095964 

GitHub+Hexo 搭建个人网站详细教程：https://zhuanlan.zhihu.com/p/26625249

