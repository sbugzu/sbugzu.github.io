---
layout: post
title:  "Wiktionary and Google Translate - Firefox addons Theme"
#excerpt: "Theme for Wiktionary and Google Translate Plugin."
categories: [soft]
modified: 2016-07-28
tags:
- firefox
- theme
- "Wiktionary and Google Translate"
comments: true
---


Firefox 在 Mac 下无法使用 `Command + Control + D` 调出系统自带字典，所以单独安装了 [Wiktionary and Google Translate](https://addons.mozilla.org/en-US/firefox/addon/google-dictionary-and-google-t) 扩展，但是原始界面无法直视

![wtg-default](/upload/2016/07/wgt-default.png)

自己动手修改，完工后效果如下（还包含一个 CSS 实现的动态加载的动画）：

<!--more-->

![wtg-custom](/upload/2016/07/wgt-custom.jpg)

##修改步骤

进入扩展设置 > Style，清空原有内容，把以下内容复制到文本框中确定，完工。

~~~ css
.gDicClassPopupBox {
  -moz-appearance: -moz-win-glass !important;
  border-style: none !important;
  background-color: rgba(200, 200, 200, 0.25) !important;
}
.gDicClassPopup {
  color: #fff !important;
  border: none !important;
  background: -moz-linear-gradient(-45deg, rgba(122, 122, 122, 0.75) 0%, rgba(0, 0, 0, 0.75) 100%) !important;
  border-radius: 2px !important;
  margin: 2px !important;
  text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.35) !important;
}
.gDicClassPopupTrans {
  color: #fff !important;
  text-decoration: none !important;
}

/* common icon */
.gDicClassPopupTrans + span > img {
  display: inline-block !important;
  -moz-box-sizing: border-box !important;
  background-size: 100% auto !important;
  width: 16px !important;
  height: 16px !important;
  padding-left: 16px !important;
  cursor: pointer !important;
}

/* option icon */
.gDicClassPopupTrans + span > img:first-child {
  background-image: url("https://cdn1.iconfinder.com/data/icons/32-soft-media-icons--Vol-1/32/config.png") !important;
}

/* copy icon */
.gDicClassPopupTrans + span > img:nth-child(2) {
  background-image: url("https://cdn1.iconfinder.com/data/icons/32-soft-media-icons--Vol-1/32/notepad.png") !important;
}

/* search icon */
.gDicClassPopupTrans + span > img:nth-child(3) {
  background-image: url("https://cdn1.iconfinder.com/data/icons/32-soft-media-icons--Vol-1/32/zoom.png") !important;
}

/* heart icon */
.gDicClassPopupTrans + span > img:nth-child(4) {
  display: none !important;
  width: 0 !important;
  height: 0 !important;
  padding-left: 0 !important;
}

/* close icon */
.gDicClassPopupTrans + span > img:nth-child(5) {
  background-image: url("https://cdn1.iconfinder.com/data/icons/32-soft-media-icons--Vol-1/32/ok.png") !important;
}

/* image style */
.gDicClassPopupImg {
  margin: 4px 3px 0 0;
  /*border-radius: 2px !important;*/
  box-shadow: 0 0 0 1px #000, 0 0 0 4px #fff;
}

/* more link */
.gDicClassPopupMore {
  color: #ddd !important;
}

/* hide site link 
.gDicClassPopup > tr:last-child {
  display: none !important;
} */

/* loading style */
.gDicClassPopupHint img {
  display: none !important;
}
.gDicClassPopupHint {
  border: 5px solid #fff;
  border-radius: 30px;
  height: 30px;
  left: 50%;
  margin: 15px 0 0 15px;
  opacity: 0;
  position: absolute;
  top: 50%;
  width: 30px;
  animation: pulsate 1s ease-out;
  animation-iteration-count: infinite;
}
@keyframes pulsate {
  0% {
    transform: scale(.1);
    opacity: 0.0;
  }
  50% {
    opacity: 1;
  }
  100% {
    transform: scale(1.2);
    opacity: 0;
  }
}
~~~

## 已知问题

* 最外层的 `gDicClassPopupBox` 总是要长一些
* 由于 CSS 代码比较复杂，偶尔 Firefox 渲染会出问题

## 特别鸣谢

图标资源使用 [Soft media icons vol 1
](https://www.iconfinder.com/iconsets/32-soft-media-icons--Vol-1) 

## 参考资料

[Wiktionary and Google Translate](https://addons.mozilla.org/en-US/firefox/addon/google-dictionary-and-google-t) - Firefox 扩展安装页
http://www.toptip.ca/2010/10/firefox-extension-google-dictionary-and.html - 扩展官网
[样式定义](http://www.toptip.ca/2011/01/how-to-change-font-and-color-of-google.html) - 基础样式 classname 的定义但是不全，可以直接查看扩展的源码
