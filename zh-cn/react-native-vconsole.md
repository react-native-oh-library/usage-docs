> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-vconsole</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/kafudev/react-native-vconsole">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/kafudev/react-native-vconsole/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/kafudev/react-native-vconsole)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @kafudev/react-native-vconsole@0.1.11
```

#### **yarn**

```bash
yarn add @kafudev/react-native-vconsole@0.1.11
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js

import React from 'react';
import { StyleSheet, View } from 'react-native';
import Vconsole from '@kafudev/react-native-vconsole';

export const ConsoleDemo = () => {
    return (
        <View style={styles.container}>
            <PropsType />
        </View>
    );
};

function PropsType() {
    const appInfo = {
        原生构建类型: "1",
        原生版本号: "ConfigReader.VERSION_NAME",
        原生构建时间: "ConfigReader.BUILD_TIME",
        热更新版本号: "codePushStore.info.label",
        热更新详情: "codePushStore.info.desc"
    }

    return (
        <View style={styles.container1}>
            <Vconsole appInfo={appInfo} console={true} showBtn={true} />
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        position: 'absolute', // 绝对定位
        bottom: 180, // 底部边界与父容器底部对齐
        width: '100%',
        height: 200,
        borderWidth: 1,
        button: 0
    },
    container1: {
        width: '100%',
        height: 200,
        borderWidth: 1,
        paddingVertical: 20,
        button: 0
    },
    box: {
        width: 60,
        height: 60,
    },
});
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.29; SDK：HarmonyOS-Next-DB6 5.0.0.61; IDE：DevEco Studio 5.0.3.706; ROM：3.0.0.65;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name    | Description                              | Type    | Required | Platform | HarmonyOS Support |
| ------- | ---------------------------------------- | ------- | -------- | -------- | ----------------- |
| appInfo | Customized Version Info you want to show | json    | no       | All      | yes               |
| console | Whether to show console                  | boolean | no       | All      | yes               |
| showBtn | Whether to show buttons                  | boolean | no       | All      | yes               |
| panels  | Custom panels                            | json    | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/kafudev/react-native-vconsole/blob/main/LICENSE) ，请自由地享受和参与开源
