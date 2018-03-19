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



