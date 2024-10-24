> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-screenshot-prevent</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/killserver/react-native-screenshot-prevent">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/killserver/react-native-screenshot-prevent/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-screenshot-prevent)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-screenshot-prevent Releases](https://github.com/react-native-oh-library/react-native-screenshot-prevent/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-screenshot-prevent@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-screenshot-prevent@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useEffect } from "react";
import { Alert } from "react-native";
import RNScreenshotPrevent, {
  addListener,
} from "react-native-screenshot-prevent";

RNScreenshotPrevent.enabled(true);

RNScreenshotPrevent.enabled(false);

useEffect(() => {
  const subscription = RNScreenshotPrevent.addListener(() => {
    Alert.alert(
      "You have taken a screenshot of the app.This is prohibited due to security reasons."
    );
  });

  return () => {
    subscription.remove();
  };
}, []);
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

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
    "@react-native-oh-tpl/react-native-screenshot-prevent": "file:../../node_modules/@react-native-oh-tpl/react-native-screenshot-prevent/harmony/react_native_screenshot_prevent.har"
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

### 3. Introducing RNScreenShotPreventPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNScreenShotPreventPackage } from "@react-native-oh-tpl/react-native-screenshot-prevent/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNScreenShotPreventPackage(ctx)
  ];
}
```

### 4. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-screenshot-prevent Releases](https://github.com/react-native-oh-library/react-native-screenshot-prevent/releases)

### Permission Requirements

- 由于此库涉及开启窗口隐私模式，调用对应接口时则需要配置对应的权限，权限需配置在 entry/src/main 目录下 module.json5 文件中。需要打开 `entry/src/main/ets/module.json5`，添加：

```diff
  ...
 "requestPermissions": [
      {
        "name": "ohos.permission.INTERNET"
      },
      {
        "name": "ohos.permission.ACCELEROMETER"
      },
+     {
+        "name": "ohos.permission.PRIVACY_WINDOW"
+     }
    ]
```

## RNScreenshotPrevent

默认导出 RNScreenshotPrevent 对象

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### RNScreenshotPrevent method

| Name              | Description                                                                                                                                                                        | Type     | Required | Platform    | HarmonyOS Support |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| enabled           | Whether to enable the function of disabling screenshot/screen recording                                                                                                            | function | no       | iOS/Android | yes               |
| addListener       | notifies when user has taken screenshot (yes, after taking) - you can show alert or do some actions                                                                                | function | no       | iOS         | yes               |
| enableSecureView  | creates a hidden secureTextField which prevents Application UI capture on screenshots and allow uses imgUri as the source of the background image (can be both https://, file:///) | function | no       | iOS         | no                |
| disableSecureView | remove a hidden secureTextField which prevents Application UI capture on screenshots                                                                                               | function | no       | iOS         | no                |

## Known Issues

- [ ] iOS 支持创建隐藏的安全文本字段，防止应用程序 UI 捕获屏幕截图 [issue#3](https://github.com/react-native-oh-library/react-native-screenshot-prevent/issues/3)
- [ ] iOS 支持创建一个隐藏的安全文本字段，防止应用程序 UI 捕获屏幕截图，并使用 imgUri 作为背景图像的来源（可以是 https://, file:///） [issue#2](https://github.com/react-native-oh-library/react-native-screenshot-prevent/issues/2)
- [ ] iOS 支持移除隐藏的安全文本字段，允许应用程序 UI 捕获屏幕截图 [issue#1](https://github.com/react-native-oh-library/react-native-screenshot-prevent/issues/1)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/killserver/react-native-screenshot-prevent/blob/main/LICENSE).
