# 将一切结合在一起

让我们来思考一个更复杂的示例，它结合了以上介绍的所有概念。我们构建一个假设的购物应用，它显示许多用于销售的产品并维护一个购物车用于想要购买的东西。让我们通过定义我们的外观类 **ShoppingListItem** 来开始：

```js
class Product {
  const Product({this.name});
  final String name;
}

typedef void CartChangedCallback(Product product, bool inCart);

class ShoppingListItem extends StatelessWidget {
  ShoppingListItem({Product product, this.inCart, this.onCartChanged})
      : product = product,
        super(key: new ObjectKey(product));

  final Product product;
  final bool inCart;
  final CartChangedCallback onCartChanged;

  Color _getColor(BuildContext context) {
    // The theme depends on the BuildContext because different parts of the tree
    // can have different themes.  The BuildContext indicates where the build is
    // taking place and therefore which theme to use.

    return inCart ? Colors.black54 : Theme.of(context).primaryColor;
  }

  TextStyle _getTextStyle(BuildContext context) {
    if (!inCart) return null;

    return new TextStyle(
      color: Colors.black54,
      decoration: TextDecoration.lineThrough,
    );
  }

  @override
  Widget build(BuildContext context) {
    return new ListTile(
      onTap: () {
        onCartChanged(product, !inCart);
      },
      leading: new CircleAvatar(
        backgroundColor: _getColor(context),
        child: new Text(product.name[0]),
      ),
      title: new Text(product.name, style: _getTextStyle(context)),
    );
  }
}
```

**ShoppingListItem** 组件继承了一个通用的无状态组件。组件储存了构造函数中所接收到的最终成员变量，这些变量将用于组件的 **build **方法中。例如，变量 **inCart** 触发两个视觉效果：一个使用当前主题的主色调的颜色，另一个使用灰色。

当用户点击列表项目，组件并没有修改直接修改它的 **inCart** 变量的值。作为代替，组件调用了 **onCartChanged** 方法

