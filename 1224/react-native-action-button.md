> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>react-native-action-button</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mastermoo/react-native-action-button/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm i react-native-action-button --save
```
<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, { Component } from 'react';
import { StyleSheet, View } from 'react-native';
import ActionButton from 'react-native-action-button';
import Icon from 'react-native-vector-icons/Ionicons';


class App extends Component {

  render() {
    return (
      <View style={{flex:1, backgroundColor: '#f3f3f3'}}>
        {/* Rest of the app comes ABOVE the action button component !*/}
        <ActionButton buttonColor="rgba(231,76,60,1)">
          <ActionButton.Item buttonColor='#9b59b6' title="New Task" onPress={() => console.log("notes tapped!")}>
            <Icon name="md-create" style={styles.actionButtonIcon} />
          </ActionButton.Item>
          <ActionButton.Item buttonColor='#3498db' title="Notifications" onPress={() => {}}>
            <Icon name="md-notifications-off" style={styles.actionButtonIcon} />
          </ActionButton.Item>
          <ActionButton.Item buttonColor='#1abc9c' title="All Tasks" onPress={() => {}}>
            <Icon name="md-done-all" style={styles.actionButtonIcon} />
          </ActionButton.Item>
        </ActionButton>
      </View>
    );
  }

}

const styles = StyleSheet.create({
  actionButtonIcon: {
    fontSize: 20,
    height: 22,
    color: 'white',
  },
});

```

## 兼容性

在以下版本验证通过
  1. IDE:4.1.3.313;
     SDK:4.1.0.53;
     测试设备：Mate40 pro(NOH-AN00);
     Rom:2.0.0.52(C00E52R1P17log);
     RNOH:0.72.11。

## 属性
详情见[react-native-action-button](https://github.com/mastermoo/react-native-action-button)

### ActionButton:

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |
| resetToken|use this to reset the internal component state (expand/collapse) in a re-render cycle. Synchronize the component state. |any| No | / | Yes |
| size |use this to change the size of the Button | number | No | / | Yes |
| active |action buttons visible or not | boolean | No | / | Yes |
| position |one of: left center and right | string | No | / | Yes |
| autoInactive |Auto hide ActionButtons when ActionButton.Item is pressed. | boolean | No | / | Yes |
| hideShadow |use this to hide the default elevation and boxShadow | boolean | No | / | Yes |
| spacing |spacing between the ActionButton.Items | number | No | / | Yes |
| offsetX |offset from the left/right side of the screen | number | No | / | Yes |
| offsetY |offset from the bottom/top of the screen | number | No | / | Yes |
| buttonText |use this to set a different text on the button | string | No | / | Yes |
| degrees |degrees to rotate icon | number | No | / | Yes |
| shadowStyle |The custom shadow style you want to pass in the action button | style | No | / | Yes |
| bgColor |background color when ActionButtons are visible | string | No | / | Yes |
| bgOpacity |set the transparency of the background color| number | No | / | Yes |
| buttonTextStyle |use this to set the textstyle of the button's text | style | No | / | Yes |
| verticalOrientation |direction action buttons should expand. One of: up or down | string | No | / | Yes |
| backgroundTappable |make background tappable in active state of ActionButton | boolean | No | / | Yes |
| activeOpacity |activeOpacity props of TouchableOpacity | number | No | / | Yes |
| renderIcon   |Function to render the component for ActionButton Icon. It is passed a boolean, active, which is true if the FAB has been expanded, and false if it is collapsed, allowing you to show a different icon when the ActionButton Items are expanded. | function | No | / | Yes |
| onPress   |fires, when ActionButton is tapped| function | No | / | Yes |
| useNativeFeedback   |Android: Whether to use a TouchableNativeFeedback| boolean | No | Android | No |
| fixNativeFeedbackRadius   |Android: Activate this to fix TouchableNativeFeedback Ripple UI problems| boolean | No | Android | No |
| nativeFeedbackRippleColor   |Android: Pass a color to the Ripple Effect of a TouchableNativeFeedback| string | No | Android | No |
### ActionButton.Item:

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |
| size |use this to change the size of the Button | number | No | / | Yes |
| buttonColor |background color of the Button | string | No | / | Yes |
| title |the title shown next to the button. When undefined the title is not hidden| string | No | / | Yes |
| textStyle |use this to set the textstyle of the button's item text | style | No | / | Yes |
| shadowStyle |The custom shadow style you want to pass in the action button item | style | No | / | Yes |
| textContainerStyle |use this to set the textstyle of the button's item text container | style | No | / | Yes |
| spaceBetween |use this to set the space between the Button and the text container | number | No | / | Yes |
| hideLabelShadow |use this to hide the button's label default elevation and boxShadow | boolean | No | / | Yes |
| activeOpacity |	activeOpacity props of TouchableOpacity | number | No | / | Yes |
| onPress   |required function, triggers when a button is tapped| function | No | / | Yes |
| useNativeFeedback   |Android: Whether to use a TouchableNativeFeedback| boolean | No | Android | No |
| fixNativeFeedbackRadius   |Android: Activate this to fix TouchableNativeFeedback Ripple UI problems| boolean | No | Android | No |
| nativeFeedbackRippleColor   |Android: Pass a color to the Ripple Effect of a TouchableNativeFeedback| string | No | Android | No |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/mastermoo/react-native-action-button/blob/master/LICENSE) ，请自由地享受和参与开源。
