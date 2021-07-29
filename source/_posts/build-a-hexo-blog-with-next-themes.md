---
title: 使用 GitHub Pages、Hexo 和 NexT 主题搭建 Blog
date: 2021/7/28 20:46:25
categories: # 分类
- Blog 搭建记录
tags: # 标签
- GitHub Pages
- Hexo
- NexT
- Git
sticky: 0
copyright: true # 是否开启版权声明，true 是； false 否。
---

最近打算把散落各地的文章汇聚过来，使用 GitHub Pages、Hexo 和 NexT 主题搭建 Blog，简单记录一下折腾过程，以备后用。

<!-- more -->

# 简介

[Hexo](https://hexo.io/)：快速、简洁且高效的博客框架；
[NexT](https://github.com/theme-next/hexo-theme-next)：一款风格优雅的高质量 Hexo 主题，自点点滴滴中用爱雕琢而成。
主要采用以上两个开源产品及其插件进行 Blog 开发，方案比较成熟，新版 Next 主题可配置性比之前高，用法与之前有些出入。

# Hexo 安装

## 环境配置

安装 Hexo 需要提前装好 [Node.js](https://nodejs.org/en/) 和 [Git](https://git-scm.com/)。

计划安装目前最新版 Hexo，所以需要安装 `10.13.0` 以上的 Node.js；Git 无具体版本要求。

- 本地 Node.js 版本 `v14.16.0`；
- 本地 Git 版本 `2.21.0.windows.1`。

## Hexo 安装

- 全局安装 Hexo：

```shell
npm install hexo-cli -g
```

- 在 Blog 文件夹的父文件下执行初始化 Blog 命令：

``` shell
hexo init <fileName>
```

`<fileName>` 是 Blog 的文件夹名，执行此命令后，在执行该命令的文件目录下，新建了一个名为 `<fileName>` 的文件夹，这个新建的文件夹是 **Blog 站点的根文件**，Blog 站点的根文件夹下的 `_config.yml` 是**Hexo 配置文件**。

- 进入上一步创建的文件夹：

```shell
cd <fileName>
```

- 安装 Hexo 相关依赖：

```shell
npm install
```

- 启动 Hexo 本地服务，测试是否成功：

```shell
hexo server
```

也可以用 `hexo s` 代替上面的命令。

这时命令行工具会出现：

```log
INFO  Hexo is running at http://localhost:4000 . Press Ctrl+C to stop.
```

可以通过浏览器访问 `http://localhost:4000` 来观察是否安装成功。

> **Tips：** 光标移到命令行工具，按住 `ctrl` + `C`，关闭本地服务器。

# 安装 Next 主题

## 方法一

- 进入 `./themes` 文件夹，执行：

```shell
git clone https://github.com/theme-next/hexo-theme-next.git
```

此时，在 `./themes` 下应该会有一个 `next` 文件夹。

- 通过文件管理器进入 `next` 文件夹，删除 `.git` 文件夹（这一步的目的是保证可以将个性化修改后的 `next` 文件夹上传到 GitHub）。

## 方法二

下载在 NexT 的 [Release 版本](https://github.com/theme-next/hexo-theme-next/releases)，并将下载的压缩包解压到 `./themes` 下，此时 `themes` 文件夹下应该有一个 `next` 文件夹。

> **注意：** 有两种方式可选，完成后，Blog 根文件夹下应该有一个 `themes` 文件夹，在 `themes` 文件夹下有一个 `next` 文件夹，在 `next` 根文件夹下有若干个文件、文件夹。`next` 是**主题根文件**，主题根文件下的 `_config.yml` 是**主题配置文件**。

## 验证

修改 Hexo 配置文件：

```diff _config.yml
- theme: landscape
+ theme: next
```

在 Blog 根文件夹下，执行:

```shell
hexo clean
hexo g
hexo s
```

在浏览器访问本地服务器地址，查看是否已经成功更换主题。

# 配置与美化

## 修改基本配置

可按 [Hexo 官方配置文件说明](https://hexo.io/zh-cn/docs/configuration.html) 对 Hexo 配置文件进行配置。


### 语言配置
如果预览时发现网站出现非中文，可按以下两种方式进行配置：

```diff _config.yml
- language: en
+ language: zh-CN
```

## Bug 修复

主题会有一些 Bug，记录一下打补丁方法。

### 中文文章 Toc 无法跳转

在 Hexo 更新至 5.x 版本，Next 更新至 7.x 版本后，会出现文章的中文目录点击跳转失效的 bug。

中文文章目录（TOC）点击可能跳转失败，[NexT 官方已经给出了修复方法](https://github.com/theme-next/hexo-theme-next/pull/1540/files#)。

下面记录一下：

```diff /themes/next/source/js/utils.js
      const sections = [...navItems].map(element => {
        var link = element.querySelector('a.nav-link');
+       var target = document.getElementById(decodeURI(link.getAttribute('href')).replace('#', ''));
        // TOC item animation navigate.
        link.addEventListener('click', event => {
          event.preventDefault();
-         var target = document.getElementById(event.currentTarget.getAttribute('href').replace('#', ''));
          var offset = target.getBoundingClientRect().top + window.scrollY;
          window.anime({
            targets  : document.scrollingElement,
            duration : 500,
            easing   : 'linear',
            scrollTop: offset + 10
          });
        });
-       return document.getElementById(link.getAttribute('href').replace('#', ''));
+       return target;
      });
```

## 其他配置与美化

### 站内搜索

在站点根文件夹下，执行：

```shell
npm install hexo-generator-searchdb --save
```

在 Hexo 配置文件末尾添加：
```diff _config.yml
+ search:
+   path: search.xml
+   field: post # 指定搜索范围，可选 post | page | all
+   format: html # 指定页面内容形式，可选 html | raw (Markdown) | excerpt | more
+   limit: 10000
```

将 NexT 主题配置文件 `local_search` 项目修改如下：

```diff /themes/next/_config.yml
  local_search:
-   enable: false
+   enable: true
    # If auto, trigger search by changing input.
    # If manual, trigger search by pressing enter key or search button.
    trigger: auto # 每次输入改变都执行搜索
    # Show top n results per article, show all results by setting to -1
    top_n_per_article: 1 # 每篇文章显示的搜索结果数量
    # Unescape html strings to the readable one.
    unescape: false
    # Preload the search data when the page loads.
    preload: false
```

`local_search` 的其他配置项可根据注释修改。

### 添加 rss

在站点根文件夹下，执行：

```shell
npm install hexo-generator-feed --save
```

在 Hexo 配置文件末尾添加：

```diff _config.yml
+ # Extensions
+ ## Plugins: http://hexo.io/plugins/
+ plugins: hexo-generate-feed
+ 
+ #Feed Atom
+ feed:
+   type: atom
+   path: atom.xml
+   limit: 20
```

在 NexT 主题配置文件，给配置项 `social` 添加 `rss: atom.xml || rss`：

``` diff /themes/next/_config.yml
  social:
+   rss: atom.xml || rss
```

`rss` 在 `social` 中的顺序会影响实际图标的顺序。

### 文末版权说明配置

在 NexT 主题配置文件，将配置项 `creative_commons` 的 `post` 修改为 `true`：

```diff /themes/next/_config.yml
  creative_commons:
    license: by-nc-sa
    sidebar: false
-   post: false
+   post: true
    language:
```

修改 `/themes/next/layout/_partials/post/post-copyright.swig` 文件：
```diff /themes/next/layout/_partials/post/post-copyright.swig
+ {% if page.copyright %}
    {%- set ccIcon = '<i class="fa fa-fw fa-creative-commons"></i>' %}
    {%- set ccText = theme.creative_commons.license | upper %}

    <div>
    <ul class="post-copyright">
      <li class="post-copyright-author">
        <strong>{{ __('post.copyright.author') + __('symbol.colon') }} </strong>
        {{- page.author or author }}
      </li>
      <li class="post-copyright-link">
        <strong>{{ __('post.copyright.link') + __('symbol.colon') }}</strong>
        {{ next_url(page.permalink, page.permalink, {title: page.title}) }}
      </li>
      <li class="post-copyright-license">
        <strong>{{ __('post.copyright.license_title') + __('symbol.colon') }} </strong>
        {{- __('post.copyright.license_content', next_url(ccURL, ccIcon + ccText)) }}
      </li>
    </ul>
    </div>
+ {% endif %}
```

在 `post` 模板中增加 `copyright` 这一配置项：

```diff  /scaffolds/post.md
+ copyright: false # 是否开启版权声明，true 是； false 否。
```

### 配置标签、分类、归档、关于页面

#### 配置标签页面

在 Blog 根文件夹下执行：
```shell
hexo new page tags # 新建“标签”页面
```

在主题配置文件对 `menu` 进行配置：
```diff /themes/next/_config.yml
  menu:
    home: / || home
    #about: /about/ || user
-   #tags: /tags/ || tags
+   tags: /tags/ || tags
    #categories: /categories/ || th
    archives: /archives/ || archive
    #schedule: /schedule/ || calendar
    #sitemap: /sitemap.xml || sitemap
    #commonweal: /404/ || heartbeat
```

修改 tags 页面：
```diff /source/tags/index.md
  ---
- title: tags
+ title: 标签
  date: 2021-07-27 21:58:57
+ type: "tags"
  ---
```

在 `post` 模板中增加 `tags` 这一配置项：

```diff  /scaffolds/post.md
+ tags: # 标签
```

#### 配置分类页面

在 Blog 根文件夹下执行：
```shell
hexo new page categories # 新建“分类”页面
```

在主题配置文件对 `menu` 进行配置：
```diff /themes/next/_config.yml
  menu:
    home: / || home
    #about: /about/ || user
    tags: /tags/ || tags
-   #categories: /categories/ || th
+   categories: /categories/ || th
    archives: /archives/ || archive
    #schedule: /schedule/ || calendar
    #sitemap: /sitemap.xml || sitemap
    #commonweal: /404/ || heartbeat
```

修改 categories 页面：
```diff /source/categories/index.md
  ---
- title: categories
+ title: 文章分类
  date: 2021-07-27 21:58:35
+ type: "categories"
  ---
```

在 `post` 模板中增加 `categories` 这一配置项：

```diff  /scaffolds/post.md
+ categories: # 分类
```

#### 配置归档页面

默认已经开启，如果没有按以下方式配置：

在 Blog 根文件夹下执行：
```shell
hexo new page archives # 新建“归档”页面
```

在主题配置文件对 `menu` 进行配置：
```diff /themes/next/_config.yml
  menu:
    home: / || home
    #about: /about/ || user
    tags: /tags/ || tags
    categories: /categories/ || th
-   #archives: /archives/ || archive
+   archives: /archives/ || archive
    #schedule: /schedule/ || calendar
    #sitemap: /sitemap.xml || sitemap
    #commonweal: /404/ || heartbeat
```

修改 archives 页面：
```diff /source/archives/index.md
  ---
- title: archives
+ title: 归档
  date: 2021-07-27 21:58:46
+ type: "archives"
  ---
```

#### 配置关于页面

在 Blog 根文件夹下执行：

```shell
hexo new page about # 新建“关于”页面
```

在主题配置文件对 `menu` 进行配置：
```diff /themes/next/_config.yml
  menu:
    home: / || home
-   #about: /about/ || user
+   about: /about/ || user
    tags: /tags/ || tags
    categories: /categories/ || th
    archives: /archives/ || archive
    #schedule: /schedule/ || calendar
    #sitemap: /sitemap.xml || sitemap
    #commonweal: /404/ || heartbeat
```

修改 about 页面：

```diff /source/about/index.md
  ---
- title: about
+ title: 关于
  date: 2021-07-27 21:45:02"
  ---
```

后面可以增加其他希望在“关于”页面添加的内容。

### 调整菜单排列顺序

在主题配置文件对 `menu` 进行配置,调整各项目的顺序：

```text /themes/next/_config.yml
menu:
  home: / || home
  tags: /tags/ || tags
  categories: /categories/ || th
  archives: /archives/ || archive
  #schedule: /schedule/ || calendar
  #sitemap: /sitemap.xml || sitemap
  #commonweal: /404/ || heartbeat
  about: /about/ || user
```

### 增加顶置功能

在页面增加 `sticky: 0` 即可，`0` 代表不顶置，可以将 `0`替换成其他数字，数字越大，权重越大，排名越靠前。

可以在 `post` 模板，增加 `sticky` 这一配置项。

```diff /scaffolds/post.md
  sticky: 0
```

### 首页折叠配置

NexT 主题自带 2 种首页折叠方式：

1. 配置 `description` 项目：

```diff
+ # description: XXXXXXXXXXX # 折叠简介
```

`XXXXXXXXXXX` 将作为简介显示在首页，其他内容将折叠，点击 `阅读全文》`，才能了解更多文章内容。

2. 在正文增加 `<!-- more -->`, 前面的正文将作为简介显示在首页，其他内容将折叠，点击 `阅读全文》`，才能了解更多文章内容。

配置 `post` 模板：

```diff /scaffolds/post.md
  ---
  title: {{ title }}
  date: {{ date }} # "2013/7/13 20:46:25"
  sticky: 0 # 顶置
  categories: # 分类
  tags: # 标签
+ # description: '' # 折叠简介
  copyright: false # 是否开启版权声明，true 是； false 否。
  ---
  
+ <!-- more -->
+ 
```

## GitHub 部署

如果托管在 GitHub Pages。

有两种方式访问 GitHub 的 GitHub Pages，这两种方式体现在 URL 的不同：`https://username.github.io/` 和 `https://username.github.io/ProjectName/`，其中 `username` **自己的**是用户 id，`ProjectName` 是项目名。

### 注册 GitHub 账号

过程略。


### 建立 GitHub 远程仓库

如果把 `https://username.github.io/` 作为 Blog 首页地址，则将仓库命名 `username.github.io`，其中 `username` 是**自己的**用户 id，无法修改。

如果把 `https://username.github.io/ProjectName/` 作为 Blog 首页地址，则将仓库命名 `ProjectName`，其中 `username` 是**自己的**用户 id，无法修改。

> **注意：** 远程仓库应该不含任何文件、文件夹。否则后续处理会有些麻烦。

### 配置 ssh

为了避免处理每次都推送都需要输入账号、密码，这里需要配置 ssh。本地已经配置过的，这里就不用配置了。具体过程略。

### 网址配置

- 如果把 `https://username.github.io/` 作为 Blog 首页地址，则在 Hexo 配置文件设置：

```diff _config.yml
  # URL
  ## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
- url: http://example.com
+ url: https://username.github.io
```

- 如果把 `https://username.github.io/ProjectName/` 作为 Blog 首页地址则，在 Hexo 配置文件设置：

```diff _config.yml
  # URL
  ## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
- url: http://example.com
+ url: https://username.github.io/ProjectName
+ root: /ProjectName/
```

### Hexo 命令部署配置

- 如果把 `https://username.github.io/` 作为 Blog 首页地址，则在 Hexo 配置文件设置：

```diff _config.yml
  # Deployment
  ## Docs: https://hexo.io/docs/one-command-deployment
  deploy:
+   type: git
+   repo: git@github.com:username/username.github.io.git
+   branch: gh-pages
```

- 如果把 `https://username.github.io/ProjectName/` 作为 Blog 首页地址，则在 Hexo 配置文件设置：

```diff _config.yml
  # Deployment
  ## Docs: https://hexo.io/docs/one-command-deployment
  deploy:
+   type: git
+   repo: git@github.com:username/ProjectName.git
+   branch: gh-pages
```

> **注意：** 实现 GitHub Pages 部署的原理是，将本地渲染好的静态文件（`/public` 文件夹内所有文件）以一个单独分支上传到 GitHub 远程仓库，GitHub Pages 服务渲染该分支的静态文件。这里 `branch` 配置了 GitHub Pages 将要渲染的 `gh-pages` 分支。

### 本地 Git 仓库配置与推送

本步骤的意义在于，切换电脑依然可以写 Blog，不用担心因为本地文件丢失，而无法继续创作。

在 Blog 站点的根文件夹执行：

- 初始化本地 Git 仓库：

```shell
git init
```

- 修改分支名称（现在许多仓库分支在去 `master` 化，如果需要将主分支修改为 `main` 可以执行下面的命令）：

```shell
git checkout -b main
git branch -d master
```

执行 `git branch -a` 可以查看目前所有的分支。

- 添加远程仓库；

```shell
git remote add <remoteName> <sshURL>
```

`<remoteName>` 是远程仓库名，一般设为`origin`；`sshURL` 是远程仓库的 ssh 链接。

- 将本地项目分支推送到远程 GitHub 仓库。

```shell
git add .
git commit -m "hexo init"
git push --set-upstream <remoteName> <branchName>
```

`<remoteName>` 是前面设定的远程仓库名；`<branchName>` 是本地仓库分支名。

### 推送静态文件到远程仓库

在 Blog 根文件夹下执行：

- 生成静态文件，并在本地服务器预览：

```shell
hexo clean
hexo g
hexo s
```

在浏览器访问本地服务器地址，查看是否正常，`ctrl` + `C` 关闭本地服务器。

- 将本地生成的静态文件上传到 GitHub 远程仓库：

```shell
hexo d
```

### 启动 GitHub Pages 服务

GitHub 项目主页、Settings -> Pages -> Source：

选择 `gh-pages` 作为渲染分支（`Branch`）；渲染文件夹选择 `/(root)`；保存（`Save`）。

保存后，GitHub 将给出提示：

> Your site is published at https://username.github.io/ProjectName/

或者

> Your site is published at https://username.github.io/

点击上面的地址，即可访问项目（有时需要等待 15 分钟左右）。

# 创建一篇文章

在 Blog 根文件夹下执行：

- 创建文章文件

``` bash
$ hexo new "My New Post"
```

更多请阅读 [Writing](https://hexo.io/docs/writing.html)

- 启动本地服务预览

``` bash
$ hexo server
```

更多请阅读 [Server](https://hexo.io/docs/server.html)

- 生成静态文件

``` bash
$ hexo generate
```

更多请阅读 [Generating](https://hexo.io/docs/generating.html)

- 部署到远程服务器

``` bash
$ hexo deploy
```

更多请阅读 [Deployment](https://hexo.io/docs/one-command-deployment.html)


> **参考资料**
> - [Hexo 官网](https://hexo.io/zh-cn/)
> - [Git个人博客hexo设置关于、标签、分类、归档、时间线](https://www.jianshu.com/p/ebbbc8edcc24)
> - [Hexo 搭建个人博客系列：主题美化篇](http://yearito.cn/posts/hexo-theme-beautify.html)
> - [Hexo 搭建个人博客系列：进阶设置篇](http://yearito.cn/posts/hexo-advanced-settings.html)
> - [知乎 - Hexo Next 主题中文目录点击失效是为什么?](https://www.zhihu.com/question/422584701)

