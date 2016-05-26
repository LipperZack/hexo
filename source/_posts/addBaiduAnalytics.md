title: hexo add baidu analytics
tags: ["hexo","analytics"]
date: 2015-03-02 4:23:00
---
由于pacman中[google analytics](http://www.google.cn/intl/zh-CN_ALL/analytics/learn/index.html)比较慢，而且容易被Q，你懂得，so，添加百度统计backup。

<!-- more -->

1.编辑文件 themes/pacman/_config.yml ,添加一行配置
``` bash
baidu_analytics: true
```
2.新建 themes/pacman/layout/_partial/baidu_analytics.ejs 内容如下
``` bash
<% if (theme.baidu_analytics) { %>
<script type="text/javascript">
#申请的百度统计代码
</script>
<% } %>
```
3.编辑themes/pacman/layout/_partial/head.ejs 在 </head> 前添加
```
<%- partial("baidu_analytics") %>
```
4.重新部署


