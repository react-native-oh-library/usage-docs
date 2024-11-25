> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-animatable</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/oblador/react-native-animatable">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/oblador/react-native-animatable/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/oblador/react-native-animatable)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-animatable@1.4.0
```

#### **yarn**

```bash
yarn add react-native-animatable@1.4.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { useState } from "react";
import { TouchableOpacity } from "react-native";
import * as Animatable from "react-native-animatable";

export default function ExampleView() {
  const [textFontSize, setTextFontSize] = useState(10);
  return (
    <Animatable.View style={{ padding: 50, backgroundColor: "#333333" }}>
      <Animatable.Text
        animation="slideInDown"
        iterationCount={5}
        direction="reverse"
        style={{ color: "white", textAlign: "center" }}
        duration={2000}
        onAnimationBegin={() => {
          console.log("test onAnimationBegin");
        }}
        onAnimationEnd={() => {
          console.log("test onAnimationEnd");
        }}
      >
        Up and down you go
      </Animatable.Text>
      <Animatable.Text
        animation="bounce"
        easing="ease-out"
        iterationCount="infinite"
        iterationDelay={1500}
        style={{ textAlign: "center" }}
        useNativeDriver={true}
        isInteraction={true}
      >
        ❤️
      </Animatable.Text>
      <Animatable.Text
        animation="fadeIn"
        delay={2000}
        style={{ textAlign: "center", marginTop: 50, color: "white" }}
      >
        (*^▽^*)
      </Animatable.Text>
      <TouchableOpacity onPress={() => setTextFontSize(textFontSize + 5)}>
        <Animatable.Text
          transition="fontSize"
          style={{
            textAlign: "center",
            marginTop: 50,
            color: "white",
            fontSize: textFontSize || 10,
          }}
          onTransitionBegin={() => {
            console.log("test onTransitionBegin");
          }}
          onTransitionEnd={() => {
            console.log("test onTransitionEnd");
          }}
        >
          O(∩_∩)O哈哈~
        </Animatable.Text>
      </TouchableOpacity>
    </Animatable.View>
  );
}
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1 B.0.18； IDE: DevEco Studio 5.0.3.200; ROM: 2.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                                                                                                     | Type                   | Required | Platform | HarmonyOS Support |
| ----------------- | --------------------------------------------------------------------------------------------------------------- | ---------------------- | -------- | -------- | ----------------- |
| animation         | 动画的名称，请参见下面的可用动画                                                                                | string/undefined       | /        | all      | yes               |
| duration          | 动画将运行的时间（毫秒）                                                                                        | number/undefined       | /        | all      | yes               |
| delay             | （可选）延迟动画（毫秒）                                                                                        | number/undefined       | /        | all      | yes               |
| direction         | 动画的方向，特别适用于重复动画。有效值: 正常、反向、交替、交替反向                                              | string/undefined       | /        | all      | yes               |
| easing            | 动画的计时功能。有效值: 自定义函数或线性、易进、易出、易入                                                      | string/undefined       | /        | all      | yes               |
| iterationCount    | 运行动画的次数，对于循环动画使用无穷大。                                                                        | number/undefined       | /        | all      | yes               |
| iterationDelay    | 关于动画迭代之间的暂停时间（毫秒）                                                                              | number/undefined       | /        | all      | yes               |
| transition        | 要转换的样式属性，例如不透明度、旋转或字体大小。对多个属性使用数组。                                            | string/array/undefined | /        | all      | yes               |
| onAnimationBegin  | 启动动画时调用的函数。                                                                                          | Function/undefined     | /        | all      | yes               |
| onAnimationEnd    | 当动画成功完成或取消时调用的函数。函数是用 endState 参数调用的，请参阅 endState.finished 以查看动画是否已完成。 | Function/undefined     | /        | all      | yes               |
| onTransitionBegin | 在样式转换开始时调用的函数。使用属性参数调用函数以区分样式。                                                    | Function/undefined     | /        | all      | yes               |
| onTransitionEnd   | 当样式转换成功完成或取消时调用的函数。使用属性参数调用函数以区分样式。                                          | Function/undefined     | /        | all      | yes               |
| useNativeDriver   | 是否使用本机或 JavaScript 动画驱动程序。本机驱动程序可以帮助提高性能，但不能处理所有类型的样式。                | Function/undefined     | /        | all      | yes               |
| isInteraction     | 此动画是否在交互管理器上创建“交互控制柄”。                                                                      | Boolean                | /        | all      | yes               |

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/oblador/react-native-animatable/blob/master/LICENSE).
