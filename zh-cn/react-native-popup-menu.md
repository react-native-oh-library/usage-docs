> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-popup-menu</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/instea/react-native-popup-menu/blob/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/instea/react-native-popup-menu/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/instea/react-native-popup-menu)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-popup-menu@0.16.1 --save
```

#### **yarn**

```bash
yarn add react-native-popup-menu@0.16.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
// your entry point
import { MenuProvider } from "react-native-popup-menu";

export const App = () => (
  <MenuProvider>
    <YourApp />
  </MenuProvider>
);

// somewhere in your app
import {
  Menu,
  MenuOptions,
  MenuOption,
  MenuTrigger,
} from "react-native-popup-menu";

export const YourComponent = () => (
  <View>
    <Text>Hello world!</Text>
    <Menu>
      <MenuTrigger text="Select action" />
      <MenuOptions>
        <MenuOption onSelect={() => alert(`Save`)} text="Save" />
        <MenuOption onSelect={() => alert(`Delete`)}>
          <Text style={{ color: "red" }}>Delete</Text>
        </MenuOption>
        <MenuOption
          onSelect={() => alert(`Not called`)}
          disabled={true}
          text="Disabled"
        />
      </MenuOptions>
    </Menu>
  </View>
);
```

## 约束与限制

### 兼容性

在以下版本验证通过

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-popup-menu](https://github.com/instea/react-native-popup-menu/blob/master/doc/api.md)

#### MenuProvider

| Name              | Description                                                                                                                                                                                                             | Type             | Required | Platform    | HarmonyOS Support |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| style             | Style of wrapping View component.                                                                                                                                                                                       | Style            | No       | IOS/Android | Yes               |
| customStyles      | Object defining wrapper, touchable and text styles                                                                                                                                                                      | Object           | No       | IOS/Android | Yes               |
| backHandler       | Whether to close the menu when the back button is pressed or custom back button handler if a function is passed (RN >= 0.44 is required)                                                                                | boolean/Function | No       | IOS/Android | Yes               |
| skipInstanceCheck | Normally your application should have only one menu provider (with exception as discussed above). If you really need more instances, set skipInstanceCheck to true to disable the check (and following warning message) | boolean          | No       | IOS/Android | Yes               |

#### Menu

| Name            | Description                                                                                                           | Type     | Required | Platform    | HarmonyOS Support |
| --------------- | --------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| name            | Unique name of menu                                                                                                   | String   | No       | IOS/Android | Yes               |
| opened          | Declaratively states if menu is opened. When this prop is provided, menu is controlled and imperative API won't work. | Boolean  | No       | IOS/Android | Yes               |
| renderer        | Defines position, animation and basic menu styles. See renderers section for more details                             | Function | No       | IOS/Android | Yes               |
| rendererProps   | Additional props which will be passed to the renderer                                                                 | Object   | No       | IOS/Android | Yes               |
| onSelect        | Triggered when menu option is selected. When event handler returns false, the popup menu remains open                 | Function | No       | IOS/Android | Yes               |
| onOpen          | Triggered when menu is opened                                                                                         | Function | No       | IOS/Android | Yes               |
| onClose         | Triggered when menu is closed                                                                                         | Function | No       | IOS/Android | Yes               |
| onBackdropPress | Triggered when user press backdrop (outside of the opened menu)                                                       | Function | No       | IOS/Android | Yes               |

#### MenuTrigger

| Name                | Description                                                                           | Type     | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| disabled            | Indicates if trigger can be pressed                                                   | Boolean  | No       | IOS/Android | Yes               |
| children            | React elements to render as menu trigger. Exclusive with text property                | Elements | No       | IOS/Android | Yes               |
| text                | Text to be rendered. When this prop is provided, trigger's children won't be rendered | String   | No       | IOS/Android | Yes               |
| customStyles        | Object defining wrapper, touchable and text styles                                    | Object   | No       | IOS/Android | Yes               |
| triggerOnLongPress  | If true, menu will trigger onLongPress instead of onPress                             | Boolean  | No       | IOS/Android | Yes               |
| testID              | Used for e2e testing to get Touchable element                                         | String   | No       | IOS/Android | Yes               |
| onPress             | Triggered when trigger is pressed (or longpressed depending on triggerOnLongPress)    | Function | No       | IOS/Android | Yes               |
| onAlternativeAction | Triggered when trigger is longpressed (or pressed depending on triggerOnLongPress)    | Function | No       | IOS/Android | Yes               |

#### MenuOptions

| Name                   | Description                                                                                                                                                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| optionsContainerStyle  | Custom styles for options container. Note: this option is deprecated, use customStyles option instead                                                                                        | Style    | No       | IOS/Android | Yes               |
| renderOptionsContainer | Custom render function for <MenuOptions />. It takes options component as argument and returns component. E.g.: options => <SomeCustomContainer>{options}</SomeCustomContainer> (Deprecated) | Function | No       | IOS/Android | Yes               |
| customStyles           | Object defining wrapper, touchable and text styles                                                                                                                                           | Object   | No       | IOS/Android | Yes               |

#### MenuOption

| Name             | Description                                                                                                                                                                                                    | Type     | Required | Platform    | HarmonyOS Support |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| value            | Value of option                                                                                                                                                                                                | Any      | No       | IOS/Android | Yes               |
| children         | React elements to render as menu option. Exclusive with text property                                                                                                                                          | Elements | No       | IOS/Android | Yes               |
| text             | Text to be rendered. When this prop is provided, option's children won't be rendered                                                                                                                           | String   | No       | IOS/Android | Yes               |
| disabled         | Indicates if option can be pressed                                                                                                                                                                             | Boolean  | No       | IOS/Android | Yes               |
| disableTouchable | Disables Touchable wrapper (no on press effect and no onSelect execution) Note: Alternatively you don't have to use MenuOption at all if you want render something "non-selectable" in the menu (e.g. divider) | Boolean  | No       | IOS/Android | Yes               |
| customStyles     | Object defining wrapper, touchable and text styles                                                                                                                                                             | Object   | No       | IOS/Android | Yes               |
| testID           | Used for e2e testing to get Touchable element. If disableTouchable=true, it is not available                                                                                                                   | String   | No       | IOS/Android | Yes               |
| onSelect         | Triggered when option is selected. When event handler returns false, the popup menu remains open. Note: If this event handler is defined, it suppress onSelect handler of <Menu />                             | Function | No       | IOS/Android | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The ISC License (ISC)](https://github.com/instea/react-native-popup-menu/blob/master/LICENSE) ，请自由地享受和参与开源。
