---
layout: post
title:  115 + Clouddrive + Plex/Emby 搭建视频服务器
categories: [software, nas]
comments: true
modified: 2021-09-17
image:
    feature: https://images.unsplash.com/photo-1505775561242-727b7fba20f0?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=2900&q=80
    credit: Timothy Eberly
    creditlink: https://unsplash.com/@timothyeberly
tags:
- QNAP
- 威联通
- 群晖
- Plex
- Emby
- Clouddrive
- 电影
- selfhost
- NAS
- 115
---


2020 年左右玩过一段时间，rclone + emby + Google Drive 搭建的多媒体服务器，后因 Google Drive 政策调整等原因慢慢放弃了。入手 QNAP 威联通后换成 PT + Kodi 的本地模式，稳定性各方面都不错，但有时候临时要看个电影还需要先下载不是太方便，最近刚好发现 CloudDrive 可以挂载 115 和阿里云盘等，测试了下效果还不错所以有了这篇文章。

## 介绍

本文基于威联通 NAS，使用 Docker 运行 CloudDrive 挂载 115 网盘，使用 Plex 搜刮并作为服务器对外提供服务。

同样适用于群晖、macOS、Ubuntu、Windows、OpenWRT 等支持 Docker 的系统，Windows 也可直接使用非 Docker 的独立 exe 版本。Plex 也可使用 Emby、Jellyfin 等代替（使用 Plex 是因为有购买终身版），如果不考虑外网也可直接使用 Kodi、Infuse 等本地播放器。

<!--more-->

**TODO:**
- [ ] 增加其它非 NAS 环境的使用方法


### 硬件

