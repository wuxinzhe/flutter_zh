# Android Studio

_Android Studio：_一个完整且完善的 Flutter 开发工具。

## 创建一个新的App

1. 选择 **File &gt; New Flutter Project。**
2. 选择 **Flutter application** 作为项目类型，并点击下一步。
3. 输入项目名称（例如：**myapp**），并点击下一步。
4. 点击 **Finish** 。
5. 等待 Android Studio 安装SDK 并创建项目。

以上命令创建一个名为 myapp 的 Flutter 项目目录，并且包含一个使用 [Material Components](https://material.io/guidelines/) 的简单Demo。

在项目目录中，app的代码在 lib/main.dart 文件中。

## 运行App

1. 找到 Android Studio 的主工具栏
   ![](/assets/main-toolbar.png)
2. 在 **Target selector** 中，选择一个安卓设备以运行app。如果列表中不存在有效选项，选择 **Tools &gt; Android &gt;AVD Manager **并且创建一个项目，具体细节，请参考 [Manager AVDs](https://developer.android.com/studio/run/managing-avds.html)。
3. 在工具栏中点击 Run icon，或调用菜单中的 Run &gt; Run.
4. 如果一切正常，你会在你的设备或模拟器中看到如下界面：
   ![](/assets/flutter-starter-app-android.png)

## 尝试热更新

Flutter 通过hot reload（热更新）提供一个快速的开发周期，依赖于此，你可以在不重启App并保持App当前运行状态的情况下重新加载代码。通过IDE或命令行工具激活热更新，然后简单的修改你的源码之后查看你设备或模拟器上的变化。

1. 修改字符串  
   **'You have pushed the button this many times:'**  变更为 **'You have clicked the button this many times:'**

2. 不要点击‘Stop’按钮，让你的App继续保持运行。

3. 执行 **Save All**（快捷键：cmd + s / ctrl + s），或点击 **Hot Reload button** （形如闪电的按钮）。

你应该会立刻在正运行的App中看到字符串的变化。

## 下一步

让我们通过创建一个精巧的App来学习Flutter的一些核心内容。

下一步：编写你的第一个App

