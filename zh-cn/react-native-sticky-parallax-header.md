> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-sticky-parallax-header)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-sticky-parallax-header Releases](https://github.com/react-native-oh-library/react-native-sticky-parallax-header/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-sticky-parallax-header
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-sticky-parallax-header
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

本库依赖以下三方库，请查看对应文档：
+ [@react-native-oh-tpl/react-native-reanimated](/zh-cn/react-native-reanimated.md)
+ [@react-native-oh-tpl/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-reanimated的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-reanimated 文档](/zh-cn/react-native-reanimated.md)、[@react-native-oh-tpl/react-native-safe-area-context 文档](/zh-cn/react-native-safe-area-context.md)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-sticky-parallax-header Releases](https://github.com/react-native-oh-library/react-native-sticky-parallax-header/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## Headers

包含 Tabbed Header Pager、Tabbed Header List、Details Header、Avatar Header、Custom Sticky Header 以及 FlashList Headers 几个大类

### Tabbed Header Pager 组件

Tabbed Header Pager 属性

Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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
| logo                           | 设置顶部 Logo 图片资源                  | image source - ImageSourcePropType                     | no       | iOS/Android | yes               |
| logoContainerStyle             | 设置 logo 容器样式                      | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| logoStyle                      | 设置 logo 样式                          | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| onChangeTab                    | Tab 栏切换回调                          | function - (prevPage: number, newPage: number) => void | no       | iOS/Android | yes               |
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

### Methods 方法

| Name     | Description                             | Type     | Required | Platform    | HarmonyOS Support |
| -------- | --------------------------------------- | -------- | -------- | ----------- | ----------------- |
| goToPage | function - (pageNumber: number) => void | function | no       | iOS/Android | no                |

### Tabbed Header List 组件

Tabbed Header List 属性

Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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
| onMomentumScrollBegin          | 滑动开始事件回调                        | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onMomentumScrollEnd            | 滑动结束事件回调                        | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScroll                       | 滑动事件回调                            | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollBeginDrag              | 滑动开始拖拽事件回调                    | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollEndDrag                | 滑动结束拖拽事件回调                    | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onTabsLayout                   | Tab 栏布局改变事件回调                  | function - (e: LayoutChangeEvent) => void         | no       | iOS/Android | yes               |
| onTopReached                   | 触顶事件回调                            | function - () => void                             | no       | iOS/Android | yes               |
| parallaxHeight                 | 视差高度值(默认 53% of screen's height) | number                                            | no       | iOS/Android | yes               |
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

### Details Header ScrollView 组件

Details Header ScrollView 属性
Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props)及 Shared DetailsHeader props 属性。

### Details Header FlatList 组件

Details Header FlatList 属性
Inherits [FlatListProps](https://reactnative.dev/docs/next/flatlist#props)及 Shared DetailsHeader props 属性。

### Details Header SectionList 组件

Details Header SectionList 属性
Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props)及 Shared DetailsHeader props 属性。

### Shared DetailsHeader props 属性

DetailsHeaderScrollView、DetailsHeaderFlatList 以及 DetailsHeaderSectionList 三个组件共享属性。

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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
| subtitle                      | 子标题                                  | string                                                | no       | iOS/Android | yes               |
| subtitleStyle                 | 子标题样式                              | style - StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| subtitleTestID                | 子标题测试 ID                           | string                                                | no       | iOS/Android | yes               |
| tag                            | 标签文字                                | string                                                | no       | iOS/Android | yes               |
| tagStyle                       | 标签文字样式                            | style = StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| tagTestID                      | 标签文字测试 ID                         | string                                                | no       | iOS/Android | yes               |
| title                          | 标题文字                                | string                                                | no       | iOS/Android | yes               |
| titleStyle                     | 标题文字样式                            | style = StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| titleTestID                    | 标题测试 ID                             | string                                                | no       | iOS/Android | yes               |

## Avatar Header

包含 AvatarHeaderScrollView、AvatarHeaderFlatList 以及 AvatarHeaderSectionList 三个组件。

### Avatar Header ScrollView 组件

Avatar Header ScrollView 属性
Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props)及 Shared AvatarHeader props 属性。

### Avatar Header FlatList 组件

