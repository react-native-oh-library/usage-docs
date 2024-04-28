> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-image-header-scroll-view</code></h1>
</p>
<p align="center">
    <a href="https://github.com/meliorence/react-native-render-html">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/meliorence/react-native-render-html/blob/master/README.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址(v0.10.3)](https://github.com/bamlab/react-native-image-header-scroll-view/tree/0.10.3)  
> 因 v1.0.0 中存在无法触发 TriggeringView 组件回调的问题，以下基于 v0.10.3 版本验证

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-image-header-scroll-view@0.10.3 --save
```

#### **yarn**

```bash
yarn add react-native-image-header-scroll-view@0.10.3
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import { View, TouchableOpacity, Text } from "react-native";
import React from "react";
import HeaderImageScrollView, {
  TriggeringView,
} from "react-native-image-header-scroll-view";

export function ImageHeaderPropertyTest() {
  return (
    <HeaderImageScrollView
      maxHeight={200}
      minHeight={88}
      headerImage={require("./assets/NZ.jpg")}
      renderForeground={() => (
        <View
          style={{
            height: 150,
            justifyContent: "center",
            alignItems: "center",
          }}
        >
          <TouchableOpacity onPress={() => console.log("tap!!")}>
            <Text>Tap Me!</Text>
          </TouchableOpacity>
        </View>
      )}
    >
      <View style={{ height: 800 }}>
        <TriggeringView onHide={() => console.log("text hidden")}>
          <Text>Scroll Me!</Text>
        </TriggeringView>
      </View>
    </HeaderImageScrollView>
  );
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 属性

以下属性已验证，详情见 [react-native-image-header-scroll-view 源库地址](https://github.com/bamlab/react-native-image-header-scroll-view/blob/0.10.3/README.md)

## 其他

- 如何去除图片阴影蒙层？
  可通过设置 maxOverlayOpacity、minOverlayOpacity 属性为 0，去除图片阴影蒙层。
- 如何禁止滑动回弹效果？
  - 方法 1：设置 disableHeaderGrow 属性为 true
  - 方法 2：设置 bounces 属性为 false

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/meliorence/react-native-render-html/blob/master/LICENSE) ，请自由地享受和参与开源。
