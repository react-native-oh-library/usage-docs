<!-- {% raw %} -->


> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-easy-toast</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/crazycodeboy/react-native-easy-toast">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/<原库源码仓LICENSE的路径（如有）>">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/crazycodeboy/react-native-easy-toast)


## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-easy-toast@2.3.0
```

#### **yarn**

```bash
yarn add react-native-easy-toast@2.3.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, { Component } from "react";
import { Text, View, Button } from "react-native";
import {
  Toast
} from "react-native-easy-toast";

export default class App extends Component {
    constructor(props) {
        super(props);
    }
    render() {
      return (
        <View>
            <Button title={'Press me'} onPress={()=>{
                this.toast.show('hello world!',2000);
            }}/>
            <Toast ref={(toast) => this.toast = toast}/>
        </View>
      )
    }
}


```

更多使用场景可查看 [react-native-easy-toast 源库地址](https://github.com/crazycodeboy/react-native-easy-toast)

## 约束与限制

### 兼容性

在下述版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2(B.0.73); IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.58;


## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
> 详情见 [react-native-easy-toast 源库地址](https://github.com/crazycodeboy/react-native-easy-toast)

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style  | Custom style toast | View.propTypes.style  | no | All | yes |
| position  | Custom toast position | PropTypes.oneOf(['top','center','bottom',])  | no | All | yes |
| positionValue  | Custom toast position value | React.PropTypes.number | no | All | yes |
| fadeInDuration  | Custom toast show duration | React.PropTypes.number  | no | All | yes |
| fadeOutDuration  | Custom toast close duration | React.PropTypes.number  | no | All | yes |
| opacity  | Custom toast opacity | React.PropTypes.number  | no | All | yes |
| textStyle  | Custom style text | View.propTypes.style  | no | All | yes |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show  | show a toast,unit is millisecond，and do callback  | (text: string, duration: number, callback: function, onPress: function)  | no | All      | yes |
| close  | start the close timer  | -  | no | All | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT Licensed](https://github.com/crazycodeboy/react-native-easy-toast/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->