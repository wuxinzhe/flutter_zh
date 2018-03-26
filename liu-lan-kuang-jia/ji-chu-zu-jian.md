# 基础组件

主要文章：[组件浏览 - 布局模型](https://flutter.io/widgets/layout)

Flutter 带来了一套强有力的基础组件，以下组件都会频繁的被使用到：

* Text：文字组件可以让你在应用中创建一个丰富样式的文字。
* Row，Column：这些弹性组件让你可以创建一个可在横向或纵向伸缩扩展的布局。他是基于Web的弹性布局模型上构建设计的。
* Stack：非线性布局中（不论是横向还是纵向），Stack（堆栈）组件让你可以按照顺序堆叠你的组件。你可以对任一一个Stack组件中的子组件使用 **Positioned** 组件去定位他们相对于Stack组件而言的top、right、left、bottom位置。Stack组件是基于Web的绝对定位布局模型而设计构建的。
* Container：容器组件让你可以创建一个矩形的视觉元素。一个容器可以通过一个 BoxDecoration 以及 background 、border 、shadow 来修饰。一个容器组件也可以拥有外边距、内边距，以及限制他们的尺寸。另外，一个容器组件可以通过矩阵模型在三维的空间中进行变换。

以下是一些以这些基础组件进行简单的组合的而出的组件：

```js
import 'package:flutter/material.dart';

class MyAppBar extends StatelessWidget {
  MyAppBar({this.title});

  // Fields in a Widget subclass are always marked "final".

  final Widget title;

  @override
  Widget build(BuildContext context) {
    return new Container(
      height: 56.0, // in logical pixels
      padding: const EdgeInsets.symmetric(horizontal: 8.0),
      decoration: new BoxDecoration(color: Colors.blue[500]),
      // Row is a horizontal, linear layout.
      child: new Row(
        // <Widget> is the type of items in the list.
        children: <Widget>[
          new IconButton(
            icon: new Icon(Icons.menu),
            tooltip: 'Navigation menu',
            onPressed: null, // null disables the button
          ),
          // Expanded expands its child to fill the available space.
          new Expanded(
            child: title,
          ),
          new IconButton(
            icon: new Icon(Icons.search),
            tooltip: 'Search',
            onPressed: null,
          ),
        ],
      ),
    );
  }
}

class MyScaffold extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Material is a conceptual piece of paper on which the UI appears.
    return new Material(
      // Column is a vertical, linear layout.
      child: new Column(
        children: <Widget>[
          new MyAppBar(
            title: new Text(
              'Example title',
              style: Theme.of(context).primaryTextTheme.title,
            ),
          ),
          new Expanded(
            child: new Center(
              child: new Text('Hello, world!'),
            ),
          ),
        ],
      ),
    );
  }
}

void main() {
  runApp(new MaterialApp(
    title: 'My app', // used by the OS task switcher
    home: new MyScaffold(),
  ));
}
```

请确保在** pubspec.yaml **文件中的 **flutter** 部分入口处添加了 **users-material-design：true**。它允许使用在 **Materal icons** 中预定义的Icon。

许多组件为了继承数据，可能需要在 **MaterialApp** 中显示。所以，我们通过 **MaterialApp** 运行应用。

**MyAppBar** 组件创建了一个高56设备独立像素的容器组件，并且包含了左右8个设备独立像素的内边距。容器内部，**MyAppBar** 使用了一个 **Row** 布局来排列它的子组件。位于中间的子组件 **title**，被 **Expanded** 标记，这意味着它可以扩展填充任何其他子组件未占用的剩余空间。你可以为多个子组件标记上 **Expanded** 属性并使用flex属性来确定他们所要填充的剩余空间的比例。

**MyScaffold** 组件在垂直的方向上排列它的子组件。在列的顶端，放置了一个 **MyAppBar** 的实例，作为 app bar，一个 Text 组件被用于作为他的标题。通过使用组件作为其他组件的参数的方式，是一个强力的组件复用方式。最终，MyScaffold 使用一个 Expanded 组件去填充一个中心包含一条信息的剩余空间。

