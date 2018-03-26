# 介绍

Flutter 部件是受到了 **React** 的启发，基于最新的 **React** 风格框架。其核心思想是通过各个组件构建UI页面。组件通过当前的配置和状态描述了他们的视图样式。当一个组件的状态发生改变，组件将会重建他们的描述信息，框架将会针对组件之前的描述差异，最小程度的通过渲染树，将组件从一个状态过度到下一个状态。

> Note：如果你希望通过代码来更加深入的了解Flutter，请查看 [在Flutter中构建布局](https://flutter.io/tutorials/layout/) 及 [添加一个动态组件到你的FlutterApp中](https://flutter.io/tutorials/interactive/)。

## Hello World

最精简的 **Flutter App** 只需要简单的使用 **runApp** 方法来执行一个组件。

```js
import 'package:flutter/material.dart';

void main() {
  runApp(
    new Center(
      child: new Text(
        'Hello, world!',
        textDirection: TextDirection.ltr,
      ),
    ),
  );
}
```

**runApp** 方法通过给定的部件作为整个组件树的根部件。在这个案例中，组件树包含2个组件，**Center** 组件和他的子组件——**Text**组件。框架凭借根组件覆盖屏幕，这意味着文字“Hello，world”最终出现在屏幕中心。在这个组件实例中，文字的方向需要专门定义。

当编写一个App，你通常都会基于 **StatelessWidget** 或 **StatefulWidget** 创建你自己的组件，而选择哪个作为继承的基类取决于你的组件是否需要管理某些状态。 一个组件的主要工作就是通过一些更基础的小组件去实现一个 **build** 方法。框架将会依次构建这些组件直到用于计算和描绘组件几何样式的 **RenderObject** 方法执行完毕。

