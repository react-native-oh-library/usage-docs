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

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-scrollable-tab-view Releases](https://github.com/react-native-oh-library/react-native-scrollable-tab-view/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

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


The HarmonyOS implementation of this library relies on the native code of @react-native-oh-tpl/react-native-pager-view，If the library has already been introduced in the HarmonyOS project, there is no need to introduce it again. You can skip the steps in this chapter and use it directly.

If not introduced, please refer to the Link section of the document[@react-native-oh-tpl/react-native-pager-view](react-native-pager-view.md#link)for introduction.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-scrollable-tab-view Releases](https://github.com/react-native-oh-library/react-native-scrollable-tab-view/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                       | Description                                                  | Type                 | Required | Platform     | HarmonyOS Support |
| -------------------------- | ------------------------------------------------------------ | -------------------- | -------- | ------------ | ----------------- |
| renderTabBar               | 用于渲染TabBar。添加该属性，需要在引入组件之时加上它的子组件。系统提供两种方式，DefaultTabBar和ScrollableTabBar。DefaultTabBar表示Tab.item会平分水平方向上的空间，而ScrollableTabBar表示所有的tabBar.item的长度将会超过屏幕宽度，但是当滚动屏幕之时可以显示出来。当然也可以自定义它的模式。 | Function             | no       | ios，android | yes               |
| tabBarPosition             | 表示TabBar的位置。一共有四个取值：top(放在界面上方)、bottom(放在界面底部)、overlayTop(有悬浮效果在上方)、overlayBottom(有悬浮效果在下方) | String               | no       | ios，android | yes               |
| onChangeTab                | 切换界面的时候会调用该方法，该属性中包含一个参数，它是一个object对象，这个对象有两个参数，i表示被选中的下标，ref表示被选中的对象。 | Function             | no       | ios，android | yes               |
| onScroll                   | 视图滑动时调用，该属性会传递一个Float类型的数字，范围是[0,tab的数量-1] | Function             | no       | ios，android | yes               |
| locked                     | 手指是否能拖动，默认为false（可拖动）,如为true则表示只能通过点击tab来切换视图。 | Bool                 | no       | ios，android | yes               |
| initialPage                | 初始化时被选中的下标，默认为0                                | Integer              | no       | ios，android | yes               |
| page                       | 设置选中指定的tab(已废弃,详情请看 [#126](https://github.com/ptomasroos/react-native-scrollable-tab-view/issues/126)) | Integer              | no       | ios,android  | no                |
| children                   | 每个顶级子组件都应该有一个tabLabel属性，选项卡栏组件可以使用它来呈现标签。默认是字符串，但也可以自定义内容。 | ReactComponents      | no       | ios，android | yes               |
| tabBarUnderlineStyle       | 设置选项卡栏下划线的样式。注意，该属性只是在系统提供的ScrollableTabBarTab状态下才有效果。 | View.propTypes.style | no       | ios，android | yes               |
| tabBarBackgroundColor      | 设置选项卡栏背景的颜色，默认为white。                        | String               | no       | ios，android | yes               |
| tabBarActiveTextColor      | 设置选中的tabBar的文字颜色,默认navy。                        | String               | no       | ios，android | yes               |
| tabBarInactiveTextColor    | 设置未选中的tabBar的文字颜色,默认black。                     | String               | no       | android,ios  | yes               |
| tabBarTextStyle            | 选项卡栏文本的其他样式。例如：{fontFamily: 'Roboto', fontSize: 15} | Object               | no       | android,ios  | yes               |
| style                      | view所拥有的属性                                             | View.propTypes.style | no       | android,ios  | yes               |
| contentProps               | 应用于ScrollView/ViewPagerAndroid的属性。请注意，重写库设置的默认值可能会破坏功能； | Object               | no       | android,ios  | yes               |
| scrollWithoutAnimation     | 设置点击Tab时，视图切换是否有动画，默认为false（即：有动画效果）。 | Bool                 | no       | android,ios  | yes               |
| prerenderingSiblingsNumber | 预渲染附近的同级，Infinity===渲染所有同级，默认为0===渲染当前页面。 | Integer              | no       | android,ios  | yes               |

## Known Issues

- [x] `Known issue in the original library: the scrollTo() in the RN component's ScrollView reports undefined (fixed)`[#I95OVM](https://gitee.com/react-native-oh-library/usage-docs/issues/I95OVM)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://www.mit-license.org/).
