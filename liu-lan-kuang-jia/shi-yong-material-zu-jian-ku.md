# 使用Material组件库

主要文章：[组件浏览 - Material组件库](https://flutter.io/widgets/material)

Flutter 提供许多根据Material设计的组件帮助你构建App。一个 Material风格的App 始于 MaterialApp 组件，这是一个作为 App 组件树的根的组件，并提供了许多非常有用的组件，其中包括了 Navigator 组件，一个通过字符串定义并管理你的组件的堆栈，亦称之为“路由”。Navigator 组件让你能够在你的应用中的不同屏幕之间进行平滑过渡。使用 MaterialApp 组件是完全可选的，但推荐使用它。

```js
import 'package:flutter/material.dart';

void main() {
  runApp(new MaterialApp(
    title: 'Flutter Tutorial',
    home: new TutorialHome(),
  ));
}

class TutorialHome extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Scaffold is a layout for the major Material Components.
    return new Scaffold(
      appBar: new AppBar(
        leading: new IconButton(
          icon: new Icon(Icons.menu),
          tooltip: 'Navigation menu',
          onPressed: null,
        ),
        title: new Text('Example title'),
        actions: <Widget>[
          new IconButton(
            icon: new Icon(Icons.search),
            tooltip: 'Search',
            onPressed: null,
          ),
        ],
      ),
      // body is the majority of the screen.
      body: new Center(
        child: new Text('Hello, world!'),
      ),
      floatingActionButton: new FloatingActionButton(
        tooltip: 'Add', // used by assistive technologies
        child: new Icon(Icons.add),
        onPressed: null,
      ),
    );
  }
}
```

现在我们已经从 **MyAppBar** 和 **MyScaffold** 切换到来自于 **marterial.dart** 的 **AppBar** 和 **Scaffold** 组件，我们的app开始看到了一点Material。举个例子，app bar 拥有一个阴影并且标题文字自动的继承了正确的样式风格。我们也为计数器添加了一个浮动的按钮。

再次提醒，我们再次通过将组件作为其他组件的参数。Scaffold 组件将许多不同的小组件作为参数命名，每一个都背放置在里Scaffold布局中合适的位置。显而易见的，**AppBar**组件让我们通过在 **leading**、**actions**和**title**上进行设置组件。这个模式遍布了整个框架，你也可能会在你自己设计的组件中采用。

