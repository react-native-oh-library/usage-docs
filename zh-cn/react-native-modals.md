模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-modals</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/jacklam718/react-native-modals">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jacklam718/react-native-modals/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/jacklam718/react-native-modals)


## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-modals@0.22.3
```

#### **yarn**

```bash
yarn add react-native-modals@0.22.3
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
// The Component can not be used until ModalPortal is mounted. You should register in your app root. For example (App.tsx):

import { SafeAreaView, View } from 'react-native';
import { ModalPortal } from 'react-native-modals';
import { ModalsDemo  } from './modalsDemo';

const App = () => {
  return (
    <View style={{flex:1}}>
      <SafeAreaView style={{flex:1}}>
        <ModalsDemo />
        <ModalPortal />
      </SafeAreaView>
    </View>
  );
}

```


```js

// create modalsDemo.tsx in the same directory as the App.tsx file

import React, { useState } from 'react'
import { Modal, ModalContent } from 'react-native-modals';
import { Button, Text } from 'react-native'

export default ModalsDemo = () => {

  return (
    <>
      <View style={{flex:1}}>
        <Button
            title="Show Modal"
            onPress={() => {
            this.setState({ visible: true });
            }}
        />
        <Modal
            visible={this.state.visible}
            onTouchOutside={() => {
            this.setState({ visible: false });
            }}
        >
            <ModalContent>
                <Text>Default Animation</Text>
                <Text>No onTouchOutside handler. will not dismiss when touch overlay.</Text>
            </ModalContent>
        </Modal>
       </View>
    </>
  )
}


