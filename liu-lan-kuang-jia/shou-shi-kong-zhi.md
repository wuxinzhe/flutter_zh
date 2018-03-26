# 交互控制

主要文章：[在Flutter中使用手势](https://flutter.io/gestures/)

大多数应用包含了一些系统提供的用户交互表单。在构建交互式应用的第一步就是发现输入手势。让我们通过创建一个简单的按钮来看看它是如何通过工作的。

```js
class MyButton extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return new GestureDetector(
      onTap: () {
        print('MyButton was tapped!');
      },
      child: new Container(
        height: 36.0,
        padding: const EdgeInsets.all(8.0),
        margin: const EdgeInsets.symmetric(horizontal: 8.0),
        decoration: new BoxDecoration(
          borderRadius: new BorderRadius.circular(5.0),
          color: Colors.lightGreen[500],
        ),
        child: new Center(
          child: new Text('Engage'),
        ),
      ),
    );
  }
}
```

**GestureDetector** 组件不包含任何可视部分，但是能发现用户的手势。当用户触碰 **Container** 组件时，它会调起 **onTap** 的回调函数，在本例中将会在控制台中打印一条信息。你可以使用 **GestureDetector** 发现一系列输入手势，包括触碰手势、拖拽手势以及缩放手势。

许多组件使用 **GestureDetector** 去提供一个可选的回调函数给其他组件。举个例子，**IconButton **组件、**RasedButton **组件和**FloatingActionButton **有一个 **onPressed** 方法，当用户触碰组件时，它就会被触发。

