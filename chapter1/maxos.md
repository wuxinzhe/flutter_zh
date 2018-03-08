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

    git clone -b beta https://github.com/flutter/flutter.git
    export PATH=`pwd`/flutter/bin:$PATH

以上命令仅暂时地向你的系统中添加了环境变量，所以它仅适用于你当前操作的控制台。要永久的添加 **“flutter” **环境变量，请参考** **[**更新你的环境变量**](https://flutter.io/setup-macos/#update-your-path)。

更新现有的Flutter，请参考[**升级Flutter**](https://flutter.io/upgrading/)**。**

