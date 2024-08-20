> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-material-ripple</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/n4kz/react-native-material-ripple">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/n4kz/react-native-material-ripple/blob/master/license.txt">
        <img src="https://img.shields.io/npm/l/react-native-material-ripple.svg?colorB=448aff" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/n4kz/react-native-material-ripple)

## 安装与使用

进入到工程目录并输入以下命令：


#### **npm**

```bash
npm install react-native-material-ripple@0.9.1
```

#### **yarn**

```bash
yarn add react-native-material-ripple@0.9.1
```

下面的代码展示了这个库的基本使用场景：

```ts
import React, { useState } from "react";
import { Text, ScrollView } from "react-native";
import Ripple from "react-native-material-ripple";

export const MateriaRippleExample = () => {
  const [value1, setValue1] = useState<string>("1");
  const [value2, setValue2] = useState<string>("2");
  const [value3, setValue3] = useState<string>("3");
  const [value4, setValue4] = useState<string>("4");
  const [value5, setValue5] = useState<string>("5");
  const [value6, setValue6] = useState<string>("6");
  const [value7, setValue7] = useState<string>("7");
  const [value8, setValue8] = useState<string>("8");

  return (
    <ScrollView>
      <Ripple rippleColor="rgb(255, 0,0 )">
        <Text style={{ padding: 30 }}>change rippleColor</Text>
      </Ripple>

      <Ripple rippleOpacity={1}>
        <Text style={{ padding: 30 }}>change rippleOpacity</Text>
      </Ripple>

      <Ripple rippleDuration={1000}>
        <Text style={{ padding: 30 }}>change rippleDuration</Text>
      </Ripple>

      <Ripple rippleSize={100}>
        <Text style={{ padding: 30 }}>change rippleSize</Text>
      </Ripple>

      <Ripple
        style={{ borderRadius: 40, backgroundColor: "#0288D1" }}
        rippleContainerBorderRadius={40}
      >
        <Text style={{ padding: 30 }}>change rippleContainerBorderRadius</Text>
      </Ripple>

      <Ripple rippleCentered>
        <Text style={{ padding: 30 }}>change rippleCentered</Text>
      </Ripple>

      <Ripple rippleSequential>
        <Text style={{ padding: 30 }}>change rippleSequential</Text>
      </Ripple>

      <Ripple rippleFades={false}>
        <Text style={{ padding: 30 }}>change rippleFades</Text>
      </Ripple>

      <Ripple disabled>
        <Text style={{ padding: 30 }}>change disabled</Text>
      </Ripple>

      <Ripple onPressIn={() => setValue1("changed")}>
        <Text style={{ padding: 30 }}>onPressIn touch {value1}</Text>
      </Ripple>

      <Ripple delayPressIn={1000} onPressIn={() => setValue2("changed")}>
        <Text style={{ padding: 30 }}>delay onPressIn touch {value2}</Text>
      </Ripple>

      <Ripple onPressOut={() => setValue3("changed")}>
        <Text style={{ padding: 30 }}>onPressOut touch {value3}</Text>
      </Ripple>

      <Ripple delayPressOut={1000} onPressOut={() => setValue4("changed")}>
        <Text style={{ padding: 30 }}>delay onPressOut {value4}</Text>
      </Ripple>

      <Ripple onPress={() => setValue5("changed")}>
        <Text style={{ padding: 30 }}>onPress touch {value5}</Text>
      </Ripple>

      <Ripple onLongPress={() => setValue6("changed")}>
        <Text style={{ padding: 30 }}>onLongPress touch {value6}</Text>
      </Ripple>

      <Ripple delayLongPress={1000} onLongPress={() => setValue7("changed")}>
        <Text style={{ padding: 30 }}>delay onLongPress touch {value7}</Text>
      </Ripple>

      <Ripple onRippleAnimation={() => setValue8("changed")}>
        <Text style={{ padding: 30 }}>onRippleAnimation touch {value8}</Text>
      </Ripple>
    </ScrollView>
  );
};
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25
2. RNOH：0.72.28; SDK：HarmonyOS NEXT Developer Beta3 5.0.0.36; IDE：DevEco Studio 5.0.3.535; ROM：5.0.0.36

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                          | Description                                     | Type     | Required | Platform    | HarmonyOS Support |
| ----------------------------- | ----------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| `rippleColor`                 | Ripple color(default:rgb(0, 0, 0))              | String   | no       | iOS/Android | yes               |
| `rippleOpacity`               | Ripple opacity(default:0.3)                     | Number   | no       | iOS/Android | yes               |
| `rippleDuration`              | Ripple duration in ms(default:400)              | Number   | no       | iOS/Android | yes               |
| `rippleSize`                  | Ripple size restriction(default:0)              | Number   | no       | iOS/Android | yes               |
| `rippleContainerBorderRadius` | Ripple container border radius (default:0)      | Number   | no       | iOS/Android | yes               |
| `rippleCentered`              | Ripple always starts from center(default:false) | Boolean  | no       | iOS/Android | yes               |
| `rippleSequential`            | Ripple should start in sequence(default:false)  | Boolean  | no       | iOS/Android | yes               |
| `rippleFades`                 | Ripple fades out(default:true)                  | Boolean  | no       | iOS/Android | yes               |
| `disabled`                    | Ripple should ignore touches(default:false)     | Boolean  | no       | iOS/Android | yes               |
| `onPressIn`                   | Touch moved in or started callback              | Function | no       | iOS/Android | yes               |
| `onPressOut`                  | Touch moved out or terminated callback          | Function | no       | iOS/Android | yes               |
| `onPress`                     | Touch up inside bounds callback                  | Function | no       | iOS/Android | yes               |
| `onLongPress`                 | Touch delayed after onPressIn callback          | Function | no       | iOS/Android | yes               |
| `onRippleAnimation`           | Animation start callback                        | Function | no       | iOS/Android | yes               |

Other [TouchableWithoutFeedback](https://facebook.github.io/react-native/docs/touchablewithoutfeedback.html) properties will also work

## 遗留问题

## 其他

## 开源协议

本项目基于 [The BSD License (BSD)](https://github.com/n4kz/react-native-material-ripple/blob/master/license.txt) ，请自由地享受和参与开源。

