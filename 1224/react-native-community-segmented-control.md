> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>react-native-community/segmented-control</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-segmented-control/segmented-control">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-segmented-control/segmented-control/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-segmented-control/segmented-control)

## 安装与使用

进入到工程目录并输入以下命令：

#### **yarn**

```bash
yarn add @react-native-segmented-control/segmented-control@^2.5.0
```

<!-- tabs:start -->

#### **npm**

```bash
npm install --save @react-native-segmented-control/segmented-control@^2.5.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import SegmentedControl from '@react-native-segmented-control/segmented-control';

return (
  <SegmentedControl
    values={['One', 'Two']}
    selectedIndex={this.state.selectedIndex}
    onChange={(event) => {
      this.setState({selectedIndex: event.nativeEvent.selectedSegmentIndex});
    }}
  />
);
```

## 约束与限制

### 兼容性

在下述版本验证通过：

1. IDE：DevEco Studio 4.1.3.412;SDK：OpenHarmony(api11) 4.1.0.53;测试设备：Mate40 Pro(NOH-AN00);ROM：2.0.0.52(SP22C00E52R1P17log);RNOH：0.72.11

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [react-native-community/segmented-control 源库地址](https://github.com/react-native-segmented-control/segmented-control)

| Name | Description | Type | Required | Platform | HarmonyOS Support | Notes |
| ---------|------- | ------------- | -------- | -------- | -------- |-------- |
| enabled     | If false the user won't be able to interact with the control. Default value is true. | boolean     | No       |All | Yes      |
| momentary               | If true, then selecting a segment won't persist visually. The onValueChange callback will still work as expected.| boolean          | No       |iOS        | No      | Android和HarmonyOS侧,效果一致，不生效，iOS侧有效果
| onChange      |Callback that is called when the user taps a segment; passes the event as an argument | function      | No       | All     | Yes      |
| onValueChange      | Callback that is called when the user taps a segment; passes the segment's value as an argument | function | No       |All        | Yes      |
| selectedIndex |The index in props.values of the segment to be (pre)selected. | number      | No       | All     | Yes      |
| tintColor         | Accent color of the control. | string      | No       |All   | Yes      |
| backgroundColor          |  Background color color of the control. | string      | No       | All   | Yes      |
| values     |  The labels for the control's segment buttons, in order.| string | Yes       | All      | Yes      |
| appearance | Overrides the control's appearance irrespective of the OS theme  | 'dark', 'light'       | No       | All      | Yes       |
| fontStyle         | An object container,color: color of segment;fontSize: font-size of segment text;fontFamily: font-family of segment text;fontWeight: font-weight of segment text| object      | No       | All      | Yes       | Android和HarmonyOS侧，fontFamily效果一致，均不生效
| activeFontStyle         | An object container,color: overrides color of selected segment text;fontSize: overrides font-size of selected segment text;fontFamily: overrides font-family of selected segment text;fontWeight: overrides font-weight of selected segment text| object      | No       | All    | Yes       |  Android和HarmonyOS侧，fontFamily效果一致，均不生效
| tabStyle         | Styles the clickable surface which is responsible to change tabs| object      | No       | Android, Web      | Yes       |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-segmented-control/segmented-control/blob/master/LICENSE) ，请自由地享受和参与开源。
