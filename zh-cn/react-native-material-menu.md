模板版本：v0.2.2

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


> [!TIP] [Github 地址](https://github.com/mxck/react-native-material-menu)


## 安装与使用

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。


```js
import React, { useState } from 'react';

import { View, Text } from 'react-native';
import { Menu, MenuItem, MenuDivider } from 'react-native-material-menu';

export default function App() {
  const [visible, setVisible] = useState(false);

  const hideMenu = () => setVisible(false);

  const showMenu = () => setVisible(true);

  return (
    <View style={{ height: '100%', alignItems: 'center', justifyContent: 'center' }}>
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


## 约束与限制
### 兼容性

本文档内容基于以下版本验证通过：

RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Menu

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| children | Components rendered in menu (required)   | ReactNode  | yes |     all  |       yes|
| anchor | Button component (required)   |  ReactNode  | yes |     all  |       yes|
| visible | Whether the Menu is currently visible   | Boolean  | no |     all  |       yes|
| style | Menu style.   | [ViewStyle](https://reactnative.dev/docs/view-style-props)  | no |     all  |       yes|
| onRequestClose | Callback when menu has become hidden	   | () => void  | no |     all  |       yes|
| animationDuration | Changes show/hide animation duration. default is 300   | Number  | no |     all  |       yes|


### MenuItem

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| children | Rendered children (required)   | ReactNode  | yes |     all  |       yes|
| disabled | Disabled flag. default is false.   | Boolean  | no |     all  |       yes|
| disabledTextColor | Disabled text color. default is #bdbdbd.   | String  | no |     all  |       yes|
| onPress | Called function on press | ()=>void  | no |     all  |       yes|
| style | Container style | [ViewStyle](https://reactnative.dev/docs/view-style-props)  | no |     all  |       yes|
| textStyle | Text style | [TextStyle](https://reactnative.dev/docs/text-style-props)  | no |     all  |       yes|
| pressColor | Pressed color. default is #e0e0e0.   | String  | no |     all  |       yes|


### MenuDivider

| Name  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| color | Line color. default is 'rgba(0,0,0,0.12)'   | String  | no |     all  |       yes|


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mxck/react-native-material-menu/blob/master/LICENSE) ，请自由地享受和参与开源。
