title: 深入浅出javascript原型和闭包
tags: ["javascript","prototype","closure","原型","闭包"]
date: 2015-03-30 1:24:00
---
javascript原型和闭包，一直是javascript中比较难理解的两个部分，却又非常重要、非常基础，也是与其他主流面向对象语言的最大区别。这部分网上教程遍地都是，水平也是层出不穷，但是真正能说对、而且说的透彻的非常少，为了不被复制粘贴的水军搞晕，所以还是按自己的思路整理了一套。

<!-- more -->

目的是为了用`最简单`的语言描述清楚这两个重要且基础的概念。如果你是个其他语言的开发，看了这个教程能明白，那我的目的就达到了。


##1.简单概述
其实，“原型和闭包”，只是一种简单的称呼，真正要理解的，不是“原型和闭包”，而是“原型链”和“作用域链”。原型和闭包[没什么关系](chrome://not-a-link "是因为他们说的不是一件事情")，但是又有那么一点点的[类似](chrome://not-a-link "是因为他们都是取值问题，在哪里取的问题。还有为了解释他们，引入的两个概念都有“链”一说，类似树形结构查找父节点")。有很多人也在这个问题上[混淆](http://stackoverflow.com/questions/27434357/scope-chain-look-up-vs-prototype-look-up-which-is-when)。

简单来讲，
`闭包`（`作用域链`）说的是`变量`在某个场景下的取值问题。
`原型`（`原型链`）说的是`变量的属性`在某个场景下的取值问题。

当然这里我只是简单的用`变量`这个词，为的是让大家把关注点放在这两个关键概念的[四个关键词](chrome://not-a-link "闭包->作用域链 & 原型->原型链")和他们的区别上。但是其实在js中，一切都是[对象](chrome://not-a-link "这里还有Object和Function的关系，稍后讨论")。

##2.闭包
1、说到闭包一定要提到[上下文](chrome://not-a-link "执行上下文环境(execution context)，简称上下文，在执行的时候才确定。")和[作用域](chrome://not-a-link "作用域(scope)，函数创建时就确定了。")。这两个概念也十分类似，经常容易[混淆](chrome://not-a-link "作用域是静态的，上下文是动态的。")。在我们开始执行一个函数之前，[上下文](chrome://not-a-link "执行上下文环境(execution context)，简称上下文，在执行的时候才确定。")帮我们做了很多[铺垫](chrome://not-a-link "比如变量(函数表达式)的声明为undefined、赋值this、函数声明的赋值等等")。而[作用域](chrome://not-a-link "还包括作用域链")却是一个静态的概念，在函数创建的时候就已经确定好了。
2、同一个作用域，每次都会创建不同的上下文。它们的关系类似淘宝上同一套衣服(scope)，模特的图片和买家秀(不同的execution context)可能差别很大也可能差不多。
3、大家一般说的闭包，都是纠结[自由变量](chrome://not-a-link "在A作用域中使用的变量x，却没有在A作用域中声明（即在其他作用域中声明的），对于A作用域来说，x就是一个自由变量")的取值。那么其实很简单，一句话，即，要到`创建`这个函数的那个[作用域链](chrome://not-a-link "函数嵌套则产生作用域链，最里面的作用域如果找不到，可以到父一层的作用域取，其实在执行的时候这里应该是被保留的压栈的上下文")取值，而不是`调用`的[父作用域](chrome://not-a-link "很多人说自由变量从"父作用域"中取，这样描述容易产生歧义。")。
4、为了能够到创建的作用域中取值，必须暂时[不销毁](chrome://not-a-link "一般来说执行完毕后，gc会去销毁这部分内存")创建时候的上下文，即便已经执行完毕。所以闭包会增加内存开销。
5、函数作为返回值，函数作为参数传递时，就会产生闭包。
一个比较经典的栗子：
``` bash
function a() { 
    var i = 0; 
    function b() { 
        alert(++i); 
    } 
    return b; 
} 
var c = a(); 
c(); 
```
这个闭包里面，a的上下文一直没有销毁，每次调用c()，都可以使i自增。

##3.原型
说到原型归根到底就是要讨论下Object和Function(还有根源对象和内置函数)，不过这个篇幅太大，我还是稍后做个专栏，现在我们还是讨论下比较表面的问题。
一个对象的大致[创建](chrome://not-a-link "这里指的是用new")过程，和它的属性a，我们是如何对其定义和取值的。
1、新建一个对象并赋值给变量a1：var a1 = {};
2、把这个对象的[[Prototype]]属性指向函数A的原型对象：a1.[[Prototype]] = A.prototype
3、调用函数A，同时把this指向1中创建的对象a1，对对象进行初始化：A.apply(a1,arguments)
我们找属性a的时候，通过对象的[[Prototype]]保存对另一个对象的引用，通过这个引用往上进行属性的查找，这就是原型链。
还是等有空把Object和Function讲一下吧，原型链这部分说的太浅显了。

##refer
[深入理解javascript原型和闭包（完结）](http://www.cnblogs.com/wangfupeng1988/p/3977924.html)
[JavaScript概念总结:作用域、闭包、对象与原型链](http://blog.csdn.net/zzulp/article/details/8144520)
[JavaScript原型和继承](http://blog.jobbole.com/19795/)
[js闭包(转载)](http://www.cnblogs.com/zhjjNo1/archive/2011/02/12/1951905.html)
[javascript Prototype constructor的理解(一)](http://blog.csdn.net/chunqiuwei/article/details/22092551)