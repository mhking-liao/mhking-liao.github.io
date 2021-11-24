---
title: "go语言"
date: 2021-11-24T11:57:03+08:00
categories:
- 广西贵港
- 家中
tags:
- 安装
keywords:
- tech
#thumbnailImage: //example.com/image.jpg


---

# go语言编译安装Hugo

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

添加到`$PATH`环境变量

`GOROOT`是系统上安装Go软件包的位置

`GOPATH`是工作目录的位置

```shell
# src：go在包安装、文件编译时自动寻找区，bin：go执行命令区
mkdir ~/home_opt/go_work ~/home_opt/go_work/src ~/home_opt/go_work/bin	#go工作区
sudo chmod -R 0777 go_work
```

修改环境变量，我的shell改为zsh了。

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

默认shell的修改使用下面的：

```shell
echo $shell			#查看默认shell
sudo gedit ~/.bashrc
source ~/.bashrc	#环境变量生效
export				#输出
```

效果：关闭shell，重启终端输入（任意shell能输出版本）

```shell
go version
```

![截屏-20211123173529-319x63](https://photoline-1259169166.cos.ap-guangzhou.myqcloud.com/202111242116100.png)

## 二、编译hugo

[官网安装](https://github.com/gohugoio/hugo)（Mac，windows，linux如下）

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

![截屏-20211123180633-803x36](https://photoline-1259169166.cos.ap-guangzhou.myqcloud.com/202111242116423.png)

```shell
#国内ping不通proxy.golang.org
#输入以下即可：
go env -w GOPROXY=https://goproxy.cn
```

![截屏-20211123180648-473x62](https://photoline-1259169166.cos.ap-guangzhou.myqcloud.com/202111242116485.png)

```shell
hugo version
```
