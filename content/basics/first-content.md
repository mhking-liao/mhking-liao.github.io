---
title: "第一章"
date: 2021-11-24T15:53:43+08:00
draft: fault
---

## 1.目录命令：

`chapter=true`在顶部，这意味着这个页面是一个*章节*，

默认情况下，所有章节和页面都创建为草稿。如果要呈现这些页面，请删除该属性`draft: true` 从元数据。

```shell
draft: true			#隐藏文章
draft: fault		#显示文章
```

```python
hugo new --kind chapter basics/_index.md
```

## 2.文章命令：

通过添加一些示例内容并替换`title`文件开头的值，可以随意编辑这些文件。

```shell
hugo new basics/first-content.md 
hugo new basics/second-content/_index.md
```

## 3.网页图标

如果您的图标是 png，只需将您的图像放在本地 `static/images/` 文件夹并命名 `favicon.png`

如果您需要更改此默认位置，请在 `layouts/partials/` 命名 `favicon.html`. 然后像这样写：

```html
<link rel="shortcut icon" href="/images/favicon.png" type="image/x-icon" />
```

## 4.网页颜色

[params]  

```shell
*# Change default color scheme with a variant one. Can be "red", "blue", "green".*  
themeVariant = "green"
```

