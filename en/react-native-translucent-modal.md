> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-translucent-modal</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/23mf/react-native-translucent-modal">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/23mf/react-native-translucent-modal/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-translucent-modal)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-translucent-modal Releases](https://github.com/react-native-oh-library/react-native-translucent-modal/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-translucent-modal
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-translucent-modal
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import { View, TouchableWithoutFeedback, Image, Button, StyleSheet } from "react-native-harmony";
// @ts-expect-error
import Modal from "react-native-translucent-modal";

const STYLES = StyleSheet.create({
    wrapper: {
        flex: 1,
    },
    imageBackground: {
        width: 300,
        height: 200,
    }
});

export const E_ReactNativeTranslucentModal: React.FC = (): JSX.Element => {

    const [transparent, setTransparent] = useState(false)
    const [visible, setVisible] = useState(false)
    const [animationType, setAnimationType] = useState('none')

    return <View style={STYLES.wrapper}>
        <Modal transparent={transparent} animationType={animationType}
            visible={visible} onRequestClose={() => setVisible(!visible)}>
            <TouchableWithoutFeedback onPress={() => setVisible(false)}>
             {/* 注意：1、此图片组件为示例，需要根据自己的项目需求，去引入对应组件；
                2、示例图片地址需要根据自己的项目情况去引入 */}
                <Image source={{ uri: "https://hbimg.huabanimg.com/ed258f740ab675e3b3a0b6e7abc44eb7bd832c523396b-cJL1G9_fw658"}} style={STYLES.imageBackground} />
            </TouchableWithoutFeedback>
        </Modal>
        <Button title="显示Modal" onPress={() => setVisible(true)}></Button>
        <Button title="设置transparent为true" onPress={() => setTransparent(true)}></Button>
        <Button title="设置animationType为'slide'" onPress={() => setAnimationType('slide')}></Button>
        <Button title="设置animationType为'fade'" onPress={() => setAnimationType('fade')}></Button>
    </View>;
}

```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-translucent-modal Releases](https://github.com/react-native-oh-library/react-native-translucent-modal/releases)

Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> [!tip] react-native提供的Modal组件，在HarmonyOS、iOS平台一样可以实现状态栏沉浸式效果。

| Name                          | Description                                         | Type     | Required | Platform | HarmonyOS Support |
| ----------------------------- | --------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `animationType`               | Animation type of modal.                            | string   | yes      | All      | yes               |
| `transparent`                 | Whether the background of the modal is transparent. | boolean  | yes      | All      | yes               |
| `visible`                     | Controls whether the modal is displayed.            | boolean  | yes      | All      | yes               |
| `onRequestClose?: () => void` | Called when the model request close.                | function | yes      | ALL      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/23mf/react-native-translucent-modal/blob/master/LICENSE.md).