Avatar Header FlatList 属性
Inherits [FlatListProps](https://reactnative.dev/docs/next/flatlist#props)及 Shared AvatarHeader props 属性。

### Avatar Header SectionList 组件

Avatar Header SectionList 属性
Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props)及 Shared AvatarHeader props 属性。

### Shared AvatarHeader props 属性

AvatarHeaderScrollView、AvatarHeaderFlatList 以及 AvatarHeaderSectionList 三个组件共享属性。

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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
| subtitle                      | 子标题                                  | string                                                | no       | iOS/Android | yes               |
| subtitleStyle                 | 子标题样式                              | style - StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| subtitleTestID                | 子标题测试 ID                           | string                                                | no       | iOS/Android | yes               |
| title                          | 标题文字                                | string                                                | no       | iOS/Android | yes               |
| titleStyle                     | 标题文字样式                            | style = StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| titleTestID                    | 标题测试 ID                             | string                                                | no       | iOS/Android | yes               |

## Custom Sticky Header

包含 StickyHeaderScrollView、StickyHeaderFlatList 以及 StickyHeaderSectionList 三个组件。

### Sticky Header ScrollView 组件

Sticky Header ScrollView 属性
Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props)及 Shared StickyHeader props 属性。

### Sticky Header FlatList 组件

Sticky Header FlatList 属性
Inherits [FlatListProps](https://reactnative.dev/docs/next/flatlist#props)及 Shared StickyHeader props 属性。

### Sticky Header SectionList 组件

Avatar Header SectionList 属性
Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props)及 Shared StickyHeader props 属性。

### Shared StickyHeader props 属性

StickyHeaderScrollView、StickyHeaderFlatList 以及 StickyHeaderSectionList 三个组件共享属性。

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                         | Type                                              | Required | Platform    | HarmonyOS Support |
| --------------------- | ----------------------------------- | ------------------------------------------------- | -------- | ----------- | ----------------- |
| containerStyle        | 设置整个组件容器的样式              | style - StyleProp<ViewStyle>                      | yes      | iOS/Android | yes               |
| onHeaderLayout        | header 布局调整回调                 | function - (e: LayoutChangeEvent) => void         | no       | iOS/Android | yes               |
| onMomentumScrollBegin | 滑动开始事件回调                    | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onMomentumScrollEnd   | 滑动结束事件回调                    | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScroll              | 滑动事件回调                        | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollBeginDrag     | 滑动开始拖拽事件回调                | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollEndDrag       | 滑动结束拖拽事件回调                | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| renderHeader          | header 渲染方法                     | render function                                   | no       | iOS/Android | yes               |
| renderTabs            | tab 渲染方法                        | render function                                   | no       | iOS/Android | yes               |
| stickyTabs            | Tab 栏是否可以固定位置（默认 true） | number                                            | no       | iOS/Android | yes               |

## FlashList Headers

包含 AvatarHeaderFlashList、DetailsHeaderFlashList 以及 TabbedHeaderFlashList 三个组件。

### Avatar Header FlashList 组件

Avatar Header FlashList 属性
Inherits [FlashListProps](https://shopify.github.io/flash-list/docs/usage/)及 Shared AvatarHeader props 属性。

### Details Header FlashList 组件

Details Header FlashList 属性
Inherits [FlashListProps](https://shopify.github.io/flash-list/docs/usage/)及 Shared DetailsHeader props 属性。

### Tabbed Header FlashList 组件

Tabbed Header FlashList 属性
Inherits [FlashListProps](https://shopify.github.io/flash-list/docs/usage/)及 Tabbed Header List props 属性。

## 遗留问题

## 其他

- [ ] 原库TabbedHeaderPager组件部分属性不生效[issue#415](https://github.com/netguru/sticky-parallax-header/issues/415)
- [ ] 原库DetailHeader、AvatarHeader组件部分属性不生效 [issue#416](https://github.com/netguru/sticky-parallax-header/issues/416)
- [ ] 原库ref.current.goToPage方法不存在 [issue#412](https://github.com/netguru/sticky-parallax-header/issues/412)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/netguru/sticky-parallax-header/blob/master/LICENSE) ，请自由地享受和参与开源。
