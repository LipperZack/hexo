title: debug in angular (could use when hack)
tags: ["javascript","debug","angular","hack","trick"]
date: 2016-01-02 16:33:00
---
开发angular也有一段时间了，使用上来说，大大提高了开发效率，搞个小网站就是分分钟的事。但开发没什么，主要头疼的问题是调试，当然可以在源码断点。但我要的是一个更优雅方便的方法，即网页任何元素，都能方便查看它的scope、controller等等

<!-- more -->

排查生产问题杠杠的，其实也能作为一种hack的手段。

# 1.查看元素scope
chrome选定一个元素（$0就是chrome选定当前的元素）
```
$($0).scope()
//或者
angular.element($0).scope()
```
如果是isolate scope
```
$($0).isolateScope()
```

# 2.找到元素并改变
拿到scope后可以点`$parent`和`$root`找到你元素真正的scope
```
$($0).scope().$digest()
```

# 3.查看绑定的services/provider/controller
```
$($0).injector().get('MyService')
$($0).injector().get('My') //Provider
$($0).controller()
```


# 另外的工具Batarang（不推荐）
之前最简单暴力的想法，在chrome的store搜索angular，也就这么一个plugin，果断装之，然而并没有什么想象中的那么便利
首先是卡，在页面元素绑定多的时候，而且在scope的视图里的scope树，并不知道怎么去用它。。。
比较方便的是有个inspector，可以让你select，然后看里面的值。但我始终感觉没有console拿到的方便，比如一个函数，我并没有办法定位到源码。
另外的Service Dependencies貌似也没什么卵用

# use as hack
其实这样的话，完全能定位到一个组件的directive，界面的UI基本一览无遗

# refer
[Tips & Tricks for debugging unfamiliar AngularJS code](http://eng.localytics.com/tips-and-tricks-for-debugging-unfamiliar-angularjs-code/)
[Debugging AngularJS Apps from the Console](http://blog.ionic.io/angularjs-console/)
[How can I test an AngularJS service from the console?](http://stackoverflow.com/questions/15527832/how-can-i-test-an-angularjs-service-from-the-console)
