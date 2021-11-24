# hugo安装



## 一、安装Git



```shell
sudo apt install git
```

<font size=5 face="微软雅黑">配置ssh</font>

```shell

```



## 二、安装go

```shell
mkdir ~/home_opt		#home下软件安装包位置的home_opt，可设置自己的位置
cd ~/home_opt
wget -c https://go.dev/dl/go1.17.3.linux-amd64.tar.gz
sudo tar -xz go1.17.3.linux-amd64.tar.gz
mv -f go go_install						#重命名
sudo mv -f  go_install /usr/local		#移动到安装区
cd /usr/local
sudo chmod -R 0777 go_install
```

<font size=5 face="微软雅黑">添加到`$PATH`环境变量</font>

<font size=5 face="微软雅黑">`GOROOT`是系统上安装Go软件包的位置</font>

<font size=5 face="微软雅黑">`GOPATH`是工作目录的位置</font>

```shell
# src：go在包安装、文件编译时自动寻找区，bin：go执行命令区
mkdir ~/home_opt/go_work ~/home_opt/go_work/src ~/home_opt/go_work/bin	#go工作区
sudo chmod -R 0777 go_work
```

<font size=5 face="微软雅黑">修改环境变量，我的shell改为zsh了。</font>

```shell
sudo gedit ~/.zshrc
```

```shell
#内容：
export GOROOT=/usr/local/go_install
export GOPATH=~/home_opt/go_work
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

```shell
source ~/.zshrc		#环境变量生效
export				#输出
```

<font size=5 face="微软雅黑">默认shell的修改使用下面的：</font>

```shell
echo $shell			#查看默认shell
sudo gedit ~/.bashrc
source ~/.bashrc	#环境变量生效
export				#输出
```

<font size=5 face="微软雅黑">效果：关闭shell，重启终端输入（任意shell能输出版本）</font>

```shell
go version
```

![截屏-20211123173529-319x63](/home/mhking/Pictures/截屏-20211123173529-319x63.png)

## 二、编译hugo

<font size=5 face="微软雅黑">[官网安装](https://github.com/gohugoio/hugo)（Mac，windows，linux如下）</font>

```shell
mkdir ~/home_opt/src
cd ~/home_opt/src
git clone https://github.com/gohugoio/hugo.git
cd hugo
go install
```

```shell
#错误：
go: github.com/bep/debounce@v1.2.0: Get "https://proxy.golang.org/github.com/bep/debounce/@v/v1.2.0.mod": EOF

```

![截屏-20211123180633-803x36](/home/mhking/Pictures/截屏-20211123180633-803x36.png)

```shell
#国内ping不通proxy.golang.org
#输入以下即可：
go env -w GOPROXY=https://goproxy.cn
```

![截屏-20211123180648-473x62](/home/mhking/Pictures/截屏-20211123180648-473x62.png)

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

![截屏-20211123181431-632x59](/home/mhking/Pictures/截屏-20211123181431-632x59.png)

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
#克隆主题到themes，主题对应一个作者的github仓库，submodule add将他人仓库链接到自己的仓库，主题更新时我们网页同步更新
git submodule add https://github.com/kakawait/hugo-tranquilpeak-theme.git themes/hugo-tranquilpeak-theme themes/hugo-tranquilpeak-theme
#自己看主题配置，每个主题都不同，都需要修改一些配置。有些还要装插件
```

![截屏-20211123182529-2539x1050](/home/mhking/Pictures/截屏-20211123182529-2539x1050.png)

![截屏-20211123182627-2254x1055](/home/mhking/Pictures/截屏-20211123182627-2254x1055.png)

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

![截屏-20211123185932-814x478](/home/mhking/Pictures/截屏-20211123185932-814x478.png)

<font size=5 face="微软雅黑">浏览器输入：http://localhost:1313/</font>

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

<font size=5 face="微软雅黑">建立工作流，这是静态网页生成脚本，hugo官网有介绍，[Host on GitHub](https://gohugo.io/hosting-and-deployment/hosting-on-github/)</font>

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

![截屏-20211123233301-1715x1034](/home/mhking/Pictures/截屏-20211123233301-1715x1034.png)

```shell
git status
git add .
git commit -m "update toml"
git push

git status
git add .
git commit -m "hugo install to github"
git push

```

<font size=5 face="微软雅黑">githut分支源默认改为gh-pages</font>

## 总结：

<font size=5 face="微软雅黑">虽说国内外教程挺多，但是一堆坑还不一定能弄完，有搞一半就没了，多多少少有缺斤少两的。（windows坑最多，hexo兼容最差，那个npm一言难尽，一堆过期包，修都要半天，主题都没法装）</font>

<font size=5 face="微软雅黑">最后两步骤，上传Hugo源码和静态文件的就没几个讲清楚的，整完主题不能显示的一堆.....themes没链接好，还是太小白，大神不大想讲</font>

<font size=5 face="微软雅黑">学好github的分布式开发吧。用官网的安装方式就行，个人向的水平参差不齐。</font>

------

[Hugo And Deploy To Github]: https://www.youtube.com/watch?v=psyz4UPnGAA&amp;ab_channel=CodeNanshu	"这是讲的最好的"

------

[Creating a Blog with Hugo and Github in 10 minutes]: https://www.youtube.com/watch?v=LIFvgrRxdt4&amp;ab_channel=RyanSchachte
[使用Hugo和GitHub搭建博客]: https://zhuanlan.zhihu.com/p/150095964
[GitHub+Hexo 搭建个人网站详细教程]: https://zhuanlan.zhihu.com/p/26625249

