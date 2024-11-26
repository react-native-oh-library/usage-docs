> Template version: v0.2.2

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


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-material-dropdown)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-material-dropdown Releases](https://github.com/react-native-oh-library/react-native-material-dropdown/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

> [!TIP] This library depends on [@react-native-oh-tpl/react-native-material-textfield](/zh-cn/react-native-material-textfield.md) and [@react-native-oh-tpl/react-native-material-buttons](/zh-cn/react-native-material-buttons.md)

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-material-textfield and @react-native-oh-tpl/react-native-material-buttons. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in @react-native-oh-tpl/react-native-material-textfield and @react-native-oh-tpl/react-native-material-buttons to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-material-dropdown Releases](https://github.com/react-native-oh-library/react-native-material-dropdown/releases)


## Properties

### This component has the following properties:

>[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

>[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

>[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

>[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|        Name         |       Description       |  Type   | Required |  Platform   | HarmonyOS Support |
| :-----------------: | :---------------------: | :-----: | :------: | :---------: | :---------------: |
|     **focus()**     |      Acquire focus      |         |    No    | iOS/Android |        Yes        |
|     **blur()**      |      Release focus      |         |    No    | iOS/Android |        Yes        |
| **selectedIndex()** |   Get selected index    | Number  |    No    | iOS/Android |        Yes        |
|     **value()**     |    Get current value    | String  |    No    | iOS/Android |        Yes        |
| **selectedItem()**  |    Get selected item    | Object  |    No    | iOS/Android |        Yes        |
|   **isFocused()**   | Get current focus state | Boolean |    No    | iOS/Android |        Yes        |

## Known Issues

## Others

- RenderAccessory property: You need to specify renderRightAccessory or renderLeftAccessory

## License

This project is licensed under [The BSD License (BSD )](https://github.com/n4kz/react-native-material-dropdown/blob/master/license.txt).

