> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-sticky-parallax-header</code></h1>
</p>
<p align="center">
    <a href="https://github.com/netguru/sticky-parallax-header">
        <img src="https://img.shields.io/badge/platforms-android%20|%20iOS%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/netguru/sticky-parallax-header/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-sticky-parallax-header)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-sticky-parallax-header Releases](https://github.com/react-native-oh-library/react-native-sticky-parallax-header/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-sticky-parallax-header@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-sticky-parallax-header@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from "react";
import { TabbedHeaderPager } from "react-native-sticky-parallax-header";

const TabbedHeaderPagerExample: React.FC = () => {
  const isDarkTheme = useColorScheme() === "dark";
  return (
    <>
      <TabbedHeaderPager
        contentContainerStyle={[
          isDarkTheme
            ? screenStyles.darkBackground
            : screenStyles.lightBackground,
        ]}
        containerStyle={screenStyles.stretchContainer}
        backgroundColor={colors.primaryGreen}
        foregroundImage={photosPortraitMe}
        rememberTabScrollPosition
        logo={logo}
        title={"Mornin' Mark! \nReady for a quiz?"}
        titleStyle={screenStyles.text}
        tabs={TABBED_SECTIONS.map((section) => ({
          title: section.title,
        }))}
        tabTextStyle={screenStyles.text}
        showsVerticalScrollIndicator={false}
      >
        <View style={styles.content}>
          {Brandon.cards.map((data, i, arr) => (
            <QuizCard
              data={data}
              num={i}
              key={data.question}
              cardsAmount={arr.length}
            />
          ))}
        </View>
        <View style={styles.content}>
          {Ewa.cards.map((data, i, arr) => (
            <QuizCard
              data={data}
              num={i}
              key={data.question}
              cardsAmount={arr.length}
            />
          ))}
        </View>
        <View style={styles.content}>
          {Jennifer.cards.map((data, i, arr) => (
            <QuizCard
              data={data}
              num={i}
              key={data.question}
              cardsAmount={arr.length}
            />
          ))}
        </View>
        <View style={styles.content}>
          {Brandon.cards.map((data, i, arr) => (
            <QuizCard
              data={data}
              num={i}
              key={data.question}
              cardsAmount={arr.length}
            />
          ))}
        </View>
        <View style={styles.content}>
          {Ewa.cards.map((data, i, arr) => (
            <QuizCard
              data={data}
              num={i}
              key={data.question}
              cardsAmount={arr.length}
            />
          ))}
        </View>
        <View style={styles.content}>
          {Jennifer.cards.map((data, i, arr) => (
            <QuizCard
              data={data}
              num={i}
              key={data.question}
              cardsAmount={arr.length}
            />
          ))}
        </View>
      </TabbedHeaderPager>
      <StatusBar
        barStyle="light-content"
        backgroundColor={colors.primaryGreen}
        translucent
      />
    </>
  );
};
```

## Link

This repository depends on the following libraries, please refer to the corresponding documentation: 

- [@react-native-oh-tpl/react-native-reanimated](/en/react-native-reanimated.md)
- [@react-native-oh-tpl/react-native-safe-area-context](/en/react-native-safe-area-context.md)

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-reanimated. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-reanimated](/en/react-native-reanimated.md)、[@react-native-oh-tpl/react-native-safe-area-context ](/en/react-native-safe-area-context.md) to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-sticky-parallax-header Releases](https://github.com/react-native-oh-library/react-native-sticky-parallax-header/releases).

## Headers

包含 Tabbed Header Pager、Tabbed Header List、Details Header、Avatar Header、Custom Sticky Header 以及 FlashList Headers 几个大类

### Tabbed Header Pager components

Tabbed Header Pager Properties

Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                           | Description                             | Type                                                   | Required | Platform    | HarmonyOS Support |
| ------------------------------ | --------------------------------------- | ------------------------------------------------------ | -------- | ----------- | ----------------- |
| backgroundColor                | 设置组件的背景色                        | color - ColorValue                                     | no       | iOS/Android | yes               |
| backgroundImage                | 设置组件的背景图片                      | image source - ImageSourcePropType                     | no       | iOS/Android | no                |
| containerStyle                 | 设置整个组件容器的样式                  | style - StyleProp<ViewStyle>                           | yes      | iOS/Android | yes               |
| disableScrollToPosition        | 是否禁用滑动                            | boolean                                                | no       | iOS/Android | no                |
| enableSafeAreaTopInset         | 是否设置安全区域                        | boolean                                                | yes      | iOS/Android | yes               |
| foregroundImage                | 设置头像图片资源                        | image source - ImageSourcePropType                     | no       | iOS/Android | yes               |
| headerHeight                   | 设置组件上部分 header 高度              | number                                                 | no       | iOS/Android | yes               |
| initialPage                    | 设置组件下部分 page 初始页              | number                                                 | no       | iOS/Android | yes               |
| headerHeight                   | 设置 header 高度                        | number                                                 | no       | iOS/Android | yes               |
| logo                           | 设置顶部 Logo 图片资源                  | image source - ImageSourcePropType                     | no       | iOS/Android | yes               |
| logoContainerStyle             | 设置 logo 容器样式                      | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| logoStyle                      | 设置 logo 样式                          | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| onChangeTab                    | Tab 栏切换回调                          | function - (prevPage: number, newPage: number) => void | no       | iOS/Android | yes               |
| onHeaderLayout                 | header 布局调整回调                     | function - (e: LayoutChangeEvent) => void              | no       | iOS/Android | yes               |
| onMomentumScrollBegin          | 滑动开始事件回调                        | worklet function - (e: NativeScrollEvent) => void      | no       | iOS/Android | yes               |
| onMomentumScrollEnd            | 滑动结束事件回调                        | worklet function - (e: NativeScrollEvent) => void      | no       | iOS/Android | yes               |
| onScroll                       | 滑动事件回调                            | worklet function - (e: NativeScrollEvent) => void      | no       | iOS/Android | yes               |
| onScrollBeginDrag              | 滑动开始拖拽事件回调                    | worklet function - (e: NativeScrollEvent) => void      | no       | iOS/Android | yes               |
| onScrollEndDrag                | 滑动结束拖拽事件回调                    | worklet function - (e: NativeScrollEvent) => void      | no       | iOS/Android | yes               |
| onTabsLayout                   | Tab 栏布局改变事件回调                  | function - (e: LayoutChangeEvent) => void              | no       | iOS/Android | yes               |
| onTopReached                   | 触顶事件回调                            | function - () => void                                  | no       | iOS/Android | yes               |
| parallaxHeight                 | 视差高度值(默认 53% of screen's height) | number                                                 | no       | iOS/Android | yes               |
| rememberTabScrollPosition      | 是否保留 Tab 面板滑动位置               | boolean                                                | no       | iOS/Android | yes               |
| renderHeaderBar                | headerBar 渲染方法                      | render function                                        | no       | iOS/Android | yes               |
| rememberTabScrollPosition      | 是否保留 Tab 面板滑动位置               | boolean                                                | no       | iOS/Android | yes               |
| snapStartThreshold             | 滑动开始时阻力值                        | number                                                 | no       | iOS/Android | yes               |
| snapStopThreshold              | 滑动结束时阻力值                        | number                                                 | no       | iOS/Android | no                |
| snapToEdge                     | 是否可以滑动到 Edge（默认 true）        | number                                                 | no       | iOS/Android | no                |
| stickyTabs                     | Tab 栏是否可以固定位置（默认 true）     | number                                                 | no       | iOS/Android | yes               |
| tabTextActiveStyle             | Tab 栏选中文字样式                      | style - StyleProp<TextStyle>                           | no       | iOS/Android | yes               |
| tabTextContainerStyle          | Tab 栏文字容器样式                      | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| tabTextContainerActiveStyle    | Tab 栏文字容器选中样式                  | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| tabTextStyle                   | Tab 栏文字样式                          | style - StyleProp<TextStyle>                           | no       | iOS/Android | yes               |
| tabUnderlineColor              | Tab 栏文字底部横线颜色                  | color - ColorValue                                     | no       | iOS/Android | yes               |
| tabWrapperStyle                | Tab 栏包裹容器样式                      | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| tabs                           | Tab 栏数据源                            | Tabs array - Tab[]                                     | no       | iOS/Android | yes               |
| tabsContainerBackgroundColor   | Tab 栏容器背景颜色                      | color - ColorValue                                     | no       | iOS/Android | yes               |
| tabsContainerHorizontalPadding | Tab 栏容器水平内边距（默认 20）         | number                                                 | no       | iOS/Android | yes               |
| tabsContainerStyle             | Tab 栏容器样式                          | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| title                          | 标题文字                                | string                                                 | no       | iOS/Android | yes               |
| titleStyle                     | 标题文字样式                            | style = StyleProp<TextStyle>                           | no       | iOS/Android | yes               |
| titleTestID                    | 标题测试 ID                             | string                                                 | no       | iOS/Android | yes               |

### Static Methods

| Name     | Description                             | Type     | Required | Platform    | HarmonyOS Support |
| -------- | --------------------------------------- | -------- | -------- | ----------- | ----------------- |
| goToPage | function - (pageNumber: number) => void | function | no       | iOS/Android | no                |

### Tabbed Header List components

Tabbed Header List Properties

Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                           | Description                             | Type                                              | Required | Platform    | HarmonyOS Support |
| ------------------------------ | --------------------------------------- | ------------------------------------------------- | -------- | ----------- | ----------------- |
| backgroundColor                | 设置组件的背景色                        | color - ColorValue                                | no       | iOS/Android | yes               |
| backgroundImage                | 设置组件的背景图片                      | image source - ImageSourcePropType                | no       | iOS/Android | no                |
| containerStyle                 | 设置整个组件容器的样式                  | style - StyleProp<ViewStyle>                      | yes      | iOS/Android | yes               |
| enableSafeAreaTopInset         | 是否设置安全区域                        | boolean                                           | yes      | iOS/Android | yes               |
| foregroundImage                | 设置头像图片资源                        | image source - ImageSourcePropType                | no       | iOS/Android | yes               |
| headerHeight                   | 设置 header 高度                        | number                                            | no       | iOS/Android | yes               |
| logo                           | 设置顶部 Logo 图片资源                  | image source - ImageSourcePropType                | no       | iOS/Android | yes               |
| logoContainerStyle             | 设置 logo 容器样式                      | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| logoStyle                      | 设置 logo 样式                          | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| onHeaderLayout                 | header 布局调整回调                     | function - (e: LayoutChangeEvent) => void         | no       | iOS/Android | yes               |
| onMomentumScrollBegin          | 滑动开始事件回调                        | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onMomentumScrollEnd            | 滑动结束事件回调                        | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScroll                       | 滑动事件回调                            | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollBeginDrag              | 滑动开始拖拽事件回调                    | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollEndDrag                | 滑动结束拖拽事件回调                    | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onTabsLayout                   | Tab 栏布局改变事件回调                  | function - (e: LayoutChangeEvent) => void         | no       | iOS/Android | yes               |
| onTopReached                   | 触顶事件回调                            | function - () => void                             | no       | iOS/Android | yes               |
| parallaxHeight                 | 视差高度值(默认 53% of screen's height) | number                                            | no       | iOS/Android | yes               |
| rememberTabScrollPosition      | 是否保留 Tab 面板滑动位置               | boolean                                           | no       | iOS/Android | yes               |
| renderHeaderBar                | headerBar 渲染方法                      | render function                                   | no       | iOS/Android | yes               |
| snapStartThreshold             | 滑动开始时阻力值                        | number                                            | no       | iOS/Android | yes               |
| snapStopThreshold              | 滑动结束时阻力值                        | number                                            | no       | iOS/Android | no                |
| snapToEdge                     | 是否可以滑动到 Edge（默认 true）        | number                                            | no       | iOS/Android | no                |
| stickyTabs                     | Tab 栏是否可以固定位置（默认 true）     | number                                            | no       | iOS/Android | yes               |
| tabTextActiveStyle             | Tab 栏选中文字样式                      | style - StyleProp<TextStyle>                      | no       | iOS/Android | yes               |
| tabTextContainerStyle          | Tab 栏文字容器样式                      | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| tabTextContainerActiveStyle    | Tab 栏文字容器选中样式                  | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| tabTextStyle                   | Tab 栏文字样式                          | style - StyleProp<TextStyle>                      | no       | iOS/Android | yes               |
| tabUnderlineColor              | Tab 栏文字底部横线颜色                  | color - ColorValue                                | no       | iOS/Android | yes               |
| tabWrapperStyle                | Tab 栏包裹容器样式                      | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| tabs                           | Tab 栏数据源                            | Tabs array - Tab[]                                | no       | iOS/Android | yes               |
| tabsContainerBackgroundColor   | Tab 栏容器背景颜色                      | color - ColorValue                                | no       | iOS/Android | yes               |
| tabsContainerHorizontalPadding | Tab 栏容器水平内边距（默认 20）         | number                                            | no       | iOS/Android | yes               |
| tabsContainerStyle             | Tab 栏容器样式                          | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| title                          | 标题文字                                | string                                            | no       | iOS/Android | yes               |
| titleStyle                     | 标题文字样式                            | style = StyleProp<TextStyle>                      | no       | iOS/Android | yes               |
| titleTestID                    | 标题测试 ID                             | string                                            | no       | iOS/Android | yes               |

## Details Header

包含 DetailsHeaderScrollView、DetailsHeaderFlatList 以及 DetailsHeaderSectionList 三个组件。

### Details Header ScrollView components

Details Header ScrollView Properties
Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props)及 Shared DetailsHeader props Properties。

### Details Header FlatList components

Details Header FlatList Properties
Inherits [FlatListProps](https://reactnative.dev/docs/next/flatlist#props)及 Shared DetailsHeader props Properties。

### Details Header SectionList components

Details Header SectionList Properties
Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props)及 Shared DetailsHeader props Properties。

### Shared DetailsHeader props Properties

DetailsHeaderScrollView、DetailsHeaderFlatList 以及 DetailsHeaderSectionList 三个组件共享 Properties。

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                           | Description                             | Type                                                  | Required | Platform    | HarmonyOS Support |
| ------------------------------ | --------------------------------------- | ----------------------------------------------------- | -------- | ----------- | ----------------- |
| backgroundColor                | 设置组件的背景色                        | color - ColorValue                                    | no       | iOS/Android | yes               |
| backgroundImage                | 设置组件的背景图片                      | image source - ImageSourcePropType                    | no       | iOS/Android | no                |
| containerStyle                 | 设置整个组件容器的样式                  | style - StyleProp<ViewStyle>                          | yes      | iOS/Android | yes               |
| contentIcon                    | 头像左侧卡片的 icon 图标                | image source - ImageSourcePropType                    | no       | iOS/Android | yes               |
| contentIconNumber              | 头像左侧卡片数字                        | number                                                | no       | iOS/Android | yes               |
| contentIconNumberStyle         | 头像左侧卡片数字样式                    | style - StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| contentIconNumberTestID        | 测试 ID                                 | string                                                | no       | iOS/Android | yes               |
| enableSafeAreaTopInset         | 是否设置安全区域                        | boolean                                               | yes      | iOS/Android | yes               |
| leftTopIcon                    | 设置头部左侧 logo                       | render function or image source - ImageSourcePropType | no       | iOS/Android | yes               |
| leftTopIconAccessibilityLabel  | 设置头部左侧 logo 辅助标签              | string                                                | no       | iOS/Android | no                |
| leftTopIconOnPress             | 头部左侧 logo 点击事件回调              | function - () => void                                 | no       | iOS/Android | yes               |
| leftTopIconTestID              | 头部左侧 logo 测试 ID                   | string                                                | no       | iOS/Android | yes               |
| hasBorderRadius                | 上部分是否是右下角带圆角的布局          | boolean                                               | no       | iOS/Android | yes               |
| headerHeight                   | 设置 header 高度                        | number                                                | no       | iOS/Android | yes               |
| image                          | 任务头像图片资源                        | image source - ImageSourcePropType                    | no       | iOS/Android | yes               |
| onHeaderLayout                 | header 布局调整回调                     | function - (e: LayoutChangeEvent) => void             | no       | iOS/Android | yes               |
| onMomentumScrollBegin          | 滑动开始事件回调                        | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onMomentumScrollEnd            | 滑动结束事件回调                        | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScroll                       | 滑动事件回调                            | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScrollBeginDrag              | 滑动开始拖拽事件回调                    | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScrollEndDrag                | 滑动结束拖拽事件回调                    | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onTabsLayout                   | Tab 栏布局改变事件回调                  | function - (e: LayoutChangeEvent) => void             | no       | iOS/Android | yes               |
| onTopReached                   | 触顶事件回调                            | function - () => void                                 | no       | iOS/Android | yes               |
| parallaxHeight                 | 视差高度值(默认 53% of screen's height) | number                                                | no       | iOS/Android | yes               |
| renderHeaderBar                | headerBar 渲染方法                      | render function                                       | no       | iOS/Android | yes               |
| rightTopIcon                   | 设置头部右侧图标                        | render function or image source - ImageSourcePropType | no       | iOS/Android | yes               |
| rightTopIconAccessibilityLabel | 设置头部右侧 icon 辅助标签              | string                                                | no       | iOS/Android | no                |
| rightTopIconOnPress            | 头部右侧 icon 点击事件回调              | function - () => void                                 | no       | iOS/Android | yes               |
| rightTopIconTestID             | 头部右侧 icon 测试 ID                   | string                                                | no       | iOS/Android | yes               |
| snapStartThreshold             | 滑动开始时阻力值                        | number                                                | no       | iOS/Android | yes               |
| snapStopThreshold              | 滑动结束时阻力值                        | number                                                | no       | iOS/Android | no                |
| snapToEdge                     | 是否可以滑动到 Edge（默认 true）        | number                                                | no       | iOS/Android | no                |
| stickyTabs                     | Tab 栏是否可以固定位置（默认 true）     | number                                                | no       | iOS/Android | yes               |
| substitle                      | 子标题                                  | string                                                | no       | iOS/Android | yes               |
| substitleStyle                 | 子标题样式                              | style - StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| substitleTestID                | 子标题测试 ID                           | string                                                | no       | iOS/Android | yes               |
| tabsContainerBackgroundColor   | Tab 栏容器背景颜色                      | color - ColorValue                                    | no       | iOS/Android | yes               |
| tag                            | 标签文字                                | string                                                | no       | iOS/Android | yes               |
| tagStyle                       | 标签文字样式                            | style = StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| tagTestID                      | 标签文字测试 ID                         | string                                                | no       | iOS/Android | yes               |
| title                          | 标题文字                                | string                                                | no       | iOS/Android | yes               |
| titleStyle                     | 标题文字样式                            | style = StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| titleTestID                    | 标题测试 ID                             | string                                                | no       | iOS/Android | yes               |

## Avatar Header

包含 AvatarHeaderScrollView、AvatarHeaderFlatList 以及 AvatarHeaderSectionList 三个组件。

### Avatar Header ScrollView components

Avatar Header ScrollView Properties
Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props)及 Shared AvatarHeader props Properties。

### Avatar Header FlatList components

Avatar Header FlatList Properties
Inherits [FlatListProps](https://reactnative.dev/docs/next/flatlist#props)及 Shared AvatarHeader props Properties。

### Avatar Header SectionList components

Avatar Header SectionList Properties
Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props)及 Shared AvatarHeader props Properties。

### Shared AvatarHeader props Properties

AvatarHeaderScrollView、AvatarHeaderFlatList 以及 AvatarHeaderSectionList 三个组件共享 Properties。

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                           | Description                             | Type                                                  | Required | Platform    | HarmonyOS Support |
| ------------------------------ | --------------------------------------- | ----------------------------------------------------- | -------- | ----------- | ----------------- |
| backgroundColor                | 设置组件的背景色                        | color - ColorValue                                    | no       | iOS/Android | yes               |
| backgroundImage                | 设置组件的背景图片                      | image source - ImageSourcePropType                    | no       | iOS/Android | no                |
| containerStyle                 | 设置整个组件容器的样式                  | style - StyleProp<ViewStyle>                          | yes      | iOS/Android | yes               |
| enableSafeAreaTopInset         | 是否设置安全区域                        | boolean                                               | yes      | iOS/Android | yes               |
| leftTopIcon                    | 设置头部左侧 logo                       | render function or image source - ImageSourcePropType | no       | iOS/Android | yes               |
| leftTopIconAccessibilityLabel  | 设置头部左侧 logo 辅助标签              | string                                                | no       | iOS/Android | no                |
| leftTopIconOnPress             | 头部左侧 logo 点击事件回调              | function - () => void                                 | no       | iOS/Android | yes               |
| leftTopIconTestID              | 头部左侧 logo 测试 ID                   | string                                                | no       | iOS/Android | yes               |
| hasBorderRadius                | 上部分是否是右下角带圆角的布局          | boolean                                               | no       | iOS/Android | yes               |
| headerHeight                   | 设置 header 高度                        | number                                                | no       | iOS/Android | yes               |
| image                          | 任务头像图片资源                        | image source - ImageSourcePropType                    | no       | iOS/Android | yes               |
| onHeaderLayout                 | header 布局调整回调                     | function - (e: LayoutChangeEvent) => void             | no       | iOS/Android | yes               |
| onMomentumScrollBegin          | 滑动开始事件回调                        | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onMomentumScrollEnd            | 滑动结束事件回调                        | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScroll                       | 滑动事件回调                            | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScrollBeginDrag              | 滑动开始拖拽事件回调                    | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScrollEndDrag                | 滑动结束拖拽事件回调                    | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onTabsLayout                   | Tab 栏布局改变事件回调                  | function - (e: LayoutChangeEvent) => void             | no       | iOS/Android | yes               |
| onTopReached                   | 触顶事件回调                            | function - () => void                                 | no       | iOS/Android | yes               |
| parallaxHeight                 | 视差高度值(默认 53% of screen's height) | number                                                | no       | iOS/Android | yes               |
| renderHeaderBar                | headerBar 渲染方法                      | render function                                       | no       | iOS/Android | yes               |
| rightTopIcon                   | 设置头部右侧图标                        | render function or image source - ImageSourcePropType | no       | iOS/Android | yes               |
| rightTopIconAccessibilityLabel | 设置头部右侧 icon 辅助标签              | string                                                | no       | iOS/Android | no                |
| rightTopIconOnPress            | 头部右侧 icon 点击事件回调              | function - () => void                                 | no       | iOS/Android | yes               |
| rightTopIconTestID             | 头部右侧 icon 测试 ID                   | string                                                | no       | iOS/Android | yes               |
| snapStartThreshold             | 滑动开始时阻力值                        | number                                                | no       | iOS/Android | yes               |
| snapStopThreshold              | 滑动结束时阻力值                        | number                                                | no       | iOS/Android | no                |
| snapToEdge                     | 是否可以滑动到 Edge（默认 true）        | number                                                | no       | iOS/Android | no                |
| stickyTabs                     | Tab 栏是否可以固定位置（默认 true）     | number                                                | no       | iOS/Android | yes               |
| substitle                      | 子标题                                  | string                                                | no       | iOS/Android | yes               |
| substitleStyle                 | 子标题样式                              | style - StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| substitleTestID                | 子标题测试 ID                           | string                                                | no       | iOS/Android | yes               |
| tabsContainerBackgroundColor   | Tab 栏容器背景颜色                      | color - ColorValue                                    | no       | iOS/Android | yes               |
| title                          | 标题文字                                | string                                                | no       | iOS/Android | yes               |
| titleStyle                     | 标题文字样式                            | style = StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| titleTestID                    | 标题测试 ID                             | string                                                | no       | iOS/Android | yes               |

## Custom Sticky Header

包含 StickyHeaderScrollView、StickyHeaderFlatList 以及 StickyHeaderSectionList 三个组件。

### Sticky Header ScrollView components

Sticky Header ScrollView Properties
Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props)及 Shared StickyHeader props Properties。

### Sticky Header FlatList components

Sticky Header FlatList Properties
Inherits [FlatListProps](https://reactnative.dev/docs/next/flatlist#props)及 Shared StickyHeader props Properties。

### Sticky Header SectionList components

Avatar Header SectionList Properties
Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props)及 Shared StickyHeader props Properties。

### Shared StickyHeader props Properties

StickyHeaderScrollView、StickyHeaderFlatList 以及 StickyHeaderSectionList 三个组件共享 Properties。

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                         | Type                                              | Required | Platform    | HarmonyOS Support |
| --------------------- | ----------------------------------- | ------------------------------------------------- | -------- | ----------- | ----------------- |
| containerStyle        | 设置整个组件容器的样式              | style - StyleProp<ViewStyle>                      | yes      | iOS/Android | yes               |
| onHeaderLayout        | header 布局调整回调                 | function - (e: LayoutChangeEvent) => void         | no       | iOS/Android | yes               |
| onMomentumScrollBegin | 滑动开始事件回调                    | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onMomentumScrollEnd   | 滑动结束事件回调                    | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScroll              | 滑动事件回调                        | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollBeginDrag     | 滑动开始拖拽事件回调                | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollEndDrag       | 滑动结束拖拽事件回调                | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onTabsLayout          | Tab 栏布局改变事件回调              | function - (e: LayoutChangeEvent) => void         | no       | iOS/Android | yes               |
| renderHeader          | header 渲染方法                     | render function                                   | no       | iOS/Android | yes               |
| renderTabs            | tab 渲染方法                        | render function                                   | no       | iOS/Android | yes               |
| stickyTabs            | Tab 栏是否可以固定位置（默认 true） | number                                            | no       | iOS/Android | yes               |

## FlashList Headers

包含 AvatarHeaderFlashList、DetailsHeaderFlashList 以及 TabbedHeaderFlashList 三个组件。

### Avatar Header FlashList 组件

Avatar Header FlashList Properties
Inherits [FlashListProps](https://shopify.github.io/flash-list/docs/usage/)及 Shared AvatarHeader props Properties。

### Details Header FlashList 组件

Details Header FlashList Properties
Inherits [FlashListProps](https://shopify.github.io/flash-list/docs/usage/)及 Shared DetailsHeader props Properties。

### Tabbed Header FlashList 组件

Tabbed Header FlashList Properties
Inherits [FlashListProps](https://shopify.github.io/flash-list/docs/usage/)及 Tabbed Header List props Properties。

## Known Issues

## Others

- [ ] 原库 TabbedHeaderPager 组件部分 Properties 不生效[issue#415](https://github.com/netguru/sticky-parallax-header/issues/415)
- [ ] 原库 DetailHeader、AvatarHeader 组件部分 Properties 不生效 [issue#416](https://github.com/netguru/sticky-parallax-header/issues/416)
- [ ] 原库 ref.current.goToPage 方法不存在 [issue#412](https://github.com/netguru/sticky-parallax-header/issues/412)

## License

This project is licensed under [The MIT License (MIT)](https://github.com/netguru/sticky-parallax-header/blob/master/LICENSE).
