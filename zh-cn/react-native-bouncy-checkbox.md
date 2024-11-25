> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-bouncy-checkbox</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/WrathChaos/react-native-bouncy-checkbox">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/WrathChaos/react-native-bouncy-checkbox/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/WrathChaos/react-native-bouncy-checkbox)

## 安装与使用

> [!TIP] 需要配套的服务和三方依赖

| Dependencies                         | Version |
| ------------------------------------ | ------- |
| @freakycoder/react-native-bounceable | 1.0.3   |

本库依赖[@freakycoder/react-native-bounceable文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/freakycoder-react-native-bounceable.md)

#### **npm**

```bash
npm install --save react-native-bouncy-checkbox@4.0.1
```

#### **yarn**

```bash
yarn install --save react-native-bouncy-checkbox@4.0.1
```

下面的代码展示了这个库的基本使用场景：
```js
import React, { useState } from "react";
import { StyleSheet,View,Image } from 'react-native';
import BouncyCheckbox from  "react-native-bouncy-checkbox";

export default function BouncyCheckboxwy () {
  const [checkboxState, setCheckboxState] = React.useState(false);
  return (
  <View style={styles.container}>      
  <BouncyCheckbox
        bounceEffectIn={0.3}
        bounceEffectOut={1}
        bounceVelocityIn={0.5}
        bounceVelocityOut={0.8}
        bouncinessIn={30}
        bouncinessOut={30}
        size={80}
        text="please press me!"
        textStyle={styles.textstyle}
        style={styles.container}
        textContainerStyle={styles.textContainer}
        fillColor={'black'}
        unFillColor={"red"}
        innerIconStyle={{ borderWidth: 5,borderColor:"black"}}
        isChecked={checkboxState}
        iconComponent={
            <Image
              style={{ height: 105, width: 105}}
              source={require("./local-assets/smile.png")}
            />
          }
        onPress={() => setCheckboxState(!checkboxState)}
      />
        </View>
 
  );
};
const styles = StyleSheet.create({
  container: {
    width: '100%',
    height: '100%',
  },
   textContainer:{
    backgroundColor: 'lightblue',
    borderWidth: 5,
    borderColor: 'black',
    padding: 5,
  },
  textstyle: {
    fontSize: 30,
    color: '#010101',
    fontWeight: '600',
    textDecorationLine: "none",
  }
}); 
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证：

1. RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio  5.0.3.404; ROM：5.0.0.31;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name                 | Description                                                  | Type      | Required | Platform | HarmonyOS Support |
| :------------------- | ------------------------------------------------------------ | --------- | -------- | -------- | ----------------- |
| isChecked            | if you want to control check state yourself, you can use `isChecked` prop now! | boolean   | no       | All      | yes               |
| onPress              | set your own onPress functionality after the bounce effect, callback receives the next `isChecked` boolean if disableBuiltInState is false | function  | no       | All      | yes               |
| onLongPress          | set your own onLongPress functionality after the bounce effect, callback receives the next `isChecked` boolean if disableBuiltInState is false | function  | no       | All      | yes               |
| text                 | set the checkbox's text                                      | string    | no       | All      | yes               |
| textComponent        | set the checkbox's text by a React Component                 | component | no       | All      | yes               |
| disableText          | if you want to use checkbox without text, you can enable it  | boolean   | no       | All      | yes               |
| size                 | size of `width` and `height` of the checkbox                 | number    | no       | All      | yes               |
| style                | set/override the container style                             | style     | no       | All      | yes               |
| textStyle            | set/override the text style                                  | style     | no       | All      | yes               |
| iconStyle            | set/override the outer icon container style                  | style     | no       | All      | yes               |
| innerIconStyle       | set/override the inner icon container style                  | style     | no       | All      | yes               |
| fillColor            | change the checkbox's filled color                           | color     | no       | All      | yes               |
| unfillColor          | change the checkbox's un-filled color when it's not checked  | color     | no       | All      | yes               |
| iconComponent        | set your own icon component                                  | component | no       | All      | yes               |
| checkIconImageSource | set your own check icon image                                | image     | no       | All      | yes               |
| textContainerStyle   | set/override the text container style                        | ViewStyle | no       | All      | yes               |
| ImageComponent       | set your own Image component instead of RN's default Image   | component | no       | All      | yes               |
| TouchableComponent   | set/override the main TouchableOpacity component with any Touchable Component like Pressable | component | no       | All      | yes               |
| bounceEffectIn       | change the bounce effect when press in                       | number    | no       | All      | yes               |
| bounceEffectOut      | change the bounce effect when press out                      | number    | no       | All      | yes               |
| bounceVelocityIn     | change the bounce velocity when press in                     | number    | no       | All      | yes               |
| bounceVelocityOut    | change the bounce velocity when press out                    | number    | no       | All      | yes               |
| bouncinessIn         | change the bounciness when press in                          | number    | no       | All      | yes               |
| bouncinessOut        | change the bounciness when press out                         | number    | no       | All      | yes               |

### 

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/WrathChaos/react-native-bouncy-checkbox/blob/master/LICENSE) ，请自由地享受和参与开源。