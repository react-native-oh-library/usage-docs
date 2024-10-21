> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-drop-shadow</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/hoanglam10499/react-native-drop-shadow">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/hoanglam10499/react-native-drop-shadow/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/hoanglam10499/react-native-drop-shadow)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-drop-shadow@1.0.0
```

#### **yarn**

```bash
yarn add react-native-drop-shadow@1.0.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import DropShadow from "react-native-drop-shadow";
```

```js
export default function usage() {
  return (
    <DropShadow
      style={{
        shadowColor: "#000",
        shadowOffset: {
          width: 0,
          height: 0,
        },
        shadowOpacity: 1,
        shadowRadius: 5,
      }}
    >
      ...
    </DropShadow>
  );
}
```

 Usage with `FlatList`

```js
export default function withFlatList() {
  return (
    <FlatList
      data={[""]}
      keyExtractor={(item, index) => "List-" + index}
      CellRendererComponent={DropShadow} // <==== add line
      renderItem={({ item, index }) => (
        <DropShadow
          style={{
            shadowColor: "#000",
            shadowOffset: {
              width: 0,
              height: 0,
            },
            shadowOpacity: 1,
            shadowRadius: 5,
          }}
        >
          ...
        </DropShadow>
      )}
    />
  );
}
```

Usage with `Animated.View`

To make this work in place of an `Animated.View`, you need to use `Animated.createAnimatedComponent` to create an animatable version of `DropShadow`. For example: Animated.ViewAnimated.createAnimatedComponentDropShadow

```js
const AnimatedDropShadow = Animated.createAnimatedComponent(DropShadow);

export default function withAnimatedViews() {
  return (
    <AnimatedDropShadow
      style={{
        shadowColor: "#000",
        shadowOffset: {
          width: 0,
          height: 0,
        },
        shadowOpacity: 1,
        shadowRadius: 5,
      }}
    >
      ...
    </AnimatedDropShadow>
  );
}
```
You can then use `AnimatedDropShadow` in place of `Animated.View`.

## Constraints
- Android 的位图限制为 2048x2048，但这可能取决于 API 版本。
- 使用位图渲染来模拟阴影，如果同时渲染多个阴影和动画，则阴影可能会影响性能。

### Compatibility

This document is verified based on the following versions:

react-native-harmony: 0.72.23; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.27; ROM: 3.0.0.19;

react-native-harmony: 0.72.33; SDK: Openharmony 5.0.0.71(API Version 12 Release); IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style  | 设置阴影的样式，可以使用常规的样式属性  | style  | no | Android/IOS  | yes |
| shadowColor  | 设置阴影的颜色，可以使用CSS颜色值或RGBA值  | string  | no | Android/IOS  | yes |
| shadowOffset  | 设置阴影的偏移量  | number  | no | Android/IOS  | yes |
| shadowOpacity  | 设置阴影的不透明度，取值范围为0到1之间，0表示完全透明，1表示完全不透明  | number  | no | Android/IOS  | yes |
| shadowRadius  | 设置阴影的模糊半径，用于控制阴影的模糊程度  | number  | no | Android/IOS  | yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/hoanglam10499/react-native-drop-shadow/blob/master/LICENSE).