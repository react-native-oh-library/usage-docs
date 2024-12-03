> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-root-toast</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/magicismight/react-native-root-toast">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/magicismight/react-native-root-toast/blob/master/LICENSE.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/magicismight/react-native-root-toast)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-root-toast@3.5.1
```

#### **yarn**

```bash
yarn add react-native-root-toast@3.5.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!TIP] 在react native >= 0.62中，新的LogBox组件会影响Toast组件的初始化。要使其工作，我们必须在应用程序中显式插入一个挂载点，挂载点推荐使用 [`react-native-root-siblings`](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-root-siblings.md) 如下所示：

```js
import React, { useState } from "react";
import { View,Button } from "react-native";
import Toast from "react-native-root-toast";
import { RootSiblingParent } from 'react-native-root-siblings';

export function ReactNativeRootToastExample() {
  let PToast: any = null;
  function startPToast() {
    PToast = Toast.show("超长待机弹窗实例", {
      duration: 99999999,
      position: 20,
      shadow: true,
      animation: true,
      hideOnPress: false,
      delay: 0,
      onHidden: () => {
        PToast.destroy();
        PToast = null;
      },
    });
  }

  function hidePToast() {
    Toast.hide(PToast);
  }
  return (
    <RootSiblingParent> // <- use RootSiblingParent to wrap your root component
      <Button title="开一个弹窗" onPress={startPToast} />
      <Button title="关掉这个弹窗" onPress={hidePToast} />
    </RootSiblingParent>
  );
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20-CAPI; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                                                                           | Type     | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| duration        | Toast.durations.SHORT Number The duration of the toast. (Only for api calling method) | Number   | no       | All      | yes               |
| visible         | The visibility of toast. (Only for Toast Component)                                   | Bool     | no       | All      | yes               |
| position        | The position of toast showing on screen (A negative number represents the distance from the bottom of screen. A positive number represents the distance form the top of screen.)| Number   | no       | All      | yes               |
| animation       | Should preform an animation on toast appearing or disappearing.                       | Bool     | no       | All      | yes               |
| shadow          | Should drop shadow around Toast element.                                              | Bool     | no       | All      | yes               |
| backgroundColor | The background color of the toast.                                                    | string   | no       | All      | yes               |
| shadowColor     | The shadow color of the toast.                                                        | string   | no       | All      | yes               |
| textColor       | The text color of the toast.                                                          | string   | no       | All      | yes               |
| delay           | The delay duration before toast start appearing on screen.                            | Number   | no       | All      | yes               |
| hideOnPress     | Should hide toast that appears by pressing on the toast.                              | Bool     | no       | All      | yes               |
| opacity         | The Toast opacity.                                                                    | Number   | no       | All      | yes               |
| onShow          | Callback for toast`s appear animation start                                           | function | no       | All      | yes               |
| onShown         | Callback for toast`s appear animation end                                             | function | no       | All      | yes               |
| onHide          | Callback for toast`s hide animation start                                             | function | no       | All      | yes               |
| onHidden        | Callback for toast`s hide animation end                                               | function | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/magicismight/react-native-root-toast/blob/master/LICENSE.txt) ，请自由地享受和参与开源。