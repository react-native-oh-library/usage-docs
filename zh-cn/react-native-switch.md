> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-switch</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/shahen94/react-native-switch">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/shahen94/react-native-switch/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/shahen94/react-native-switch)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-switch@1.5.1
```

#### **yarn**

```bash
yarn add react-native-switch@1.5.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { Switch } from "react-native-switch";
import {SafeAreaView, StyleSheet,Button, Text, View, Alert} from 'react-native';


export function SwitchDemo(){
  const [isEnabled, setIsEnabled] = useState(false);
  const toggleSwitch = (val:boolean) => {setIsEnabled(val) };
  
  return(
    <View  style={styles.container}>
      <Text style={{fontSize:32}}>Welcome to React Native !</Text>
      <Switch
        value={isEnabled}
        onValueChange={(val) => toggleSwitch((val))}
        disabled={false}
        activeText={'On'}
        inActiveText={'Off'}
        circleSize={30}
        barHeight={30}
        circleBorderWidth={3}
        backgroundActive={'green'}
        backgroundInactive={'gray'}
        circleActiveColor={'#30a566'}
        circleInActiveColor={'#fff'}
        renderInsideCircle={() => ''} // custom component to render inside the Switch circle (Text, Image, etc.)
        changeValueImmediately={true} // if rendering inside circle, change state immediately or wait for animation to complete
        innerCircleStyle={{ alignItems: "center", justifyContent: "center" }} // style for inner animated circle for what you (may) be rendering inside the circle
        outerCircleStyle={{ }} // style for outer animated circle
        renderActiveText={true}
        renderInActiveText={true}
        switchLeftPx={2} // denominator for logic when sliding to TRUE position. Higher number = more space from RIGHT of the circle to END of the slider
        switchRightPx={2} // denominator for logic when sliding to FALSE position. Higher number = more space from LEFT of the circle to BEGINNING of the slider
        switchWidthMultiplier={3} // multiplied by the `circleSize` prop to calculate total width of the Switch
        switchBorderRadius={50} // Sets the border Radius of the switch slider. If unset, it remains the circleSize.
      />
      <Text style={{color:'gray',fontSize:20,marginBottom:10}}>To get started,edit index.harmony.js</Text>
      <Text style={{color:'gray',fontSize:20}}>Press Cmd +R to reload,</Text>
      <Text style={{color:'gray',fontSize:20}}>Cmd+D or shake for dev menu</Text>
    </View>
    )
  }
  const styles = StyleSheet.create({
    container: {
      flex: 1,
      alignItems: "center",
      justifyContent: "center",
      backgroundColor:"#fff",
      
    }
  });
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 Yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|        Name        |                         Description                          |        Type         | Required |  Platform   | HarmonyOS Support |
| :----------------: | :----------------------------------------------------------: | :-----------------: | :------: | :---------: | :---------------: |
|     onValueChange      |     when to change value(value: `boolean`)    | function |    No    | Android/IOS |        Yes        |
|       disabled        |          Display or not         |       boolean       |    No    | Android/IOS |        Yes        |
|      activeText       | active text |   string  |    No    | Android/IOS |        Yes        |
|     inActiveText      |         in Active Text    |      string      |    No    | Android/IOS |        Yes        |
|     backgroundActive      | background active |      string      |    No    | Android/IOS |        Yes        |
|      backgroundInactive      | background in active |   string   |    No    | Android/IOS |        Yes        |
|      value       | swtich value |  boolean   |    No    | Android/IOS |        Yes        |
|      circleActiveColor       | circle active color |      string       |    No    | Android/IOS |        Yes        |
|    circleInActiveColor     | circle in active color |      string       |    No    | Android/IOS |        Yes        |
|       circleSize        | circle Size|  number  |    No    | Android/IOS |        Yes        |
|     circleBorderWidth     | circle Border Width |      number |    No    | Android/IOS |        Yes        |
|     circleBorderActiveColor     | circle Border Active Color|      string |    No    | Android/IOS |        Yes        |
|     circleBorderInactiveColor      |circle Border Inactive Color |       string       |    No    | Android/IOS |        Yes        |
| activeTextStyle |active Text Style | StyleProp`<TextStyle> ` | No | Android/IOS | Yes |
| inactiveTextStyle |in Active Text Style | StyleProp`<TextStyle> ` | No | Android/IOS | Yes |
| containerStyle |container Styl | StyleProp`<ViewStyle> ` | No | Android/IOS | Yes |
| barHeight |Bar Height | number | No | Android/IOS | Yes |
| renderInsideCircle |custom component to render inside the Switch circle | function | No | Android/IOS | Yes |
| changeValueImmediately |if rendering inside circle, change state immediately or wait for animation to complete | boolean | No | Android/IOS | Yes |
| innerCircleStyle |style for inner animated circle for what you (may) be rendering inside the circle | StyleProp`<ViewStyle> ` | No | Android/IOS | Yes |
| outerCircleStyle |style for outer animated circle | StyleProp`<ViewStyle> ` | No | Android/IOS | Yes |
| renderActiveText |render Active Text | boolean | No | Android/IOS | Yes |
| renderInActiveText |render In Active Text | boolean | No | Android/IOS | Yes |
| switchLeftPx |denominator for logic when sliding to TRUE position. Higher number = more space from RIGHT of the circle to END of the slider | number | No | Android/IOS | Yes |
| switchRightPx |multiplied by the `circleSize` prop to calculate total width of the Switch | number | No | Android/IOS | Yes |
| switchWidthMultiplier |multiplied by the `circleSize` prop to calculate total width of the Switch | number | No | Android/IOS | Yes |
| switchBorderRadius |Sets the border Radius of the switch slider. If unset, it remains the circleSize | number | No | Android/IOS | Yes |
| testID |swtich test ID | string | No | Android/IOS | Yes |
## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/shahen94/react-native-switch/blob/master/LICENSE) ，请自由地享受和参与开源。
