# 使用主题分配颜色和字体风格

为了在我们的App中分配颜色和字体风格，我们可以利用主题。有两种方式来定义主题：App-wide 或者使用 **Theme** 组件，以此来为我们的应用程序定义特定的颜色和字体。事实上，app-wide 主题也只不过是 **Theme** 组件通过 MaterialApp 在根节点上创建的一个主题组件。

在我们定义了一个主题之后，我们可以在我们的组件中使用。另外，Flutter 提供的 Material 组件库也将会使用主题来为 AppBars、Buttons、Checkboxes 以及其他组件设置颜色和字体风格。

## 创建一个App主题

为了在整个App中共享颜色和字体样式主题，我们可以为 **MaterialApp** 的构造器提供 **ThemeData。**

如果没有提供主题，Flutter会创建一个备用的主题。

```js
new MaterialApp(
  title: title,
  theme: new ThemeData(
    brightness: Brightness.dark,
    primaryColor: Colors.lightBlue[800],
    accentColor: Colors.cyan[600],
  ),
);
```

请查看 [**ThemeData**](https://docs.flutter.io/flutter/material/ThemeData-class.html) 文档以了解可以定义颜色和字体风格。

## 应用程序部分的主题

如果我们想要在我们的应用中重写 app-wide 的主题，我们可以将我们的App封装在一个主题组件当中。

有两种办法可以做到：创建唯一的 **ThemeData**，或者继承原主题的父主题。

### 创建唯一的 **ThemeData**

如果我们不想继承任何应用程序的颜色和字体风格，我们可以创建一个** new ThemeData\(\) **新实例，并将其传递给主题组件。

```js
new Theme(
  // Create a unique theme with "new ThemeData"
  data: new ThemeData(
    accentColor: Colors.yellow,
  ),
  child: new FloatingActionButton(
    onPressed: () {},
    child: new Icon(Icons.add),
  ),
);
```

### 继承父主题

继承父主题通常是比较有意义的，而不是重写所有细节。我们可以通过使用 **copyWith** 方法来达到这个目的。

```js
new Theme(
  // Find and Extend the parent theme using "copyWith". Please see the next 
  // section for more info on `Theme.of`.
  data: Theme.of(context).copyWith(accentColor: Colors.yellow),
  child: new FloatingActionButton(
    onPressed: null,
    child: new Icon(Icons.add),
  ),
);
```

### 使用主题

如今我们定义了一个主题，我们可以通过 **Theme.of\(context\) **方法在组件build阶段使用它！

**Theme.of\(context\)  **将会查找组件树并返回一个树中最近的主题。如果我们在组件上单独定义了一个主题，则会返回这个主题。如果没有，则返回App的全局主题。

事实上，**FloatingActionButton** 就是使用这个准确的方式找到 **accentColor**。

```js
new Container(
  color: Theme.of(context).accentColor,
  child: new Text(
    'Text with a background color',
    style: Theme.of(context).textTheme.title,
  ),
);
```

## 完整示例

```js
import 'package:flutter/foundation.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(new MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final appName = 'Custom Themes';

    return new MaterialApp(
      title: appName,
      theme: new ThemeData(
        brightness: Brightness.dark,
        primaryColor: Colors.lightBlue[800],
        accentColor: Colors.cyan[600],
      ),
      home: new MyHomePage(
        title: appName,
      ),
    );
  }
}

class MyHomePage extends StatelessWidget {
  final String title;

  MyHomePage({Key key, @required this.title}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text(title),
      ),
      body: new Center(
        child: new Container(
          color: Theme.of(context).accentColor,
          child: new Text(
            'Text with a background color',
            style: Theme.of(context).textTheme.title,
          ),
        ),
      ),
      floatingActionButton: new Theme(
        data: Theme.of(context).copyWith(accentColor: Colors.yellow),
        child: new FloatingActionButton(
          onPressed: null,
          child: new Icon(Icons.add),
        ),
      ),
    );
  }
}
```

![](/assets/themes.png)

