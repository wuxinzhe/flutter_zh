# 显示 SnackBars

在一些场景下，在某些动作发生时，可以通过一些简单的方式通知我们的用户。例如。当用户划走列表中的消息，我们或许希望提示他们信息已经被删除。我们甚至希望给他们一个操作菜单。

在Material设计中，这是 [SnackBar](https://docs.flutter.io/flutter/material/SnackBar-class.html) 的工作。

## 引导步骤

1. 创建一个 **Scaffold** 组件
2. 显示一个 **SnackBar**
3. 提供一个额外的操作

### 1.创建一个 **Scaffold** 组件

当跟随 **Material** 设计指南创建App时，我们希望给我们的App一个统一的视觉风格。在这个场景下，我们需要在屏幕下方显示 **SnackBar **，不会与其他重要的组件重叠，就像 **FloatingActionButton **一样！

[**Scaffold**](https://docs.flutter.io/flutter/material/Scaffold-class.html) 组件来自 [**meterial** 库](https://docs.flutter.io/flutter/material/material-library.html)，它为我们创建了这个视觉结构并保证重要的组件不会被重叠遮挡。

```js
new Scaffold(
  appBar: new AppBar(
    title: new Text('SnackBar Demo'),
  ),
  body: new SnackBarPage(), // We'll fill this in below!
);
```

### 2.显示一个SnackBar

在 **Scaffold **的区域内，我们可以显示一个 **SnackBar **！首先，我们需要创建一个 **SnackBar **，然后用 **Scaffold** 显示它。

```js
final snackBar = new SnackBar(content: new Text('Yay! A SnackBar!'));

// Find the Scaffold in the Widget tree and use it to show a SnackBar
Scaffold.of(context).showSnackBar(snackBar);
```

### 3.添加一个额外的动作

在一些场景下，当我们显示SnackBar后，我们可能想要提供一个额外的动作来使用。例如，如果我们不小心删掉一条消息，我们可以提供一个机制回退这个操作。

为了实现这个需求，我们可以提供额外的动作给 **SnackBar** 组件。

```js
final snackBar = new SnackBar(
  content: new Text('Yay! A SnackBar!'),
  action: new SnackBarAction(
    label: 'Undo',
    onPressed: () {
      // Some code to undo the change!
    },
  ),
);
```

## 完整示例

提示：在这个示例中，当用户轻触一个按钮时我们将现实一个 **SnackBar **。更多关于用户输入的信息，请参考规范手册的[**手势控制**](/liu-lan-kuang-jia/shou-shi-kong-zhi.md)相关章节。

```js
import 'package:flutter/material.dart';

void main() => runApp(new SnackBarDemo());

class SnackBarDemo extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new MaterialApp(
      title: 'SnackBar Demo',
      home: new Scaffold(
        appBar: new AppBar(
          title: new Text('SnackBar Demo'),
        ),
        body: new SnackBarPage(),
      ),
    );
  }
}

class SnackBarPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new Center(
      child: new RaisedButton(
        onPressed: () {
          final snackBar = new SnackBar(
            content: new Text('Yay! A SnackBar!'),
            action: new SnackBarAction(
              label: 'Undo',
              onPressed: () {
                // Some code to undo the change!
              },
            ),
          );

          // Find the Scaffold in the Widget tree and use it to show a SnackBar!
          Scaffold.of(context).showSnackBar(snackBar);
        },
        child: new Text('Show SnackBar'),
      ),
    );
  }
}
```

![](/assets/snackbar.gif)

