> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-size-matters</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/nirsky/react-native-size-matters">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/nirsky/react-native-size-matters/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/nirsky/react-native-size-matters)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-size-matters@0.4.2
```
#### **yarn**

```bash
yarn add react-native-size-matters@0.4.2
```
<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：
> [!WARNING] 使用时 import 的库名不变。

**这里是该插件提供的基础用法**

```js
<!---->
<!-- 方法 -->
import { Text, View } from 'react-native';
import { scale, verticalScale, moderateScale, moderateVerticalScale } from 'react-native-size-matters';
<!-- 别名方法 -->
import { s, vs, ms, mvs } from 'react-native-size-matters';

let scale = () =>{
    return (
        <View style={{
            width: scale(100),
            height: 100,
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{scale(100}</Text>
        </View>
    )
}

let verticalScale = () =>{
    return (
        <View style={{
            width: 100,
            height: verticalScale(100),
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{verticalScale(100}</Text>
        </View>
    )
}

let moderateScale = () =>{
    return (
    <View style={{
        width: 100,
        height: 100,
        padding: 5,
        borderWidth:moderateScale(10),
        borderColor: 'red',
        backgroundColor: 'blue'
    }} >
        <Text>borderWidth{moderateScale(10)}</Text>
    </View>
    )
}


let moderateVerticalScale = ()=>{
    return (
        <View style={{
            width: 100,
            height: moderateVerticalScale(100),
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{moderateVerticalScale(100}</Text>
        </View>
    )
}

let s = () =>{
    return (
        <View style={{
            width: s(100),
            height: 100,
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{s(100}</Text>
        </View>
    )
}

let vs = () =>{
    return (
        <View style={{
            width: 100,
            height: vs(100),
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{vs(100}</Text>
        </View>
    )
}

let ms = () =>{
    return (
    <View style={{
        width: 100,
        height: 100,
        padding: 5,
        borderWidth:ms(10),
        borderColor: 'red',
        backgroundColor: 'blue'
    }} >
        <Text>borderWidth{ms(10)}</Text>
    </View>
    )
}


let mvs = ()=>{
    return (
        <View style={{
            width: 100,
            height: mvs(100),
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{mvs(100}</Text>
        </View>
    )
}

export default class sizeMattersDemo {
  render() {
    return (
        <>
            <Scale />
            <VerticalScale />
            <ModerateScale />
            <ModerateVerticalScale />
            <S />
            <Vs />
            <Ms />
            <Mvs />
        </>
    );
  }
}

```
**这里提供注解用法**
```javascript
import { Text, View } from 'react-native';
import { ScaledSheet } from 'react-native-size-matters';

const styles = ScaledSheet.create({
    container: {
        width: '100@s', // = scale(100)
        height: '200@vs', // = verticalScale(200)
        padding: '2@msr', // = Math.round(moderateScale(2))
        margin: 5
    }
});

export default class sizeMattersDemo {
  render() {
    return (
        <View style={styles.container} >
            <Text>调用create方法</Text>
        </View>
    );
  }
}
```
 [!TIP] 这里展示[自定义默认尺寸](https://github.com/nirsky/react-native-size-matters/blob/master/examples/change-guideline-sizes.md)

## 约束与限制
### 兼容性
本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                   | Description                                                                                                                  | Type                      | Required | Platform    |  HarmonyOS Support |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------- | -------- | ----------- | -------- |
| scale    | 将根据您设备的屏幕宽度返回所提供尺寸的线性缩放结果。                                                                                                 | Function       | No       | Android、iOS | Yes      |
| verticalScale    | 将根据您设备的屏幕高度返回所提供尺寸的线性缩放结果。                                                                                                 | Function       | No       | Android、iOS | Yes      |
| moderateScale    | 有时您不想以线性方式缩放所有内容，这时可以使用 moderateScale。它的妙处在于您可以控制调整大小的因子（默认值为 0.5）。如果正常缩放会将您的尺寸增加 +2X，则 moderateScale 只会将其增加 +X                                                                                                 | Function       | No       | Android、iOS | Yes      |
| moderateVerticalScale    | 与 moderateScale 相同，但使用 verticalScale 而不是 scale。                                                                                                 | Function       | No       | Android、iOS | Yes      |
| s    | scale方法的别名                                                                                                 | Function       | No       | Android、iOS | Yes      |
| vs    | verticalScale方法的别名                                                                                          | Function       | No       | Android、iOS | Yes      |
| ms    | moderateScale别名方法                                                                                               | Function       | No       | Android、iOS | Yes      |
| mvs     | moderateVerticalScale的别名方法                                                                                                 | Function       | No       | Android、iOS | Yes      |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License(MIT)](https://github.com/nirsky/react-native-size-matters/blob/master/LICENSE) ，请自由地享受和参与开源。
