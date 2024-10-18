> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-check-box</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/crazycodeboy/react-native-check-box">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/crazycodeboy/react-native-check-box/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/crazycodeboy/react-native-check-box)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-check-box@2.1.7
```
#### **yarn**

```bash
yarn add react-native-check-box@2.1.7
```
<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, {Component} from 'react';
import {StyleSheet, View} from 'react-native';
import CheckBox from 'react-native-check-box'

type Props = {};
export default class CheckBoxDemo extends Component<Props> {
  constructor(props){
    super(props);
    this.state={
      isChecked:true
    }
  }
  render() {
    return (
      <View style={styles.container}>
        <CheckBox
            style={{flex: 1, padding: 10}}
            onClick={()=>{
              this.setState({
                  isChecked:!this.state.isChecked
              })
            }}
            isChecked={this.state.isChecked}
            rightText={"CheckBox"}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    height:'100%',
    backgroundColor: '#F5FCFF',
  }
});
```

## 兼容性

在以下版本验证通过

1. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                   | Description                                                                                                                  | Type                      | Required | Platform    |  HarmonyOS Support |
| ---------------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------- | -------- | ----------- | -------- |
| style                  | Custom style checkbox                                                                                                 | ViewPropTypes.style       | No       | Android、IOS | Yes      |
| leftText               | Custom left Text                                                                                                      | PropTypes.string          | No       | Android、IOS | Yes      |
| leftTextStyle          | Custom left Text style                                                                                                | Text.propTypes.style      | No       | Android、IOS | Yes      |
| rightText              | Custom right Text                                                                                                     | PropTypes.string          | No       | Android、IOS | Yes      |
| rightTextView          | Custom right TextView                                                                                                 | PropTypes.element         | No       | Android、IOS | Yes      |
| rightTextStyle         | Custom right Text style                                                                                               | Text.propTypes.style      | No       | Android、IOS | Yes      |
| checkedImage           | Custom checked Image                                                                                                  | PropTypes.element         | No       | Android、IOS | Yes      |
| unCheckedImage         | Custom unchecked Image                                                                                                | PropTypes.element         | No       | Android、IOS | Yes      |
| isChecked              | checkbox checked state                                                                                                | PropTypes.bool            | Yes      | Android、IOS | Yes      |
| onClick                | callback function                                                                                                     | PropTypes.func.isRequired | Yes      | Android、IOS | Yes      |
| disabled               | Disable the checkbox button                                                                                           | PropTypes.bool            | No       | Android、IOS | Yes      |
| checkBoxColor          | Tint color of the checkbox image (this props is for both checked and unchecked state)                                 | PropTypes.string          | Yes      | Android、IOS | Yes      |
| checkedCheckBoxColor   | Tint color of the checked state checkbox image (this prop will override value of checkBoxColor for checked state)     | PropTypes.string          | No       | Android、IOS | Yes      |
| uncheckedCheckBoxColor | Tint color of the unchecked state checkbox image (this prop will override value of checkBoxColor for unchecked state) | PropTypes.string          | No       | Android、IOS | Yes      |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/crazycodeboy/react-native-check-box/blob/master/LICENSE) ，请自由地享受和参与开源。