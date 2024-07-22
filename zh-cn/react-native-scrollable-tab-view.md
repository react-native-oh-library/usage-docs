<!-- {% raw %} -->
> 模板版本：v0.2.2

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



> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-scrollable-tab-view)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-scrollable-tab-view Releases](https://github.com/react-native-oh-library/react-native-scrollable-tab-view/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-scrollable-tab-view@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-scrollable-tab-view@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { Text, View } from "react-native";

import ScrollableTabView from "react-native-scrollable-tab-view";

export default () => {
  return (
    <View>
      <ScrollableTabView>
        <Text tabLabel="Tab #1">My</Text>
        <Text tabLabel="Tab #2 word word">favorite</Text>
        <Text tabLabel="Tab #3 word word word">project</Text>
        <Text tabLabel="Tab #4 word word word word">favorite</Text>
        <Text tabLabel="Tab #5">project</Text>
      </ScrollableTabView>
    </View>
  );
};
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-pager-view 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-pager-view 文档的 Link 章节](react-native-pager-view.md#link)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-scrollable-tab-view Releases](https://github.com/react-native-oh-library/react-native-scrollable-tab-view/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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

## 遗留问题

- [x] `原库已知问题RN组件ScrollView里面的scrollTo()报undefined(已修复)`[#I95OVM](https://gitee.com/react-native-oh-library/usage-docs/issues/I95OVM)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://www.mit-license.org/) ，请自由地享受和参与开源。

<!-- {% endraw %} -->