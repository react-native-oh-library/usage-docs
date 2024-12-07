> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-splash-screen</code> </h1>
</p>

本项目基于 [react-native-splash-screen@3.3.0](https://github.com/crazycodeboy/react-native-splash-screen) 开发。

该第三方库的仓库已迁移至 Gitee，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-splash-screen`，具体版本所属关系如下：

| Version                   | Package Name                                      | Repository         | Release                    |
|---------------------------| ------------------------------------------------- | ------------------ | -------------------------- |
| <= 3.3.0-0.0.2@deprecated | @react-native-oh-tpl/react-native-splash-screen | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-splash-screen) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-splash-screen/releases) |
| > 3.3.0                   | @react-native-ohos/react-native-splash-screen   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-splash-screen) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-splash-screen/releases) |

## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-splash-screen
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-splash-screen
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。


##### **在 entry/src/main/ets/pages 目录下新建启动页SplashScreenPage.ets**

```ets
import { SplashScreenView } from '@react-native-ohos/react-native-splash-screen/src/main/ets/SplashScreenView'

@Entry
@Component
export struct SplashScreenPage {
  build() {
    Row() {
      SplashScreenView();
    }
  }
}
```

##### **在 entry/src/resources/base/profile/main_pages.json 内添加 `pages/SplashScreenPage`**
```json
{
  "src": [
    "pages/SplashScreenPage"
  ]
}
```

##### **在 entry/src/main/ets/entryability/EntryAbility.ets 内添加**
```ets
import window from '@ohos.window';
import { SplashScreen } from '@react-native-ohos/react-native-splash-screen/src/main/ets/SplashScreen'

export default class EntryAbility extends RNAbility {
  onWindowStageCreate(windowStage: window.WindowStage): void {
    let startWindowIcon = $r('app.media.splashIcon'); // 启动页图片（用户改成自己 App 的启动图片，一般在 entry/src/main/resources/base/media 文件夹中）
    let startWindowBackground = "#FFFFFF"; // 启动页背景色
    let startPageUrl = 'pages/SplashScreenPage'; // 启动页
    SplashScreen.show(this.context, windowStage, startWindowIcon, startWindowBackground, startPageUrl).then(() => {
      super.onWindowStageCreate(windowStage);
    })
  }
}
```

##### **在适当的时候关闭启动屏幕（如：启动初始化完成后）**
```ets
import SplashScreen from 'react-native-splash-screen';
export default class WelcomePage extends Component {
    componentDidMount() {
        SplashScreen.hide(); // 关闭启动屏幕
    }
}
```

## 2. Manual Link

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 2.2. 引入原生端代码

目前有两种方法：

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@react-native-ohos/react-native-splash-screen": "file:../../node_modules/@react-native-ohos/react-native-splash-screen/harmony/splash_screen.har"
  }
```

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)
> 
### 2.3. 配置 CMakeLists 和引入 SplashScreenPackage

打开 entry/src/main/cpp/CMakeLists.txt，添加：
```diff
  ...
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-splash-screen/src/main/cpp" ./splash_screen)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_splash_screen)
# RNOH_END: manual_package_linking_2

```

打开 entry/src/main/cpp/PackageProvider.cpp，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "SplashScreenPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<SplashScreenPackage>(ctx)
    };
}
```

### 2.4. 在 ArkTs 侧引入 SplashScreenPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {SplashScreenPackage} from '@react-native-ohos/react-native-splash-screen/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SplashScreenPackage(ctx)
  ];
}
```

### 2.5. 运行

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。


## 3. 约束与限制

### 3.1. 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/react-native-splash-screen Releases](https://gitee.com/openharmony-sig/rntpc_react-native-splash-screen/releases)


## 4. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


|Name | Description | Type | Required | Platform | HarmonyOS Support|
|----- | ----- | ----- | ----- | ----- | -----|
|show() | 显示启动屏幕(原生方法) | function | Yes | iOS | No  |
|show(abilityContext: UIAbilityContext, windowStage: window.WindowStage, iconResource: any, backgroundColor: string, pageUrl: string) | 显示启动屏幕(原生方法) | function | Yes | iOS/Android | Yes|  
| hide() | 隐藏启动屏幕 | function | Yes | iOS/Android | Yes | 


> [!TIP] **show(abilityContext: UIAbilityContext, windowStage: window.WindowStage, iconResource: any, backgroundColor: string, pageUrl: string) 方法的参数说明：**

| Name                                                      | Description                                                                                                         | Type     |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- |
| abilityContext | 应用上下文 | UIAbilityContext |
| windowStage | 窗口管理器 | window.WindowStage |
| iconResource | 启动页图片 | Resource |
| backgroundColor | 启动页背景色 | string |
| pageUrl | 首页路由 | bool |

## 5. 遗留问题

## 6. 其他

- 在 iOS 中，show() 方法的工作原理是： 在入口 application 方法中，首先加载 App 首页，然后使用 while 循环让界面停留在 App 启动屏，此时首页仍然会异步加载，加载完成后，停止 while 循环即可隐藏启动屏，显示首页。
HarmonyOS 中，在入口 onWindowStageCreate 中调用 windowStage.loadContent 加载首页，如果此时使用 while 循环，首页无法异步加载。

## 7. 开源协议

本项目基于 [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-splash-screen/blob/master/LICENSE) ，请自由地享受和参与开源。