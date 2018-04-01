# 携带数据到新屏幕

大多数情况下，我们不仅仅只是想要导航到新的屏幕，也同时希望携带一些数据到新屏幕中。例如，我们经常希望携带一些关于触碰选项的信息。

记住：屏幕只不过是组件。在这个示例中，我们创建一个代办列表。当一个代办记录被触碰时，我们到导航到新的屏幕组件并显示相关代办信息。

## 引导步骤

1. 定义一个代办类
2. 显示一个代办列表
3. 创建一个详情屏幕用于显示相关代办信息
4. 导航并携带相关数据到详情屏幕

### 1.定义一个代办类

首先，我们需要一个简单的途径代表一个代办。这个例子中，我们创建了一个类包含两条数据：标题和描述。

```js
class Todo {
  final String title;
  final String description;

  Todo(this.title, this.description);
}
```

### 2.创建一个代办列表

其次，我们希望显示一个代办列表。在这个示例中，我们产生20条代办记录，并使用ListView组件来显示他们。更多的Lists组件的相关细节，请参考 [**Basic List**](https://flutter.io/cookbook/lists/basic-list/) 章节。

#### 产生一个代办列表

```js
final todos = new List<Todo>.generate(
  20,
  (i) => new Todo(
        'Todo $i',
        'A description of what needs to be done for Todo $i',
      ),
);
```

#### 利用ListView来显示列表中的代表记录

```js
new ListView.builder(
  itemCount: todos.length,
  itemBuilder: (context, index) {
    return new ListTile(
      title: new Text(todos[index].title),
    );
  },
);
```

如此以来，甚好。我们产生了20条代办记录并将他们显示在ListView组件中。

### 3.创建一个详情屏幕用于显示相关代办信息

现在，我们创建第二个屏幕。屏幕的标题要包含代办的标题，内容将显示代办的描述。

因为他是一个 **StatelessWidget** 无状态组件，所以我们只需要用户在创建屏幕时携带代办信息即可。然后我们将会使用给定的代办信息来创建UI界面。

```js
class DetailScreen extends StatelessWidget {
  // Declare a field that holds the Todo
  final Todo todo;

  // In the constructor, require a Todo
  DetailScreen({Key key, @required this.todo}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // Use the Todo to create our UI
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("${todo.title}"),
      ),
      body: new Padding(
        padding: new EdgeInsets.all(16.0),
        child: new Text('${todo.description}'),
      ),
    );
  }
}
```

### 4.导航并携带相关数据到详情屏幕

在我们的 **DetailScreen** 区域中，我们已经准备好演示导航！在我们的场景下，我们希望在用户轻触列表中的代办记录时导航到 DetailScreen。当我们这么做后，我们也希望携带代办记录到详情屏幕。

为此，我们要为 **ListTile** 组件编写 onTap 回调函数。在 **onTap** 回调函数中，我们再一次享受 **Navigator.push** 方法。

```js
new ListView.builder(
  itemCount: todos.length,
  itemBuilder: (context, index) {
    return new ListTile(
      title: new Text(todos[index].title),
      // When a user taps on the ListTile, navigate to the DetailScreen.
      // Notice that we're not only creating a new DetailScreen, we're
      // also passing the current todo to it!
      onTap: () {
        Navigator.push(
          context,
          new MaterialPageRoute(
            builder: (context) => new DetailScreen(todo: todos[index]),
          ),
        );
      },
    );
  },
);
```

## 完整示例

```js
import 'package:flutter/foundation.dart';
import 'package:flutter/material.dart';

class Todo {
  final String title;
  final String description;

  Todo(this.title, this.description);
}

void main() {
  runApp(new MaterialApp(
    title: 'Passing Data',
    home: new TodosScreen(
      todos: new List.generate(
        20,
        (i) => new Todo(
              'Todo $i',
              'A description of what needs to be done for Todo $i',
            ),
      ),
    ),
  ));
}

class TodosScreen extends StatelessWidget {
  final List<Todo> todos;

  TodosScreen({Key key, @required this.todos}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text('Todos'),
      ),
      body: new ListView.builder(
        itemCount: todos.length,
        itemBuilder: (context, index) {
          return new ListTile(
            title: new Text(todos[index].title),
            // When a user taps on the ListTile, navigate to the DetailScreen.
            // Notice that we're not only creating a new DetailScreen, we're
            // also passing the current todo through to it!
            onTap: () {
              Navigator.push(
                context,
                new MaterialPageRoute(
                  builder: (context) => new DetailScreen(todo: todos[index]),
                ),
              );
            },
          );
        },
      ),
    );
  }
}

class DetailScreen extends StatelessWidget {
  // Declare a field that holds the Todo
  final Todo todo;

  // In the constructor, require a Todo
  DetailScreen({Key key, @required this.todo}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    // Use the Todo to create our UI
    return new Scaffold(
      appBar: new AppBar(
        title: new Text("${todo.title}"),
      ),
      body: new Padding(
        padding: new EdgeInsets.all(16.0),
        child: new Text('${todo.description}'),
      ),
    );
  }
}
```

![](/assets/passing-data.gif)

