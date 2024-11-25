> 模板版本：v0.2.2

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

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-root-modal Releases](https://github.com/react-native-oh-library/react-native-root-modal/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-root-modal
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-root-modal
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import React, {
    StyleSheet,
    Text,
    View,
    TouchableHighlight,
} from 'react-native';

import Modal from 'react-native-root-modal';
import { Component } from 'react';

const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: '#fff'
    },
    button: {
        backgroundColor: '#ccc',
        borderRadius: 5,
        padding: 10,
    },
    modal: {
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: 'rgba(58, 93, 15, 0.8)',
        borderRadius: 40,
        height: '80%',
        width: '80%',
        bottom: 100,
        flex: 1,
        position: 'absolute',
    },
    close: {
        position: 'absolute',
        width: 20,
        height: 20,
        borderRadius: 10,
        justifyContent: 'center',
        alignItems: 'center',
        right: 20,
        top: 40,
        backgroundColor: 'red'
    },
    modalContainer: {
        height: 100,
        width: 200,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: 'blue',
        margin: 50
    },
    text: {
        color: '#fff'
    }
});

class CustomStyleDemo extends Component{
    constructor() {
        super(...arguments);
        this.state = {
            visible: false
        };
    }

    showModal = () => {
        this.setState({
            visible: true
        });
    };

    hideModal = () => {
        this.setState({
            visible: false
        });
    };

    render() {
        return <View style={styles.container}>
             <TouchableHighlight
                style={styles.button}
                underlayColor="#aaa"
                onPress={this.showModal}
            >
                <Text>Show Modal</Text>
            </TouchableHighlight>
            <Modal style={styles.modal} visible={this.state.visible}>
                <TouchableHighlight
                    style={[styles.button, styles.close]}
                    underlayColor="#aaa"
                    onPress={this.hideModal}
                >
                    <Text>X</Text>
                </TouchableHighlight>

                <View style={styles.modalContainer}>
                    <Text style={styles.text}>You can custom your own Modal style</Text>
                </View>
            </Modal>
        </View>;
    }

}

export default CustomStyleDemo;
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-root-modal Releases](https://github.com/react-native-oh-library/react-native-root-modal/releases)


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

react-native-root-modal组件接收所有[React Native View](https://reactnative.dev/docs/view#props)组件的Props.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| visible  | 控制模态框是否可见  | boolean  | no | Android/iOS  | yes |
| style  | 设置modal的样式，可以使用常规的样式属性  | style  | no | Android/iOS  | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/magicismight/react-native-root-modal/blob/master/LICENSE) ，请自由地享受和参与开源。
