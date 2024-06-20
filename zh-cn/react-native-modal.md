<!-- {% raw %} -->
 

> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-modal</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-modal/react-native-modal">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="" />
    </a>
     <a href="https://github.com/react-native-modal/react-native-modal/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-modal/react-native-modal)

 

## 安装与使用
 

进入到工程目录并输入以下命令：
 

#### **npm**

```bash
npm i react-native-modal@13.0.1
```

#### **yarn**

```bash
yarn add react-native-modal@13.0.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react';
import {
    AppRegistry,
    StyleSheet,
    View,
    Text
} from 'react-native';

import Modal from 'react-native-modal';

export default class RNApplyComponent extends Component {

    //初始化state
    constructor(props){
        super(props);
        this.state = {visible: false};
    }

    //显示
    show(){
        this.setState({
            visible: true
        });
    }

    //隐藏
    hide(){
        this.setState({
            visible: false
        });
    }

    //弹框
    _renderModal() {
        return (
            <Modal
                isVisible={true}
                animationIn={'bounceInUp'}
                backdropColor={'red'}
                backdropOpacity={0.4}
                onBackdropPress={() => this.hide()}
                onModalWillShow={() => { console.log("---onModalWillShow---")}}
                onModalShow={() => { console.log("---onModalShow---")}}
                onModalWillHide={() => { console.log("---onModalWillHide---")}}
                onModalHide={() => { console.log("---onModalHide---")}}
            >
                <View style={[styles.center]}>
                    <View style={[styles.parent,styles.center]}>
                        <Text style={styles.content}>欢迎您的到来</Text>
                    </View>
                </View>
            </Modal>
        )
    }
 
    render() {

        return (
            <View style={[styles.container,styles.center]}>
                <Text style={styles.content} onPress={() => this.show()}>show</Text>
                {
                    this.state.visible ?  this._renderModal() : null
                }
            </View>
        );
    }
}

const styles = StyleSheet.create({
    container:{
        flex: 1,
        backgroundColor: '#FFFFFF'
    },
    center: {
        justifyContent: 'center',
        alignItems: 'center'
    },
    parent: {
        width:300,
        height:200,
        backgroundColor:'#FFFFFF',
        borderRadius:10
    },
    content: {
        fontSize: 25,
        color: 'black',
        textAlign: 'center'
    }
});

AppRegistry.registerComponent('RNApplyComponent', () => RNApplyComponent);

```
 

## 约束与限制

### 兼容性


RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
 

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

 
 

| Name | Description | Type |Default | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | -------- | ------------------ |
| animationIn  | 模态显示动画.   | string     | "slideInUp"  | no | all      | yes |
| animationInTiming      | 模态显示动画计时（单位：ms）.                              |number            | 300           | no | all      | yes |
| animationOutTiming | 模态隐藏动画计时，单位ms. |number | 300           | no               | all      | yes |
| avoidKeyboard        | 如果键盘打开，则向上移动模态.   |bool         | false         | no           | all      | yes |
| coverScreen        | 将使用RN模态组件覆盖整个屏幕，无论模态组件安装在组件层次结构中的哪个位置. |bool           | true         | no              | all      | yes |
| hasBackdrop        | 渲染背景.           | bool         | true               | no      |  all      | yes |
| backdropColor        | 背景色.   | string        | "black"         | no                    |  all      | yes |
| backdropOpacity        | 模态可见时的背景不透明度.        |number     | 0.70         |no|  all      | yes |
| backdropTransitionInTiming        | 背景显示计时（单位：ms）.           |number  | 300         | no      |  all      | yes |
   | backdropTransitionOutTiming        | 后台隐藏时间（单位：ms）.          |number   | 300         | no      |  all      | yes |
 | customBackdrop        | 自定义背景元素.           | bool         | yes               |no      |  all      | yes |
  | children        | 模态内容.           | bool         | yes               |no      |  all      | yes |
| deviceHeight        | 设备高度（在可以隐藏导航栏的设备上很有用）.           | bool         | yes       |no      |  all      | yes |
 | deviceWidth        | 设备宽度（在可以隐藏导航栏的设备上很有用）).           | bool         | yes      |no      |  all      | yes |
 | isVisible        | 显示模态.           | bool         | yes               |yes      |  all      | yes |
  | onBackButtonPress        | 当Android返回按钮被按下时调用.        | func   | () => null         | no      |  all      | yes
| onBackdropPress        | 按下背景时调用.  | func         | () => null         | no              | all      | yes |
 | onModalWillHide        |在模态隐藏动画开始之前调用.       | func    | () => null         | no              | all      | yes |              | 
 | onModalHide        |当模态完全隐藏时调用.   | func        | () => null         | no              | all      | yes | 
 | onModalWillShow        |在模态显示动画开始之前调用.       | func    |   () => null         | no              | all      | yes |
  | onSwipeStart        |当滑动动作开始时调用.   | func        |   () => null         | no              | all      | yes |
   | onSwipeMove        |在每次滑动事件时调用.    | func       |   () => null         | no              | all      | yes |
 | onSwipeComplete        |当达到swipeThreshold时调用.      | func     |   () => null         | no              | all      | yes |
| onSwipeCancel        |当未达到swipeThreshold时调用.      | func     |   () => null         | no              | all      | yes |
| panResponderThreshold        |panResponder应何时拾取滑动事件的阈值.       | number   |   4        | no              | all      | yes |
| scrollOffset        |当>0时，禁用滑动关闭，以实现可滚动内容.          | number  |   0         | no              | all      | yes | 
 | scrollOffsetMax        |用于在内容可滚动时实现过度滚动的感觉。请参见/example目录.       | number     |   0        | no              | all      | yes |
 | scrollTo        |用于实现可滚动的模态。有关如何使用它的参考，请参见/example目录.        | number    |   0         | no              | all      | yes |
 | scrollHorizontal        |如果您的scrollView是水平的，则设置为true（用于正确的滚动处理）.        | bool    |   false         | no              | all      | yes |
 | swipeThreshold        |达到时调用onSwipeComplete的滑动阈值.         | number   |   100        | no              | all      | yes |
 | useNativeDriver        |定义动画是否应使用本机驱动程序.           | bool   |   false        | no              | all      | yes |
 | hideModalContentWhileAnimating        |通过在动画完成之前隐藏模态内容来增强性能.          | bool    |   false        | no              | all      | yes |
 


 
## 遗留问题

 

## 其他

## 开源协议
 本项目基于 [The ISC License (ISC)](https://github.com/react-native-modal/react-native-modal/blob/master/LICENSE.md) ，请自由地享受和参与开源。

 
<!-- {% endraw %} -->