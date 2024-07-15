<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-modalbox</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/maxs15/react-native-modalbox">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/maxs15/react-native-modalbox/blob/master/License.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-modalbox)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-modalbox Releases](https://github.com/react-native-oh-library/react-native-modalbox/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-modalbox@file:#
```

#### **yarn**

```bash
yarn add  @react-native-oh-tpl/react-native-modalbox@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import {
  ScrollView,
  Easing,
  View,
  Button,
  Text,
  StyleSheet,
  TextInput,
} from 'react-native';

import React, {useState, useRef} from 'react';

import ModalBox from 'react-native-modalbox';

export const ModalBoxDemo = () => {
  const [isOpenVal, setIsOpenVal] = useState(false);
  const [isOpenVal1, setIsOpenVal1] = useState(false);
  const [isOpenVal2, setIsOpenVal2] = useState(false);
  const [isOpenVal3, setIsOpenVal3] = useState(false);
  const [isOpenVal4, setIsOpenVal4] = useState(false);
  const [isOpenVal5, setIsOpenVal5] = useState(false);
  const [isOpenVal6, setIsOpenVal6] = useState(false);
  const [isOpenVal7, setIsOpenVal7] = useState(false);
  const [isOpenVal8, setIsOpenVal8] = useState(false);
  const [isOpenVal9, setIsOpenVal9] = useState(false);
  const [isOpenVal10, setIsOpenVal10] = useState(false);
  const [isOpenVal11, setIsOpenVal11] = useState(false);
  const [isOpenVal12, setIsOpenVal12] = useState(false);
  const [isOpenVal13, setIsOpenVal13] = useState(false);
  const [isOpenVal14, setIsOpenVal14] = useState(false);
  const [isOpenVal15, setIsOpenVal15] = useState(false);
  const [isOpenVal16, setIsOpenVal16] = useState(false);
  const [isOpenVal17, setIsOpenVal17] = useState(false);
  const [isOpenVal18, setIsOpenVal18] = useState(false);
  const [isOpenVal19, setIsOpenVal19] = useState(false);
  const [isOpenVal20, setIsOpenVal20] = useState(false);
  const [isOpenVal21, setIsOpenVal21] = useState(false);
  const [isOpenVal22, setIsOpenVal22] = useState(false);
  const [isOpenVal23, setIsOpenVal23] = useState(false);
  const [isOpenVal24, setIsOpenVal24] = useState(false);

  const btnRef1 = useRef(null);

  const openModalBox = () => {
    btnRef1.current?.open();
  };
  const closeModalBox = () => {
    btnRef1.current?.close();
  };
  return (
    <ScrollView>
      <View style={styles.body}>
        <Button title="isOpen" onPress={() => setIsOpenVal(!isOpenVal)} />
        <ModalBox style={[styles.modal]} isOpen={isOpenVal} coverScreen={true}>
          <Text style={[styles.modalText]}>Modal is open</Text>
          <Button
            title={'close ModalBox'}
            onPress={() => setIsOpenVal(!isOpenVal)}
          />
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button title="isDisabled" onPress={() => setIsOpenVal1(!isOpenVal1)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal1}
          isDisabled={true}
          coverScreen={true}>
          <Text style={[styles.modalText]}>Modal is isDisabled</Text>
          <Button title={'close ModalBox'} />
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="backdropPressToClose"
          onPress={() => setIsOpenVal2(!isOpenVal2)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal2}
          coverScreen={true}
          backdropPressToClose={true}>
          <Text style={[styles.modalText]}>
            Close the the modal by pressing on the backdrop
          </Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="swipeToClose"
          onPress={() => setIsOpenVal3(!isOpenVal3)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal3}
          coverScreen={true}
          swipeToClose={true}>
          <Text style={[styles.modalText]}>
            Close the the modal by swipe down
          </Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="swipeThreshold"
          onPress={() => setIsOpenVal4(!isOpenVal4)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal4}
          coverScreen={true}
          swipeToClose={true}
          swipeThreshold={10}>
          <Text style={[styles.modalText]}>
            Close the the modal by swipe down 10px
          </Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button title="swipeArea" onPress={() => setIsOpenVal5(!isOpenVal5)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal5}
          coverScreen={true}
          swipeToClose={true}
          swipeArea={20}>
          <Text style={[styles.modalText]}>
            Close the the modal by swipe down swipeArea:20
          </Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="position:center"
          onPress={() => setIsOpenVal6(!isOpenVal6)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal6}
          coverScreen={true}
          backdropPressToClose={true}
          position={'center'}>
          <Text style={[styles.modalText]}>position is center</Text>
        </ModalBox>
        <Button
          title="position:bottom"
          onPress={() => setIsOpenVal7(!isOpenVal7)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal7}
          coverScreen={true}
          backdropPressToClose={true}
          position={'bottom'}>
          <Text style={[styles.modalText]}>position is bottom</Text>
        </ModalBox>
      </View>

      <View style={styles.body}>
        <Button title="entry:top" onPress={() => setIsOpenVal8(!isOpenVal8)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal8}
          coverScreen={true}
          backdropPressToClose={true}
          entry={'top'}>
          <Text style={[styles.modalText]}>entry is top</Text>
        </ModalBox>
        <Button
          title="entry:bottom"
          onPress={() => setIsOpenVal9(!isOpenVal9)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal9}
          coverScreen={true}
          backdropPressToClose={true}
          entry={'bottom'}>
          <Text style={[styles.modalText]}>entry is bottom</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button title="backdrop" onPress={() => setIsOpenVal10(!isOpenVal10)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal10}
          coverScreen={true}
          backdropPressToClose={true}
          backdrop={false}>
          <Text style={[styles.modalText]}>backdrop is false</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="backdropOpacity"
          onPress={() => setIsOpenVal11(!isOpenVal11)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal11}
          coverScreen={true}
          backdropPressToClose={true}
          backdropOpacity={0.5}>
          <Text style={[styles.modalText]}>backdropOpacity: 0.5</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="backdropColor"
          onPress={() => setIsOpenVal12(!isOpenVal12)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal12}
          coverScreen={true}
          backdropPressToClose={true}
          backdropColor={'green'}>
          <Text style={[styles.modalText]}>backdropColor: 'green'</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="backdropContent"
          onPress={() => setIsOpenVal13(!isOpenVal13)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal13}
          coverScreen={true}
          backdropPressToClose={true}
          backdropOpacity={0.5}
          backdropContent={
            <View style={{flex: 1, backgroundColor: 'rgba(0, 0, 0, 0.5)'}}>
              <Text style={{color: 'red', fontSize: 20}}>这是背景内容</Text>
            </View>
          }>
          <Text style={[styles.modalText]}>ModalBoxContent</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="animationDuration"
          onPress={() => setIsOpenVal14(!isOpenVal14)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal14}
          coverScreen={true}
          backdropPressToClose={true}
          animationDuration={1000}>
          <Text style={[styles.modalText]}>animationDuration:1000ms</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button title="easing" onPress={() => setIsOpenVal15(!isOpenVal15)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal15}
          coverScreen={true}
          backdropPressToClose={true}
          easing={ModalBox.easing}>
          <Text style={[styles.modalText]}>easing: 使用预定义的easing函数</Text>
        </ModalBox>
        <Button
          title="easing:custom"
          onPress={() => setIsOpenVal16(!isOpenVal16)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal16}
          coverScreen={true}
          backdropPressToClose={true}
          easing={Easing.elastic(8)}>
          <Text style={[styles.modalText]}>easing: 自定义easing函数</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="startOpen"
          onPress={() => setIsOpenVal18(!isOpenVal18)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal18}
          coverScreen={true}
          backdropPressToClose={true}
          startOpen={true}
          onClosed={() => console.log('Modal closed')}
          onOpened={() => console.log('Modal opened')}
          onClosingState={() => console.log('Modal closing state changed')}>
          <Text style={[styles.modalText]}>startOpen is true</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="coverScreen"
          onPress={() => setIsOpenVal19(!isOpenVal19)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal19}
          coverScreen={true}
          backdropPressToClose={true}>
          <Text style={[styles.modalText]}>coverScreen is true</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="keyboardTopOffset"
          onPress={() => setIsOpenVal20(!isOpenVal20)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal20}
          coverScreen={true}
          keyboardTopOffset={10}
          position={'bottom'}
          backdropPressToClose={true}>
          <Text style={[styles.modalText]}>keyboardTopOffset: 50</Text>
          <TextInput
            placeholder="text"
            placeholderTextColor="#9a73ef"
            autoCapitalize="none"
          />
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button
          title="useNativeDriver"
          onPress={() => setIsOpenVal21(!isOpenVal21)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal21}
          coverScreen={true}
          easing={Easing.elastic(8)}
          useNativeDriver={true}
          backdropPressToClose={true}>
          <Text style={[styles.modalText]}>useNativeDriver is true</Text>
        </ModalBox>
      </View>
      <View style={styles.body}>
        <Button title="onOpened" onPress={() => setIsOpenVal22(!isOpenVal22)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal22}
          coverScreen={true}
          onOpened={()=>console.log('...onOpened')}>
          <Text style={[styles.modalText]}>onOpened</Text>
        </ModalBox>
      </View>

      <View style={styles.body}>
        <Button title="onClosed" onPress={() => setIsOpenVal23(!isOpenVal23)} />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal23}
          coverScreen={true}
          onClosed={()=>console.log('...onClosed')}>
          <Text style={[styles.modalText]}>onClosed</Text>
        </ModalBox>
      </View>

      <View style={styles.body}>
        <Button
          title="onClosingState"
          onPress={() => setIsOpenVal24(!isOpenVal24)}
        />
        <ModalBox
          style={[styles.modal]}
          isOpen={isOpenVal24}
          coverScreen={true}
          onClosingState={()=>console.log('...onClosingState')}>
          <Text style={[styles.modalText]}>onClosingState</Text>
        </ModalBox>
      </View>

      <View style={styles.body}>
        <Button title="open" onPress={openModalBox} />
        <Button title="close" onPress={closeModalBox} />
        <ModalBox ref={btnRef1} style={[styles.modal]} coverScreen={true}>
          <Text style={[styles.modalText]}>ModalBox open</Text>
        </ModalBox>
      </View>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  input: {},
  modal: {
    height: 300,
    width: 300,
    justifyContent: 'center',
    alignItems: 'center',
  },
  modalText: {
    fontSize: 20,
    margin: 10,
    color: 'black',
  },
  module: {
    margin: 15,
  },
  moduleName: {
    fontSize: 25,
    fontWeight: '700',
    marginBottom: 4,
    color: '#fff',
  },
  moduleContent: {
    fontSize: 16,
    fontWeight: '500',
    marginBottom: 4,
    color: '#fff',
  },
  moduleButton: {
    backgroundColor: 'deepskyblue',
    height: 34,
  },
  buttonText: {
    fontSize: 18,
    fontWeight: '400',
    color: '#fff',
    textAlign: 'center',
    lineHeight: 32,
    verticalAlign: 'middle',
  },
  body: {},
});
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-modalbox Releases](https://github.com/react-native-oh-library/react-native-modalbox/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                 |                         Description                          |      Type      | Required |  Platform   | HarmonyOS Support |
| :------------------- | :----------------------------------------------------------: | :------------: | :------: | :---------: | :---------------: |
| isOpen               | Open/close the modal, optional, you can use the open/close methods instead |     `bool`     |    no    | iOS/Android |        yes        |
| isDisabled           |     Disable any action on the modal (open, close, swipe)     |     `bool`     |    no    | iOS/Android |        yes        |
| backdropPressToClose |       Close the the modal by pressing on the backdrop        |     `bool`     |    no    | iOS/Android |        yes        |
| swipeToClose         |    Set to true to enable the swipe down to close feature     |     `bool`     |    no    | iOS/Android |        yes        |
| swipeThreshold       |     The threshold to reach in pixels to close the modal      |    `number`    |    no    | iOS/Android |        yes        |
| swipeArea            | The height in pixels of the swipeable area, window height by default |    `number`    |    no    | iOS/Android |        yes        |
| position             |   Control the modal position using top or center or bottom   |    `string`    |    no    | iOS/Android |        yes        |
| entry                |        Control the modal entry position top or bottom        |    `string`    |    no    | iOS/Android |        yes        |
| backdrop             |             Display a backdrop behind the modal              |     `bool`     |    no    | iOS/Android |        yes        |
| backdropOpacity      |                   Opacity of the backdrop                    |    `number`    |    no    | iOS/Android |        yes        |
| backdropColor        |               backgroundColor of the backdrop                |    `string`    |    no    | iOS/Android |        yes        |
| backdropContent      | Add an element in the backdrop (a close button for example)  | `ReactElement` |    no    | iOS/Android |        yes        |
| animationDuration    |                  Duration of the animation                   |    `number`    |    no    | iOS/Android |        yes        |
| easing               |      Easing function applied to opening modal animation      |   `function`   |    no    | iOS/Android |        yes        |
| backButtonClose      | (Android only) Close modal when receiving back button event  |     `bool`     |    no    |   Android   |        no         |
| startOpen            | Allow modal to appear open without animation upon first mount |     `bool`     |    no    | iOS/Android |        yes        |
| coverScreen          | Will use RN Modal component to cover the entire screen wherever the modal is mounted in the component hierarchy |     `bool`     |    no    | iOS/Android |        yes        |
| keyboardTopOffset    | This property prevent the modal to cover the ios status bar when the modal is scrolling up because the keyboard is opening |    `number`    |    no    | iOS/Android |        yes        |
| useNativeDriver      | Enables the hardware acceleration to animate the modal. Please note that enabling this can cause some flashes in a weird way when animating |     `bool`     |    no    | iOS/Android |        yes        |
| onClosed       |                                          When the modal is close and the animation is done                                           | `function` |    no    | iOS/Android |        yes        |
| onOpened       |                                           When the modal is open and the animation is done                                           | `function` |    no    | iOS/Android |        yes        |
| onClosingState | When the state of the swipe to close feature has changed (usefull to change the content of the modal, display a message for example) | `function` |    no    | iOS/Android |        yes        |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name  |   Description   |    Type    | Required |  Platform   | HarmonyOS Support |
| :---- | :-------------: | :--------: | :------: | :---------: | :---------------: |
| open  | Open the modal  | `function` |    no    | iOS/Android |        yes        |
| close | Close the modal | `function` |    no    | iOS/Android |        yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/maxs15/react-native-modalbox/blob/master/License.txt) ，请自由地享受和参与开源。

<!-- {% endraw %} -->
