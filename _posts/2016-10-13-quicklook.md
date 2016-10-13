---
layout: post
title:  "提升「一指禅」功力 -- Quicklook plugins"
categories: [mac]
modified: 2016-10-13
tags:
- quicklook
- mac
comments: true
---

![quicklook](/upload/2016/10/quicklook.png)

## 介绍

Quicklook 俗称「一指禅」，在 Mac 中可以使用 `空格键` 在不打开文件或者文件夹的情况下对其进行快速的预览。

## Install

### brew cask 安装

使用 [HomebrewCask](https://github.com/caskroom/homebrew-cask) 进行安装，命令 `brew cask install xxx`。

### 手动安装

安装非常简单，直接把 `.qlgenerator` 文件复制到下面两个文件夹中的一个：复制到 `/Library/QuickLook` 所有用户都能使用，复制到 `~/Library/QuickLook` 只能当前用户能使用。

复制后使用 `qlmanage -r` 命令刷新即可使用。

<!--more-->

## Plugins

### BetterZipQL

预览各种压缩格式的文件，具体格式如下，安装 `brew cask install betterzipql` 或者[手动下载](https://macitbetter.com/BetterZip-Quick-Look-Generator/)

> The currently supported archive formats are: ZIP, RAR, 7-Zip, TAR, TGZ, TBZ, TXZ, GZip, BZip2, ARJ, LZH, ISO, CHM, CAB, CPIO, DEB, RPM, StuffIt's SIT, BinHex, and MacBinary. And now also Apple Disk Images (DMG) and winmail.dat!

![ql-betterzip](/upload/2016/10/ql-betterzip.png)

### Markdown

预览 Markdown 文件，安装 `brew cask install qlmarkdown` 或者[手动下载](http://inkmarkapp.com/markdown-quick-look-plugin-mac-os-x/)

![ql-markdown](/upload/2016/10/ql-md.png)

### qlImageSize

在标题栏显示图片文件的尺寸和大小，另外也能让 Finder 的预览和缩略图支持之前不支持的格式 [bpg](http://bellard.org/bpg/) 和 [WebP](https://developers.google.com/speed/webp/)，安装 `brew cask install qlimagesize` 或者[手动下载](https://github.com/Nyx0uf/qlImageSize)

![ql-imagesize](/upload/2016/10/ql-image.png)

### Webp

直接查看 Webp 文件，安装 `brew cask install webpquicklook` 或者[手动下载](https://github.com/dchest/webp-quicklook)

![ql-webp](/upload/2016/10/ql-webp.png)

### QLVideo

支持预览更多编码格式的视频，安装 `brew cask install qlvideo` 或者[手动下载](https://github.com/Marginal/QLVideo)

> This package adds support for wide range of other codecs and "non-native" media file types, including .asf, .avi, .flv, .mkv, .rm, .webm, .wmf etc.

![ql-video](/upload/2016/10/ql-video.jpeg)

(电脑上实在是没有视频，直接从作者网站上抓的)

### QLStephen

预览纯文本文件，即使文件名中包含未知的扩展名，安装 `brew cask install qlstephen` 或者[手动下载](https://github.com/whomwah/qlstephen/)

![ql-stephen](/upload/2016/10/ql-stephen.png)

### BT

预览 BT 文件，文件从 [Transmission](https://transmissionbt.com/) 中提取出来的，[[手动下载 1]](https://pan.baidu.com/s/1jIEwUaE) [[手动下载 2]](https://mega.nz/#!zdoC3agB!AwD1S7sIP2RnLUKjO7raPZ45hgSMe_GfNIKSrEniOo8)。如果涉及版权等将移除。

![ql-bt](/upload/2016/10/ql-bt.png)

### QLColorCode

使用 [Highlight 库](http://www.andre-simon.de/) 对代码进行高亮显示，安装 `brew cask install qlcolorcode` 或者[手动下载](https://github.com/anthonygelibert/QLColorCode)。

该 generator 还提供了丰富的[设置项](https://github.com/anthonygelibert/QLColorCode#settings)。同时依赖外部工具还能进行代码[反编译](https://github.com/anthonygelibert/QLColorCode#settings)，良心产品，程序员居家必备工具。

![ql-colorcode](/upload/2016/10/ql-colorcode.png)

### JSON

高亮显示 json 文件，同时提供折叠/展开节点的功能，安装 `brew cask install quicklook-json` 或者[手动下载](http://www.sagtau.com/quicklookjson.html)

![ql-json](/upload/2016/10/ql-json.png)


