title: Debug Webview In Wechat
tags: ["debug","微信","wechat","tools"]
date: 2015-08-23 3:24:00
---
之前的[微信、手Q、Qzone之x5内核inspect调试解决方案](http://bbs.mb.qq.com/thread-243399-1-1.html?fid=93&gid=45)调试比较麻烦，现在新版本已经完善了X5中的debug解决方案。
You dont need alert any more. 

<!-- more -->

# Reqiure
1、一台微信版本不低于6.2.4的安卓机，并开启调试模式
2、安装[QQ浏览器9最新版](http://browser.qq.com/mac/index.html)(必须是windows版，mac木有插件)
3、安装微信调试插件，地址栏直接输入qqbrowser://extensions#id=kghjlmdefodljabnacklekelfimgalmi 
4.1、点击插件的“网页调试”，安装TBS环境
![](http://7xlaf5.com1.z0.glb.clouddn.com/debugWX-tbsstep1.png)
4.2、点击"一键安装TBS"按钮
![](http://7xlaf5.com1.z0.glb.clouddn.com/debugWX-tbsstep2.png)
4.3、打开微信,扫描二维码,微信上会弹出对应页面
![](http://7xlaf5.com1.z0.glb.clouddn.com/debugWX-tbssaoma.png)
4.4、依次点击"清除TBS内核"->"安装本地TBS内核"
![](http://7xlaf5.com1.z0.glb.clouddn.com/debugWX-cleartbs.png)
![](http://7xlaf5.com1.z0.glb.clouddn.com/debugWX-localtbs.png)
4.5、等待不超过20s,会弹出确认框提示安装成功
![](http://7xlaf5.com1.z0.glb.clouddn.com/debugWX-installsuccess.png)
4.6、若等待超过30s无反应,请重新尝试"清除TBS内核"->"安装本地TBS内核"

# Debug Steps
1、微信打开网页
2、点击插件"开始调试"
![](http://7xlaf5.com1.z0.glb.clouddn.com/debugWX-startdebug.png)
3、之后就是熟悉的[chrome的devtools](https://developer.chrome.com/devtools/docs/contributing)，[webinspect](https://github.com/GoogleChrome/devtools-docs)

# Other Usage
基于微信X5的，都可以调试了，还有公众号、手机QQ webview调试、手机QQ空间 webview、以及手机QQ浏览器网页调试

#Refer: 
[微信、手Q、Qzone之x5内核inspect调试解决方案](http://bbs.mb.qq.com/thread-243399-1-1.html?fid=93&gid=45)
[开启网页调试教程](http://blog.qqbrowser.cc/kai-qi-wang-ye-diao-shi-jiao-cheng/)

