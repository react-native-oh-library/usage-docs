> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-material-design-styles</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/binggg/react-native-material-design-styles">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/binggg/react-native-material-design-styles)



## 安装与使用



<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-material-design-styles@0.2.7 --save
```
#### **yarn**

```bash
yarn add react-native-material-design-styles@0.2.7
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：




```js
import { StyleSheet, Text, View, ScrollView } from 'react-native';
import { typography, color } from 'react-native-material-design-styles';
const typographyStyle = StyleSheet.create(typography);
const colorStyle = StyleSheet.create(color);
export function MetailDesignColor() {
    return (
        <View style={{ flex: 1, backgroundColor: "#fff" }}>
            <ScrollView>
                <Text style={[typographyStyle.paperFontHeadline, colorStyle.paperTeal500]}>Typography</Text>
                <Text style={[typographyStyle.paperFontDisplay4]}>Display4</Text>
                <Text style={typographyStyle.paperFontDisplay3}>Display3</Text>
                <Text style={typographyStyle.paperFontDisplay2}>Display2</Text>
                <Text style={typographyStyle.paperFontDisplay1}>Display1</Text>
                <Text style={typographyStyle.paperFontHeadline}>Headline</Text>
                <Text style={typographyStyle.paperFontTitle}>Title</Text>
                <Text style={typographyStyle.paperFontSubhead}>Subhead</Text>
                <Text style={typographyStyle.paperFontBody2}>Body2</Text>
                <Text style={typographyStyle.paperFontBody1}>Body1</Text>
                <Text style={typographyStyle.paperFontCaption}>Caption</Text>
                <Text style={typographyStyle.paperFontButton}>Button</Text>
                <Text style={typographyStyle.paperFontCode2}>Code2</Text>
                <Text style={typographyStyle.paperFontCode1}>Code1</Text>

                <Text style={[typographyStyle.paperFontHeadline, colorStyle.paperTeal500]}>Text Color</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPink500]}>paperPink500</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPink50]}>paperPink50</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPink100]}>paperPink100</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPink200]}>paperPink200</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPink300]}>paperPink300</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPink400]}>paperPink400</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPink500]}>paperPink500</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPink600]}>paperPink600</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPink700]}>paperPink700</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPink800]}>paperPink800</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPink900]}>paperPink900</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPinkA100]}>paperPinkA100</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPinkA200]}>paperPinkA200</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPinkA400]}>paperPinkA400</Text>
                <Text style={[typographyStyle.paperFontTitle, colorStyle.paperPinkA700]}>paperPinkA700</Text>

                <View style={[styles.colorItem, { backgroundColor: color.paperBlue500.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlue50.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlue100.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlue200.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlue300.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlue400.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlue500.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlue600.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlue700.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlue800.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlue900.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlueA200.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlueA400.color }]}></View>
                <View style={[styles.colorItem, { backgroundColor: color.paperBlueA700.color }]}></View>
            </ScrollView>
        </View>
    )
}

const styles = StyleSheet.create({
    colorItem: {
        height: 50
    }
})
```


## 约束与限制

### 兼容性


本文档内容基于以下版本验证通过：


1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;



## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| typography  | use StyleSheet.create(typography)        | function  | yes | iOS/android      | yes |
| color  | use color.paperBlue500.color        | function  | yes | iOS/android      | yes |
| defaultTheme  | use StyleSheet.create(defaultTheme)         | function  | yes | iOS/android      | yes |
## 遗留问题



## 其他

## 开源协议

本项目基于 [MIT License (MIT)](https://www.mit-license.org/) ，请自由地享受和参与开源。


