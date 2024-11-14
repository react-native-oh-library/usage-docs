> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-material-dropdown</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/n4kz/react-native-material-dropdown/">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/n4kz/react-native-material-dropdown/blob/master/license.txt">
        <img src="https://img.shields.io/npm/l/react-native-material-ripple.svg?colorB=448aff" alt="License" />
    </a>
</p>





> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-material-dropdown)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-material-dropdown Releases](https://github.com/react-native-oh-library/react-native-material-dropdown/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

> [!TIP] 本库依赖[@react-native-oh-tpl/react-native-material-textfield 文档](/zh-cn/react-native-material-textfield.md) 

和 [@react-native-oh-tpl/react-native-material-buttons 文档](/zh-cn/react-native-material-buttons.md)


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-material-dropdown
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-material-dropdown
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react';
import { Dropdown } from 'react-native-material-dropdown';

class Example extends Component {
  render() {
    let data = [{
      value: 'Banana',
    }, {
      value: 'Mango',
    }, {
      value: 'Pear',
    }];

    return (
      <Dropdown
        label='Favorite Fruit'
        data={data}
      />
    );
  }
}
```



## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-material-textfield和@react-native-oh-tpl/react-native-material-buttons 的代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-material-textfield 文档](/zh-cn/react-native-material-textfield.md) 

和 [@react-native-oh-tpl/react-native-material-buttons 文档](/zh-cn/react-native-material-buttons.md)进行引入



## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-material-dropdown Releases](https://github.com/react-native-oh-library/react-native-material-dropdown/releases)


## 属性

### 此组件有以下属性:

>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|         Name          |                 Description                 |   Type   | Required |  Platform   | HarmonyOS Support |
| :-------------------: | :-----------------------------------------: | :------: | :------: | :---------: | :---------------: |
|       **label**       |            Text field label text            |  String  |    No    | iOS/Android |        Yes        |
|       **error**       |            Text field error text            |  String  |    No    | iOS/Android |        Yes        |
| **animationDuration** |     Text field animation duration in ms     |  Number  |    No    | iOS/Android |        Yes        |
|     **fontSize**      |            Text field font size             |  Number  |    No    | iOS/Android |        Yes        |
|   **labelFontSize**   |         Text field label font size          |  Number  |    No    | iOS/Android |        Yes        |
|     **baseColor**     |            Text field base color            |  String  |    No    | iOS/Android |        Yes        |
|     **textColor**     |            Text field text color            |  String  |    No    | iOS/Android |        Yes        |
|     **itemColor**     |  Dropdown item text color (inactive item)   |  String  |    No    | iOS/Android |        Yes        |
| **selectedItemColor** |   Dropdown item text color (active item)    |  String  |    No    | iOS/Android |        Yes        |
| **disabledItemColor** |  Dropdown item text color (disabled item)   |  String  |    No    | iOS/Android |        Yes        |
| **dropdownPosition**  |  Dropdown position (dynamic if undefined)   |  Number  |    No    | iOS/Android |        Yes        |
|     **itemCount**     |         Dropdown visible item count         |  Number  |    No    | iOS/Android |        Yes        |
|    **itemPadding**    |       Dropdown item vertical padding        |  Number  |    No    | iOS/Android |        Yes        |
|   **itemTextStyle**   |          Dropdown item text styles          |  Object  |    No    | iOS/Android |        Yes        |
|  **dropdownOffset**   |               Dropdown offset               |  Object  |    No    | iOS/Android |        Yes        |
|  **dropdownMargins**  |              Dropdown margins               |  Object  |    No    | iOS/Android |        Yes        |
|       **data**        |             Dropdown item data              | Array[]  |    No    | iOS/Android |        Yes        |
|       **value**       |               Selected value                |  String  |    No    | iOS/Android |        Yes        |
|  **containerStyle**   |          Styles for container view          |  Object  |    No    | iOS/Android |        Yes        |
|   **overlayStyle**    |           Styles for overlay view           |  Object  |    No    | iOS/Android |        Yes        |
|    **pickerStyle**    |         Styles for item picker view         |  Object  |    No    | iOS/Android |        Yes        |
|   **shadeOpacity**    |      Shade opacity for dropdown items       |  Number  |    No    | iOS/Android |        Yes        |
|   **rippleOpacity**   |          Opacity for ripple effect          |  Number  |    No    | iOS/Android |        Yes        |
|   **rippleInsets**    |     Insets for ripple on base component     |  Object  |    No    | iOS/Android |        Yes        |
|  **rippleCentered**   | Ripple on base component should be centered | Boolean  |    No    | iOS/Android |        Yes        |
|    **renderBase**     |            Render base component            | Function |    No    | iOS/Android |        Yes        |
|  **renderAccessory**  |         Render text field accessory         | Function |    No    | iOS/Android |        Yes        |
|  **valueExtractor**   | Extract value from item (args: item, index) | Function |    No    | iOS/Android |        Yes        |
|  **labelExtractor**   | Extract label from item (args: item, index) | Function |    No    | iOS/Android |        Yes        |
|  **propsExtractor**   | Extract props from item (args: item, index) | Function |    No    | iOS/Android |        Yes        |
|   **onChangeText**    |            Change text callback             | Function |    No    | iOS/Android |        Yes        |

## **API**

>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|        Name         |       Description       |  Type   | Required |  Platform   | HarmonyOS Support |
| :-----------------: | :---------------------: | :-----: | :------: | :---------: | :---------------: |
|     **focus()**     |      Acquire focus      |         |    No    | iOS/Android |        Yes        |
|     **blur()**      |      Release focus      |         |    No    | iOS/Android |        Yes        |
| **selectedIndex()** |   Get selected index    | Number  |    No    | iOS/Android |        Yes        |
|     **value()**     |    Get current value    | String  |    No    | iOS/Android |        Yes        |
| **selectedItem()**  |    Get selected item    | Object  |    No    | iOS/Android |        Yes        |
|   **isFocused()**   | Get current focus state | Boolean |    No    | iOS/Android |        Yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The BSD License (BSD )](https://github.com/n4kz/react-native-material-dropdown/blob/master/license.txt) ，请自由地享受和参与开源。

