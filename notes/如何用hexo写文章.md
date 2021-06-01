## Step 0: 基本了解 + 准备工作

1. 我们打开hexo所在目录 -> source -> _posts, 可以看到一个hello-world.md文件，这就是hexo自动帮我们生成的第一篇文章。
2. 回到hexo文件夹，就是里面有_config.yml, source, themes等等的那个。
3. 用hexo server来启动本地预览，在浏览器输入[http://localhost:4000/](https://link.jianshu.com?t=http://localhost:4000/)即可。

```
hexo server
```

## Step 1: 新建文章

在hexo所在目录下，打开terminal，在命令行输入：

```
hexo new a
```

a是文章标题，也可以加上双引号,如“a”。
 通过这行命令，我们新建出来了一个page，而且是一个post page，page还有其他种，稍后我们会提到。
 正确的结果：我们会在_posts里看见多了一个a.md文件。
 因此我们也知道了，默认情况下，hexo为我们创建的是markdown文件。刷新页面（[http://localhost:4000/](https://link.jianshu.com?t=http://localhost:4000/)）我们能看见新添一个名字叫a的文章，没有任何内容。
 而这个_posts文件夹，算是一个比较特殊的文件夹，因为它装着所有你发布出去的文章。

打开a.md文件，我们会看到



```css
---
title: 1
date: 2017-09-15 19:00:41
tags:
---
在这里随便写点什么
```

然后刷新页面,就会看到你写的内容。与此同时，hexo也会自动为这个post生成一个页面，当我们点击标题，就会进入那个页面。

![img](https:////upload-images.jianshu.io/upload_images/6995514-7481aad7a09a229c.png?imageMogr2/auto-orient/strip|imageView2/2/w/298/format/webp)

a.png

## Step 2:  草稿箱

上一步我们新建出来的，叫做post page。除了post page，我们还可以新建draft page，也就是草稿。很多时候我们需要先写成草稿，而暂时不发布出去。draft page就可以满足我们的要求，我们的网站上是看不到草稿文件的。

在terminal输入

```
hexo new draft b
```

我们会在source下看见一个新的文件夹，_drafts，这个里面会装我们所有的草稿文件。

那写好了的草稿，如何可以在不发布的情况下，预览一下文章在网站上的样子呢？

```
hexo server --draft
```

当然，你要先shut down原来开着那个server，才可以开启新的server。如此一来，我们就可以预览草稿文件啦

## Step 3: 发布草稿

当你准备好了要发布草稿时:

```
hexo publish b
```

你会发现_drafts里的b.md不见了，跑到了_posts里面,也就说明你的草稿发布成功了。

## Step 4: normal page

我目前还不知道该如何用中文称呼这类页面。我们可以把post和draft统称为blog pages，在这之外的一种就是normal pages， 类似一个网站上的“关于”，“了解我们”之类的页面。

这类page要如何新建呢？

```
hexo new page c
```

和前两种不同，这个命令会在source文件夹内创建出c文件夹，与_posts，_drafts并列。文件夹里面有一个index.md文件。

刷新页面，你会发现c并没有出现在页面内，那它在哪儿呢？

在网址后面加上c/， 即[http://localhost:4000/c/](https://link.jianshu.com?t=http://localhost:4000/c/)，就可以看到了。

正因为c不是一个blog page，所以它也不会出现在blog列表中，而是要通过URL去access。

## Step 5: 一个小tip

现在我们了解到page一共有三种，post，draft，normal。

![img](https:////upload-images.jianshu.io/upload_images/6995514-4608b4504a133a6e.png?imageMogr2/auto-orient/strip|imageView2/2/w/494/format/webp)

page_layout.png

那为什么一开始的时候我们用

```
hexo new a
```

就直接生成了post page呢？

因为默认的设置。

打开熟悉的_config.yml文件，找到

> default_layout: post

这句表示默认的页面会新建成post格式的。

所以，如果你习惯先把文章写成草稿，那就把它改成draft就好。

> default_layout: draft

* 执行`hexo d`即可部署到 GitHub 仓库。
* 新增或修改主题配置后部署时请执行 `hexo clean && hexo d`