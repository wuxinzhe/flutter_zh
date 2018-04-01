# 导向一个新的屏幕并回退

大多数App都用数个屏幕来现实不同类型的信息。例如，我们或许有一个屏幕显示产品库。我们的用户可以轻触其中的产品，从而在新的屏幕上获取产品的详细信息。

在安卓的体系中，我们的屏幕都是一个个新的 **Activity**。在iOS体系中，是新的视图控制器。而在Flutter，新的屏幕只不过是一个组件！

所以我们如何跳转到新的屏幕当中？使用 **Navigator** 组件。

## 引导步骤

1. 创建两个屏幕
2. 使用 Navigator.push 导航到第二个屏幕
3. 使用 Navigator.pop 返回到第一个屏幕

### 1.创建两个屏幕

首先，我们需要两个屏幕来执行演示。因为这是一个基础的示例，我们创建两个屏幕，并且每个都包含一个单独的按钮。轻触第一个屏幕的按钮将会导航到第二个屏幕，轻触第二个屏幕的按钮将会回退到第一个屏幕！

首先我们构建一个视觉结构。

```js
class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text('First Screen'),
      ),
      body: new Center(
        child: new RaisedButton(
          child: new Text('Launch new screen'),
          onPressed: () {
            // Navigate to second screen when tapped!
          },
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Second Screen"),
      ),
      body: new Center(
        child: new RaisedButton(
          onPressed: () {
            // Navigate back to first screen when tapped!
          },
          child: new Text('Go back!'),
        ),
      ),
    );
  }
}
```

### 2.使用 **Navigator.push** 导航到第二个屏幕

为了导航到一个新的屏幕，我们需要使用 **Navigator.push** 方法。**push** 方法将会增加一个 **Route（路由）** 到Navigator管理的路由堆栈当中。

**push** 方法需要一个 **Route（路由）**，但是我们要从哪里获取 **Route（路由）**呢？我们可以创建属于我们自己的，也可以使用 **MaterialPageRoute** 。**MaterialPageRoute **是非常好用的，因为他使用平台特定的动画进行屏幕间的过度。

在 FirsScreen 组件的build方法中，我们更新一下 onPressed 回调方法：

```js
// Within the `FirstScreen` Widget
onPressed: () {
  Navigator.push(
    context,
    new MaterialPageRoute(builder: (context) => new SecondScreen()),
  );
}
```

### 3.使用 Navigator.pop 返回到第一个屏幕

现在我们处于第二屏幕，我们要如何关闭它并返回第一屏幕呢？利用** Navigator.pop** 方法！pop 方法将会从navigator管理的堆栈中移除当前的路由。

我们需要更新第二屏组件中的 **onPressed** 回调方法：

```js
// Within the SecondScreen Widget
onPressed: () {
  Navigator.pop(context);
}
```

## 完整示例

```js
import 'package:flutter/material.dart';

void main() {
  runApp(new MaterialApp(
    title: 'Navigation Basics',
    home: new FirstScreen(),
  ));
}

class FirstScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text('First Screen'),
      ),
      body: new Center(
        child: new RaisedButton(
          child: new Text('Launch new screen'),
          onPressed: () {
            Navigator.push(
              context,
              new MaterialPageRoute(builder: (context) => new SecondScreen()),
            );
          },
        ),
      ),
    );
  }
}

class SecondScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("Second Screen"),
      ),
      body: new Center(
        child: new RaisedButton(
          onPressed: () {
            Navigator.pop(context);
          },
          child: new Text('Go back!'),
        ),
      ),
    );
  }
}
```

![](/assets/navigation-basics.gif)

