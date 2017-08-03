---
layout: post
title:  RaspberryPI 之伪 HIFI 篇
categories: [soft, hardware]
comments: true
modified: 2017-08-03
image:
    feature: http://sbugzu.github.io/upload/2017/08/hifi-banner.jpg
    creditlink: https://pxhere.com/en/photo/745724
tags:
- raspberry pi
- 树莓派
- 06MX
- HIFI
- 声卡
- DIY
---


## 背景
前段时间 RaspberryPI 系统突然断电，系统损坏无法启动，闲置了一段时间，最近重新启用准备用来当播放器使用。

插上耳机那一刻，网上说底噪感人都是骗人的，尼玛完全就全是噪音。突然想起有只闲置的 06MX，所以有了下面的折腾。

![raspberrypi with 06MX](/upload/2017/08/raspberrypi-with-06mx.jpg)

树莓派 RaspberryPI 3，已安装 Raspbian Jessie Lite

乐之邦（MUSLAND） 06 MX
<!--more-->

## 步骤
### 设置声卡

先把 06MX 装好电池再插在 PI 的 USB 口（切记一定要装电池，后面会说原因）。

使用 `aplay -l` 查看下设备是否正常识别，正常识别会有类似以下的信息：

~~~ shell
**** List of PLAYBACK Hardware Devices ****
card 0: ALSA [bcm2835 ALSA], device 0: bcm2835 ALSA [bcm2835 ALSA]
  Subdevices: 8/8
  Subdevice #0: subdevice #0
  Subdevice #1: subdevice #1
  Subdevice #2: subdevice #2
  Subdevice #3: subdevice #3
  Subdevice #4: subdevice #4
  Subdevice #5: subdevice #5
  Subdevice #6: subdevice #6
  Subdevice #7: subdevice #7
card 0: ALSA [bcm2835 ALSA], device 1: bcm2835 ALSA [bcm2835 IEC958/HDMI]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: MX [Monitor 06 MX], device 0: USB Audio [USB Audio]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
~~~

接下来，再测试下是否能正常出声

~~~ shell
 speaker-test -Dplughw:CARD=MX -c2 -twav
~~~

如果正常应该能听到左右声道交替出现`Front Right` 和 `Front Left`。

为了正常使用，设置默认声卡为 06MX，使用 vim 或者 nano 打开 `/lib/modprobe.d/aliases.conf`，并用 `#` 注释掉下面这句：

~~~ shell
#options snd-usb-audio index=-2
~~~

重启 PI，再次使用 `aplay -l` 命令，显示应该会变成下面这样：

~~~ shell

**** List of PLAYBACK Hardware Devices ****
card 0: MX [Monitor 06 MX], device 0: USB Audio [USB Audio]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
card 1: ALSA [bcm2835 ALSA], device 0: bcm2835 ALSA [bcm2835 ALSA]
  Subdevices: 8/8
  Subdevice #0: subdevice #0
  Subdevice #1: subdevice #1
  Subdevice #2: subdevice #2
  Subdevice #3: subdevice #3
  Subdevice #4: subdevice #4
  Subdevice #5: subdevice #5
  Subdevice #6: subdevice #6
  Subdevice #7: subdevice #7
card 1: ALSA [bcm2835 ALSA], device 1: bcm2835 ALSA [bcm2835 IEC958/HDMI]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
~~~

可使用 `alsamixer` 命令调整系统音量。

### 安装播放器

![musicbox-screenshot](/upload/2017/08/musicbox-screenshot.png)

选择播放器，因为 PI 安装的是 Lite 版系统没有 UI，所以选了 [NetEase-MusicBox](https://github.com/darknessomi/musicbox) 作为 CLI 下的播放器。

~~~ shell
# 安装依赖
sudo apt-get install mpg123 libxml2-dev libxslt-dev python3-dev python3-lxml python3-pip
# 安装播放器
pip3 install NetEase-MusicBox
# 打开播放器
musicbox
~~~

具体操作快捷键可查看[快捷键](https://github.com/darknessomi/musicbox#键盘快捷键)

## 问题

* 由于 PI 的 USB 接口电压输出不够，如果 06MX 不加电池会无法使用。
* 第一次使用 `speaker-test` 或者播放器可能会出现 USB 声卡不出声，一般情况下重新执行就会有声音了。
* 06MX 没有独立供电，信号和电源在同一个 USB 口上不够 HIFI。

## TODO

* 对 06MX 的 USB 口进行改造，分离信号和电源，使用线性电源给 PI 和 06MX 进行供电。
* 显示屏增加歌词显示功能，感觉可以开个 musicbox 的 Raspberry 分支了。

## 后记
发现网上还有一些专为 PI 编译的多媒体系统，有机会体验下。

* Max2Play ([官网](https://www.max2play.com/en/))
* LibreELEC ([官网](https://libreelec.tv/))
* OSMC ([官网](https://osmc.tv/))
