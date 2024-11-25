> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-switch-pro</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/poberwong/react-native-switch-pro">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/poberwong/react-native-switch-pro/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-switch-pro)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-switch-pro Releases](https://github.com/react-native-oh-library/react-native-switch-pro/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-switch-pro
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-switch-pro
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import Switch from 'react-native-switch-pro'
...
  render() {
    return (
      <View style={styles.container}>
        <Switch onSyncPress={value => {...}}/>
      </View>
    )
  }
...

```
## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-switch-pro Releases](https://github.com/react-native-oh-library/react-native-switch-pro/releases)

本文档内容基于以下版本验证通过：

react-native-harmony: 0.72.23; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.27; ROM: 3.0.0.19;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| width| width of switch  | number  | no | Android/IOS      | yes              |
| height  | height of switch         | number  | no | Android/IOS      | yes                |
| value  | state of switch which can be used to bidirectional binding | bool  | no | Android/IOS      | yes |
| disabled  | whether switch is clickable | bool  | no | Android/IOS      | yes |
| circleColorActive  | color for circle handler of switch when it is on | string  | no | Android/IOS      | yes |
| circleColorInactive  | color for circle handler of switch when it is off | string  | no | Android/IOS      | yes |
| style  | styles that will be applied for switch container | style  | no | Android/IOS      | yes |
| circleStyle  | styles that will be applied for the circle | style  | no | Android/IOS      | yes |
| backgroundActive  | color of switch when it is on | string  | no | Android/IOS      | yes |
| backgroundInactive  | color of switch when it is of | string  | no | Android/IOS      | yes |
| onSyncPress  | callback when switch is clicked | func  | no | Android/IOS      | yes |
| onAsyncPress | has a callback with result of async | func  | no | Android/IOS      | yes | 


## 注意
* 最好不要同时使用 onSyncPress 和 onAsyncPress，否则只会调用 onSyncPress。

* value 与双向绑定一起使用，可以是 redux、state 等。
在 onAsyncPress 中，您应该写如下（带有状态）：

	```javascript
	<Switch
	  value={this.state.value}
	  onAsyncPress={(callback) => {
	    callback(false or true, value => this.setState({value}))
     }}
	/>
	```
	`value => this.setState({value})仅当 result 为 true 时才会调用。

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/poberwong/react-native-switch-pro/blob/master/LICENSE) ，请自由地享受和参与开源。