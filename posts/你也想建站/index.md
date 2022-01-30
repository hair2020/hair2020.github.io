# 想建站？


[TOC]

# 如何建站？（以本站为例）

## 本教程需要

- 注册github账号能力

- 搜索引擎使用能力

- 科学上网能力

- 文档阅读能力

- 英语能力 或 使用翻译功能能力

- Markdown使用能力

- 一个脑子

  你没有？请退出吧，本教程不适合你。

## 大致流程

- 注册github账号

- 建立仓库，并命名为如下格式：

  `<USERNAME>.github.io` 例：`ZhangSan.github.io`

- 在仓库中点击`setting`找到`GitHub Pages`点击`Check it out here!`。看到绿背景写着"Your site is published at `https://...`"，则成功白嫖到地址。注意：用它做域名的网站不能用数据库。

- 可选择gitPages自带的 Jekyll theme， 我没相中的所以没用。

- 本站用的[hugo](https://github.com/gohugoio/hugo)项目。阅读官方文档进行建站。

  

  有人想问为啥我用hugo不用别的，引用如下

  > The world’s fastest framework for building websites.
  >
  > A Fast and Flexible Static Site Generator built with love by [bep](https://github.com/bep), [spf13](http://spf13.com/) and [friends](https://github.com/gohugoio/hugo/graphs/contributors) in [Go](https://golang.org/).

## 主题选用

强迫症选择主题真是太困难了，还好我不是。

官方主题地址：[Complete List | Hugo Themes (gohugo.io)](https://themes.gohugo.io/)

本站主题由[B站视频](https://www.bilibili.com/video/BV1cv411N7kz?p=3)得知，名为[LoveIt](https://github.com/dillonzq/LoveIt)

## 本主题踩坑

### 更换favicon.ico

#### 问题

​	文档说，直接把做好的图标，放./status文件夹中。

​	我放完弄了半天都没看到效果，还是默认的。

​	我到`./themes/LoveIt/layouts/partials/head/links.html`看也没啥问题，F12调试看<link>，点进去还是默认图标？？？？？？？？？？？烦死了

#### 解决

​	本地测试时，由于Edge缓存的原因，无法得到实时更新。看生成public中的favicon.ico换了就没问题。

​	如果调试中看不到如下标签{{< figure src="/images/links.png">}}

​	去config.toml找`noFavicon = false`

### 内嵌图片

#### 问题

​	用原本的Markdown语法没用

#### 解决

​	用LoveIt内置 Shortcodes

​	{{< figure src="/images/ImageInMD.png">}}

## 参考文档

> [The world’s fastest framework for building websites | Hugo (gohugo.io)](https://gohugo.io/)
>
> [LoveIt (hugoloveit.com)](https://hugoloveit.com/zh-cn/)
>
> [Favicon Generator for perfect icons on all browsers (realfavicongenerator.net)](https://realfavicongenerator.net/)
>
> [Full text search in hugo website - tato's note (hommalab.io)](https://note.hommalab.io/posts/web/full-text-search-in-hugo/#11-setup-algolia-in-loveit-theme)
>
> https://www.bootcdn.cn/lunr.js/

