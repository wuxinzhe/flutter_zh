# 显示 SnackBars

在一些场景下，在某些动作发生时，可以通过一些简单的方式通知我们的用户。例如。当用户划走列表中的消息，我们或许希望提示他们信息已经被删除。我们甚至希望给他们一个操作菜单。

在Material设计中，这是 [SnackBar](https://docs.flutter.io/flutter/material/SnackBar-class.html) 的工作。

## 提示

1. 创建一个 **Scaffold** 组件
2. 显示一个 **SnackBar**
3. 提供一个额外的操作

### 1.创建一个 **Scaffold** 组件

当跟随 **Material** 设计指南创建App时，我们希望给我们的App一个统一的视觉风格。在这个场景下，我们需要在屏幕下方显示 **SnackBar **，不会与其他重要的组件重叠，就像 **FloatingActionButton **一样！



