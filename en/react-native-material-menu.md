Template version: v0.2.2

<p align="center">
  <h1 align="center"> 
    <code>react-native-material-menu</code> 
  </h1>
</p>

<p align="center">
    <a href="https://github.com/mxck/react-native-material-menu">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mxck/react-native-material-menu/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/mxck/react-native-material-menu)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-material-menu@2.0.0
```

#### **yarn**

```bash
yarn add react-native-material-menu@2.0.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";

import { View, Text } from "react-native";
import { Menu, MenuItem, MenuDivider } from "react-native-material-menu";

export default function App() {
  const [visible, setVisible] = useState(false);

  const hideMenu = () => setVisible(false);

  const showMenu = () => setVisible(true);

  return (
    <View
      style={{ height: "100%", alignItems: "center", justifyContent: "center" }}
    >
      <Menu
        visible={visible}
        anchor={<Text onPress={showMenu}>Show menu</Text>}
        onRequestClose={hideMenu}
      >
        <MenuItem onPress={hideMenu}>Menu item 1</MenuItem>
        <MenuItem onPress={hideMenu}>Menu item 2</MenuItem>
        <MenuItem disabled>Disabled item</MenuItem>
        <MenuDivider />
        <MenuItem onPress={hideMenu}>Menu item 4</MenuItem>
      </Menu>
    </View>
  );
}
```

## Constraints

### Compatibility

This document is verified based on the following versions:

RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### Menu

| Name              | Description                                          | Type                                                       | Required | Platform | HarmonyOS Support |
| ----------------- | ---------------------------------------------------- | ---------------------------------------------------------- | -------- | -------- | ----------------- |
| children          | Components rendered in menu (required)               | ReactNode                                                  | yes      | all      | yes               |
| anchor            | Button component (required)                          | ReactNode                                                  | yes      | all      | yes               |
| visible           | Whether the Menu is currently visible                | Boolean                                                    | no       | all      | yes               |
| style             | Menu style.                                          | [ViewStyle](https://reactnative.dev/docs/view-style-props) | no       | all      | yes               |
| onRequestClose    | Callback when menu has become hidden                 | () => void                                                 | no       | all      | yes               |
| animationDuration | Changes show/hide animation duration. default is 300 | Number                                                     | no       | all      | yes               |

### MenuItem

| Name              | Description                              | Type                                                       | Required | Platform | HarmonyOS Support |
| ----------------- | ---------------------------------------- | ---------------------------------------------------------- | -------- | -------- | ----------------- |
| children          | Rendered children (required)             | ReactNode                                                  | yes      | all      | yes               |
| disabled          | Disabled flag. default is false.         | Boolean                                                    | no       | all      | yes               |
| disabledTextColor | Disabled text color. default is #bdbdbd. | String                                                     | no       | all      | yes               |
| onPress           | Called function on press                 | ()=>void                                                   | no       | all      | yes               |
| style             | Container style                          | [ViewStyle](https://reactnative.dev/docs/view-style-props) | no       | all      | yes               |
| textStyle         | Text style                               | [TextStyle](https://reactnative.dev/docs/text-style-props) | no       | all      | yes               |
| pressColor        | Pressed color. default is #e0e0e0.       | String                                                     | no       | all      | yes               |

### MenuDivider

| Name  | Description                               | Type   | Required | Platform | HarmonyOS Support |
| ----- | ----------------------------------------- | ------ | -------- | -------- | ----------------- |
| color | Line color. default is 'rgba(0,0,0,0.12)' | String | no       | all      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mxck/react-native-material-menu/blob/master/LICENSE).
