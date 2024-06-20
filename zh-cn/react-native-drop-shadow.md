<!-- {% raw %} -->
> 模板版本：v0.2.0

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

> [!TIP] [Github 地址](https://github.com/hoanglam10499/react-native-drop-shadow)

## 安装与使用

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

 与 FlatList 一起使用

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

与动画视图一起使用

要使它代替 ，您需要用来创建 的可动画版本。例如：Animated.ViewAnimated.createAnimatedComponentDropShadow。

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
然后，您可以使用`AnimatedDropShadow`来代替`Animated.View` 。

## 约束与限制
- Android 的位图限制为 2048x2048，但这可能取决于 API 版本。
- 使用位图渲染来模拟阴影，如果同时渲染多个阴影和动画，则阴影可能会影响性能。

### 兼容性

本文档内容基于以下版本验证通过：

react-native-harmony: 0.72.23; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.27; ROM: 3.0.0.19;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style  | 设置阴影的样式，可以使用常规的样式属性  | style  | no | Android/IOS  | yes |
| shadowColor  | 设置阴影的颜色，可以使用CSS颜色值或RGBA值  | string  | no | Android/IOS  | yes |
| shadowOffset  | 设置阴影的偏移量  | number  | no | Android/IOS  | yes |
| shadowOpacity  | 设置阴影的不透明度，取值范围为0到1之间，0表示完全透明，1表示完全不透明  | number  | no | Android/IOS  | yes |
| shadowRadius  | 设置阴影的模糊半径，用于控制阴影的模糊程度  | number  | no | Android/IOS  | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/hoanglam10499/react-native-drop-shadow/blob/master/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->