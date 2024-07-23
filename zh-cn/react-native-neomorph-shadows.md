<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-neomorph-shadows</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/tokkozhin/react-native-neomorph-shadows">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/tokkozhin/react-native-neomorph-shadows/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-neomorph-shadows)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-neomorph-shadows Releases](https://github.com/react-native-oh-library/react-native-neomorph-shadows/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-neomorph-shadows@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-neomorph-shadows@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React from 'react';
import { View, StyleSheet, Text } from 'react-native';
import { Shadow } from 'react-native-neomorph-shadows';

export default function () {
    return (
        <View style={styles.container}>
            <Shadow
                style={{
                    // shadowOffset: { width: 0, height: 5 },
                    fillOpacity: 0.6,
                    // borderRadius: 25,
                    stopColor:"#f0f0f0",//渐变结束的颜色
                    startColor:"#FF3A3A",//渐变开始的颜色
                    width: 110,
                    height: 110,
                    alignItems: "center",
                    justifyContent: "center"
                }}>
                <View
                    style={{
                        borderRadius: 25,
                        backgroundColor: "#FF3A3A",
                        width: 110,
                        height: 44,
                        alignItems: "center",
                        justifyContent: "center",
                        // shadowColor: "#FFC0C0",
                        // shadowOffset: {
                        //     width: 0,
                        //     height: 20
                        // },
                        // shadowOpacity: 1,
                        // shadowRadius: 3.84,
                        // elevation: 5 // 添加阴影效果
                    }}>
                    <Text
                        style={{
                            color: "#ffffff",
                            fontWeight: "bold",
                            textAlign: "center",
                            fontSize: 16
                        }}>
                        登录/注册
                    </Text>
                </View>
            </Shadow>
        </View>
    );
};

const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: '#f0f0f0',
    },
});


```
## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档](/zh-cn/react-native-svg-capi.md)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-neomorph-shadows Releases](https://github.com/react-native-oh-library/react-native-neomorph-shadows/releases)

## 属性

### 此组件有以下属性:
## **API（Shadow）**
>[!tip] "Platform"列表示该属性在原三方库上支持的平台。

>[!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|     **style**      |       Style object        |                         Object                           |    No    | iOS/Android |        Yes        |
|        **fillOpacity**        |                   shadow transparency                    |                         String                           |    YES   | iOS/Android |        Yes        |
|     **stopColor**      |                  Shadow Gradient End Color              |                         String                           |    No    | iOS/Android |        Yes        |
| **startColor**  |       Shadow Gradient Start Color       |                         String                           |    No    | iOS/Android |        Yes        |


## 遗留问题

目前仅设计Shadow组件阴影效果。Neomorph组件暂未涉及。[issue#5](https://github.com/react-native-oh-library/react-native-neomorph-shadows/issues/5)

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/tokkozhin/react-native-neomorph-shadows/blob/master/LICENSE) ，请自由地享受和参与开源。 
<!-- {% endraw %} -->