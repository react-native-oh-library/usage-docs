> Template version: v0.2.2

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

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-root-modal)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-root-modal Releases](https://github.com/react-native-oh-library/react-native-root-modal/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

### Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-root-modal Releases](https://github.com/react-native-oh-library/react-native-root-modal/releases)


## Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

react-native-root-modal is compatible with all properties of [React Native View](https://reactnative.dev/docs/view#props).

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| visible  | 控制模态框是否可见  | boolean  | no | Android/iOS  | yes |
| style  | 设置modal的样式，可以使用常规的样式属性  | style  | no | Android/iOS  | yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/magicismight/react-native-root-modal/blob/master/LICENSE).
