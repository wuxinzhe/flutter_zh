# 响应组件生命周期事件

主要文章：[**State**（状态）](https://docs.flutter.io/flutter/widgets/State-class.html)

在 **StatefulWidget** （状态组件）调用 createState 之后，框架将会向树中插入新的状态对象，然后对这个新状态对象调起 **initState** 。**State** 的基类可以重写 **initState** 方法使其在工作时只触发一次。例如，你可以重写 initState 以设置动画效果或者订阅平台服务。**initState** 的重写方法需要以 **super.initState** 作为首行代码开始方法。

当一个一个状态对象再也不被需要时，框架会对这个状态对象调用 **dispose** 方法。你可以重写 **dispose** 方法来完成一些清理工作。例如，你可以通过重写 **dispose** 方法来取消定时器或取消订阅平台服务。一般情况下，**dispose** 的实现方法都是以调用 **supper.dispose** 作为末行代码以结束方法。

