---
title: "使用hugo搭建个人博客mac版"
date: 2020-01-01T22:15:24+08:00
draft: false
---

## 大家好，今天给大家分享下如何使用 hugo 搭建个人博客

### 1.安装 hugo

在终端中输入
`brew install hugo`安装。

安装成功后可输入`hugo version`查看版本信息。

---

### 2.创建新网址

`hugo new site quickstart`
其中`quickstart`更改为`用户名.github.io-creator`（用户名为 github 用户名，需要小写）
使用`code 用户名.github.io-creator`使用 vscode 查看目录

---

### 3.添加一个主题

在 vscode 目录下打开新的终端，输入
`git init`

`git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke`

然后，将默认主题添加到站点配置中：

`echo 'theme = "ananke"' >> config.toml`

还可自定义主题，具体可浏览<a href="https://gohugo.io/getting-started/quick-start/">hugo</a>官网查看教程。

---

### 4.添加一些文件

`hugo new posts/my-first-post.md`

其中`my-first-post`可更改博客名。
可从下图内容后编辑
![](https://user-gold-cdn.xitu.io/2020/1/4/16f707cfef95191f?w=315&h=90&f=png&s=10148)
并将`draft：ture`更改为`draft：false`。

---

### 5.启动 Hugo 服务器

`hugo server -D`

---

### 6.建立静态页面

`hugo -D`
自动创建一个 public 目录。

### 7.上传至 github

1. 在 vscode 新建一个.gitignore，进入后输入
   ![](https://user-gold-cdn.xitu.io/2020/1/4/16f7090c28139a8a?w=276&h=107&f=png&s=4268)
2. 终端下输入

   `cd public/`

   `git init`

   `git add .`

   `git commit -v`备注后关闭，第一篇文章就部署完毕。

3. 在 github 上新建仓库，名称为：`用户名.github.io`

终端中输入
`git remote add origin git@github.com:github用户名/用户名.github.io.git`

`git push -u origin master`后，刷新页面即可

4.  在 github settings 中找到 GitHub Pages，点击`https://github用户名.github.io/`即可
