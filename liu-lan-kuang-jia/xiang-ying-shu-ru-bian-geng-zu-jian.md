# 响应输入变更组件

主要文章：[StatefulWidget](https://docs.flutter.io/flutter/widgets/StatefulWidget-class.html)，[State.setState](https://docs.flutter.io/flutter/widgets/State/setState.html)

到目前为止，我们只使用了无状态组件。无状态组件从父级组件中接收存储在 final （静态）成员变量中的参数。当一个组件被要求构建时，它将使用这些已储存的值作为它创建的组件的新的参数。

为了构建更复杂的经验-比如：为了对更多丰富的用户输入进行响应，应用程序通常具有某种状态。**Flutter **使用状态组件去捕捉这些想法。响应式组件是特殊的组件，它知道如何产生一个用于保持状态的状态对象。思考这个基础的示例：

```js
class Counter extends StatefulWidget {
  // This class is the configuration for the state. It holds the
  // values (in this nothing) provided by the parent and used by the build
  // method of the State. Fields in a Widget subclass are always marked "final".

  @override
  _CounterState createState() => new _CounterState();
}

class _CounterState extends State<Counter> {
  int _counter = 0;

  void _increment() {
    setState(() {
      // This call to setState tells the Flutter framework that
      // something has changed in this State, which causes it to rerun
      // the build method below so that the display can reflect the
      // updated values. If we changed _counter without calling
      // setState(), then the build method would not be called again,
      // and so nothing would appear to happen.
      _counter++;
    });
  }

  @override
  Widget build(BuildContext context) {
    // This method is rerun every time setState is called, for instance
    // as done by the _increment method above.
    // The Flutter framework has been optimized to make rerunning
    // build methods fast, so that you can just rebuild anything that
    // needs updating rather than having to individually change
    // instances of widgets.
    return new Row(
      children: <Widget>[
        new RaisedButton(
          onPressed: _increment,
          child: new Text('Increment'),
        ),
        new Text('Count: $_counter'),
      ],
    );
  }
}
```

你或许会经验与为何 **StatefulWidget** 状态组件和 **State** 状态是分开的。在 **Flutter** 中，这两个不同类型的对象有着不同的生命周期。组件只是一个临时的对象，用于构造一个应用在当前状态下的外观。而另一方面，状态对象在执行build（）方法的过程中是持续存在的，以此记录相关信息。

以上示例接收用户输入并直接在他的构建方法中使用输入结果。在更复杂的应用程序中，不同体系间的组件可能负责不同的事物；比例如，一个组件提供一个复杂的用户接口用于收集特定的目标信息，就像日期或定位，然而另一个组件也许会使用这些信息来更整体的外观。

在Flutter当中，通过回调函数的方式向组件体系上游传递变化通知，而当前状态向下流动到无状态组件。（简单的说，就是组件向上级父组件传递通知，向下级子组件传递状态）。让我们来通过以下这个稍微有点复杂的示例，看看它实际是怎么工作的：

```js
class CounterDisplay extends StatelessWidget {
  CounterDisplay({this.count});

  final int count;

  @override
  Widget build(BuildContext context) {
    return new Text('Count: $count');
  }
}

class CounterIncrementor extends StatelessWidget {
  CounterIncrementor({this.onPressed});

  final VoidCallback onPressed;

  @override
  Widget build(BuildContext context) {
    return new RaisedButton(
      onPressed: onPressed,
      child: new Text('Increment'),
    );
  }
}

class Counter extends StatefulWidget {
  @override
  _CounterState createState() => new _CounterState();
}

class _CounterState extends State<Counter> {
  int _counter = 0;

  void _increment() {
    setState(() {
      ++_counter;
    });
  }

  @override
  Widget build(BuildContext context) {
    return new Row(children: <Widget>[
      new CounterIncrementor(onPressed: _increment),
      new CounterDisplay(count: _counter),
    ]);
  }
}
```

注意我们是如何创建两个新的无状态组件来清楚的分离**显示**和**改变**计数器。虽然就结果上与上一个示例相同，但拆分责任允许更错综复杂的情况被包含在独立的组件当中，而在父级组件中保持一个简单的形态。

