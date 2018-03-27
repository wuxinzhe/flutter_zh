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

当用户点击列表项目，组件并没有直接修改它的 **inCart** 变量的值。作为代替，组件调用了 **onCartChanged** 方法，这个方法来自于父组件。这个模式允许组件存储构建层次中较高层级的状态，这将使得状态可以持续较长的时间。在极端情况下，组件的状态通过 **runApp **保存于整个应用的生命周期中。

当父组件接到 onCartChanged 回调，父组件将会通过新的 **inCart** 值，更新他的内部状态，这将会触发父组件重建并创建一个新的 **ShoppingListItem** 实例。虽然父组件在重建时会创建新的ShoppingListItem实例，但这个性能的消耗是非常少的，因为框架会通过对之前构建的组件和新的组件进行对比，只接受有变化的部分进行 **RenderObject**。

让我们来看一个父组件保存多状态的例子：

```js
class ShoppingList extends StatefulWidget {
  ShoppingList({Key key, this.products}) : super(key: key);

  final List<Product> products;

  // The framework calls createState the first time a widget appears at a given
  // location in the tree. If the parent rebuilds and uses the same type of
  // widget (with the same key), the framework will re-use the State object
  // instead of creating a new State object.

  @override
  _ShoppingListState createState() => new _ShoppingListState();
}

class _ShoppingListState extends State<ShoppingList> {
  Set<Product> _shoppingCart = new Set<Product>();

  void _handleCartChanged(Product product, bool inCart) {
    setState(() {
      // When user changes what is in the cart, we need to change _shoppingCart
      // inside a setState call to trigger a rebuild. The framework then calls
      // build, below, which updates the visual appearance of the app.

      if (inCart)
        _shoppingCart.add(product);
      else
        _shoppingCart.remove(product);
    });
  }

  @override
  Widget build(BuildContext context) {
    return new Scaffold(
      appBar: new AppBar(
        title: new Text('Shopping List'),
      ),
      body: new ListView(
        padding: new EdgeInsets.symmetric(vertical: 8.0),
        children: widget.products.map((Product product) {
          return new ShoppingListItem(
            product: product,
            inCart: _shoppingCart.contains(product),
            onCartChanged: _handleCartChanged,
          );
        }).toList(),
      ),
    );
  }
}

void main() {
  runApp(new MaterialApp(
    title: 'Shopping App',
    home: new ShoppingList(
      products: <Product>[
        new Product(name: 'Eggs'),
        new Product(name: 'Flour'),
        new Product(name: 'Chocolate chips'),
      ],
    ),
  ));
}
```

**ShoppingList** 类继承了 **StatefulWidget** 组件，这意味着这个组件储存了多个状态。当 **ShoppingList **组件第一次插入到节点树中时，框架调用 **createState** 方法去创建一个新的 **\_ShoppingListState** 实例将其关联到本地的节点树中。（注意，我们一般通过下划线来命名 State 基类中的私有成员。）当这个父组件重建时，父组件将会创建一个ShoppingList实例，但是框架会重复使用已存在于节点树种的 **\_ShoppingListState **实例而不是再次调用 **createState** 。

