---
title: "我的笔记系统"
date: 2020-01-01
draft: false
tags: ["笔记系统", "笔记管理", "知识管理", "个人Wiki", "TiddlyWiki", "Wayback Machine", "AWS S3"]
aliases: [
    "/zh-cn/self/note-system/"
]
keywords: ["笔记系统", "笔记管理", "知识系统", "个人Wiki", "TiddlyWiki", "Wayback Machine", "AWS S3"]
description: "本文介绍了如何使用TiddlyWiki打造个人长期的知识管理系统（图片使用AWS S3云存储管理），同时介绍了OneNote、EveryNote、Emacs Org等工具的优缺点"
series: ["自我成长"]
---

一个好的笔记系统，应该把你所学习到的任何资料串联起来，形成一个知识系统，在你需要他们的时候，可以很容易找到他们，然后形成自己新的知识。

{{< ad_embed_post >}}

在[《用OneNote管理你的知识》](/zh-cn/self/onenote-intro/)这篇文章中介绍了我用OneNote管理我的各种资料，虽然OneNote已经做的非常好了，但是存在以下问题无法达到我的要求:

1. 排版不支持语法高亮。作为一个经常写代码的，这点不能忍。
2. 没有Tag系统。无法很灵活的给页面插入各种tag，导致资料无法有效互联，形成一个个知识孤岛，最终变成一个资料备份工具。
3. 数据格式专有。只能用OneNote才能打开笔记本，假如微软突然放弃了这个工具，那就很尴尬了。
4. 体积庞大。在使用了近5年之后，我的OneNote已经上几GB大小了，每次换电脑同步总是很慢，这可能和我的使用习惯有关系，遇到好的资料都是复制进去。
5. 扩展能力差。无法安装插件，也没有定制能力，更无法将你的笔记发布成网站，也很难与别人分享你的知识。

因为这些问题，驱使我开始寻求新的解决方案，新方案应该满足以下需求：

1. 有强大的capture能力。OneNote的这点很不错，你可以通过OneNote的浏览器插件很容易将外部文章存至OneNote的分区中，也可以将微信公众号文章发送给OneNote公众号将其保存。
2. 有好的Tag系统。可以将分散的知识串联起来。虽然OneNote通过分页这种树形的方式组织相关的知识，但是资料一旦多了，分页这种方式真的很不方便，会让找资料变的很痛苦。
3. 能容易的更新tag/link/text。如果重命名相关的资料名或者Tag，应该很方便去自动重命名关联的链接。
4. 文件格式最好是纯文本的。如果不是纯文本，至少格式也不是专有的才好。
5. 有强大的扩展能力。能通过插件去扩展定制。
6. 开源。这点可以让我们放行的去使用，不太可能无人维护。

经过一番查找对比后，最终找到两个可以满足我需求的工具，Emacs orgmode和Tiddlywiki。虽然wiki工具非常多，比如Wikipedia使用的mediawiki之类，但这类系统过于庞大，要运行起来也很麻烦。

## Emacs orgmode

提到笔记系统，Emacs的orgmode总是绕不过去，当你想要找一个个人笔记系统的时候，在网上很容易看到大家对orgmode的盛赞，甚至很多人花长时间学习Emacs也是为了用orgmode。

