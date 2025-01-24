> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-scrollable-tab-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ptomasroos/react-native-scrollable-tab-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-scrollable-tab-view)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-scrollable-tab-view Releases](https://github.com/react-native-oh-library/react-native-scrollable-tab-view/releases). For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-scrollable-tab-view
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-scrollable-tab-view
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The library name imported during use remains unchanged.

```js
import React from 'react';
import {
  Text,
} from 'react-native';

import ScrollableTabView, { DefaultTabBar } from 'react-native-scrollable-tab-view';

export default () => {
  return <ScrollableTabView
    style={{ marginTop: 20 }}
    initialPage={1}
    renderTabBar={() => <DefaultTabBar />}
  >
    <Text tabLabel='Tab #1'>My</Text>
    <Text tabLabel='Tab #2'>favorite</Text>
    <Text tabLabel='Tab #3'>project</Text>
  </ScrollableTabView>;
}
```

## Link


The HarmonyOS implementation of this library relies on the native code of @react-native-oh-tpl/react-native-pager-view. If the library has already been introduced in the HarmonyOS project, there is no need to introduce it again.You can skip the steps in this chapter and use it directly.

If not introduced, please refer to the Link section of the document [@react-native-oh-tpl/react-native-pager-view](react-native-pager-view.md#link) for introduction.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-scrollable-tab-view Releases](https://github.com/react-native-oh-library/react-native-scrollable-tab-view/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                       | Description                                                  | Type                 | Required | Platform     | HarmonyOS Support |
| -------------------------- | ------------------------------------------------------------ | -------------------- | -------- | ------------ | ----------------- |
| renderTabBar               | Renders the tab bar. To add this property, you need to add its subcomponents when introducing the component. The system provides two tab bar types: **DefaultTabBar** and **ScrollableTabBar**. **DefaultTabBar** indicates that tab items are evenly distributed in the horizontal space. **ScrollableTabBar** indicates that the length of all tab bar items exceeds the screen width, but they can be displayed when the screen is scrolled. You can also customize the mode. | Function             | no       | iOS, Android | yes               |
| tabBarPosition             | Indicates the position of the tab bar. You can set this parameter to **top** (on the top of the UI), **bottom** (on the bottom of the UI), **overlayTop** (on the top with the floating effect), or **overlayBottom** (on the bottom with the floating effect). | String               | no       | iOS, Android | yes               |
| onChangeTab                | Called when the tab is switched. This function contains a parameter, which is an object containing two parameters: **i** indicates the selected index of the tab, and **ref** indicates the selected tab. | Function             | no       | iOS, Android | yes               |
| onScroll                   | Called when the view slides. This function contains a parameter, which is a number of the Float type. Value range: [0, number of tabs – 1]. | Function             | no       | iOS, Android | yes               |
| locked                     | Indicates whether the tab can be dragged. The default value is **false**, indicating that the tab can be dragged. If the value is **true**, the view can be switched only by clicking the tab. | Bool                 | no       | iOS, Android | yes               |
| initialPage                | Indicates the index of the selected tab during initialization. The default value is **0**. | Integer              | no       | iOS, Android | yes               |
| page                       | Sets the selected tab. This property is deprecated. For details, see [#126](https://github.com/ptomasroos/react-native-scrollable-tab-view/issues/126). | Integer              | no       | iOS, Android | no                |
| children                   | Each top-level child component should have a **tabLabel** property that can be used by the tab bar component to render out the labels. The default value of the tab bar is a string. You can also customize the value. | ReactComponents      | no       | iOS, Android | yes               |
| tabBarUnderlineStyle       | Sets the underline style of the tab bar. Note that this property is valid only in the **ScrollableTabBarTab** state provided by the system. | View.propTypes.style | no       | iOS, Android | yes               |
| tabBarBackgroundColor      | Sets the background color of the tab bar. The default color is **white**. | String               | no       | iOS, Android | yes               |
| tabBarActiveTextColor      | Sets the text color of the selected tab bar. The default value is **navy**. | String               | no       | iOS, Android | yes               |
| tabBarInactiveTextColor    | Sets the text color of the tab bar that is not selected. The default value is **black**. | String               | no       | Android, iOS | yes               |
| tabBarTextStyle            | Sets other styles of the tab bar text. Example: {fontFamily: 'Roboto', fontSize: 15} | Object               | no       | Android, iOS | yes               |
| style                      | Indicates a property of View.                                | View.propTypes.style | no       | Android, iOS | yes               |
| contentProps               | Indicates a property applied to **ScrollView** and **ViewPagerAndroid**. Note that overriding the default values set by the library may damage the functionality. | Object               | no       | Android, iOS | yes               |
| scrollWithoutAnimation     | Sets whether animation is displayed during view switching when a tab is clicked. The default value is **false**, indicating that animation is displayed. | Bool                 | no       | Android, iOS | yes               |
| prerenderingSiblingsNumber | Pre-renders the nearby siblings. If this property is set to **Infinity**, all siblings are rendered. The default value is **0**, indicating that the current page is rendered. | Integer              | no       | Android, iOS | yes               |

## Known Issues

- [x] `Known issue in the original library: the scrollTo() in the RN component's ScrollView reports undefined (fixed)`[#I95OVM](https://gitee.com/react-native-oh-library/usage-docs/issues/I95OVM)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://www.mit-license.org/).