```

## 约束与限制
### 兼容性

本文档内容基于以下版本验证通过：

RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Modal/BottomModal

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| visible | show or hide the modal by setting true/false.default is false.   | Boolean  | no |     all  |       yes|
| rounded | Whether the content of the modal box is rounded by setting true/false.default is true.   |  Boolean  | no |     all  |       yes|
| useNativeDriver | Whether to enable the native animation driver by setting the default animation of the true/false modal box.default is true.   | Boolean  | no |     all  |       yes|
| children | Content component displayed in the modal box.   | React Element  | no |     all  |       yes|
| modalTitle | You can pass a modalTitle component or pass a View for customizing titlebar   | React Element  | no |     all  |       yes|
| width | The Width of modal, you can use fixed width or use percentage. For example 0.5 it means 50%.default is your device width.    | Number  | no |     all  |       yes|
| height | The Height of modal, you can use fixed height or use percentage. For example 0.5 it means 50%.default is 300   | Number  | no |     all  |       yes|
| modalAnimation | animation for modal.default is FadeAnimation.   | Animation  | no |     all  |       yes|
| modalStyle | Set a custom style for the modal box content.   | Object  | no |     all  |       yes|
| style | Set custom styles for the modal box itself   | Object  | no |     all  |       yes|
| animationDuration | Set modal box animation time.default is 200   | Number  | no |     all  |       yes|
| overlayPointerEvents | Available option: auto, none.   | 'auto' \| 'none'  | no |     all  |       yes|
| overlayBackgroundColor | Sets the background color of the overlay area outside the modal box.default is #000   | String  | no |     all  |       yes|
| overlayOpacity | Sets the transparency of the overlay area outside the modal box.default is 0.5   | Number  | no |     all  |       yes|
| hasOverlay | Set the display and hiding of overlay in the area outside the modal box.default is true.   | Boolean  | no |     all  |       yes|
| onShow | You can pass shown function as a callback function, will call the function when modal shown   | ()=>void  | no |     all  |       yes|
| onDismiss | You can pass onDismiss function as a callback function, will call the function when modal dismissed   | ()=>void  | no |     all  |       yes|
| onTouchOutside | Sets the click event of the overlay area outside the modal box.   | () => void  | no |     all  |       yes|
| onHardwareBackPress | [Handle hardware button presses](https://facebook.github.io/react-native/docs/backhandler)   | () => true  | no |     Android  |       yes|
| onMove | Sets the callback for the modal box content swipe animation value   | (e:DragEvent)=>void  | no |     all  |       yes|
| onSwiping | Sets the callback for moving the modal box content.   | (e:DragEvent)=>void  | no |     all  |       yes|
| onSwipeRelease | Set the end of the modal box swipe gesture   | (e:DragEvent)=>void  | no |     all  |       yes|
| onSwipingOut | Sets a callback for the modalbox spool reaching the specified threshold   | (e:DragEvent)=>void  | no |     all  |       yes|
| onSwipeOut | Sets the callback function of the animation when the modal box swipe reaches the threshold.   | (e:DragEvent)=>void  | no |     all  |       yes|
| swipeDirection | Available option: up, down, left, right.The prop is only bottom of BottomModal.   | String or Array\<String>  | no |     all  |       yes|
| swipeThreshold | Set the threshold of the swipe movement.default is 100   | Number  | no |     all  |       yes|
| footer | for example: <View><Button text=\"DISMISS\" align=\"center\" onPress={() => {}}/></View>  | React Element  | no |     all  |       yes|


### ModalTitle

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| title | set title text   | String  | yes |     all  |       yes|
| style | Setting a Custom Container Style   | Object  | no |     all  |       yes|
| textStyle | Set custom style for title text   | Object  | no |     all  |       yes|
| align | Available option: left, center, right | 'left' \| 'center'\|'right'  | no |     all  |       yes|
| hasTitleBar | Sets the component to the specified TitleBar style.default is true. | Boolean  | no |     all  |       yes|

### ModalContent

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| children | Set Container Subcomponent   | any  | no |     all  |       yes|
| style | Setting a Custom Container Style   | any  | no |     all  |       yes|


### ModalFooter

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| children | Set Container Subcomponent   | ModalButton  | no |     all  |       yes|
| bordered | Set the display and close of the container top dividing line.default is true.   | Boolean  | no |     all  |       yes|
| style | Setting a Custom Container Style   | any  | no |     all  |       yes|


### ModalButton

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| text | Set button text   | String  | yes |     all  |       yes|
| onPress |    | () => void  | yes |     all  |       yes|
| align | Available option: left, center, right.default is center.   | 'left' \| 'center'\|'right'  | no |     all  |       yes|
| style | Setting a Custom Container Style   | Object  | no |     all  |       yes|
| textStyle | Set the button text custom style   | Object  | no |     all  |       yes|
| activeOpacity | Set button click background opacity. default is 0.6   | Number  | no |     all  |       yes|
| disabled | Sets whether the button is available.default is false.   | Boolean  | no |     all  |       yes|
| bordered | Sets whether there is a dividing line on the left of the button.default is false.   | Boolean  | no |     all  |       yes|


### Backdrop

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| visible | Set Container Subcomponent   | ModalButton  | yes |     all  |       yes|
| opacity | Set the transparency of the component container.default is 0.5.   | Number  | yes |     all  |       yes|
| onPress | Setting the container click event.   | ()=>void  | no |     all  |       yes|
| backgroundColor | Setting the Background of a Component Container.default is #000   | String  | no |     all  |       yes|
| animationDuration | Set animation time.default is 200   | Number  | no |     all  |       yes|
| pointerEvents | Available option: auto, none   | 'auto' \| 'none'  | no |     all  |       yes|
| useNativeDriver | Whether to enable the native animation driver. default is true.   | Boolean  | no |     all  |       yes|

### Animation

#### Params for (*)Animation

#### FadeAnimation

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| initialValue | Set Animated Initial Value.default is 0.   | Number  | no |     all  |       yes|
| animationDuration | Set Animation Execution Time.default is 150.   | Number  | no |     all  |       yes|
| useNativeDriver | Whether to enable the native animation driver. default is true.   | Boolean  | no |     all  |       yes|

#### ScaleAnimation

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| initialValue | Set Animated Initial Value.default is 0.   | Number  | no |     all  |       yes|
| useNativeDriver | Whether to enable the native animation driver. default is true.   | Boolean  | no |     all  |       yes|

#### SlideAnimation

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| initialValue | Set Animated Initial Value.default is 0.   | Number  | no |     all  |       yes|
| slideFrom | Available option: top, bottom, left, right.default is bottom.   | 'top' \| 'bottom' \|'left' \| 'right'  | no |     all  |       yes|
| useNativeDriver | Whether to enable the native animation driver. default is true.   | Boolean  | no |     all  |       yes|


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/jacklam718/react-native-modals/blob/master/LICENSE.md) ，请自由地享受和参与开源。
