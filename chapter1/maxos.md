# 系统要求

要安装并运行Flutter，你的开发环境至少需要满足以下要求：

* 操作系统：macOS（64-bit）
* 磁盘空间：700MB（这不包含Xcode及Android Studio所需要磁盘容量）
* 工具：确保在你的开发环境中包含以下命令行工具：
  * bash，mkdir，rm，git，curl，unzip，which

# 获取 Flutter SDK

请使用git工具从flutter的 [**Github仓库**](https://github.com/flutter/flutter.git) 中获取 Flutter SDK ，并且添加** “flutter” **命令行指令到你的环境变量中。之后在控制台中运行** “flutter doctor” **命令后所显示的所有依赖包都将是你需要安装的内容。

# 克隆代码仓库

如果这是你第一次安装Flutter，请克隆仓库中的 **beta** 分支，之后添加 “flutter” 命令到你的环境变量中。

    $ git clone -b beta https://github.com/flutter/flutter.git
    $ export PATH=`pwd`/flutter/bin:$PATH

以上命令仅暂时地向你的系统中添加了环境变量，所以它仅适用于你当前操作的控制台。要永久的添加 **“flutter” **环境变量，请参考[** 更新你的环境变量**](#更新路径)。

更新现有的Flutter，请参考[**升级Flutter**](https://flutter.io/upgrading/)**。**

# 运行 flutter doctor

通过运行以下命令，安装所有列出的依赖包以完成安装步骤。

```
$ flutter doctor
```

这个命令会检查你的运行环境并在你的控制台中显示一份报告。Dark SDK 已经被集成在 Flutter 当中，这样你就没有必要单独的再去安装Dark。仔细检查一下控制台的输出信息，也许你需要安装其他软件或执行其他更详细的操作（将会以加粗文字显示）。

例如：

```
[-] Android toolchain - develop for Android devices
    • Android SDK at /Users/obiwan/Library/Android/sdk
    ✗ Android SDK is missing command line tools; download from https://goo.gl/XxQghQ
    • Try re-installing or updating your Android SDK,
      visit https://flutter.io/setup/#android-setup for detailed instructions.
```

当你第一次运行 flutter 的相关命令（比如 **flutter doctor**），flutter 将会下载他的相关依赖包并且自行编译。这样之后再运行相关命令则会变得更有效率。

以下部分将描述如何执行这些任务并且完成相关步骤。如果你选择使用IDE相关插件如：IntelliJ IDEA、Android Studio及VS Code，你将会看到flutter的相关输出信息。

在你的安装过程中，一旦错过了某些依赖包，你可以通过再次运行 **flutter doctor** 命令来验证你是否已经正确的安装了所有的依赖包。

> flutter 构建工具使用 Google Analytics 收集匿名的数据统计及基础的崩溃报告。这些数据是用来在不就得将来，帮助改进 flutter 构建工具。

# 更新路径

你可以为你当前的控制台添加命令路径的环境变量，参考[克隆代码仓库](#克隆代码仓库)。你可能也会希望永久的添加这个环境变量，让你在任何控制台中均可使用 **flutter** 命令。

永久的添加环境变量的步骤在不同的操作系统中是不一样的。

1. 确认 flutter 的目录地址，这个地址将会在第三步时使用；
2. 打开 或 创建 **$HOME/.bash\_profile 。**文件名及路径可能会因为操作系统的不同而不同；
3. 添加下面这行代码，并用第一步获取的路径替换代码中 **\[PATH\_TO\_FLUTTER\_GIT\_DIRECTORY\] **部分。

```
$ export PATH=[PATH_TO_FLUTTER_GIT_DIRECTORY]/flutter/bin:$PATH
```

1. 运行 **source $HOME/.bash\_profile **以刷新当前窗口。
2. 通过运行下面的命令验证 flutter/bin 目录已经添加到了你的路径变量中

```
$ echo $PATH
```

# 编辑器配置

你可以使用 **flutter** 命令行工具在任何编辑器中开发 Flutter 应用。使用 **flutter help** 命令，可快速查看有效的工具。

我们建议使用我们为专业 IDE 提供的插件以得到最佳的编辑、运行及调试 Flutter App 的体验。查看[编辑器配置](/pei-zhi-bian-ji-qi.md)的相关细节以进行下一步操作。

# 目标平台配置

macOS 同时支持开发IOS和Android的Flutter App。现在来完成至少一个目标平台的配置以构建并运行你第一个Flutter App。

# IOS 配置

## 安装 Xcode

为了要开发IOS的的Flutter App，你至少需要一台Mac并且安装了7.2版本或更新版本的Xcode。

1. 安装7.2版本或更新版本的Xcode（可以通过[Web下载](https://developer.apple.com/xcode/)或从[Mac App Store下载](https://itunes.apple.com/us/app/xcode/id497799835)）；
2. 从控制台运行 **sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer **命令来配置Xcode命令行工具使用最新安装的Xcode版本。在一般情况下，当你使用最新版本的Xcode时，这个路径都是正确的。如果你需要使用其他不同的版本，只需要将路径替换掉即可。
3. 一旦打开Xcode就要确认Xcode的许可协议已经被签署。或者通过控制台运行 **sudo xcodebuild -license** 命令来确认。

通过Xcode你可以在IOS设备或虚拟机上运行Flutter App

## 配置IOS模拟器

为了准备在你的IOS模拟器上运行和测试Flutter App，请跟随以下步骤进行操作

```
$ open -a Simulator
```

1. 通过菜单 **Hardware &gt; Device** 来检查你的虚拟机设置以确保你的虚拟机模拟的是64位的设备（IPhone 5s 或更新的机器）；
2. 取决于你开发机器的屏幕尺寸，被虚拟的高屏密度的IOS设备可能会超出你的屏幕。通过菜单 **Window &gt; Scale **来设置你设备的缩放比例。
3. 通过执行 **flutter run** 命令来开始运行你的App

## 真机运行

如果你想要在真机上运行你的Flutter App，你需要一些额外的工具以及一个 Apple 账户。当然你也需要在Xcode中部署应用到真机。

1. 安装 [homebrew](http://brew.sh/)；
2. 打开控制台并运行以下命令安装相关部署工具

```
$ brew update
$ brew install --HEAD libimobiledevice
$ brew install ideviceinstaller ios-deploy cocoapods
$ pod setup
```

如果这些命令中有任何一条出现了错误，可以通过执行 brew doctor 命令并跟着响应的介绍去处理这些问题。

1. 依照XCode的签约流程：

   1. 通过控制台在你的Flutter工程目录下运行命令 **open ios/Runner.xcworkspace** 来打开你项目的默认Xcode工程；

   2. 在Xcode中选择左边导航栏的 **Runner** 项目；

      * 在 Runner 的设置页面中，确保在 General &gt; Signing &gt; Team 选项下，你已经选择了一个开发团队。当你选择一个团队时，Xcode会创建并下载开发证书，以你的账号来注册你的设备，并创建和下载一个规则描述文件 Provinsioning profile（如果需要）；

      * 在开始开发你第一个IOS项目之前，你或许需要使用你的苹果账号注册Xcode。![](/assets/xcode-account.png)

      * 任何苹果账号都支持开发及测试。但只有注册了苹果开发者资格才能够将你的引用发布到苹果商店中。查看[苹果账户不同会员类型之间的差别](https://developer.apple.com/support/compare-memberships)。

      * 当你第一次使用真机开发IOS时，你需要同时在你的设备上信任Mac和开发者证书。当你第一次将你的IOS设备连接上电脑时，在弹出的提示窗口中选择上选择 **Trust** 信任。

      ![](/assets/trust-computer.png)

      * 然后，打开苹果设备的系统设置，找到 **General &gt; Device Management** 并信任你的开发证书.

      * 如果在Xcode中，自动签名失败，找到项目的 **General &gt; Identity &gt; Bundle Identifier **，检验一下这个值是否是唯一的。

        ![](/assets/xcode-unique-bundle-id.png)

2. 通过执行 flutter run 命令开始运行你的app。

# 安卓配置

## 安装 Android Studio

你可以使用Mac、Windows、或者Linux（64位）系统来开发安卓的Flutter App。

Flutter 要求安装并设置Android Studio：

1. 下载并安装[ Android Studio](https://developer.android.com/studio/index.html)。
2. 运行并通过 “**Android Studio Setup Wizard”。**这么做将会安装最新的 Android SDK、Android SDK Platform-Tools 以及 Android SDK Build-Tools ，这些都是用Flutter开发安卓所必须的工具。

## 设置你的安卓设备

为了准备在你的安卓设备上运行并测试Flutter app，你需要一个运行Android 4.1（API level 16）或更高版本的安卓设备。

1. 在你的安卓设备上激活开发者选项以及USB调试模式，更多的细节介绍可以在[安卓文档](https://developer.android.com/studio/debug/dev-options.html)中获取；
2. 将你的安卓设备通过USB线与电脑连接。如果你的设备有弹出提示，就授权你的电脑让它连接你的手机；
3. 在控制台中，运行 **flutter devices** 命令以验证Fluuter识别出了你所链接的安卓设备；
4. 通过运行 **flutter run** 命令，开始你的app。

默认情况下，Flutter 使用你 **adb** 工具所基于的 Android SDK 版本。如果你希望Flutter使用不同的Android SDK，那你必须为安装目录设置 **ANDROID\_HOME **环境变量。

## 设置安卓模拟器

请跟随以下步骤来为在安卓模拟器上运行和测试Flutter App而做准备。

1. 激活你机器上的[模拟器加速（VM acceleration）](https://developer.android.com/studio/run/emulator-acceleration.html)；
2. 打开 **Android Studio&gt;Tools&gt;Android&gt;AVD Manager **并选择** Create Virtual Device**；
3. 选择一个设备并选择** Next**；
4. 为你想要虚拟的安卓版本选择一个或多个系统镜像，并选择 **Next。推荐使用x86及x86\_64的镜像**；
5. 在虚拟机性能方面，选择 **Hardware - GLES 2.0 **以激活[硬件加速](https://developer.android.com/studio/run/emulator-acceleration.html)；
6. 检验AVD配置是否正确，然后选择 **Finish**。
   以上步骤的细节，详见 [AVDs 管理](https://developer.android.com/studio/run/managing-avds.html)。
7. 在安卓虚拟设备管理中，点击工具栏里的 Run。虚拟机开始运行并显示你所选择的操作系统版本的默认图像；
8. 通过执行 flutter run 命令开始运行你的App，被链接的设备名称叫做 **Android SDK built for &lt;platform&gt; ，**其中platform是指集成电路，例如 x86。

## [下一章节：配置编辑器](/pei-zhi-bian-ji-qi.md)



