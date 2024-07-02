<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-modalbox</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/maxs15/react-native-modalbox">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/maxs15/react-native-modalbox/blob/master/License.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/maxs15/react-native-modalbox)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-modalbox@2.0.2
```

#### **yarn**

```bash
yarn add react-native-modalbox@2.0.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js

import React from 'react';
import Modal from 'react-native-modalbox';

import { TestSuite, Tester, TestCase } from '@rnoh/testerino';
import {
  Text,
  Button,
  StyleSheet,
  ScrollView,
  View,
  Dimensions,
  Easing,
  TextInput
} from 'react-native';

var screen = Dimensions.get('window');

export default class ModalBoxExample extends React.Component<any, any> {

  constructor(props:any) {
    super(props);
    this.state = {
      isOpen: false,
      isDisabled: false,
      swipeToClose: true,
      sliderValue: 0.3
    };
  }


  onClose() {
    console.log('Modal just closed');
  }
  animalEase(){
    Easing.elastic(8)
  }

  onOpen() {
    console.log('Modal just opened');
  }

  onClosingState(state:any) {
    console.log('the open/close of the swipeToClose just changed');
  }

  renderList() {
    var list = [];

    for (var i=0;i<50;i++) {
      list.push(<Text style={styles.text} key={i}>Elem {i}</Text>);
    }

    return list;
  }

  render() {
    var BContent = (
      <View style={[styles.btn, styles.btnModal]}>
        <Button title="X" color="white" onPress={() => this.setState({isOpen: false})}/>
      </View>
    );

    return (
      <Tester>
        <TestSuite name='ModalTesteDemo'>
          <TestCase itShould='Basic modal' tags={['C_API']}>
            <Button title="Basic modal" onPress={() =>this.refs.modal1.open()} />
            <Modal
              style={[styles.modal, styles.modal2]}
              ref={'modal1'}
              swipeToClose={this.state.swipeToClose}
              onClosed={this.onClose}
              onOpened={this.onOpen}
              animationDuration={4000}
              easing={Easing.elastic(8)}
              onClosingState={this.onClosingState}>
                <Text style={styles.text}>Basic modal</Text>
                <Button title={`Disable swipeToClose(${this.state.swipeToClose ? "true" : "false"})`} onPress={() => this.setState({swipeToClose: !this.state.swipeToClose})} />
            </Modal>
          </TestCase>
          <TestCase itShould='Position top' tags={['C_API']}>
            <Button title="Position top" onPress={() =>this.refs.modal2.open()} />
            <Modal style={[styles.modal, styles.modal2]} startOpen={true} backdrop={false}  position={"top"} ref={"modal2"}>
              <Text style={[styles.text, {color: "white"}]}>Modal on top</Text>
            </Modal>
          </TestCase>
          <TestCase itShould='Position centered + backdrop + disable' tags={['C_API']}>
            <Button title="Position centered + backdrop + disable" onPress={() =>this.refs.modal3.open()} />
            <Modal style={[styles.modal, styles.modal3]} position={"center"} ref={"modal3"} isDisabled={this.state.isDisabled}>
              <Text style={styles.text}>Modal centered</Text>
              <Button title={`Disable (${this.state.isDisabled ? "true" : "false"})`} onPress={() => this.setState({isDisabled: !this.state.isDisabled})} />
            </Modal>
          </TestCase>
          <TestCase itShould='Position bottom + backdrop' tags={['C_API']}>
            <Button title="Position bottom + backdrop " onPress={() => this.refs.modal4.open()} />
            <Modal style={[styles.modal, styles.modal4]} position={"bottom"} ref={"modal4"}>
              <Text style={styles.text}>Modal on bottom with backdrop</Text>
            </Modal>
          </TestCase>
          <TestCase itShould='Backdrop + backdropContent' tags={['C_API']}>
            <Button title="Backdrop + backdropContent" onPress={() => this.setState({isOpen: true})} />
            <Modal isOpen={this.state.isOpen} coverScreen={false} onClosed={() => this.setState({isOpen: false})} style={[styles.modal, styles.modal4]} position={"center"} backdropPressToClose={false} backdropContent={BContent} backdropColor={'red'} backdropOpacity={0.2}>
              <Text style={styles.text}>Modal with backdrop content</Text>
            </Modal>
          </TestCase>
          <TestCase itShould='Position bottom + ScrollView' tags={['C_API']}>
            <Button title="Position bottom + ScrollView" onPress={() => this.refs.modal6.open()} />
            <Modal style={[styles.modal, styles.modal4]} position={"bottom"} ref={"modal6"} swipeArea={20} swipeThreshold={10}>
              <ScrollView>
                <View style={{width: screen.width, paddingLeft: 10}}>
                  {this.renderList()}
                </View>
              </ScrollView>
            </Modal>
          </TestCase>
          <TestCase itShould='Modal with keyboard support' tags={['C_API']}>
            <Button title="Modal with keyboard support" onPress={() => this.refs.modal7.open()} />
            <Modal ref={"modal7"} style={[styles.modal, styles.modal4]} position={"center"}>
              <View>
                <TextInput style={{height: 50, width: 200, backgroundColor: '#DDDDDD'}}/>
              </View>
            </Modal>
          </TestCase>
          <TestCase itShould='Entry from top' tags={['C_API']}>
            <Button title="Entry from top" onPress={() => this.refs.modal8.open()} />
            <Modal ref={"modal8"} style={[styles.modal, styles.modal2]} position={"top"} entry={"top"}>
              <Text style={[styles.text, {color: "white"}]}>Modal entry from top</Text>
            </Modal>
          </TestCase>
        </TestSuite>
      </Tester>
    );
  }

}

