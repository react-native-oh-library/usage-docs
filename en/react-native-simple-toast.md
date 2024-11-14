> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-simple-toast</code></h1>
</p>
<p align="center">
    <a href="https://github.com/vonovak/react-native-simple-toast">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vonovak/react-native-simple-toast/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-simple-toast)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-simple-toast Releases](https://github.com/react-native-oh-library/react-native-simple-toast/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-simple-toast
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-simple-toast
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from 'react';

import {
  StyleSheet,
  View,
  Button,
  Alert,
  TextInput,
  ScrollView,
  Pressable,
  Modal,
  Text,
} from 'react-native';
import Toast from 'react-native-simple-toast';
import { useState } from 'react';

export default function App() {
  const [modalVisible, setModalVisible] = useState(false);

  return (
    <>
      <Modal
        animationType="slide"
        transparent={true}
        visible={modalVisible}
        onRequestClose={() => {
          Alert.alert('Modal has been closed.');
          setModalVisible(!modalVisible);
        }}
      >
        <View style={styles.centeredView}>
          <View style={styles.modalView}>
            <Text style={styles.modalText}>Hello World!</Text>
            <Pressable
              style={[styles.button, styles.buttonClose]}
              onPress={() => setModalVisible(!modalVisible)}
            >
              <Text style={styles.textStyle}>Hide Modal</Text>
            </Pressable>
          </View>
        </View>
      </Modal>

      <ScrollView
        keyboardDismissMode={'on-drag'}
        keyboardShouldPersistTaps={'always'}
        automaticallyAdjustKeyboardInsets
        style={{ backgroundColor: 'white' }}
      >
      <View style={styles.container}>
        <Button
          title={'simple toast'}
          onPress={() => {
            Toast.show('This is a toast.', Toast.SHORT);
          }}
      />
      <Button
      title={'tap to dismiss toast'}
      onPress={() => {
        Toast.show('Tap to dismiss toast.', Toast.LONG, {
        tapToDismissEnabled: true,
      });
    }}
  /> 
    </View>
    </ScrollView> 
  </>
  );
}
```
## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

This document is verified based on the following versions:

1. RNOH：0.72.23; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.19

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name                                                         | Description                                                 | Required | Platform | HarmonyOS Support |
| ------------------------------------------------------------ | ----------------------------------------------------------- | -------- | -------- | ----------------- |
| show(message, duration, options)                             | show toast                                                  | No       | All      | partially         |
| showWithGravity(message, duration, gravity, options)         | Toast that can be set to top, bottom, and center positions. | No       | All      | No                |
| showWithGravityAndOffset(message,duration,gravity,xOffset,yOffset,options,); | Toast that can be set with x-axis and y-axis offsets.       | No       | All      | No                |


## Properties 

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description      | Type             | Required |   HarmonyOS Support  |
| ---- |------------------|------------------| -------- |  ------------------ |
|LONG  | Toast Display Duration: LONG | number           | / | yes|
|SHORT | Toast Display Duration: SHORT | number | / | yes|
|TOP | Toast Display Position:TOP | number | / | no|
|BOTTOM | Toast Display Position: BOTTOM | number | / | no|
|CENTER | Toast Display Position: CENTER | number | / | no|

## Known Issues
- [ ]  Does not support modifying font, background color in HarmonyOS [issue#3](https://github.com/react-native-oh-library/react-native-simple-toast/issues/3)
- [ ]  The Toast component in the RNOH framework does not support setting position or offset. [issue#2](https://github.com/react-native-oh-library/react-native-simple-toast/issues/2)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/vonovak/react-native-simple-toast/blob/master/LICENSE).