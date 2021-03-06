# 图形用户界面 #

## 简介 ##

RTGUI 是一系列 RT-Thread 组件的一部分。它的目的是为开发人员提供一个便于在嵌入式
系统中使用的图形界面库。以其和 RT-Thread 天然集成的优势，方便开发人员开发。这个
图形用户界面组件能够为RT-Thread上的应用程序提供人机界面交互的功能，例如人机界面
设备，设备信息显示，播放器界面等。图形用户界面组件的功能包括：

*  多线程图形用户界面；
*  依赖于RT-Thread线程调度器的实时图形用户界面；
*  C语言方式的全面向对象设计：
    -  对象具备运行时类型信息；
    -  对象自动销毁，使得内存的管理更为轻松；
*  界面主题支持；
*  中文文本显示支持；
*  丰富的控件支持：
    -  button，checkbox，radiobox
    -  textbox
    -  progressbar，slider
    -  列表视图，文件列表视图
    -  等等

本文档先介绍 RTGUI 中的对象基础：`rtgui_object`，然后再介绍事件的分发者和 RTGUI
中对线程的抽象 --- `rtgui_app`；在介绍完绘图功能、剪切域和 widget 基类之后我们
会引入 window 和 server 的概念，最后我们再介绍各种 widget。

## `rtgui_object` --- 创建，销毁与事件 ##

在编写 GUI 程序的时候，我们会用到各种各样的控件，各种控件之间会有各种继承关系。
在RTGUI 中，我们是用 C 语言实现的继承复用。继承关系可以在很多地方发挥作用。一个
典型的例子就是对象的创建和销毁。比如说，label 继承自 widget，那么当我们初始化一
个 label的时候，我们希望属于 widget 的部分已经被初始化完成了。这样子类就只用关
心子类自己相关的部分，而不用再去显式的初始化父类。同理，在对象被销毁的时候我们
希望子类先去释放自己的资源，把自己的功能退化掉，然后父类的部分由父类去进行销毁
。当对象以父类的身份进行销毁的时候不用担心子类的资源产生泄漏，因为这时候子类那
部分资源已经被释放了。这样，在进行父子继承重用代码的同时，我们做到了关注点分离
。使得程序的编写更加简单。

在 GUI 当中，事件可以说是处于一个核心的地位。用户的键盘输入是事件，触摸屏的点击
是事件，一个窗口的绘制也可以抽象为事件。可以说，在程序中各种对象的主要区别就在
于对各种事件不同的响应。当一个对象对所接收到的事件不感兴趣的时候，它可以以父类
的身份去处理事件。这就实现了父子间功能的复用。当子类对相同事件进行不同处理的时
候，它就可以拥有父类所不具有的功能，甚至完全改变行为。这样就实现了对象间行为的
多态。

## `rtgui_app` --- 线程与事件循环 ##

## `rtgui_widget` --- 绘图与剪切域 ##

## window 与 server --- 多窗口多 app 情景下的事件派发和窗口序 ##

## RTGUI 中的控件 ##
