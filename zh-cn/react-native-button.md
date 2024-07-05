<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-button</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ide/react-native-button">       
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ide/react-native-button/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!tip] [Github 地址](https://github.com/ide/react-native-button)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-button@3.1.0 --save
```

#### **yarn**

```bash
yarn add react-native-button@3.1.0 --save
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 * @flow
 */

import React, { Component } from 'react';
import Button from 'react-native-button';
import {
    View, Text
} from 'react-native';

export default class ExampleComponent extends Component {
    constructor(props, context) {
        super(props, context);
        this.state = {
            isDisabled: false
        }
    }
    _handlePress() {
        this.setState({
            isDisabled: true
        });
        console.log('Now, button disabled');
    }
    render() {
        const { isDisabled } = this.state;
        return (
            <View style={{ marginTop: 50 }}>
                <Button
                    allowFontScaling={false}
                    accessibilityLabel="Learn more about this purple button"
                    style={{ fontSize: 20, color: 'yellow' }}
                    styleDisabled={{ color: 'white' }}
                    disabled={isDisabled}
                    containerStyle={{ padding: 10, height: 45, overflow: 'hidden', borderRadius: 4, backgroundColor: 'aqua' }}
                    disabledContainerStyle={{ backgroundColor: 'pink' }}
                    onPress={() => this._handlePress()}>
                    Hello World
                </Button>
            </View>
        );
    }
};
```



## 约束与限制

## 兼容性

本文档内容基于以下版本验证通过：

react-native-harmony：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                                                            | Type     | default | Required | Platform | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- | ----------------- |
| `accessibilityLabel` | VoiceOver will read this string when a user selects the associated element. | String |  | No     | All      | yes               |
| `allowFontScaling` | Specifies whether fonts should scale to respect Text Size accessibility settings. | Bool |  | No     | All      | yes               |
| `Disabled` | Disables the button                | Bool | false   | No       | All      | yes               |
| `Style` | The style for the button                                       | View Style Prop | ｛｝ | No       | All      | yes               |
| `styleDisabled` | The style for the disabled button | View Style Prop | ｛｝ | No       | All      | yes               |
| `containerStyle` | The style for the container | View Style Prop | ｛｝ | No       | All      | yes               |
| `disabledContainerStyle` | The style for the container when the button is disabled | View Style Prop | ｛｝ | No       | All      | yes               |
| `childGroupStyle` | The style for the child views               | View Style Prop | ｛｝ | No       | All      | yes               |
| `androidBackground` | The background for andriod devices.                      | Background Prop Type |  | No       | Android | no             |
| `onPress`   | Handler to be called when the user taps the button.   | Function |         | No       | All      | yes              |



## 遗留问题

 无

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ide/react-native-button/blob/main/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->