威联通 TS-453Dmini，搭载 Intel J4125 四核心处理器/8G 内存/双埠 2.5GbE 网卡/4 盘位相当不错的 NAS。[「点击京东购买，有返利」](https://u.jd.com/rLqtRcU)

[![QNAP 453Dmini](/upload/2021/qnap-453dmini.png)](https://u.jd.com/rLqtRcU)

### CloudDrive
**🔴IMPORTANT❗🔴 该软件非开源软件，无法确定其安全性，建议使用单独帐号**

**🔴IMPORTANT❗🔴 该软件非开源软件，无法确定其安全性，建议使用单独帐号**

**🔴IMPORTANT❗🔴 该软件非开源软件，无法确定其安全性，建议使用单独帐号**

该软件无官网和作者详细信息，通过 Telegram 频道进行代码分发。

Docker Hub: [https://hub.docker.com/r/cloudnas/clouddrive](https://hub.docker.com/r/cloudnas/clouddrive)

Telegram Channel: [https://t.me/cloud_nas](https://t.me/cloud_nas)

Telegram 讨论组：[https://t.me/cloudnaschat](https://t.me/cloudnaschat)

Windows 版本搬运 v1.1.41 下载地址「[32 位](https://www.aliyundrive.com/s/VWPXK2t9qCw) ｜ [64 位](https://www.aliyundrive.com/s/bt3vQ1S3KLj)」，因为作者更新比较频繁，建议订阅上面的 Telegram 频道。

### Plex/Emby/Jellyfin (可选)

如果不需要海报墙以及远程播放等功能，可忽略该部分内容。

![Plex Screenshot](/upload/2021/plex-screenshot.png)

Plex 官网（免费版有限制）：[https://plex.tv](https://plex.tv)

官网终身版 119.99 刀，偶尔有活动 89.99 刀。选择 Plex 因为客户端非常非常丰富，能想到设备都有，界面也非常漂亮，搜刮效果也不错，定制性上稍弱。

其它替换软件：

Emby 官网（免费版有限制）：[https://emby.media](https://emby.media)

Jellyfin 官网（免费）： [https://jellyfin.org](https://jellyfin.org)

Kodi 官网（免费）：[https://kodi.tv](https://kodi.tv)

其中 Kodi 更多是本地播放方案，不支持远程流媒体，几个软件对比可以参考下面文章：

[Plex vs Emby vs Jellyfin vs Kodi: In-depth Comparison](https://www.smarthomebeginner.com/plex-vs-emby-kodi-jellyfin-2020/)

[ Protektor-Desura/compare-media-servers ](https://github.com/Protektor-Desura/compare-media-servers)

[选择emby，plex还是jellyfin？](https://www.bilibili.com/read/cv7345029)

## 安装
### 安装 Docker 环境
#### QNAP
QNAP 中已带 Docker 运行环境，如未安装在 `AppCenter -> QNAP Store -> QTS Essentials -> Container Station` 直接点击安装。若已安装直接跳到下一步。

![Install Container Station](/upload/2021/install-container-station.png)

#### 其它系统
**TBD**

### 安装 CloudDrive
#### QNAP
首先创建挂载点，在第一个磁盘下创建共享文件夹 `CloudDrive`（只是挂载点不会实际占用磁盘空间）

![Create Sharefolder](/upload/2021/sharefolder.png)

启动 ContainerStation，点击左侧 `Create -> Create Application`

![Create docker application](/upload/2021/docker-compose.png)

在 Application name 中输入 `clouddrive`，YAML 中输入以下内容：

```yaml

version: '3'

services:
  cloudnas:
    image: cloudnas/clouddrive
    container_name: clouddrive
    volumes:
      - /share/CACHEDEV1_DATA/CloudDrive:/CloudNAS:shared
      - /share/Container/clouddrive/config:/Config
    environment:
      - FuseUID=1000
      - FuseGID=100
    devices:
      - /dev/fuse:/dev/fuse
    restart: unless-stopped
    privileged: true
    ports:
       - 9798:9798
    restart: unless-stopped
```

点击创建，等待几分钟时间容器启动完成。

#### 其它系统
**TBD**

### CloudDrive 配置
容器启动完成后，使用以下地址访问 CloudDrive `http://${nas_ip}:9798`，需要通过邮箱进行简单的注册，完成后即可进入到界面，增加需要的网盘。

![CloudDrive add pan](/upload/2021/clouddrive-pan.png)

目前支持以下几种网盘：
* 115「支持 Cookie 和扫码登录」 [https://115.com](https://115.com)
* 沃家云盘「支持帐号密码登录」 [https://wocloud.com.cn](https://wocloud.com.cn)
* 天翼云盘「支持帐号密码和扫码登录」 [https://cloud.189.cn](https://cloud.189.cn)
* 阿里云盘「支持扫码登录」 [https://aliyundrive.com](https://aliyundrive.com)
* WebDAV「支持帐号密码登录」
* LocalFolder

帐号创建完成后，就可以在以下挂载路径上 `/share/CACHEDEV1_DATA/CloudDrive/CloudDrive` 看到挂载的网盘和对应文件。

挂载完成后可直接使用本地播放器，或者通过 NAS 共享出去后使用播放工具进行播放，关于共享协议的选择可参考文章最后的协议部分。

### Plex 配置（可选）
QNAP 中安装 Plex 同上 ContainerStation 的安装方式，安装完成后使用 `http://{nas_ip}:32400` 进行访问并注册登录。

点击右上角 `Settings -> MANAGE/Libraries -> Add Library`，选择 library type 为 Movies，修改 Name 为显示名称，Language 为中文。Add folders中，增加文件路径 `/share/CACHEDEV1_DATA/CloudDrive/CloudDrive/115`。

如果有电视剧集资源，因为电影和电视剧需使用不同的搜刮器，所以在网盘中分别放在两个不同目录中（如：Movies, TVShows），在 libraries 中电视剧集选择 TV Shows 类型。

![Plex library configuration](/upload/2021/plex-library.png)

保存后会花一段时间进行搜刮，完成后手机上如下效果：

![Plex mobile screenshot](/upload/2021/plex-mobile.jpeg)

如果希望在家以外也能访问，可以使用端口映射和 DDNS 的方式，暂不展开。

## 杂项

### 网盘
目前使用的是 115 网盘（付费会员，非会员限速严重不可用），前段时间刚好搞 11.5 年半的活动入手，使用磁力链很多电影都是秒下。

**已知问题：** 受 115 下载的限制，播放时目前最高只能达到 6~8MB 左右的速度，所以下载电影的码率不要超过这个值，否则会出现卡顿，从经验来看一般单个电影在 25G 以内问题不大（当然和电影的时长也有关）。

挂载其它网盘理论上也是可以的，但是具体限速未进行测试。

### 关于协议
当 QNAP 使用 nfs 协议分享时，挂载目录为空无法访问，使用 SMB 协议后能正常访问，但使用 Kodi 直接播放时，会出现播放过程中自动跳出的情况，查询资料后应该是网速不稳定，同时针对 SMB 协议也不会进行缓存。解决方案 Kodi 19 之前版本可以使用增大缓存的方式调整（参考：[增加 Kodi 缓存](https://zhuanlan.zhihu.com/p/44945041)），但 Kodi 19 中该修改不生效，最后使用 FTP 协议进行分享后解决，播放时 Kodi 也能自动进行缓存。

