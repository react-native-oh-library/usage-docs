> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-splash-screen</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/crazycodeboy/react-native-splash-screen">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/crazycodeboy/react-native-splash-screen/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-splash-screen)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-splash-screen Releases](https://github.com/react-native-oh-library/react-native-splash-screen/releases).


Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-splash-screen@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-splash-screen@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.


##### **Create a launch page `SplashScreenPage.ets` in the entry/src/main/ets/pages directory**

```ets
import { SplashScreenView } from '@react-native-oh-tpl/react-native-splash-screen/src/main/ets/SplashScreenView'

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

##### **Add `pages/SplashScreenPage` in entry/src/resources/base/profile/main_pages.json **
```json
{
  "src": [
    "pages/SplashScreenPage"
  ]
}
```

##### **Open the `entry/src/main/ets/entryability/EntryAbility.ets` file and add the following code: **
```ets
import window from '@ohos.window';
import { SplashScreen } from '@react-native-oh-tpl/react-native-splash-screen/src/main/ets/SplashScreen'

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

##### Close the launch screen at the appropriate time (e.g., after initialization is complete).
```ets
import SplashScreen from 'react-native-splash-screen';
export default class WelcomePage extends Component {
    componentDidMount() {
        SplashScreen.hide(); // close launch screen
    }
}
```

## Use Codegen

This repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:


Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-splash-screen": "file:../../node_modules/@react-native-oh-tpl/react-native-splash-screen/harmony/splash_screen.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing  SplashScreenPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {SplashScreenPackage} from '@react-native-oh-tpl/react-native-splash-screen/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SplashScreenPackage(ctx)
  ];
}
```

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-splash-screen Releases](https://github.com/react-native-oh-library/react-native-splash-screen/releases)


## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


Name | Description | Type | Required | Platform | HarmonyOS Support
-- | -- | -- | -- | -- | --
show() | 显示启动屏幕(原生方法) | function | Yes | iOS | No  
show(abilityContext: UIAbilityContext, windowStage: window.WindowStage, iconResource: any, backgroundColor: string, pageUrl: string) | 显示启动屏幕(原生方法) | function | Yes | iOS/Android | Yes  
hide() | 隐藏启动屏幕 | function | Yes | iOS/Android | Yes  


> [!TIP] **show(abilityContext: UIAbilityContext, windowStage: window.WindowStage, iconResource: any, backgroundColor: string, pageUrl: string) 方法的参数说明：**

| Name                                                      | Description                                                                                                         | Type     |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- |
| abilityContext | 应用上下文 | UIAbilityContext |
| windowStage | 窗口管理器 | window.WindowStage |
| iconResource | 启动页图片 | Resource |
| backgroundColor | 启动页背景色 | string |
| pageUrl | 首页路由 | bool |

## Known Issues

## Others

在 iOS 中，show() 方法的工作原理是： 在入口 application 方法中，首先加载 App 首页，然后使用 while 循环让界面停留在 App 启动屏，此时首页仍然会异步加载，加载完成后，停止 while 循环即可隐藏启动屏，显示首页。
HarmonyOS 中，在入口 onWindowStageCreate 中调用 windowStage.loadContent 加载首页，如果此时使用 while 循环，首页无法异步加载。

## License

This project is licensed under [The MIT License (MIT)](https://github.com/crazycodeboy/react-native-splash-screen/blob/master/LICENSE).