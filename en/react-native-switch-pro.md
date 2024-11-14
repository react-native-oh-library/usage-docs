> Template version: v0.2.0

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

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-switch-pro)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-switch-pro Releases](https://github.com/react-native-oh-library/react-native-switch-pro/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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
## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-switch-pro Releases](https://github.com/react-native-oh-library/react-native-switch-pro/releases)

This document is verified based on the following versions:

1. react-native-harmony: 0.72.23; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.27; ROM: 3.0.0.19;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/poberwong/react-native-switch-pro/blob/master/LICENSE).