> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-theme-switch-animation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/WadhahEssam/react-native-theme-switch-animation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/WadhahEssam/react-native-theme-switch-animation/blob/main/README.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-theme-switch-animation)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-theme-switch-animation Releases](https://github.com/react-native-oh-library/react-native-theme-switch-animation/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-theme-switch-animation
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-theme-switch-animation
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import { StyleSheet, View, Button, Text } from 'react-native';
import switchTheme from 'react-native-theme-switch-animation';

export function ReactNativeThemeSwitchAnimationDemo() {
  const [theme, setTheme] = React.useState('light');
  
  return (
      <View
        style={{
          ...styles.container,
          backgroundColor: theme === 'light' ? 'white' : 'black',
        }}
      >
        <View
          style={{
            borderWidth: 1,
            borderColor: theme === 'light' ? 'black' : 'white',
            borderRadius: 1.4,
            padding: 50,
          }}
        >
          <Text
            style={{
              color: theme === 'light' ? 'black' : 'white',
            }}
          >
            tests
          </Text>
        </View>

        <View style={{ marginTop: 10 }}>
          <Button
            title="start"
            onPress={() => {
              switchTheme({
                switchThemeFunction: () => {
                  setTheme(theme === 'light' ? 'dark' : 'light');
                },
                animationConfig: {
                  type: 'inverted-circular',
                  duration: 2000,
                  startingPoint: {
                    cxRatio: 0.5,
                    cyRatio: 0.5,
                  },
                },
              });
            }}
          />
        </View>
      </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  box: {
    width: 60,
    height: 60,
    marginVertical: 20,
  },
});

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

    "@react-native-oh-tpl/react-native-theme-switch-animation": "file:../../node_modules/@react-native-oh-tpl/react-native-theme-switch-animation/harmony/react_native_theme_switch.har"
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
### 3.在 ArkTs 侧引入 RNThemeSwitch Package

打开 `entry/src/main/ets/RNPackagesFactory.ets`，添加：

```diff
...
+ import { RNThemeSwitchPackage } from "@react-native-oh-tpl/react-native-theme-switch-animation/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNThemeSwitchPackage(ctx),
  ];
}

```
### 4.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 注意事项

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-safe-area-context的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入react-native-safe-area-context请参照[@react-native-oh-tpl/react-native-safe-area-context 文档](/zh-cn/react-native-safe-area-context.md)进行引入

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-theme-switch-animation Releases](https://github.com/react-native-oh-library/react-native-theme-switch-animation/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**switchTheme Function Props**

| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `switchThemeFunction`  |Adds the function you use in your app to switch themes, doesn't matter if you use redux/context/zustand/mobx or any other way |  () => void | no     | All  | yes      |
| `animationConfig`  | Configuration for the animation -> type, duration, starting point | AnimationConfig |  no     | All   | yes      |

**animationConfig options**

| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `type`  | Specifies animation type | fade circular inverted-circular |  no     | All   | yes      |
| `duration`  | Specifies duration in milliseconds | number |  no     | All   | yes      |
| `startingPoint`  | Configuration for the circular animation, where does the animation start in the screen | 	StartingPointConfig |  no     | All   | yes      |

**startingPoint options**

| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `cx`  | Specifies starting x point for circular and inverted-circular animation (should not exceed your screen width) |number|  no     | All   | yes      |
| `cy`  | Specifies starting y point for circular and inverted-circular animation (should not exceed your screen height) |number|  no     | All   | yes      |
| `cxRatio`  | Specifies starting percentage of x point for circular and inverted-circular animation (should be number between -1 and 1) |number|  no     | All   | yes      |
| `cyRatio`  | Specifies starting percentage of y point for circular and inverted-circular animation (should be number between -1 and 1) |number|  no     | All   | yes      |

## 遗留问题

- [ ] circular动画效果动画开始前有一个闪屏的问题，后续需要提供在图片上剪裁出一个圆形，透过圆形可以看到下方节点的接口或方法。[issue#6](https://github.com/react-native-oh-library/react-native-theme-switch-animation/issues/6)

## 其他

## 开源协议
本项目基于 [The MIT License (MIT)](https://github.com/WadhahEssam/react-native-theme-switch-animation/blob/main/LICENSE) ，请自由地享受和参与开源。