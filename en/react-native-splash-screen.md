> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-splash-screen</code> </h1>
</p>

This project is based on [react-native-splash-screen@3.3.0](https://github.com/crazycodeboy/react-native-splash-screen).

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-splash-screen`, The version correspondence details are as follows:

| Version                   | Package Name                                      | Repository         | Release                    |
|---------------------------| ------------------------------------------------- | ------------------ | -------------------------- |
| <= 3.3.0-0.0.2@deprecated | @react-native-oh-tpl/react-native-splash-screen | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-splash-screen) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-splash-screen/releases) |
| > 3.3.0                   | @react-native-ohos/react-native-splash-screen   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-splash-screen) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-splash-screen/releases) |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.


##### **Create a launch page `SplashScreenPage.ets` in the entry/src/main/ets/pages directory**

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

##### **Add `pages/SplashScreenPage` in entry/src/resources/base/profile/main_pages.json**
```json
{
  "src": [
    "pages/SplashScreenPage"
  ]
}
```

##### **Open the `entry/src/main/ets/entryability/EntryAbility.ets` file and add the following code:**
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

##### Close the launch screen at the appropriate time (e.g., after initialization is complete).
```ets
import SplashScreen from 'react-native-splash-screen';
export default class WelcomePage extends Component {
    componentDidMount() {
        SplashScreen.hide(); // close launch screen
    }
}
```

## 2. Manual Link

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1. Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2. Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/react-native-splash-screen": "file:../../node_modules/@react-native-ohos/react-native-splash-screen/harmony/splash_screen.har"
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

### 2.3. Configuring CMakeLists and Introducing SplashScreenPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-splash-screen/src/main/cpp" ./splash_screen))
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_splash_screen)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "SplashScreenPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<SplashScreenPackage>(ctx),
    };
}
```

### 2.4. Introducing  SplashScreenPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 2.5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1. Compatibility

Check the release version information in the release address of the third-party library: [@react-native-ohos/react-native-splash-screen Releases](https://gitee.com/openharmony-sig/rntpc_react-native-splash-screen/releases)

## 4. API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name                                                                                                                                 | Description | Type | Required | Platform | HarmonyOS Support|
|--------------------------------------------------------------------------------------------------------------------------------------| ----- | ----- | ----- | ----- | -----|
|show()                                                                                                                               | 显示启动屏幕(原生方法) | function | Yes | iOS | No  |
|show(abilityContext: UIAbilityContext, windowStage: window.WindowStage, iconResource: any, backgroundColor: string, pageUrl: string) | 显示启动屏幕(原生方法) | function | Yes | iOS/Android | Yes  |
| hide()                                                                                                                               | 隐藏启动屏幕 | function | Yes | iOS/Android | Yes | 


> [!TIP] **show(abilityContext: UIAbilityContext, windowStage: window.WindowStage, iconResource: any, backgroundColor: string, pageUrl: string) 方法的参数说明：**

| Name                                                      | Description                                                                                                         | Type     |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- |
| abilityContext | 应用上下文 | UIAbilityContext |
| windowStage | 窗口管理器 | window.WindowStage |
| iconResource | 启动页图片 | Resource |
| backgroundColor | 启动页背景色 | string |
| pageUrl | 首页路由 | bool |

## 5. Known Issues

## 6. Others

- 在 iOS 中，show() 方法的工作原理是： 在入口 application 方法中，首先加载 App 首页，然后使用 while 循环让界面停留在 App 启动屏，此时首页仍然会异步加载，加载完成后，停止 while 循环即可隐藏启动屏，显示首页。
HarmonyOS 中，在入口 onWindowStageCreate 中调用 windowStage.loadContent 加载首页，如果此时使用 while 循环，首页无法异步加载。

## 7.License

This project is licensed under [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-splash-screen/blob/master/LICENSE).