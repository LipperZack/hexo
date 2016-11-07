title: Angular Input Bug
date: 2016-09-27 11:24:00
---
最近升级了chrome53，然后同事发现在53下，输入中文的时候感知不到，触发不了ng change

<!-- more -->

然而firefox是好的，windows和ma表现一致


# Quick Start
Chrome 53 emits input -> input -> compositionend, while Chrome 52 does input -> compositionend -> input 

![code](http://7xlaf5.com1.z0.glb.clouddn.com/angularInputBug-code.png)

# Refer
[Duplicate string input when using Japanese input method editor on the latest Chrome version 53](https://github.com/ajaxorg/ace/issues/3045)
[jsrun.it](http://jsrun.it/hoge1e4/q1EH)

[](http://frontenddev.org/article/compatible-with-processing-and-chinese-input-method-to-optimize-the-input-events.html)



[](http://frontenddev.org/article/site-architecture-from-scratch.html)