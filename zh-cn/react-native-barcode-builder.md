> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-barcode-builder</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wonsikin/react-native-barcode-builder">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wonsikin/react-native-barcode-builder/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-apache-green.svg" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>





> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-barcode-builder)

## 安装与使用
1、库依赖的@react-native-community/art停止维护，与 HarmonyOS 侧不兼容，需引入@react-native-oh-tpl/react-native-svg 的原生端代码，请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](/zh-cn/react-native-svg.md#link)进行引入。

2、请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-barcode-builder](https://github.com/react-native-oh-library/react-native-barcode-builder/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-barcode-builder@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-barcode-builder@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

<!-- {% raw %} -->
```js
import React, { useEffect } from 'react';
import {
    StyleSheet,
    View,
    Text,
} from 'react-native';
import Barcode from "react-native-barcode-builder";
import {
    Colors,
} from 'react-native/Libraries/NewAppScreen';
export const BarcodeBuilderExample = () => {
    const styles = StyleSheet.create({
        scrollView: {
            backgroundColor: Colors.lighter,
        },
        body: {
            backgroundColor: Colors.white,
        },
        sectionContainer: {
            marginTop: 32,
            paddingHorizontal: 24,
        },
    });
    useEffect(() => {

    }, [])
    const error = (e) => {
        console.log(e, "click")
    }
    return (
        <View style={{
            flex: 1,
            justifyContent: "center",
            alignItems: "center",
            backgroundColor: "#F5FCFF"
        }} >

            <Text style={{ fontSize: 50 }} >
                This is a Barcode Builder
            </Text>
            <Barcode
                value=" hello~~~" //条形码扫描结果
                format="CODE128"  //条形码编码类型
                text="hello world" //条形码下方字体
                // textColor='red'  //条形码下方字体颜色
                // lineColor='blue' //条形码颜色
                // background="red"  //条形码背景颜色
                onError={error}  //扫描失败回调
                width={5} // 条形码单条宽度
                height={200}  //条形码单条高度
            />;

        </View>
    )
}

```
<!-- {% endraw %} -->

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](/zh-cn/react-native-svg.md#link)进行引入





## 约束与限制

### 兼容性


1、RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 4.1.3.700; ROM: 3.0.0.19;


## 属性
### Barcode 
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。
> 
> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

该库为UI组件库，通过配置属性标签，实现对应的功能。

| Name        |  Type       |Description  |Required |Platform      | HarmonyOS Support |
| ----------- | -------------------------------------------------- | ------------  |-----------------|------- |-----|
| value        |string|What the barcode stands for.  |yes      |IOS/Android| yes               |
|format     |string | Which barcode type to use.     [learn more](https://github.com/lindell/JsBarcode#supported-barcodes) | no |IOS/Android     | yes               |
| width   |number| Width of a single bar.       |no | IOS/Android|yes               |
| height |number|Height of the barcode.   |no   | IOS/Android     | yes               |
| text        |string| Override text that is displayed.    |no    | IOS/Android   | yes               |
| lineColor        |string| Color of the bars.    |no   |IOS/Android    | yes               |
| textColor        |string| Color of the text.    |no   |IOS/Android    | yes               |
|background       |string| Background color of the barcode.   |no   | IOS/Android|yes               |
|onError      |function| Handler for invalid barcode of selected format.   |no   |IOS/Android| yes               |


## 开源协议

本项目基于 [The Apache License (Apache)](https://github.com/wonsikin/react-native-barcode-builder/blob/master/LICENSE) ，请自由地享受和参与开源。

