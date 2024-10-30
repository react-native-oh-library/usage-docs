> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-scrollable-tabview</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/itenl/react-native-scrollable-tabview">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/itenl/react-native-scrollable-tabview/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/itenl/react-native-scrollable-tabview)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @itenl/react-native-scrollable-tabview@1.1.7
```

#### **yarn**

```bash
yarn add @itenl/react-native-scrollable-tabview@1.1.7
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useEffect, useRef } from "react";
import { View, Text, Alert, Button } from "react-native";
import ScrollableTabView from "@itenl/react-native-scrollable-tabview";

export default function ScrollTabsDemo() {
  let [scrollDate, setScrollDate] = useState(Date.now());
  const myRef = useRef < any > null;

  //  console.error('test')

  return (
    <View style={{ flex: 1 }}>
      <ScrollableTabView
        ref={myRef}
        stacks={[
          {
            screen: ({ onRefresh }: any) => {
              onRefresh((toggled: (arg0: boolean) => void) => {
                setScrollDate(Date.now());
              });
              return (
                <View
                  style={{ flex: 1, backgroundColor: "blue", height: 2000 }}
                >
                  <Text>one{scrollDate}</Text>
                </View>
              );
            },
          },
          {
            screen: () => (
              <View style={{ flex: 1, backgroundColor: "grey", height: 2000 }}>
                <Text>two{scrollDate}</Text>
              </View>
            ),
          },
          {
            screen: () => {
              return (
                <View
                  style={{
                    flex: 1,
                    backgroundColor: "green",
                    justifyContent: "center",
                    alignItems: "center",
                    height: 2000,
                  }}
                >
                  <Text>
                    {Date.now()} {scrollDate}
                  </Text>
                </View>
              );
            },
          },
        ]}
        mappingProps={{}}
        tabsStyle={{ backgroundColor: "yellow" }}
        tabWrapStyle={{ zIndex: 1 }}
        tabInnerStyle={{ paddingLeft: 5 }}
        tabActiveOpacity={0}
        tabStyle={{ backgroundColor: "orange", width: 100 }}
        textStyle={{ textAlign: "center", color: "green" }}
        textActiveStyle={{ fontSize: 30 }}
        tabUnderlineStyle={{ backgroundcolor: "red", height: 10 }}
        firstIndex={0}
        syncToSticky={true}
        onEndReachedThreshold={0.4}
        onTabviewChanged={(index: any, tabLabel: any, isFirst: any) => {
          setScrollDate(index + tabLabel + isFirst);
        }}
        screenScrollThrottle={100}
        header={() => {
          return (
            <View style={{ backgroundColor: "pink", height: 80 }}>
              <Text>header</Text>
            </View>
          );
        }}
      ></ScrollableTabView>
    </View>
  );
}
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

This document is verified based on the following versions:

