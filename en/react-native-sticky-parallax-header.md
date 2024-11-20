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

It consists of the  Tabbed Header Pager、Tabbed Header List、Details Header、Avatar Header、Custom Sticky Header and FlashList Headers categories.

### Tabbed Header Pager components

Tabbed Header Pager Properties

Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                           | Description                                                        | Type                                                   | Required | Platform    | HarmonyOS Support |
|--------------------------------|--------------------------------------------------------------------|--------------------------------------------------------|----------|-------------|-------------------|
| backgroundColor                | Sets the background color of a component                           | color - ColorValue                                     | no       | iOS/Android | yes               |
| backgroundImage                | Sets the background image of the widget                            | image source - ImageSourcePropType                     | no       | iOS/Android | no                |
| containerStyle                 | Style the entire component container                               | style - StyleProp<ViewStyle>                           | yes      | iOS/Android | yes               |
| disableScrollToPosition        | Whether to disable sliding                                         | boolean                                                | no       | iOS/Android | no                |
| enableSafeAreaTopInset         | Indicates whether to set a security zone                           | boolean                                                | yes      | iOS/Android | yes               |
| foregroundImage                | Setting the avatar resource                                        | image source - ImageSourcePropType                     | no       | iOS/Android | yes               |
| headerHeight                   | Sets the header height on the component                            | number                                                 | no       | iOS/Android | yes               |
| initialPage                    | Sets the initial page of the lower page of the component           | number                                                 | no       | iOS/Android | yes               |
| logo                           | Set the logo image resource on the top                             | image source - ImageSourcePropType                     | no       | iOS/Android | yes               |
| logoContainerStyle             | Sets the logo container style                                      | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| logoStyle                      | Setting the logo style                                             | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| onChangeTab                    | Tab bar switch callback                                            | function - (prevPage: number, newPage: number) => void | no       | iOS/Android | yes               |
| onHeaderLayout                 | Header layout adjustment callback                                  | function - (e: LayoutChangeEvent) => void              | no       | iOS/Android | yes               |
| onMomentumScrollBegin          | Sliding start event callback                                       | worklet function - (e: NativeScrollEvent) => void      | no       | iOS/Android | yes               |
| onMomentumScrollEnd            | Sliding end event callback                                         | worklet function - (e: NativeScrollEvent) => void      | no       | iOS/Android | yes               |
| onScroll                       | Sliding event callback                                             | worklet function - (e: NativeScrollEvent) => void      | no       | iOS/Android | yes               |
| onScrollBeginDrag              | Callback of the sliding start drag event                           | worklet function - (e: NativeScrollEvent) => void      | no       | iOS/Android | yes               |
| onScrollEndDrag                | Sliding end drag event callback                                    | worklet function - (e: NativeScrollEvent) => void      | no       | iOS/Android | yes               |
| onTabsLayout                   | Tab bar layout change event callback                               | function - (e: LayoutChangeEvent) => void              | no       | iOS/Android | yes               |
| onTopReached                   | Top event callback                                                 | function - () => void                                  | no       | iOS/Android | yes               |
| parallaxHeight                 | Parallax height value(default 53% of screen's height)              | number                                                 | no       | iOS/Android | yes               |
| rememberTabScrollPosition      | Indicates whether to retain the sliding position of the tab panel. | boolean                                                | no       | iOS/Android | yes               |
| renderHeaderBar                | headerBar Rendering Function                                       | render function                                        | no       | iOS/Android | yes               |
| snapStartThreshold             | Resistance value at the start of sliding                           | number                                                 | no       | iOS/Android | yes               |
| snapStopThreshold              | Resistance value at the end of sliding                             | number                                                 | no       | iOS/Android | no                |
| snapToEdge                     | enabled or not to slide to edge（default true）                      | number                                                 | no       | iOS/Android | no                |
| stickyTabs                     | Indicates whether the tab bar can be fixed（default true）           | number                                                 | no       | iOS/Android | yes               |
| tabTextActiveStyle             | Select a text style on the tab bar                                 | style - StyleProp<TextStyle>                           | no       | iOS/Android | yes               |
| tabTextContainerStyle          | Tab Bar Text Container Style                                       | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| tabTextContainerActiveStyle    | Tab Bar Text Container Selection Style                             | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| tabTextStyle                   | Tab Bar Text Style                                                 | style - StyleProp<TextStyle>                           | no       | iOS/Android | yes               |
| tabUnderlineColor              | Color of the horizontal line at the bottom of the tab bar text     | color - ColorValue                                     | no       | iOS/Android | yes               |
| tabWrapperStyle                | Tab Bar Wrap Container Style                                       | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| tabs                           | Tab Bar Data Source                                                | Tabs array - Tab[]                                     | no       | iOS/Android | yes               |
| tabsContainerBackgroundColor   | Tab Bar Container Background Color                                 | color - ColorValue                                     | no       | iOS/Android | yes               |
| tabsContainerHorizontalPadding | Tab Bar Container Horizontal Inner Margin（default 20）              | number                                                 | no       | iOS/Android | yes               |
| tabsContainerStyle             | Tab Bar Container Style                                            | style - StyleProp<ViewStyle>                           | no       | iOS/Android | yes               |
| title                          | Title Text                                                         | string                                                 | no       | iOS/Android | yes               |
| titleStyle                     | Title Text Style                                                   | style = StyleProp<TextStyle>                           | no       | iOS/Android | yes               |
| titleTestID                    | Title Test ID                                                      | string                                                 | no       | iOS/Android | yes               |

### Static Methods

| Name     | Description                             | Type     | Required | Platform    | HarmonyOS Support |
|----------|-----------------------------------------|----------|----------|-------------|-------------------|
| goToPage | function - (pageNumber: number) => void | function | no       | iOS/Android | no                |

### Tabbed Header List components

Tabbed Header List Properties

Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                           | Description                                                   | Type                                              | Required | Platform    | HarmonyOS Support |
|--------------------------------|---------------------------------------------------------------|---------------------------------------------------|----------|-------------|-------------------|
| backgroundColor                | Sets the background color of a component                      | color - ColorValue                                | no       | iOS/Android | yes               |
| backgroundImage                | Sets the background image of the widget                       | image source - ImageSourcePropType                | no       | iOS/Android | no                |
| containerStyle                 | Style the entire component container                          | style - StyleProp<ViewStyle>                      | yes      | iOS/Android | yes               |
| enableSafeAreaTopInset         | Indicates whether to set a security zone                      | boolean                                           | yes      | iOS/Android | yes               |
| foregroundImage                | Setting the avatar resource                                   | image source - ImageSourcePropType                | no       | iOS/Android | yes               |
| headerHeight                   | Sets the header height on the component                       | number                                            | no       | iOS/Android | yes               |
| logo                           | Set the logo image resource on the top                        | image source - ImageSourcePropType                | no       | iOS/Android | yes               |
| logoContainerStyle             | Sets the logo container style                                 | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| logoStyle                      | Setting the logo style                                        | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| onMomentumScrollBegin          | Sliding start event callback                                  | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onMomentumScrollEnd            | Sliding end event callback                                    | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScroll                       | Sliding event callback                                        | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollBeginDrag              | Callback of the sliding start drag event                      | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollEndDrag                | Sliding end drag event callback                               | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onTabsLayout                   | Tab bar layout change event callback                          | function - (e: LayoutChangeEvent) => void         | no       | iOS/Android | yes               |
| onTopReached                   | Top event callback                                            | function - () => void                             | no       | iOS/Android | yes               |
| parallaxHeight                 | Parallax height value(default 53% of screen's height)         | number                                            | no       | iOS/Android | yes               |
| renderHeaderBar                | headerBar Rendering Function                                  | render function                                   | no       | iOS/Android | yes               |
| snapStartThreshold             | Resistance value at the start of sliding                      | number                                            | no       | iOS/Android | yes               |
| snapStopThreshold              | Resistance value at the end of sliding                        | number                                            | no       | iOS/Android | no                |
| snapToEdge                     | enabled or not to slide to edge（default true）                 | number                                            | no       | iOS/Android | no                |
| stickyTabs                     | Indicates whether the tab bar can be fixed（default true）      | number                                            | no       | iOS/Android | yes               |
| tabTextActiveStyle             | Select a text style on the tab bar                            | style - StyleProp<TextStyle>                      | no       | iOS/Android | yes               |
| tabTextContainerStyle          | Tab Bar Text Container Style                                  | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| tabTextContainerActiveStyle    | Tab Bar Text Container Selection Style                        | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| tabTextStyle                   | Tab Bar Text Style                                            | style - StyleProp<TextStyle>                      | no       | iOS/Android | yes               |
| tabUnderlineColor              | Color of the horizontal line at the bottom of the tab bar tex | color - ColorValue                                | no       | iOS/Android | yes               |
| tabWrapperStyle                | Tab Bar Wrap Container Style                                  | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| tabs                           | Tab Bar Data Source                                           | Tabs array - Tab[]                                | no       | iOS/Android | yes               |
| tabsContainerBackgroundColor   | Tab Bar Container Background Color                            | color - ColorValue                                | no       | iOS/Android | yes               |
| tabsContainerHorizontalPadding | Tab Bar Container Horizontal Inner Margin（default 20）         | number                                            | no       | iOS/Android | yes               |
| tabsContainerStyle             | Tab Bar Container Style                                       | style - StyleProp<ViewStyle>                      | no       | iOS/Android | yes               |
| title                          | Title Text                                                    | string                                            | no       | iOS/Android | yes               |
| titleStyle                     | Title Text Style                                              | style = StyleProp<TextStyle>                      | no       | iOS/Android | yes               |
| titleTestID                    | Title Text Test ID                                            | string                                            | no       | iOS/Android | yes               |

## Details Header

It consists of the  DetailsHeaderScrollView、DetailsHeaderFlatList and DetailsHeaderSectionList components.

### Details Header ScrollView components

Details Header ScrollView Properties
Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props) and Shared DetailsHeader props Properties。

### Details Header FlatList components

Details Header FlatList Properties
Inherits [FlatListProps](https://reactnative.dev/docs/next/flatlist#props) and Shared DetailsHeader props Properties。

### Details Header SectionList components

Details Header SectionList Properties
Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props) and Shared DetailsHeader props Properties。

### Shared DetailsHeader props Properties

The DetailsHeaderScrollView, DetailsHeaderFlatList, and DetailsHeaderSectionList components share Properties.

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                           | Description                                                               | Type                                                  | Required | Platform    | HarmonyOS Support |
|--------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------|----------|-------------|-------------------|
| backgroundColor                | Sets the background color of a component                                  | color - ColorValue                                    | no       | iOS/Android | yes               |
| backgroundImage                | Sets the background image of the widget                                   | image source - ImageSourcePropType                    | no       | iOS/Android | no                |
| containerStyle                 | Style the entire component container                                      | style - StyleProp<ViewStyle>                          | yes      | iOS/Android | yes               |
| contentIcon                    | Icon on the card on the left of the profile picture                       | image source - ImageSourcePropType                    | no       | iOS/Android | yes               |
| contentIconNumber              | Number on the card on the left of the avatar                              | number                                                | no       | iOS/Android | yes               |
| contentIconNumberStyle         | Number style of the card on the left of the avatar                        | style - StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| contentIconNumberTestID        | Test ID                                                                   | string                                                | no       | iOS/Android | yes               |
| enableSafeAreaTopInset         | Indicates whether to set a security zone                                  | boolean                                               | yes      | iOS/Android | yes               |
| leftTopIcon                    | Sets the logo on the left of the head                                     | render function or image source - ImageSourcePropType | no       | iOS/Android | yes               |
| leftTopIconAccessibilityLabel  | Sets the auxiliary logo label on the left of the head                     | string                                                | no       | iOS/Android | no                |
| leftTopIconOnPress             | Callback of the logo click event on the left of the header                | function - () => void                                 | no       | iOS/Android | yes               |
| leftTopIconTestID              | Logo test ID on the left of the head                                      | string                                                | no       | iOS/Android | yes               |
| hasBorderRadius                | Whether the upper part is a layout with fillets in the lower right corner | boolean                                               | no       | iOS/Android | yes               |
| headerHeight                   | Sets the header height on the component                                   | number                                                | no       | iOS/Android | yes               |
| image                          | Character avatar image resources                                          | image source - ImageSourcePropType                    | no       | iOS/Android | yes               |
| onHeaderLayout                 | Header layout adjustment callback                                         | function - (e: LayoutChangeEvent) => void             | no       | iOS/Android | yes               |
| onMomentumScrollBegin          | Sliding start event callback                                              | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onMomentumScrollEnd            | Sliding end event callback                                                | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScroll                       | Sliding event callback                                                    | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScrollBeginDrag              | Callback of the sliding start drag event                                  | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScrollEndDrag                | Sliding end drag event callback                                           | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onTopReached                   | Top event callback                                                        | function - () => void                                 | no       | iOS/Android | yes               |
| parallaxHeight                 | Parallax height value(default 53% of screen's height)                     | number                                                | no       | iOS/Android | yes               |
| renderHeaderBar                | headerBar Rendering Function                                              | render function                                       | no       | iOS/Android | yes               |
| rightTopIcon                   | Sets the logo on the right of the head                                    | render function or image source - ImageSourcePropType | no       | iOS/Android | yes               |
| rightTopIconAccessibilityLabel | Sets the auxiliary logo label on the right of the head                    | string                                                | no       | iOS/Android | no                |
| rightTopIconOnPress            | Callback of the logo click event on the right of the header               | function - () => void                                 | no       | iOS/Android | yes               |
| rightTopIconTestID             | Logo test ID on the right of the head                                     | string                                                | no       | iOS/Android | yes               |
| snapStartThreshold             | Resistance value at the start of sliding                                  | number                                                | no       | iOS/Android | yes               |
| snapStopThreshold              | Resistance value at the end of sliding                                    | number                                                | no       | iOS/Android | no                |
| snapToEdge                     | enabled or not to slide to edge（default true）                             | number                                                | no       | iOS/Android | no                |
| subtitle                      | SubTitle Text                                                             | string                                                | no       | iOS/Android | yes               |
| subtitleStyle                 | SubTitle Text Style                                                       | style - StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| subtitleTestID                | SubTitle Text Test ID                                                     | string                                                | no       | iOS/Android | yes               |
| tag                            | Tag Text                                                                  | string                                                | no       | iOS/Android | yes               |
| tagStyle                       | Tag Text Style                                                            | style = StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| tagTestID                      | Tag Text Test ID                                                          | string                                                | no       | iOS/Android | yes               |
| title                          | Title Text                                                                | string                                                | no       | iOS/Android | yes               |
| titleStyle                     | Title Text Style                                                          | style = StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| titleTestID                    | Title Text Test ID                                                        | string                                                | no       | iOS/Android | yes               |

## Avatar Header

It consists of the AvatarHeaderScrollView, AvatarHeaderFlatList, and AvatarHeaderSectionList components.

### Avatar Header ScrollView components

Avatar Header ScrollView Properties
Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props) and Shared AvatarHeader props Properties。

### Avatar Header FlatList components

Avatar Header FlatList Properties
Inherits [FlatListProps](https://reactnative.dev/docs/next/flatlist#props)and Shared AvatarHeader props Properties。

### Avatar Header SectionList components

Avatar Header SectionList Properties
Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props) and Shared AvatarHeader props Properties。

### Shared AvatarHeader props Properties

The AvatarHeaderScrollView, AvatarHeaderFlatList, and AvatarHeaderSectionList components share Properties.

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                           | Description                                                               | Type                                                  | Required | Platform    | HarmonyOS Support |
|--------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------|----------|-------------|-------------------|
| backgroundColor                | Sets the background color of a component                                  | color - ColorValue                                    | no       | iOS/Android | yes               |
| backgroundImage                | Sets the background image of the widget                                   | image source - ImageSourcePropType                    | no       | iOS/Android | no                |
| containerStyle                 | Style the entire component container                                      | style - StyleProp<ViewStyle>                          | yes      | iOS/Android | yes               |
| enableSafeAreaTopInset         | Indicates whether to set a security zone                                  | boolean                                               | yes      | iOS/Android | yes               |
| leftTopIcon                    | Sets the logo on the left of the head                                     | render function or image source - ImageSourcePropType | no       | iOS/Android | yes               |
| leftTopIconAccessibilityLabel  | Sets the auxiliary logo label on the left of the head                     | string                                                | no       | iOS/Android | no                |
| leftTopIconOnPress             | Callback of the logo click event on the left of the header                | function - () => void                                 | no       | iOS/Android | yes               |
| leftTopIconTestID              | Logo test ID on the left of the head                                      | string                                                | no       | iOS/Android | yes               |
| hasBorderRadius                | Whether the upper part is a layout with fillets in the lower right corner | boolean                                               | no       | iOS/Android | yes               |
| headerHeight                   | Sets the header height on the component                                   | number                                                | no       | iOS/Android | yes               |
| image                          | Character avatar image resources                                          | image source - ImageSourcePropType                    | no       | iOS/Android | yes               |
| onHeaderLayout                 | Header layout adjustment callback                                         | function - (e: LayoutChangeEvent) => void             | no       | iOS/Android | yes               |
| onMomentumScrollBegin          | Sliding start event callback                                              | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onMomentumScrollEnd            | Sliding end event callback                                                | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScroll                       | Sliding event callback                                                    | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScrollBeginDrag              | Callback of the sliding start drag event                                  | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onScrollEndDrag                | Sliding end drag event callback                                           | worklet function - (e: NativeScrollEvent) => void     | no       | iOS/Android | yes               |
| onTopReached                   | Top event callback                                                        | function - () => void                                 | no       | iOS/Android | yes               |
| parallaxHeight                 | Parallax height value(default 53% of screen's height)                     | number                                                | no       | iOS/Android | yes               |
| renderHeaderBar                | headerBar Rendering Function                                              | render function                                       | no       | iOS/Android | yes               |
| rightTopIcon                   | Sets the logo on the right of the head                                    | render function or image source - ImageSourcePropType | no       | iOS/Android | yes               |
| rightTopIconAccessibilityLabel | Sets the auxiliary logo label on the right of the head                    | string                                                | no       | iOS/Android | no                |
| rightTopIconOnPress            | Callback of the logo click event on the right of the header               | function - () => void                                 | no       | iOS/Android | yes               |
| rightTopIconTestID             | Logo test ID on the right of the head                                     | string                                                | no       | iOS/Android | yes               |
| snapStartThreshold             | Resistance value at the start of sliding                                  | number                                                | no       | iOS/Android | yes               |
| snapStopThreshold              | Resistance value at the end of sliding                                    | number                                                | no       | iOS/Android | no                |
| snapToEdge                     | enabled or not to slide to edge（default true）                             | number                                                | no       | iOS/Android | no                |
| subtitle                      | SubTitle Text                                                             | string                                                | no       | iOS/Android | yes               |
| subtitleStyle                 | SubTitle Text Style                                                       | style - StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| subtitleTestID                | SubTitle Text Test ID                                                     | string                                                | no       | iOS/Android | yes               |
| title                          | Title Text                                                                | string                                                | no       | iOS/Android | yes               |
| titleStyle                     | Title Text Style                                                          | style = StyleProp<TextStyle>                          | no       | iOS/Android | yes               |
| titleTestID                    | Title Text Test ID                                                        | string                                                | no       | iOS/Android | yes               |

## Custom Sticky Header

It consists of the StickyHeaderScrollView、StickyHeaderFlatList and StickyHeaderSectionList components.

### Sticky Header ScrollView components

Sticky Header ScrollView Properties
Inherits [ScrollViewProps](https://reactnative.dev/docs/next/scrollview#props) and Shared StickyHeader props Properties。

### Sticky Header FlatList components

Sticky Header FlatList Properties
Inherits [FlatListProps](https://reactnative.dev/docs/next/flatlist#props) and Shared StickyHeader props Properties。

### Sticky Header SectionList components

Avatar Header SectionList Properties
Inherits [SectionListProps](https://reactnative.dev/docs/next/sectionlist/#props) and Shared StickyHeader props Properties。

### Shared StickyHeader props Properties

The StickyHeaderScrollView, StickyHeaderFlatList, and StickyHeaderSectionList components share Properties.

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                              | Type                                              | Required | Platform    | HarmonyOS Support |
|-----------------------|----------------------------------------------------------|---------------------------------------------------|----------|-------------|-------------------|
| containerStyle        | Style the entire component container                     | style - StyleProp<ViewStyle>                      | yes      | iOS/Android | yes               |
| onHeaderLayout        | Header layout adjustment callback                        | function - (e: LayoutChangeEvent) => void         | no       | iOS/Android | yes               |
| onMomentumScrollBegin | Sliding start event callback                             | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onMomentumScrollEnd   | Sliding end event callback                               | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScroll              | Sliding event callback                                   | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollBeginDrag     | Callback of the sliding start drag event                 | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| onScrollEndDrag       | Sliding end drag event callback                          | worklet function - (e: NativeScrollEvent) => void | no       | iOS/Android | yes               |
| renderHeader          | header rendering function                                | render function                                   | no       | iOS/Android | yes               |
| renderTabs            | tab rendering function                                   | render function                                   | no       | iOS/Android | yes               |
| stickyTabs            | Indicates whether the tab bar can be fixed（default true） | number                                            | no       | iOS/Android | yes               |

## FlashList Headers

It consists of the  AvatarHeaderFlashList、DetailsHeaderFlashList and TabbedHeaderFlashList components.

### Avatar Header FlashList Components

Avatar Header FlashList Properties
Inherits [FlashListProps](https://shopify.github.io/flash-list/docs/usage/)and Shared AvatarHeader props Properties。

### Details Header FlashList Components

Details Header FlashList Properties
Inherits [FlashListProps](https://shopify.github.io/flash-list/docs/usage/)and Shared DetailsHeader props Properties。

### Tabbed Header FlashList Components

Tabbed Header FlashList Properties
Inherits [FlashListProps](https://shopify.github.io/flash-list/docs/usage/)and Tabbed Header List props Properties。

## Known Issues

## Others

- [ ] Some Properties of the TabbedHeaderPager Component in the Original Database Do Not Take Effect[issue#415](https://github.com/netguru/sticky-parallax-header/issues/415)
- [ ] Some properties of the DetailHeader and AvatarHeader components in the original database do not take effect[issue#416](https://github.com/netguru/sticky-parallax-header/issues/416)
- [ ] The ref.current.goToPage method in the source database does not exist[issue#412](https://github.com/netguru/sticky-parallax-header/issues/412)

## License

This project is licensed under [The MIT License (MIT)](https://github.com/netguru/sticky-parallax-header/blob/master/LICENSE).
