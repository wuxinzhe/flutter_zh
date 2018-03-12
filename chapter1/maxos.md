## 系统要求

要安装并运行Flutter，你的开发环境至少需要满足以下要求：

* 操作系统：macOS（64-bit）
* 磁盘空间：700MB（这不包含Xcode及Android Studio所需要磁盘容量）
* 工具：确保在你的开发环境中包含以下命令行工具：
  * bash，mkdir，rm，git，curl，unzip，which

## 获取 Flutter SDK

请使用git工具从flutter的 [**Github仓库**](https://github.com/flutter/flutter.git) 中获取 Flutter SDK ，并且添加** “flutter” **命令行指令到你的环境变量中。之后在控制台中运行** “flutter doctor” **命令后所显示的所有依赖包都将是你需要安装的内容。

## 克隆代码仓库

如果这是你第一次安装Flutter，请克隆仓库中的 **beta** 分支，之后添加 “flutter” 命令到你的环境变量中。

    $ git clone -b beta https://github.com/flutter/flutter.git
    $ export PATH=`pwd`/flutter/bin:$PATH

以上命令仅暂时地向你的系统中添加了环境变量，所以它仅适用于你当前操作的控制台。要永久的添加 **“flutter” **环境变量，请参考[** 更新你的环境变量**](#更新路径)。

更新现有的Flutter，请参考[**升级Flutter**](https://flutter.io/upgrading/)**。**

## 运行 flutter doctor

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

## 更新路径

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

## 编辑器配置

你可以使用 **flutter** 命令行工具在任何编辑器中开发 Flutter 应用。使用 **flutter help** 命令，可快速查看有效的工具。

我们建议使用我们为专业 IDE 提供的插件以得到最佳的编辑、运行及调试 Flutter App 的体验。查看[编辑器配置](/pei-zhi-bian-ji-qi.md)的相关细节以进行下一步操作。

## 目标平台配置

macOS 同时支持开发IOS和Android的Flutter App。现在来完成至少一个目标平台的配置以构建并运行你第一个Flutter App。

## IOS 配置

### 安装 Xcode

为了要开发IOS的的Flutter App，你至少需要一台Mac并且安装了7.2版本或更新版本的Xcode。

1. 安装7.2版本或更新版本的Xcode（可以通过[Web下载](https://developer.apple.com/xcode/)或从[Mac App Store下载](https://itunes.apple.com/us/app/xcode/id497799835)）；
2. 从控制台运行 **sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer **命令来配置Xcode命令行工具使用最新安装的Xcode版本。在一般情况下，当你使用最新版本的Xcode时，这个路径都是正确的。如果你需要使用其他不同的版本，只需要将路径替换掉即可。
3. 一旦打开Xcode就要确认Xcode的许可协议已经被签署。或者通过控制台运行 **sudo xcodebuild -license** 命令来确认。



