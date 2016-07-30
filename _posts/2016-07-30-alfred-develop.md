---
layout: post
title:  Alfred 高效扩展之开发篇
categories:
- Mac
- soft
tags:
- alfred
- workflow
- Mac
- 高效
comments: true
modified: 2016-07-30
---


![alfred banner](/upload/2016/07/alfred-banner.jpg)

Alfred 这款 Mac 下的最强的效率神器（没有之一），它的功能就不过多在这里阐述了，各大报刊杂志均有介绍（如 [少数派](http://sspai.com/tag/alfred)），本篇列举一些能在开发过程中提高效率的扩展。

<!--more-->

## Colors

支持各种颜色的转换和打开系统取色器，可使用以下 keyword 触发： `c, hsl, rgb, #, [ns, [ui`，在前端 css 开发过程中处理颜色比较方便。

![screenshot of colors](/upload/2016/07/alfred-color.gif)

[Download](https://github.com/packal/repository/raw/master/tylereich.colors/colors_v2.0.1.alfredworkflow)

## Dash

[Dash](https://kapeli.com/dash) 码农必备神器（同样没有之一），提供 150+ 的 API 文档离线访问，遇到不清楚的 API 时，轻轻一搜，妈妈再也不用担心代码质量了。

![screenshot of dash](/upload/2016/07/alfred-dash.gif)

安装：该 workflow 已经集成在 Dash 的应用中，打开 Dash，` ⌘ + , ` 打开属性面板，在 Integration 中点击 Alfred 即可进行安装。

![screenshot: install dash alfred](/upload/2016/07/alfred-dash-config.png)

使用时每个 API 都会有一个对应的前缀，使用 `prefix + 空格 + 查询 API` 即可搜索出相应的 API，回车即跳转到 Dash 对应的 API 中。

## Encode / Decode

功能和名字一样简单直白，对输入的字符进行 encode 和 decode

![screenshot of encode](/upload/2016/07/alfred-encode.png)
![screenshot of decode](/upload/2016/07/alfred-decode.png)

[Homepage](https://github.com/willfarrell/alfred-encode-decode-workflow) \| [Download](https://raw.github.com/willfarrell/alfred-encode-decode-workflow/master/encode-decode.alfredworkflow)

## Github

通过扩展可以很方便的查看和管理自己的 [github](https://github.com)，也可以快速搜索 github 中的其它项目，同时还支持 github 企业功能（没有相应帐号未测试）。在官网上提供了详细的[命令清单](https://github.com/gharlan/alfred-github-workflow#commands)以及介绍。
What? 你还没有 github 帐号，怎么能在贵圈生存。

![screenshot of github](/upload/2016/07/alfred-github.png)

[Homepage](https://github.com/gharlan/alfred-github-workflow) \| [Download](https://github.com/gharlan/alfred-github-workflow/releases)

## Hash

对字符串文件进行 hash 运算，支持字符串的以下 hash 类型：` md5, sha1, sha256, sha512, htpasswd, crc32, whirlpool, base64_decode, base64_encode`；同时支持争取文件的 hash 类型：` md5, sha1, sha256, sha512, base64 `，只需要在对应的类型后面加 `f`，如 `md5f, sha1f`。

直接进行字符 hash

![screenshot: string hash](/upload/2016/07/alfred-hash.png)

对文件进行 hash，先选中文件再输入相应的 hash 规则名字，如 `md5f` 。另一种方法在 Alfred 中找到文件后，点击方向键 `➡`，再下方选择 `Calculate MD5`

![screenshot: string hash](/upload/2016/07/alfred-hash.gif)

[Homepage](https://github.com/BigLuck/alfred2-hash) \| [Download](https://github.com/BigLuck/alfred2-hash/raw/master/Hash.alfredworkflow)

## Lookup IP

快速查看本机公网 IP，同时也可查询指定 IP 所属地址信息，该 workflow 使用的淘宝 IP 库：[http://ip.taobao.com/](http://ip.taobao.com/)。查询时使用`lip` 或者 `lip + IP地址 `

![screenshot: lip local](/upload/2016/07/alfred-lip-local.png)
![screenshot: lip](/upload/2016/07/alfred-lip.png)

[Homepage](https://github.com/dangoakachan/lookup-ip/) \| [Download](https://github.com/dangoakachan/lookup-ip/raw/master/lookupip.alfredworkflow)

## MacVim

通过 `vi, vim, mvim` 的 keywords 触发 Macvim 打开相应的文件或文件夹。

![screenshot: Macvim](/upload/2016/07/alfred-macvim.png)

[Download](/upload/2016/07/alfred-macvim.alfredworkflow)

## Terminal Finder

在 Finder/Path Finder 中打开 iTerm/终端中的当前文件夹，或者反过来在 iTerm/终端中打开 Finder/Path Finder 中的地址。

**已知 Bug**：在最新版中的 iTerm2 ，该 workflow 部分功能失效已经提了 [issue](https://github.com/LeEnno/alfred-terminalfinder/issues/21) 通知作者。
{: .notice}

使用首字母代表各个应用 `i -> iTerm`, `t -> Terminal`, `f -> finder`, `p -> Path Finder`，交替前后顺序打开不同程序，如 `if, ip, tf, tp, fi, ft, pi, pt`

![screenshot: TerminalFinder](/upload/2016/07/alfred-terminalfinder.png)
![screenshot: TerminalFinder](/upload/2016/07/alfred-terminalfinder-pi.png)

[Homepage](https://github.com/LeEnno/alfred-terminalfinder) \| [Download](https://github.com/LeEnno/alfred-terminalfinder/raw/master/TerminalFinder.alfredworkflow)

