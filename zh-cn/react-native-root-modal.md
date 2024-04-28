> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-root-modal</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/magicismight/react-native-root-modal">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/magicismight/react-native-root-modal/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-root-modal)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-root-modal Releases](https://github.com/react-native-oh-library/react-native-root-modal/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-root-modal@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-root-modal@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

Import library any where inside your code before `AppRegistry.registerComponent` is called.

```
import Modal, { AnimatedModal, ModalManager } from 'react-native-root-modal';
```

Invoked by `React element` way.

```
....other elements before
<Modal
    style={{
        top: 0,
        right: 0,
        bottom: 0,
        left: 0,
        backgroundColor: 'rgba(0, 0, 0, 0.2)',
        transform: [{scale: this.state.scaleAnimation}]
    }}

    visible={this.state.modalVisible}
>
    ... You can add anything inside
</Modal>
....other elements after

```

Just put `<Modal />` element anywhere, And it will be front of other elements.
And you can set `<Modal />` element\`s style or other properties inherited from `<View />` element


Or you can invoke it by `JavaScript class` way

Import modal Manager class.
```
import { ModalManager } from 'react-native-root-modal';

```

Invoke it.
```
// Create a Modal element on screen.
let modal = new ModalManager(<View style={modal container style}>
    ...modal contents here.
</View>);

// Update (replace) the modal element which is already existed.
modal.update(<View style={modal container style}>
    ...other modal contents here.
</View>);

// Destroy it
modal.destroy();
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-root-modal Releases](https://github.com/react-native-oh-library/react-native-root-modal/releases)

本文档内容基于以下版本验证通过：

RNOH: 0.72.23; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.27; ROM: 3.0.0.19;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| visible  | 控制模态框是否可见  | boolean  | no | Android/IOS  | yes |
| style  | 设置modal的样式，可以使用常规的样式属性  | style  | no | Android/IOS  | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/magicismight/react-native-root-modal/blob/master/LICENSE) ，请自由地享受和参与开源。