orgmode神奇的魔力在这篇文章中体现的淋漓尽致：[Org Mode - Organize Your Life In Plain Text!](http://doc.norang.ca/org-mode.html) 。简单来说，作者使用orgmode管理了他人生中的方方面面，比如写作系统、待办事项提醒、笔记系统等。得益于Emacs强大的定制开发能力，几乎你的一切需求都可以通过编写一些函数去扩展，这种扩展能力比VSCode/Vim/Sublime Text的插件系统等要强大的多。可以说，除了学习难度高，几乎没啥缺点了。它有以下特点：

1. 17 years old。在时间的长河中，orgmode已经证明了自己。
2. 定制能力强大。通过elisp去开发，几乎无所不能。
3. 纯文本。可自动生成多种格式的文件，也很容易发布成网页。
4. 使用门槛很高。需要花费很多时间学习适应，这个很多时间可能比你想象的都要多一些。
5. 生态差。由于高门槛，所以用户就少一些，生态就差一些。当然你能力强，可以用它来实现各种功能，但是这样挺累的。
6. 技术迁移度差。elisp太古老了，emacs太独特了，这种上古技术，就像一把绝世好剑，注定能用好它的人会很少。这意味着你写出来的东西很多人都看不懂，当然也就无法进行技术交流互动了，自己造轮子造到心累。

## Tiddlywiki

[Tiddlywiki](http://www.tiddlywiki.cn/)是一款独特的非线性笔记本，用于捕获、组织和分享复杂信息。他的设计思想是将信息通过一种名为Tiddler的单元分割，利用它们之间丰富的关系模型，从而最大化信息的可复用性。 然后，通过聚合和构思来把片段编排在一起，以呈现具有叙述性的故事。

它具备以下特点：

1. 15 years old。这个历史足够久了，时间验证了其稳定性和可持续性，而且是开源的。
2. Tag系统强大。最让我印象深刻的就是它的Tag系统，很容易通过Tag将不同的信息组织到一起。
3. 单HTML文件架构。所有的信息都在一个Html中存放，你可以直接下载下来在浏览器中运行，非常的简单。默认的空的系统在最新的版本5中大约是2MB，一般存储几千个条目（Tiddler）大概能增长几MB，由于是单文件架构，为了不影响性能，应尽可能通过将图片外部引用来降低总体积。
4. 插件众多。很容易通过JavaScript给其扩展功能。
5. 无法多人协作。但可用作团队知识共享简单的wiki系统。

## orgmode VS Tiddlywiki

在这里可以看到一些人对这两个工具的对比评价[^0]。在花了几天时间学习了orgmode之后，我被它复杂强大的能力劝退了，所有选择了Tiddlywiki。

## Tiddlywiki使用指南

Tiddlywiki的使用和运行是极其简单的，就这点秒杀了orgmode。在这篇[Learning](http://www.tiddlywiki.cn/#Learning)文章中，你可以花费十几分钟了解下它的基本知识。

![](https://img.bmpi.dev/cf2e8f40-4c61-c32a-2a97-da5f44ea127d.png)

在上图右侧点击+号新增一个条目后：

![](https://img.bmpi.dev/451f2b30-8e51-32b8-6d05-06c1c5f94d48.png)

右侧红色的保存按钮点击了后，你会发现直接下载了一个名为`tiddlywiki.html`的文件，用浏览器打开后，会发现和你刚才在网上的tiddlywiki一摸一样。当你再对这个本地tiddlywiki进行一番操作保存后发现它又给你下载了一个`tiddlywiki.html`，也就是说每当你保存的时候，都会通过下载副本的形式保存，因为它在浏览器中运行，不具备自己更新自己的能力，这种可以通过一个chrome的app来解决，下载[tiddly-chrome-app](https://github.com/Arlen22/tiddly-chrome-app)，然后用此chrome app加载`tiddlywiki.html`即可自动更新了，当然也可以通过搭建Nodejs环境来实现自动保存，不过最简单的还是这种方式。

需要注意的有以下几点：

1. 备份。因为是单文件架构，所有的资料都在一个Html中存放，所以保护好这个文件至关重要，可以通过Git去备份。比如我的[tiddlywiki](https://wiki.bmpi.dev/)就在GitHub中备份[^1]。
2. 性能。图片、文件等资源最好通过存放第三方的云盘中，然后通过引用链接等方式引入。
3. Relink。当你重新命名一个条目或者Tag的时候，可以通过安装这个[tw5-relink](https://github.com/flibbles/tw5-relink)插件解决。

## Capture方案

Capture是一个笔记系统很重要的能力，这方面OneNote做的很好，但是tiddlywiki做的却不好，不过可以有一些方法来解决。让我们先来重新思考下一个笔记记录的过程：

1. 你看到一篇好文章，想要保存起来。这篇文章可能是一个网页，也可能是个邮件或者文件之类。
2. 你把这篇文章直接全部扔到笔记本中存起来，想象某天会用到它，或者你会将里面的某个章节，某个图片单独保存起来。

当我在用OneNote的时候，对于微信中的文章，我一般直接通过发送到公众号去保存，然后就忘了这个事情。而对于电脑端看到的一些资料，我会直接复制到OneNote中去。在某些时候我会整理一些这些资料，但是大多数他们就被遗忘了，甚至当我需要他们的时候，我都不记得我之前保存过这些资料。

在这个场景中，暴露了以下这几个问题：

1. 资料没有被处理就直接被存储了。
2. 大多数资料都是全部被存放到OneNote中去。

因为tiddlywiki本质是个网页，无法像OneNote一样可以直接复制一篇文章到里面去，而且这种复制手法会导致你的笔记越来越大，找寻有效信息变得越来越难。所以这本质是个习惯问题，资料必须被二次处理后才能进入笔记系统中，否则这个存储毫无意义，只需要存放一个链接即可了。

经过一些思考，我制定了自己资料长期归档的方式：

1. 引用文章可以保存到[Wayback Machine](https://web.archive.org/)中；
2. 文件可以保存到GitHub私有库和网盘中（包括s3等专业云存储，还有各大互联网公司的网盘）；
3. 通过第三方备份Capture资料，笔记中只存储链接。

在我的Capture方案，对于网上阅读的一些资料，考虑到互联网信息丢失的速度，大部分文章存活的寿命并不长[^2]，为了能长期保存，我会把这些网页使用Wayback Machine备份，这样再也不会丢失了，我只需要把它的链接存储起来即可，对于需要单独存储的资料可以存放到笔记系统中。对于需要存储的图片，我会存放到AWS S3[^3]中，然后引用其链接即可，当然这类云存储方案很多，你也可以选择国内七牛云（需要域名备案）等。

### Wayback Machine

20多年的历史，互联网的记忆，数字图书馆，网站时光机。这是一个非商业的项目，创立目的就是给整个互联网的网站做不停的备份，目前已经有4500多亿[^4]的缓存页面了，在这个网站你可以看到很多网站的历史，像时光机一样穿梭在网站的不同历史版本中去。

它具备以下能力：

1. 可爬取网页HTML及其外部链接。
2. 可生成网页快照图片。
3. 可将网页存储至自己的Wayback Machine账户。
4. 可以使用API来请求网页缓存[^5]。

### VSCode插件一键存储图片至S3

在Markdown文档中当你想把网页的图片黏贴过去是件很麻烦的事情，首先你要把图片下载到本地（引用网页图片地址不太好，图片可能会神秘消失），然后在文档中使用相对路径引用这个图片，当图片很多的时候，这是个非常痛苦的过程。

能不能做到复制网页图片后，在VSCode中黏贴后自动插入一个S3的链接到Markdown文档中去呢？我找到一款插件，可以做到一键上传七牛/GitHub/sm.ms等，但是它没有提供S3的支持，所以我fork后加了这个功能，如果你也需要这个功能的话，可以在这里下载安装: [markdown image paste](https://github.com/bmpi-dev/vscode-extension-mardown-image-paste)

有了这个插件后，写wiki/md文件遇到图片复制后黏贴进去自动插入S3链接，这样图片永远存放到你的S3账号中去，还自带全球CDN加速。

## Netlify发布网站

公共wiki是重新整理后的知识资料集合，其中非文本的资源如图片、PDF、Office格式文件、Keynote等存放至Amazon S3/Aliyun OSS等云服务，网页等内容的快照可使用Wayback Machine备份，然后将这些链接存放至wiki系统。

wiki资料通过GitHub公共仓库托管，通过netlify生成静态网站。

我的[wiki](https://wiki.bmpi.dev/)网站就是通过netlify自动发布，每次更新wiki后，push到GitHub，netlify自动发布，这个过程只需要不到十几秒。

## 私有Note

私人备忘和工作涉及的私有非公开的资料集合，其中非文本的资源如图片、PDF、Office格式文件、Keynote等存放至Google Drive/Microsoft OneDrive。然后将这些链接存放至私有Markdown文件中，通过GitHub私有库托管。

## 重要资料

密钥等信息通过`1Password`托管，重要的资料制作成md文件后通过Google Drive/Microsoft OneDrive等托管，经常需要的重要的资料可通过手机备忘录加密存放。

{{< ad_embed_post >}}

#### *References*
[^0]: <https://www.slant.co/versus/5116/8769/~tiddlywiki_vs_org-mode>
[^1]: <https://github.com/bmpi-dev/wiki.bmpi.dev>
[^2]: <https://web.archive.org/web/20191230143823/https://gigaom.com/2012/09/19/the-disappearing-web-information-decay-is-eating-away-our-history/>
[^3]: <https://aws.amazon.com/cn/s3/>
[^4]: <https://en.wikipedia.org/wiki/Wayback_Machine>
[^5]: <https://wiki.bmpi.dev/#wayback%20machine>