const styles = StyleSheet.create({

  wrapper: {
    paddingTop: 50,
    flex: 1
  },

  modal: {
    justifyContent: 'center',
    alignItems: 'center'
  },

  modal2: {
    height: 230,
    backgroundColor: "#3B5998"
  },

  modal3: {
    height: 300,
    width: 300
  },

  modal4: {
    height: 300
  },

  btn: {
    margin: 20,
    backgroundColor: "#3B5998",
    color: "white",
    padding: 10
  },

  btnModal: {
    position: "absolute",
    top: 0,
    right: 0,
    width: 50,
    height: 50,
    backgroundColor: "transparent"
  },

  text: {
    color: "black",
    fontSize: 22
  }

});
```




## 约束与限制

### 兼容性
要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机ROM。

本文档内容基于以下版本验证通过：

RNOH：0.72.23; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.19



## 属性
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。
> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name  | Description  | Type | Required  |Platform|HarmonyOS Support |
| :------------ |:---------------:| :---------------:|:---------------:|:---------------:|:---------------:|
| isOpen  | Open/close the modal, optional, you can use the open/close methods instead  | `bool`  | no  | IOS/Android  | yes  |
| isDisabled  | Disable any action on the modal (open, close, swipe)  | `bool`  | no  | IOS/Android  | yes  |
| backdropPressToClose  | Close the the modal by pressing on the backdrop  | `bool`  | no  | IOS/Android  | yes  |
| swipeToClose  | Set to true to enable the swipe down to close feature | `bool`  | no  | IOS/Android  | yes  |
| swipeThreshold  | The threshold to reach in pixels to close the modal | `number`  | no  | IOS/Android  | yes  |
| swipeArea  | The height in pixels of the swipeable area, window height by default | `number`  | no  | IOS/Android  | yes  |
| position  | Control the modal position using top or center or bottom | `string`  | no  | IOS/Android  | yes  |
| entry  | Control the modal entry position top or bottom | `string`  | no  | IOS/Android  | yes  |
| backdrop  | Display a backdrop behind the modal | `bool`  | no  | IOS/Android  | yes  |
| backdropOpacity  | Opacity of the backdrop | `number`  | no  | IOS/Android  | yes  |
| backdropColor  | backgroundColor of the backdrop | `string`  | no  | IOS/Android  | yes  |
| backdropContent  | Add an element in the backdrop (a close button for example) | `ReactElement`  | no  | IOS/Android  | yes  |
| animationDuration  | Duration of the animation | `number`  | no  | IOS/Android  | yes  |
| easing  | Easing function applied to opening modal animation | `function`  | no  | IOS/Android  | yes  |
| backButtonClose  | (Android only) Close modal when receiving back button event | `bool`  | no  | Android  | yes  |
| startOpen  | Allow modal to appear open without animation upon first mount| `bool`  | no  | IOS/Android  | yes  |
| coverScreen  | Will use RN Modal component to cover the entire screen wherever the modal is mounted in the component hierarchy| `bool`  | no  | IOS/Android  | yes  |
| keyboardTopOffset  | This property prevent the modal to cover the ios status bar when the modal is scrolling up because the keyboard is opening| `number`  | no  | IOS/Android  | yes  |
| useNativeDriver  | Enables the hardware acceleration to animate the modal. Please note that enabling this can cause some flashes in a weird way when animating| `bool`  | no  | IOS/Android  | yes  |

## 事件
| Name  | Description  | Type | Required  |Platform|HarmonyOS Support |
| :------------ |:---------------:| :---------------:|:---------------:|:---------------:|:---------------:|
| onClosed  | When the modal is close and the animation is done  | `function`  | no  | IOS/Android  | yes  |
| onOpened  | When the modal is open and the animation is done | `function`  | no  | IOS/Android  | yes  |
| onClosingState  | When the state of the swipe to close feature has changed (usefull to change the content of the modal, display a message for example)  | `function`  | no  | IOS/Android  | yes  |

## 方法
hese methods are optional, you can use the isOpen property instead   


| Name  | Description  | Type | Required  |Platform|HarmonyOS Support |
| :------------ |:---------------:| :---------------:|:---------------:|:---------------:|:---------------:|
| open  | Open the modal  | `function`  | no  | IOS/Android  | yes  |
| close  | Close the modal | `function`  | no  | IOS/Android  | yes  |




## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/maxs15/react-native-modalbox/blob/master/License.txt) ，请自由地享受和参与开源。
<!-- {% endraw %} -->