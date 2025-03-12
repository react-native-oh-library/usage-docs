> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-theme-control</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vonovak/react-native-theme-control">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vonovak/react-native-theme-control/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-theme-control)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-theme-control/Releases](https://github.com/react-native-oh-library/react-native-theme-control/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-theme-control
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-theme-control
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import { Text, useColorScheme, View } from 'react-native';
import {
    setThemePreference,
    SystemBars,
    ThemePreference,
    useThemePreference,
} from '@vonovak/react-native-theme-control';
// @ts-ignore
import SegmentedControl from '@react-native-segmented-control/segmented-control/js/SegmentedControl.js';

export function SimpleScreen() {
    const colorScheme = useColorScheme();
    const isDarkMode = colorScheme === 'dark';
    const themePreference = useThemePreference();
    const bgColor = isDarkMode ? '#2A2550' : '#FFF6EA';
    const textColor = isDarkMode ? 'white' : 'black';
    const barsBackground = isDarkMode ? '#9900F0' : '#A0BCC2';
    const dividerColor = textColor;
    const textColorStyle = { color: textColor };
    const values: Array<ThemePreference> = ['light', 'dark', 'system'];
    return (
        <View
    style={{
        backgroundColor: bgColor,
        flexGrow: 1,
        flexShrink: 1,
        alignItems: 'center',
        justifyContent: 'space-evenly',
    }}
>
<SystemBars
backgroundColor={barsBackground}
dividerColor={dividerColor}
/>
    <SegmentedControl
style={{ width: '100%' }}
values={values}
selectedIndex={values.indexOf(themePreference)}
onChange={({ nativeEvent }: { nativeEvent: any }) => {
    setThemePreference(nativeEvent.value as ThemePreference);
}}
/>
    <Text style={textColorStyle}>useColorScheme(): {colorScheme}</Text>
    <Text style={textColorStyle}>
useThemePreference(): {themePreference}
</Text>
    </View>
);
}
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-theme-control": "file:../../node_modules/@react-native-oh-tpl/react-native-theme-control/harmony/themecontrol.har",

  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.在 ArkTs 侧引入 RNThemeControlPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNThemeControlPackage } from '@react-native-oh-tpl/react-native-theme-control/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNThemeControlPackage(ctx)
  ];
}
```

### 4.在 entry/src/main/ets/abilityStage 新建 MyAbilityStage.ets

打开 `entry/src/main/ets/abilityStage/MyAbilityStage.ets`，添加：

```diff
import appRecovery from '@ohos.app.ability.appRecovery';
import AbilityStage from '@ohos.app.ability.AbilityStage';
import { Want } from '@kit.AbilityKit';

export default class MyAbilityStage extends AbilityStage {
  onCreate() {
      appRecovery.enableAppRecovery(
      appRecovery.RestartFlag.ALWAYS_RESTART,
      appRecovery.SaveOccasionFlag.SAVE_WHEN_ERROR,
      appRecovery.SaveModeFlag.SAVE_WITH_FILE
    );

    let wantObj: Want = {
      bundleName: 'com.rnoh.tester',
      abilityName: 'EntryAbility'
    };

    appRecovery.setRestartWant(wantObj)
  }
}
```

### 5.在 entry/src/main/ets/entryability/EntryAbility.ets 配置生命周期调用

打开 `entry/src/main/ets/entryability/EntryAbility.ets`，添加：

```diff
+ import {RNAbility} from 'rnoh';
+ import Want from '@ohos.app.ability.Want';
+ import { RNThemeControlModule } from '@react-native-oh-tpl/react-native-theme-control';

+  export default class EntryAbility extends RNAbility {
+    onCreate(want: Want): void {
+    super.onCreate(want);
+    RNThemeControlModule.recoverApplicationTheme(this.context);
+   }
  getPagePath() {
    return 'pages/Index';
  }
}
```

打开 `entry/src/main/module.json5`，添加：

```diff
"module": {
    "name": "entry",
+   "srcEntry": "./ets/abilityStage/MyAbilityStage.ets",
    "type": "entry",
    .....

"abilities": [
  {
    "name": "EntryAbility",
     .....
     "visible": true,
+    "recoverable": true,
     .....
```

### 6.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-theme-control Releases](https://github.com/react-native-oh-library/react-native-theme-control/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description                                                                                                                                               | Type       | Required | Platform    | HarmonyOS Support |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | -------- | ----------- | ----------------- |
| SystemBars          | Setting the System Status Bar                                                                                                                             | Components | No       | IOS/Android | Yes               |
| NavigationBar       | Setting the Navigation Bar                                                                                                                                | Components | No       | Android     | No                |
| AppBackground       | Sets the background color of the UIApplication window (iOS) or the current Activity (Android).                                                            | Components | No       | IOS/Android | Yes               |
| setNavbarAppearance | Set the appearance of the navigation bar imperatively                                                                                                     | Function   | No       | Android     | No                |
| setAppBackground    | Set background color                                                                                                                                      | Function   | No       | IOS/Android | Yes               |
| setThemePreference  | Set the theme                                                                                                                                             | Function   | No       | IOS/Android | Yes               |
| getThemePreference  | Get Subject                                                                                                                                               | Function   | No       | IOS/Android | Yes               |
| useThemePreference  | A React hook that returns the current theme preference, which might be dark, light (if you have set the theme before by calling setAppearance) or system. | Function   | No       | IOS/Android | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/vonovak/react-native-theme-control/blob/main/LICENSE) ，请自由地享受和参与开源。