1. RNOH: 0.72.13; SDK: HarmonyOS NEXT Developer Preview1; IDE: DevEco Studio 4.1.3.500; ROM: 204.1.0.59;
2. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1 B.0.18、HarmonyOS NEXT Developer Preview0 B.0.60、HarmonyOS NEXT Developer Preview2 B.0.73; IDE: DevEco Studio 5.0.3.200; ROM: 2.0.0.18;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                             | Description                                                                                                                                            | Type                                     | Required | HarmonyOS Support |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------- | -------- | ----------------- |
| stacks                           | 页面栈 < [阅读 Stack Property](#StackProperty) >                                                                                                       | Array                                    | /        | yes               |
| mappingProps                     | 将映射数据关联到 Stack / Sticky                                                                                                                        | Object                                   | /        | yes               |
| badges                           | 针对每个 Tab 的徽章 < [阅读 Badge Property](#BadgeProperty) >                                                                                          | Array                                    | /        | yes               |
| tabsStyle                        | 整个 Tabs 样式                                                                                                                                         | Object                                   | /        | yes               |
| tabWrapStyle                     | 单 Tab 换行样式（函数参数提供 item、index，需要返回样式对象，eg。return index == 1 && {zIndex:10}                                                      | Object / Function                        | /        | yes               |
| tabInnerStyle                    | 单 Tab 内部样式                                                                                                                                        | Object                                   | /        | yes               |
| tabActiveOpacity                 | 单击 Tab 按钮后的透明度                                                                                                                                | Number                                   | /        | yes               |
| tabStyle                         | 单标签样式                                                                                                                                             | Object                                   | /        | yes               |
| textStyle                        | 选项卡中的文本样式                                                                                                                                     | Object                                   | /        | yes               |
| textActiveStyle                  | 选择活动文本样式                                                                                                                                       | Object                                   | /        | yes               |
| tabUnderlineStyle                | 选择活动下划线样式                                                                                                                                     | Object                                   | /        | yes               |
| firstIndex                       | 设置 firstIndex 的栈为活动状态 (请在设定 firstIndex 值的时候确保 stacks 的个数大于 firstIndex )                                                        | Number / Null                            | /        | yes               |
| syncToSticky                     | 是否同步（render 在 Screen 中触发 componentDidUpdate 会更新 Sticky）                                                                                   | Boolean                                  | /        | yes               |
| onEndReachedThreshold            | 底部回调阈值                                                                                                                                           | Number                                   | /        | yes               |
| onBeforeRefresh                  | 下拉刷新前置函数，executenext 执行 onRefreshScreen 中的函数，executetoggled 切换系统加载，可以通过 true/false 来指定（回调包含 next,toggled 两个形参） | Function                                 | /        | yes               |
| onBeforeEndReached               | 向上滑动加载更多前置函数，execute next 将执行 onEndReachedScreen 中的函数（回调包含 next 形参）                                                        | Function                                 | /        | yes               |
| onTabviewChanged                 | Tab 切换完成回调（回调包含 index, tabLabel,isFirst 参数）                                                                                              | Function                                 | /        | yes               |
| screenScrollThrottle             | Screen 横向滑动时节流参数,单位 (毫秒)                                                                                                                  | Number                                   | /        | yes               |
| header                           | 顶部组件（如果函数需要返回 Element）                                                                                                                   | Function / JSX Element / Class Component | /        | yes               |
| stickyHeader                     | 顶部带吸顶效果组件 (若是函数需要返回 Element)                                                                                                          | Function / JSX Element / Class Component | /        | yes               |
| oneTabHidden                     | 当只有一个 Tab 时隐藏自身                                                                                                                              | Boolean                                  | /        | yes               |
| enableCachePage                  | 是否持久化页面切换后不销毁                                                                                                                             | Boolean                                  | /        | yes               |
| carouselProps                    | 传递给 Carousel 的剩余属性 < [阅读 Carousel](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/PROPS_METHODS_AND_GETTERS.md) >  | Object                                   | /        | yes               |
| sectionListProps                 | 传递给 SectionList 的剩余属性 < [阅读 SectionList](https://reactnative.dev/docs/sectionlist) >                                                         | Object                                   | /        | yes               |
| toHeaderOnTab                    | 点击触发激活的 Tab 会滚动到 Header（高优先级）                                                                                                         | Boolean                                  | /        | yes               |
| toTabsOnTab                      | 点击触发激活的 Tab 会滚动到 Tabs                                                                                                                       | Boolean                                  | /        | yes               |
| tabsShown                        | 配置选项卡的显示和隐藏                                                                                                                                 | Boolean                                  | /        | yes               |
| fixedTabs                        | true 时 enableCachePage，滑动切换 Screen 设置最小高度，保证 Header 和 Tabs 不会弹起                                                                    | Boolean                                  | /        | yes               |
| fixedHeader                      | 与 Tabs 一起渲染，固定顶部 Header，不跟随滚动                                                                                                          | Boolean                                  | /        | yes               |
| useScroll                        | Tabs 是否支持水平滚动（有多个类别 Tab 时需要启用，建议 tabStyle 传入固定宽度）                                                                         | Boolean                                  | /        | yes               |
| useScrollStyle                   | 设置 contentContainerStyle 为滚动 Tabs，通常会在左右两侧添加边距 paddingLeft paddingHorizontal                                                         | Object                                   | /        | yes               |
| fillScreen                       | 填满整个屏幕                                                                                                                                           | Boolean                                  | /        | yes               |
| title                            | 动画标题                                                                                                                                               | Function / JSX Element / Class Component | /        | yes               |
| titleArgs                        | 标题配置 < [阅读 interpolate](https://reactnative.dev/docs/animations#interpolation) >                                                                 | Object                                   | /        | yes               |
| onScroll                         | 滚动事件监听                                                                                                                                           | Function                                 | /        | yes               |
| onScroll2Horizontal              | 水平滚动事件监听                                                                                                                                       | Function                                 | /        | yes               |
| tabsEnableAnimated               | 为 Tabs 启用滑动效果，需要为 tabStyle 指定 width                                                                                                       | Boolean                                  | /        | yes               |
| tabsEnableAnimatedUnderlineWidth | 要为选项卡下划线设置固定宽度并添加跳跃动画，需要启用 tabsEnableAnimated=true。 （建议传入三分之一 tabStyle.width 或者固定的 30px）                     | Number                                   | /        | yes               |
| errorToThrow                     | console.error 会抛出错误 throw new Error()                                                                                                             | Boolean                                  | /        | yes               |

## stack property

| Name           | Description                                                                                  | Type            | Required | HarmonyOS Support |
| -------------- | -------------------------------------------------------------------------------------------- | --------------- | -------- | ----------------- |
| screen         | Screen 类组件                                                                                | Class Component | /        | yes               |
| sticky         | 吸顶类组件, 实例内将返回该类组件的上下文                                                     | Class Component | /        | yes               |
| tabLabel       | Tab 昵称                                                                                     | String          | /        | yes               |
| tabLabelRender | 自定义 Tab 渲染函数，优先级高于 tabLabel                                                     | Function        | /        | yes               |
| badge          | 针对当前 Tab 的徽章，与 badges 属性互斥，优先级高于最外层属性 badges < 阅读 Badge Property > | Array           | /        | yes               |
| toProps        | toProps 仅传递给 Screen，不作数据关联                                                        | Object          | /        | yes               |

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                                       | Description                                                  | Type     | Required | HarmonyOS Support |
| ---------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| getCurrentRef(index: number.optional)                      | 获取当前活动的视图的实例，可传 index 获取指定实例            | Function | /        | yes               |
| toTabView(index: number.required / label: string.required) | 跳到指定 Screen                                              | Function | /        | yes               |
| scrollTo(index: number.required)                           | 上下滑动至指定位置 (传入 0 默认定位至 tabs / 传入负数则置顶) | Function | /        | yes               |
| clearStacks(callback: function.optional)                   | 清空栈以及相关状态 (Tabs / Badge / Stacks))                  | Function | /        | yes               |

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/itenl/react-native-scrollable-tabview/blob/main/LICENSE).
