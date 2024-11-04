> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-paper</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-native-paper">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/react-native-paper/blob/main/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/callstack/react-native-paper)


## 安装与使用

<!-- tabs:start -->

#### **yarn**

```bash
yarn add react-native-paper@^5.12.3
```
#### **npm**
```bash
npm install react-native-paper@^5.12.3
```
<!-- tabs:end -->

**下面的代码展示了这个库的基本使用场景：**

> [!WARNING] 使用时 import 的库名不变。

paper使用需要安装react-native-safe-area-context来处理安全区域。另外还需要依赖react-native-vector-icons库，具体来说，MaterialCommunityIcons图标包需要包含在项目中，因为有些组件在内部使用它。

1.将根组件包装在PaperProvider中。如果您有一个原始的 React Native 项目，最好将其添加到传递给 的组件中AppRegistry.registerComponent。这通常在index.js文件中

```js
import { PaperProvider } from 'react-native-paper';
import App from '../App';

export default function PaperExample() {
    return (
      <PaperProvider>
        <App />
      </PaperProvider>
    );
}
AppRegistry.registerComponent(appName, () => PaperExample);
```
2.包装PaperProvider之后，我们需要将展示的组件传递到 Providers 中。在这一部分，我们使用ActivityIndicator作为示例展示
```js
export default function App() {
  return (
    <View style={{backgroundColor: 'black'}}>
      <StatusBar barStyle="light-content" />
      <SafeAreaView>
        <NavigationContainer>
          <PortalProvider>
           <View id="__harmony::ready" />
            <Page name="EXAMPLE: ActivityIndicatorDemo">
              <ActivityIndicatorDemo/>
            </Page>
            ......
          </PortalProvider>
        </NavigationContainer>
      </SafeAreaView>
      </StatusBar>
    </View>      
  );
}
```
3.活动指示器用于显示应用中某些活动的进度。它可以作为 React Native 附带的 ActivityIndi​​cator 的插件使用。
```js
import * as React from 'react';
import { ActivityIndicator, MD2Colors } from 'react-native-paper';

const ActivityIndicatorDemo = () => (
  <ActivityIndicator animating={true} color={MD2Colors.red800} />
);

export default ActivityIndicatorDemo;
```
## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-safe-area-context和@react-native-oh-tpl/react-native-vector-icons的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入react-native-safe-area-context请参照[@react-native-oh-tpl/react-native-safe-area-context 文档](/zh-cn/react-native-safe-area-context.md)进行引入

如未引入react-native-vector-icons请参照[@react-native-oh-tpl/react-native-vector-icons 文档](/zh-cn/react-native-vector-icons.md)进行引入

## 约束与限制
### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20-CAPI; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 组件

详情查看[Paper官方文档](https://callstack.github.io/react-native-paper)

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ActivityIndicator  | Activity indicator is used to present progress of some activity in the app. It can be used as a drop-in for the ActivityIndicator shipped with React Native | component  | No | iOS/Android      | yes |
| Appbar  | A component to display action items in a bar. It can be placed at the top or bottom | component  | No | iOS/Android      | yes |
| Avatar  | Avatars can be used to represent people in a graphical way | component  | No | iOS/Android      | yes |
| Badge  | Badges are small status descriptors for UI elements | component  | No | iOS/Android      | yes |
| Banner  | Banner displays a prominent message and related actions | component  | No | iOS/Android      | yes |
| BottomNavigation  | BottomNavigation provides quick navigation between top-level views of an app with a bottom navigation bar | component  | No | iOS/Android      | yes |
| Button  | A button is component that the user can press to trigger an action | component  | No | iOS/Android      | yes |
| Card  | A card is a sheet of material that serves as an entry point to more detailed information | component  | No | iOS/Android      | yes |
| Checkbox  | A card is a sheet of material that serves as an entry point to more detailed information | component  | No | iOS/Android      | yes |
| Chip  | Chips are compact elements that can represent inputs, attributes, or actions. They can have an icon or avatar on the left, and a close button icon on the right | component  | No | iOS/Android      | yes |
| DataTable  | Data tables allow displaying sets of data | component  | No | iOS/Android      | yes |
| Dialog  | Dialogs inform users about a specific task and may contain critical information, require decisions, or involve multiple tasks | component  | No | iOS/Android      | yes |
| Divider  | A divider is a thin, lightweight separator that groups content in lists and page layouts | component  | No | iOS/Android    | yes |
| Drawer  | Collapsed component used to show an action item with an icon and optionally label in a navigation drawer | component  | No | iOS/Android    | yes |
| FAB  | A floating action button represents the primary action on a screen. It appears in front of all screen content.  | component  | No | iOS/Android    | yes |
| HelperText  | Helper text is used in conjuction with input elements to provide additional hints for the user  | component  | No | iOS/Android    | yes |
| Icon  | An icon component which renders icon from vector library  | component  | No | iOS/Android    | yes |
| IconButton  | An icon component which renders icon from vector library  | component  | No | iOS/Android    | yes |
| List  | A component used to display an expandable list item  | component  | No | iOS/Android    | yes |
| Menu  | Menus display a list of choices on temporary elevated surfaces. Their placement varies based on the element that opens them  | component  | No | iOS/Android    | yes |
| Modal  | The Modal component is a simple way to present content above an enclosing view. To render the Modal above other components, you'll need to wrap it with the Portal component  | component  | No | iOS/Android    | yes |
| Portal  | Portal allows rendering a component at a different place in the parent tree  | component  | No | iOS/Android    | yes |
| ProgressBar  | Progress bar is an indicator used to present progress of some activity in the app.  | component  | No | iOS/Android    | yes |
| RadioButton  | Radio buttons allow the selection a single option from a set.  | component  | No | iOS/Android    | yes |
| Searchbar  | Searchbar is a simple input box where users can type search queries.  | component  | No | iOS/Android    | yes |
| SegmentedButtons  | Segmented buttons can be used to select options, switch views or sort elements  | component  | No | iOS/Android    | yes |
| Snackbar  | Snackbars provide brief feedback about an operation through a message rendered at the bottom of the container in which it's wrapped  | component  | No | iOS/Android    | yes |
| Surface  | Surface is a basic container that can give depth to an element with elevation shadow  | component  | No | iOS/Android    | yes |
| Surface  | Switch is a visual toggle between two mutually exclusive states — on and off.  | component  | No | iOS/Android    | yes |
| Text  | Typography component showing styles complied with passed variant prop and supported by the type system.  | component  | No | iOS/Android    | yes |
| TextInput  | A component to allow users to input text.  | component  | No | iOS/Android    | yes |
| ToggleButton  | Toggle buttons can be used to group related options. To emphasize groups of related toggle buttons, a group should share a common container  | component  | No | iOS/Android    | yes |
| Tooltip  | Tooltips display informative text when users hover over, focus on, or tap an element  | component  | No | iOS/Android    | yes |
| TouchableRipple  | A wrapper for views that should respond to touches  | component  | No | iOS/Android    | yes |

## 属性

详情查看[Paper官方组件介绍文档](https://callstack.github.io/react-native-paper/docs/components/ActivityIndicator#animating)

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**ActivityIndicator**：Activity indicator is used to present progress of some activity in the app. It can be used as a drop-in for the ActivityIndicator shipped with React Native
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  animating  |  Whether to show the indicator or hide it   | boolean | Yes      | All      | Yes               |
| color  |  The color of the spinner   | string | Yes      | All      | Yes               |
| size |  Size of the indicator   |      small \| large \| number     | No       | All      | Yes               |
|  hidesWhenStopped  |    Whether the indicator should hide when not animating     |     boolean      | No       | All      | Yes               |
|  theme   |  theme | ThemeProp | Yes      | All      | Yes               |
|  style   |  style | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |

**Appbar**：A component to display action items in a bar. It can be placed at the top or bottom
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children   |  Content of the Appbar   | React.ReactNode | Yes      | All      | Yes               |
| mode   |  Mode of the Appbar.   | small \| medium \| large \| center-aligned | Yes      | All      | Yes               |
| elevated  |  Whether Appbar background should have the elevation along with primary color pigment.   |     boolean      | No       | All      | Yes               |
|  safeAreaInsets   |   Safe area insets for the Appbar     |     { bottom?: number; top?: number; left?: number; right?: number; }      | No       | All      | Yes               |
|  theme   |  theme | ThemeProp | Yes      | All      | Yes               |
|  style   |  style | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |

**Appbar.Action**：A component used to display an action item in the appbar.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  color   |  Custom color for action icon   | string | Yes      | All      | Yes               |
|  rippleColor   |  Color of the ripple effect   | ColorValue | Yes      | All      | Yes               |
|  icon    |  Name of the icon to show   | IconSource | Yes      | All      | Yes               |
|  size    | Optional icon size   | number | Yes      | All      | Yes               |
|  disabled    | Whether the button is disabled. A disabled button is greyed out and onPress is not called on touch.   | boolean | Yes      | All      | Yes               |
|  accessibilityLabel    | Accessibility label for the button. This is read by the screen reader when the user taps the button   | string | Yes      | All      | Yes               |
|  onPress    | Whether it's the leading button.   | fuction | Yes      | All      | Yes               |
|  isLeading (Available in v5.x with theme version 3)    | Whether it's the leading button.   | boolean | Yes      | All      | NO               |
|  style   |  Style for Appbar.Action container | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |
|  ref   |  ref | React.RefObject<View> | Yes      | All      | Yes               |
|  theme   |  theme | ThemeProp | Yes      | All      | Yes               |

**Appbar.BackAction**：A component used to display a back button in the appbar.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  color   |  Custom color for action icon   | string | Yes      | All      | Yes               |
|  size    | Optional icon size   | number | Yes      | All      | Yes               |
|  disabled    | Whether the button is disabled. A disabled button is greyed out and onPress is not called on touch.   | boolean | Yes      | All      | Yes               |
|  accessibilityLabel    | Accessibility label for the button. This is read by the screen reader when the user taps the button   | string | Yes      | All      | Yes               |
|  onPress    | Function to execute on press.   | fuction | Yes      | All      | Yes               |
|       style        |            Style for Appbar.BackAction container             | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |
|        ref         |                             ref                              |              React.RefObject<View>               | Yes      | All      | Yes               |

**Appbar.Content**：A component used to display a title and optional subtitle in an appbar

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title (required)   |  Text or component for the title.  | React.ReactNode | Yes      | All      | Yes               |
|  titleStyle    | Style for the title, if title is a string.   | StyleProp<TextStyle> | Yes      | All      | Yes               |
|  titleRef    | Reference for the title.   | React.RefObject<TextRef> | Yes      | All      | Yes               |
|  onPress    | Function to execute on press.   | fuction | Yes      | All      | Yes               |
|  disabled    | If true, disable all interactions for this component.   | boolean | Yes      | All      | Yes               |
|  color    | Custom color for the text   | string | Yes      | All      | Yes               |
|  titleMaxFontSizeMultiplier    | Specifies the largest possible scale a title font can reach   | number | Yes      | All      | Yes               |
|  style   |  Style for Appbar.Content container | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |
|           theme            |                            theme                            |                    ThemeProp                     | Yes      | All      | Yes               |
|           testID           |                 testID to be used on tests.                 |                      string                      | Yes      | All      | Yes               |

**Appbar.Header**：A component to use as a header at the top of the screen. It can contain the screen title, controls such as navigation buttons, menu button etc.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  dark  |  Whether the background color is a dark color. A dark header will render light text and vice-versa  | boolean | Yes      | All      | Yes               |
|  statusBarHeight    | Extra padding to add at the top of header to account for translucent status bar   | number | Yes      | All      | Yes               |
|  children (required)    | Reference for the title.   | React.ReactNode | Yes      | All      | Yes               |
|  mode     | Mode of the Appbar.   | small \| medium \| large \| center-aligned | Yes      | All      | Yes               |
|  elevated      | Whether Appbar background should have the elevation along with primary color pigment   | boolean | Yes      | All      | Yes               |
|  ref   |  ref | React.RefObject<View> | Yes      | All      | Yes               |
|  theme   |  theme | ThemeProp | Yes      | All      | Yes               |
|  testID   |  testID to be used on tests. | string | Yes      | All      | Yes               |

**Avatar.Icon**：Avatars can be used to represent people in a graphical way.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)  | Icon to display for the Avatar.  | IconSource | Yes      | All      | Yes               |
|  size  | Size of the avatar.  | number | Yes      | All      | Yes               |
|  color  | Custom color for the icon.  | string | Yes      | All      | Yes               |
|  style  | style | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme   |  theme | ThemeProp | Yes      | All      | Yes               |

**Avatar.Image**：Avatars can be used to represent people in a graphical way.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  source (required)  | Image to display for the Avatar. It accepts a standard React Native Image source prop Or a function that returns an Image  | ImageSourcePropType  | Yes      | All      | Yes               |
|  size  | Size of the avatar.  | number | Yes      | All      | Yes               |
|  style   |  style | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |
|  onError   |  Invoked on load error. | fuction | Yes      | All      | Yes               |
|  onLayout   |  Invoked on mount and on layout changes. | fuction | Yes      | All      | Yes               |
|  onLoad   |  Invoked when load completes successfully. | fuction | Yes      | All      | Yes               |
|  onLoadEnd   |  Invoked when load either succeeds or fails. | fuction | Yes      | All      | Yes               |
|  onLoadStart   |  Invoked on load start. | fuction | Yes      | All      | Yes               |
|  onProgress   |  Invoked on download progress. | fuction | Yes      | All      | Yes               |
|  theme   | theme  | ThemeProp | Yes      | All      | Yes               |

**Avatar.Text**：Avatars can be used to represent people in a graphical way.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  label (required)  | Initials to show as the text in the Avatar.  | string  | Yes      | All      | Yes               |
|  size  | Size of the avatar.  | number | Yes      | All      | Yes               |
|  color  | Custom color for the text.  | string | Yes      | All      | Yes               |
|  style  | Style for text container  | StyleProp<TextStyle> | Yes      | All      | Yes               |
|  labelStyle  | Style for the title.  | StyleProp<TextStyle> | Yes      | All      | Yes               |
|  maxFontSizeMultiplier  | Specifies the largest possible scale a text font can reach.  | number | Yes      | All      | Yes               |
|  theme   | theme  | ThemeProp | Yes      | All      | Yes               |

**Badge**：Badges are small status descriptors for UI elements
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  visible  | Whether the badge is visible  | boolean  | Yes      | All      | Yes               |
|  children  | Content of the Badge  | string  \| number | Yes      | All      | Yes               |
|  size  | Size of the Badge  |  number | Yes      | All      | Yes               |
|  style  | Style for Badge container  | StyleProp<TextStyle> | Yes      | All      | Yes               |
|  ref  | ref  | React.RefObject<typeof Animated.Text> | Yes      | All      | Yes               |
|  theme   | theme  | ThemeProp | Yes      | All      | Yes               |

**Banner**：Banner displays a prominent message and related actions.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  visible  | Whether the badge is visible  | boolean  | Yes      | All      | Yes               |
|  children  | Content of the Badge  |React.ReactNode | Yes      | All      | Yes               |
|  icon  | Icon to display for the Banner. Can be an image.  |  IconSource | Yes      | All      | Yes               |
|  actions  | Action items to shown in the banner |  Array< { label: string; } | Yes      | All      | Yes               |
|  contentStyle  | Style of banner's inner content. Use this prop to apply custom width for wide layouts. |  StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  elevation   | Changes Banner shadow and background on iOS and Android.|   Animated.Value | Yes      | All      | Yes               |
|  maxFontSizeMultiplier   | Specifies the largest possible scale a text font can reach.|   number | Yes      | All      | Yes               |
|  onShowAnimationFinished   | Optional callback that will be called after the opening animation finished running normally|   Animated.EndCallback | Yes      | All      | Yes               |
|  onHideAnimationFinished   | Optional callback that will be called after the closing animation finished running normally|   Animated.EndCallback | Yes      | All      | Yes               |
|  style  | Style for Badge container  | StyleProp<TextStyle> | Yes      | All      | Yes               |
|  ref  | ref  | React.RefObject<typeof Animated.Text> | Yes      | All      | Yes               |
|  theme   | theme  | ThemeProp | Yes      | All      | Yes               |

**BottomNavigation**：BottomNavigation provides quick navigation between top-level views of an app with a bottom navigation bar.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  shifting  | Whether the shifting style is used, the active tab icon shifts up to show the label and the inactive tabs won't have a label.  | boolean  | Yes      | All      | Yes               |
|  labeled  | Whether to show labels in tabs. When false, only icons will be displayed.  |boolean | Yes      | All      | Yes               |
|  compact  | Whether tabs should be spread across the entire width.  |  boolean | Yes      | All      | Yes               |
|  navigationState (required)  | State for the bottom navigation. The state should contain the following properties|  { index: number; routes: Route[]; } | Yes      | All      | Yes               |
|  onIndexChange (required)  | Callback which is called on tab change, receives the index of the new tab as argument|  (index: number) => void | Yes      | All      | Yes               |
|  renderScene (required)  | Callback which returns a react element to render as the page for the tab |  (props: { route: Route; jumpTo: (key: string) => void; }) => React.ReactNode \| null | Yes      | All      | Yes               |
|  renderIcon  | Callback which returns a React Element to be used as tab icon. | (props: { route: Route; focused: boolean; color: string; }) => React.ReactNode \| null | Yes      | All      | Yes               |
|  renderLabel  | Callback which React Element to be used as tab label. | (props: { route: Route; focused: boolean; color: string; }) => React.ReactNode \| null | Yes      | All      | Yes               |
|  renderTouchable  | Callback which returns a React element to be used as the touchable for the tab item. | (props: TouchableProps<Route>) => React.ReactNode \| null | Yes      | All      | Yes               |
|  getAccessibilityLabel  | Get accessibility label for the tab button. | (props: { route: Route }) => string \| undefined \| null | Yes      | All      | Yes               |
|  getBadge  | Get badge for the tab, uses route.badge by default. | (props: { route: Route }) => boolean \| number \| string \| undefined \| null | Yes      | All      | Yes               |
|  getColor  | Get color for the tab, uses route.color by default. | (props: { route: Route }) => string \| undefined \| number \| string \| undefined \| null | Yes      | All      | Yes               |
|  getLabelText  | Get label text for the tab, uses route.title by default. Use renderLabel to replace label component. | (props: { route: Route }) => string \| undefined \| undefined \| number \| string \| undefined \| null | Yes      | All      | Yes               |
|  getTestID  | Get the id to locate this tab button in tests, uses route.testID by default. | (props: { route: Route }) => string \| undefined | Yes      | All      | Yes               |
|  getLazy  | Get lazy for the current screen. Uses true by default. | (props: { route: Route }) => string \| undefined | Yes      | All      | Yes               |
|  onTabPress  | Function to execute on tab press. It receives the route for the pressed tab, useful for things like scroll to top. | (props: { route: Route } & TabPressEvent) => void | Yes      | All      | Yes               |
|  onTabLongPress  | Function to execute on tab long press. It receives the route for the pressed tab, useful for things like custom action when longed pressed. | (props: { route: Route } & TabPressEvent) => void | Yes      | All      | Yes               |
|  activeColor  | Custom color for icon and label in the active tab. | string | Yes      | All      | Yes               |
|  inactiveColor  | Custom color for icon and label in the inactive tab. | string | Yes      | All      | Yes               |
|  sceneAnimationEnabled  | Whether animation is enabled for scenes transitions in shifting mode. | boolean | Yes      | All      | Yes               |
|  sceneAnimationEasing  | The scene animation Easing. | EasingFunction \| undefined | Yes      | All      | Yes               |
|  sceneAnimationType  | The scene animation effect. Specify 'shifting' for a different effect. By default, 'opacity' will be used. | 'opacity' \| 'shifting' | Yes      | All      | Yes               |
|  keyboardHidesNavigationBar  | Whether the bottom navigation bar is hidden when keyboard is shown | boolean | Yes      | All      | Yes               |
|  safeAreaInsets  | Safe area insets for the tab bar | { top?: number; right?: number; bottom?: number; left?: number; } | Yes      | All      | Yes               |
|  activeIndicatorStyle  | Style for the bottom navigation bar. You can pass a custom background color here | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  labelMaxFontSizeMultiplier  | Specifies the largest possible scale a label font can reach. | number | Yes      | All      | Yes               |
|  style  | Style for Badge container  | StyleProp<TextStyle> | Yes      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string | Yes      | All      | Yes               |

**BottomNavigation.Bar**：A navigation bar which can easily be integrated with React Navigation's Bottom Tabs Navigator.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  shifting  | Whether the shifting style is used, the active tab icon shifts up to show the label and the inactive tabs won't have a label.  | boolean  | Yes      | All      | Yes               |
|  labeled  | Whether to show labels in tabs. When false, only icons will be displayed.  |boolean | Yes      | All      | Yes               |
|  compact  | Whether tabs should be spread across the entire width.  |  boolean | Yes      | All      | Yes               |
|  navigationState (required)  | State for the bottom navigation. The state should contain the following properties|  { index: number; routes: Route[]; } | Yes      | All      | Yes               |
|  renderScene (required)  | Callback which returns a react element to render as the page for the tab |  (props: { route: Route; jumpTo: (key: string) => void; }) => React.ReactNode \| null | Yes      | All      | Yes               |
|  renderIcon  | Callback which returns a React Element to be used as tab icon. | (props: { route: Route; focused: boolean; color: string; }) => React.ReactNode \| null | Yes      | All      | Yes               |
|  renderLabel  | Callback which React Element to be used as tab label. | (props: { route: Route; focused: boolean; color: string; }) => React.ReactNode \| null | Yes      | All      | Yes               |
|  renderTouchable  | Callback which returns a React element to be used as the touchable for the tab item. | (props: TouchableProps<Route>) => React.ReactNode \| null | Yes      | All      | Yes               |
|  getAccessibilityLabel  | Get accessibility label for the tab button. | (props: { route: Route }) => string \| undefined \| null | Yes      | All      | Yes               |
|  getBadge  | Get badge for the tab, uses route.badge by default. | (props: { route: Route }) => boolean \| number \| string \| undefined \| null | Yes      | All      | Yes               |
|  getColor  | Get color for the tab, uses route.color by default. | (props: { route: Route }) => string \| undefined \| number \| string \| undefined \| null | Yes      | All      | Yes               |
|  getLabelText  | Get label text for the tab, uses route.title by default. Use renderLabel to replace label component. | (props: { route: Route }) => string \| undefined \| undefined \| number \| string \| undefined \| null | Yes      | All      | Yes               |
|  getTestID  | Get the id to locate this tab button in tests, uses route.testID by default. | (props: { route: Route }) => string \| undefined | Yes      | All      | Yes               |
|  onTabPress  | Function to execute on tab press. It receives the route for the pressed tab, useful for things like scroll to top. | (props: { route: Route } & TabPressEvent) => void | Yes      | All      | Yes               |
|  onTabLongPress  | Function to execute on tab long press. It receives the route for the pressed tab, useful for things like custom action when longed pressed. | (props: { route: Route } & TabPressEvent) => void | Yes      | All      | Yes               |
|  activeColor  | Custom color for icon and label in the active tab. | string | Yes      | All      | Yes               |
|  inactiveColor  | Custom color for icon and label in the inactive tab. | string | Yes      | All      | Yes               |
|  animationEasing  | The scene animation Easing. | EasingFunction \| undefined | Yes      | All      | Yes               |
|  keyboardHidesNavigationBar  | Whether the bottom navigation bar is hidden when keyboard is shown | boolean | Yes      | All      | Yes               |
|  safeAreaInsets  | Safe area insets for the tab bar | { top?: number; right?: number; bottom?: number; left?: number; } | Yes      | All      | Yes               |
|  barStyle  | Style for the bottom navigation bar. You can pass a custom background color here | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |
|  labelMaxFontSizeMultiplier  | Specifies the largest possible scale a label font can reach. | number | Yes      | All      | Yes               |
|  style  | Style for Badge container  | StyleProp<TextStyle> | Yes      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string | Yes      | All      | Yes               |

**Button**：A button is component that the user can press to trigger an action.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  mode  | Mode of the button. You can change the mode to adjust the styling to give it desired emphasis  | text \| outlined \| contained \| elevated \| contained-tonal | Yes      | All      | Yes               |
|  dark  | Whether the color is a dark color. A dark button will render light text and vice-versa. Only applicable for  | boolean | Yes      | All      | Yes               |
|  compact  | Use a compact look, useful for text buttons in a row.  | boolean | Yes      | All      | Yes               |
|  buttonColor  | Custom button's background color. | string | Yes      | All      | Yes               |
|  textColor  | Custom button's text color. | string | Yes      | All      | Yes               |
|  rippleColor  | Color of the ripple effect. | ColorValue | Yes      | All      | Yes               |
|  loading  | Whether to show a loading indicator. | boolean | Yes      | All      | Yes               |
|  icon  | Icon to display for the Button. | IconSource | Yes      | All      | Yes               |
|  disabled  | Whether the button is disabled. A disabled button is greyed out and onPress is not called on touch | boolean | Yes      | All      | Yes               |
|  children (required)  | Label text of the button. | React.ReactNode | Yes      | All      | Yes               |
|  uppercase  | Make the label text uppercased. Note that this won't work if you pass React elements as children. | boolean | Yes      | All      | Yes               |
|  background  | Type of background drawabale to display the feedback (Android). | PressableAndroidRippleConfig | Yes      | All      | Yes               |
|  accessibilityLabel  | Accessibility label for the button. This is read by the screen reader when the user taps the button. | string | Yes      | All      | Yes               |
|  accessibilityHint  | Accessibility hint for the button. This is read by the screen reader when the user taps the button. | string | Yes      | All      | Yes               |
|  accessibilityRole  | Accessibility role for the button. The "button" role is set by default. | AccessibilityRole | Yes      | All      | Yes               |
|  onPress  | Function to execute on press. | (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  onPressIn  | Function to execute as soon as the touchable element is pressed and invoked even before onPress. | (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  onPressOut  | Function to execute as soon as the touch is released even before onPress. | (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  onLongPress  | Function to execute on long press. | (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  delayLongPress  | The number of milliseconds a user must touch the element before executing onLongPress. | number | Yes      | All      | Yes               |
|  contentStyle  | Style of button's inner content. Use this prop to apply custom height and width and to set the icon on the right with flexDirection: 'row-reverse'. | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  maxFontSizeMultiplier  | Specifies the largest possible scale a text font can reach. | number | Yes      | All      | Yes               |
|  style  | Style for Badge Button | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |
|  labelStyle  | Style for the button text. | StyleProp<TextStyle> | Yes      | All      | Yes               |
|  theme  | theme | ThemeProp | Yes      | All      | Yes               |
|  touchableRef  | Reference for the touchable | React.RefObject<View> | Yes      | All      | Yes               |
|  testID  | string | testID to be used on tests. | Yes      | All      | Yes               |

**Card**：A card is a sheet of material that serves as an entry point to more detailed information.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  mode  | Mode of the Card.  |  outlined \| contained \| elevated | Yes      | All      | Yes               |
|  children (required)  | Content of the Card | React.ReactNode | Yes      | All      | Yes               |
|  onLongPress  | Function to execute on long press. | () => void | Yes      | All      | Yes               |
|  onPress  | Function to execute on press | (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  onPressIn  | Function to execute as soon as the touchable element is pressed and invoked even before onPress. | (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  onPressOut  | Function to execute as soon as the touch is released even before onPress. | (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  delayLongPress  | The number of milliseconds a user must touch the element before executing onLongPress. | number | Yes      | All      | Yes               |
|  disabled  | TIf true, disable all interactions for this component. | boolean | Yes      | All      | Yes               |
|  elevation  | Changes Card shadow and background on iOS and Android. | Animated.Value | Yes      | All      | Yes               |
|  contentStyle  | Style of card's inner content. | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  style  | style | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme  | theme | ThemeProp | Yes      | All      | Yes               |
|  testID  | Pass down testID from card props to touchable | string | Yes      | All      | Yes               |
|  accessible  | Pass down accessible from card props to touchable | boolean | Yes      | All      | Yes               |

**Card.Actions**：A component to show a list of actions inside a Card.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Items inside the CardActions. |  React.ReactNode | Yes      | All      | Yes               |
|  style  | style |  StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme  | theme |  ThemeProp | Yes      | All      | Yes               |

**Card.Content**：A component to show content inside a Card.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Items inside the Card.Content. |  React.ReactNode | Yes      | All      | Yes               |
|  style  | style |  StyleProp<ViewStyle> | Yes      | All      | Yes               |

**Card.Cover**：A component to show a cover image inside a Card.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  Image props  | Extends: ...Image props |  props | Yes      | All      | Yes               |
|  style  | style |  StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme  | theme |  ThemeProp | Yes      | All      | Yes               |

**Card.Title**：A component to show a title, subtitle and an avatar inside a Card.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title (required)  | Text for the title. Note that this will only accept a string or <Text>-based node.|  React.ReactNode | Yes      | All      | Yes               |
|  titleStyle  | StyleProp<TextStyle> |  Style for the title. | Yes      | All      | Yes               |
|  titleNumberOfLines  | Number of lines for the title. |  number | Yes      | All      | Yes               |
|  titleVariant(Available in v5.x with theme version 3)   | Title text variant defines appropriate text styles for type role and its size. Available variants: |  unknown | Yes      | All      | Yes               |
|  subtitle   | Text for the subtitle. Note that this will only accept a string or <Text>-based node. |  React.ReactNode | Yes      | All      | Yes               |
|  subtitleStyle   | Style for the subtitle. |  StyleProp<TextStyle> | Yes      | All      | Yes               |
|  subtitleNumberOfLines   | Number of lines for the subtitle. |  number | Yes      | All      | Yes               |
|  subtitleVariant (Available in v5.x with theme version 3)   | Subtitle text variant defines appropriate text styles for type role and its size. Available variants |  unknown | Yes      | All      | Yes               |
|  left   | Callback which returns a React element to display on the left side. |  (props: { size: number }) => React.ReactNode | Yes      | All      | Yes               |
|  leftStyle   | Style for the left element wrapper. |  StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  right   | Callback which returns a React element to display on the right side. |  (props: { size: number }) => React.ReactNode | Yes      | All      | Yes               |
|  rightStyle   |Style for the right element wrapper. |  StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  titleMaxFontSizeMultiplier   |Specifies the largest possible scale a title font can reach.|  number | Yes      | All      | Yes               |
|  subtitleMaxFontSizeMultiplier   |Specifies the largest possible scale a subtitle font can reach.|  number | Yes      | All      | Yes               |
|  style   |style|  StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme   |theme|  ThemeProp | Yes      | All      | Yes               |

**Checkbox**：Checkboxes allow the selection of multiple options from a set.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  status (required)  | Status of checkbox.  |  checked \| unchecked \| indeterminate | Yes      | All      | Yes               |
|  disabled  | Whether checkbox is disabled.  |  boolean | Yes      | All      | Yes               |
|  onPress  | Function to execute on press.  |  (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  uncheckedColor  | Custom color for unchecked checkbox.  |  string | Yes      | All      | Yes               |
|  color  | Custom color for checkbox.  |  string | Yes      | All      | Yes               |
|  theme  | theme  |  ThemeProp | Yes      | All      | Yes               |
|  testID  | theme  |  string | Yes      | All      | Yes               |

**Checkbox.Android**：Checkboxes allow the selection of multiple options from a set. This component follows platform guidelines for iOS, but can be used on any platform.

|       Name        |             Description              |       TypeTouchableRipple props       | Required | Platform | HarmonyOS Support |
| :---------------: | :----------------------------------: | :-----------------------------------: | -------- | -------- | ----------------- |
|  TouchableRipple  |              Touchable               |         TouchableRipple props         | NO       | All      | Yes               |
| status (required) |         Status of checkbox.          | checked \| unchecked \| indeterminate | Yes      | All      | Yes               |
|     disabled      |    Whether checkbox is disabled.     |                boolean                | NO       | All      | Yes               |
|      onPress      |    Function to execute on press.     |  (e: GestureResponderEvent) => void   | NO       | All      | Yes               |
|  uncheckedColor   | Custom color for unchecked checkbox. |                string                 | NO       | All      | Yes               |
|       color       |      Custom color for checkbox.      |                string                 | NO       | All      | Yes               |
|       theme       |                theme                 |               ThemeProp               | NO       | All      | Yes               |
|      testID       |                theme                 |                string                 | NO       | All      | Yes               |

**Checkbox.IOS**：Checkboxes allow the selection of multiple options from a set. This component follows platform guidelines for iOS, but can be used on any platform.

|       Name        |          Description          |                 Type                  | Required | Platform | HarmonyOS Support |
| :---------------: | :---------------------------: | :-----------------------------------: | -------- | -------- | ----------------- |
|  TouchableRipple  |           Touchable           |         TouchableRipple props         | NO       | All      | Yes               |
| status (required) |      Status of checkbox.      | checked \| unchecked \| indeterminate | Yes      | All      | Yes               |
|     disabled      | Whether checkbox is disabled. |                boolean                | NO       | All      | Yes               |
|      onPress      | Function to execute on press. |  (e: GestureResponderEvent) => void   | NO       | All      | Yes               |
|       color       |  Custom color for checkbox.   |                string                 | NO       | All      | Yes               |
|       theme       |             theme             |               ThemeProp               | NO       | All      | Yes               |
|      testID       |             theme             |                string                 | NO       | All      | Yes               |

**Checkbox.Item**：Checkbox.Item allows you to press the whole row (item) instead of only the Checkbox.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  status (required)  | Status of checkbox.  |  checked \| unchecked \| indeterminate | Yes      | All      | Yes               |
|  disabled  | Whether checkbox is disabled.  |  boolean | Yes      | All      | Yes               |
|  label (required)  | Label to be displayed on the item. |  string | Yes      | All      | Yes               |
|  onPress  | Function to execute on press. |  fuction | Yes      | All      | Yes               |
|  onLongPress  | Function to execute on long press. |  fuction | Yes      | All      | Yes               |
|  background  | Type of background drawabale to display the feedback (Android). https://reactnative.dev/docs/pressable#rippleconfig |  PressableAndroidRippleConfig | Yes      | All      | Yes               |
|  accessibilityLabel  | Accessibility label for the touchable. This is read by the screen reader when the user taps the touchable. |  string | Yes      | All      | Yes               |
|  uncheckedColor  | Custom color for unchecked checkbox. |  string | Yes      | All      | Yes               |
|  color  | Custom color for checkbox. |  string | Yes      | All      | Yes               |
|  rippleColor  | Color of the ripple effect. |  ColorValue | Yes      | All      | Yes               |
|  style  | Additional styles for container View. |  StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  labelMaxFontSizeMultiplier  | Specifies the largest possible scale a label font can reach. |  number | Yes      | All      | Yes               |
|  labelStyle  | Style that is passed to Label element. |  StyleProp<TextStyle> | Yes      | All      | Yes               |
|  labelVariant( Available in v5.x with theme version 3)   | Label text variant defines appropriate text styles for type role and its size. Available variants. |  unknown | Yes      | All      | Yes               |
|  theme   | theme |  ThemeProp | Yes      | All      | Yes               |
|  testID   | string |  ThemeProp | Yes      | All      | Yes               |
|  position   | Checkbox control position. |  leading \| trailing | Yes      | All      | Yes               |
|  mode   | Whether <Checkbox.Android /> or <Checkbox.IOS /> should be used. Left undefined <Checkbox /> will be used. |  android \| ios | Yes      | All      | Yes               |

**Chip**：Chips are compact elements that can represent inputs, attributes, or actions

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  mode  | Mode of the chip.  |  flat \| outlined  | Yes      | All      | Yes               |
|  children (required)  | Text content of the Chip.  |  React.ReactNode | Yes      | All      | Yes               |
|  icon  | Icon to display for the Chip. Both icon and avatar cannot be specified.  |  IconSource | Yes      | All      | Yes               |
|  avatar  | Avatar to display for the Chip. Both icon and avatar cannot be specified.  |  React.ReactNode | Yes      | All      | Yes               |
|  closeIcon  | Icon to display as the close button for the Chip. The icon appears only when the onClose prop is specified.  |  IconSource | Yes      | All      | Yes               |
|  selected  | Whether chip is selected.  |  boolean | Yes      | All      | Yes               |
|  selectedColor  | Whether to style the chip color as selected.  |  string | Yes      | All      | Yes               |
|  showSelectedOverlay   | Whether to display overlay on selected chip  |  boolean | Yes      | All      | Yes               |
|  showSelectedCheck   | Whether to display default check icon on selected chip.  |  boolean | Yes      | All      | Yes               |
|  rippleColor   | Color of the ripple effect.  |  ColorValue | Yes      | All      | Yes               |
|  disabled   | Whether the chip is disabled.  |  boolean | Yes      | All      | Yes               |
|  background   | Type of background drawabale to display the feedback (Android).  |  PressableAndroidRippleConfig | Yes      | Android      |No               |
|  accessibilityLabel   | Accessibility label for the chip. This is read by the screen reader when the user taps the chip.  |  string | Yes      | All      | Yes               |
|  closeIconAccessibilityLabel   | Accessibility label for the close icon. This is read by the screen reader when the user taps the close icon.  |  string | Yes      | All      | Yes               |
|  onPress   | Function to execute on press.  |  (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  onLongPress   | Function to execute on long press.  |   () => void | Yes      | All      | Yes               |
|  onPressIn   | Function to execute as soon as the touchable element is pressed and invoked even before onPress.  |   (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  onPressOut   | Function to execute as soon as the touch is released even before onPress.  |   (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  onClose   | Function to execute on close button press. The close button appears only when this prop is specified.  |   () => void | Yes      | All      | Yes               |
|  delayLongPress   | The number of milliseconds a user must touch the element before executing onLongPress.  |   number | Yes      | All      | Yes               |
|  compact    | Sets smaller horizontal paddings 12dp around label, when there is only label.  |   boolean | Yes      | All      | Yes               |
|  elevated     | Whether chip should have the elevation.  |   boolean | Yes      | All      | Yes               |
|  textStyle     | Style of chip's text  |   StyleProp<TextStyle> | Yes      | All      | Yes               |
|  style     | style  |   Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      |
|  theme     | theme  |   ThemeProp | Yes      | All      | Yes               |
|  testID     | Pass down testID from chip props to touchable for Detox tests.  |   string | Yes      | All      | Yes               |
|  ellipsizeMode     | Ellipsize Mode for the children text  |   EllipsizeProp | Yes      | All      | Yes               |
|  maxFontSizeMultiplier     | Specifies the largest possible scale a text font can reach.  |   number | Yes      | All      | Yes               |
|  accessibilityRole     | Default value: 'button'  |  string | Yes      | All      | Yes               |

**DataTable**：Data tables allow displaying sets of data.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DataTable  |  React.ReactNode  | Yes      | All      | Yes               |
|  style     | style  |    StyleProp<ViewStyle> | Yes      | All      |

**DataTable.Cell**：A component to show a single cell inside of a table.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DataTableCell.  |  React.ReactNode  | Yes      | All      | Yes               |
|  numeric  | Align the text to the right. Generally monetary or number fields are aligned to right.  |  boolean  | Yes      | All      | Yes               |
|  onPress  | Function to execute on press.  |  (e: GestureResponderEvent) => void  | Yes      | All      | Yes               |
|  style     | Text content style of the DataTableCell.  |    StyleProp<ViewStyle> | Yes      | All      |
|  textStyle  | Text content style of the DataTableCell.  |   StyleProp<TextStyle>  | Yes      | All      | Yes               |
|  maxFontSizeMultiplier  | Specifies the largest possible scale a text font can reach. |   number  | Yes      | All      | Yes               |
|  testID     | testID to be used on tests.  | string | Yes      | All      |

**DataTable.Header**：A component to display title in table header.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DataTableHeader.  |  React.ReactNode  | Yes      | All      | Yes               |
|  style     | Text content style of the DataTable.Header.  |    StyleProp<ViewStyle> | Yes      | All      |
|  theme     | theme  | ThemeProp | Yes      | All      |

**DataTable.Pagination**：A component to show pagination for data table.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  page (required)  | The currently visible page (starting with 0).  | number  | Yes      | All      | Yes               |
|  numberOfPages (required)  | The total number of pages.  | number  | Yes      | All      | Yes               |
|  onPageChange (required)  | Function to execute on page change. | (page: number) => void  | Yes      | All      | Yes               |
|  showFastPaginationControls  | Whether to show fast forward and fast rewind buttons in pagination. False by default. | boolean  | Yes      | All      | Yes               |
|  paginationControlRippleColor  | Color of the pagination control ripple effect. | ColorValue  | Yes      | All      | Yes               |
|  theme     | theme  | ThemeProp | Yes      | All      |
|  numberOfItemsPerPage  | The current number of rows per page. | number  | Yes      | All      | Yes               |
|  numberOfItemsPerPageList  | Options for a number of rows per page to choose from. | Array<number>  | Yes      | All      | Yes               |
|  onItemsPerPageChange  | The function to set the number of rows per page. | (numberOfItemsPerPage: number) => void  | Yes      | All      | Yes               |
|  dropdownItemRippleColor  | Color of the dropdown item ripple effect. | ColorValue  | Yes      | All      | Yes               |
|  selectPageDropdownRippleColor  | Color of the select page dropdown ripple effect. | ColorValue  | Yes      | All      | Yes               |
|  selectPageDropdownLabel  | Label text for select page dropdown to display. | React.ReactNode  | Yes      | All      | Yes               |
|  selectPageDropdownAccessibilityLabel  | AccessibilityLabel for selectPageDropdownLabel | string  | Yes      | All      | Yes               |
|  label  | Label text to display which indicates current pagination. | React.ReactNode  | Yes      | All      | Yes               |
|  accessibilityLabel  | AccessibilityLabel for label. | string  | Yes      | All      | Yes               |
|  style     | Text content style of the DataTable.Pagination.  |    StyleProp<ViewStyle> | Yes      | All      |

**DataTable.Row**：A component to show a single row inside of a table.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  TouchableRipple | Extends: ...TouchableRipple props  | props  | Yes      | All      | Yes               |
|  children (required)  | Content of the DataTableRow.  | React.ReactNode  | Yes      | All      | Yes               |
|  onPress  | Function to execute on press.  | (e: GestureResponderEvent) => void  | Yes      | All      | Yes               |
|  style     | Text content style of the DataTable.Pagination.  |    StyleProp<ViewStyle> | Yes      | All      |
|  theme     | theme  |  ThemeProp | Yes      | All      |
|  pointerEvents     | pointerEvents passed to the View container, which is wrapping children within TouchableRipple.  |  ViewProps['pointerEvents'] | Yes      | All      |

**DataTable.Title**：A component to display title in table header.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Text content of the DataTableTitle.  | React.ReactNode  | Yes      | All      | Yes               |
|  numeric  | Align the text to the right. Generally monetary or number fields are aligned to right.  | boolean  | Yes      | All      | Yes               |
|  sortDirection  | Direction of sorting. An arrow indicating the direction is displayed when this is given.  | boolean  | Yes      | All      | Yes               |
|  numberOfLines  | The number of lines to show.  | number  | Yes      | All      | Yes               |
|  onPress  | Function to execute on press.  | (e: GestureResponderEvent) => void  | Yes      | All      | Yes               |
|  style  | Text content style of the DataTableTitle.  | StyleProp<TextStyle>  | Yes      | All      | Yes               |
|  textStyle  | Text content style of the DataTableTitle.  | StyleProp<TextStyle>  | Yes      | All      | Yes               |
|  maxFontSizeMultiplier  | Specifies the largest possible scale a text font can reach.  | maxFontSizeMultiplier  | Yes      | All      | Yes               |
|  theme  |theme  | ThemeProp  | Yes      | All      | Yes               |

**Dialog**：Dialogs inform users about a specific task and may contain critical information, require decisions, or involve multiple tasks

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  dismissable  | Determines whether clicking outside the dialog dismiss it.  | boolean  | Yes      | All      | Yes               |
|  dismissableBackButton  | Determines whether clicking Android hardware back button dismiss dialog.  | boolean  | Yes      | All      | Yes               |
|  onDismiss  | Callback that is called when the user dismisses the dialog.  | () => void  | Yes      | All      | Yes               |
|  visible  | Determines Whether the dialog is visible.  | boolean  | Yes      | All      | Yes               |
|  children (required)  | Content of the Dialog  | React.ReactNode  | Yes      | All      | Yes               |
|  style  | Text content style of the Dialog.  | StyleProp<TextStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |
|  testID  | testID to be used on tests.  | string  | Yes      | All      | Yes               |

**Dialog.Actions**：A component to show a list of actions in a Dialog.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DialogActions.  | React.ReactNode  | Yes      | All      | Yes               |
|  style  | Text content style of the Dialog.Actions.  | StyleProp<TextStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |

**Dialog.Content**：A component to show content in a Dialog.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DialogContent.  | React.ReactNode  | Yes      | All      | Yes               |
|  style  | Text content style of the Dialog.Content.  | StyleProp<TextStyle>  | Yes      | All      | Yes               |

**Dialog.Icon**：@supported Available in v5.x with theme version 3 A component to show an icon in a Dialog.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  color  | Custom color for action icon.  | IconSource  | Yes      | All      | Yes               |
|  icon (required)  | Name of the icon to show. | IconSource  | Yes      | All      | Yes               |
|  size  | Optional icon size.  | number  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |

**Dialog.ScrollArea**：A component to show a scrollable content in a Dialog.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Content of the DialogScrollArea.  | React.ReactNode  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |

**Dialog.Title**：A component to show a title in a Dialog.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)  | Title text for the DialogTitle.  | React.ReactNode  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |

**Divider**：A divider is a thin, lightweight separator that groups content in lists and page layouts.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  leftInset   | Whether divider has a left inset.  | boolean  | Yes      | All      | Yes               |
|  horizontalInset    |Whether divider has a horizontal inset on both sides.  | boolean  | Yes      | All      | Yes               |
|  bold     | Whether divider should be bolded.  | boolean  | Yes      | All      | Yes               |
|  style  | Text content style of the Divider.  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |

**Drawer.CollapsedItem**：Collapsed component used to show an action item with an icon and optionally label in a navigation drawer.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  label   | The label text of the item.  | string  | Yes      | All      | Yes               |
|  badge   | Badge to show on the icon, can be true to show a dot, string or number to show text.  | string \| number \| boolean  | Yes      | All      | Yes               |
|  disabled   | Whether the item is disabled.  | boolean  | Yes      | All      | Yes               |
|  focusedIcon    | Icon to use as the focused destination icon, can be a string, an image source or a react component  | IconSource  | Yes      | All      | Yes               |
|  unfocusedIcon     | Icon to use as the unfocused destination icon, can be a string, an image source or a react component  | IconSource  | Yes      | All      | Yes               |
|  active     | Whether to highlight the drawer item as active.  | boolean  | Yes      | All      | Yes               |
|  onPress     | Function to execute on press.  |  (e: GestureResponderEvent) => void  | Yes      | All      | Yes               |
|  labelMaxFontSizeMultiplier     | Specifies the largest possible scale a label font can reach.  |  number  | Yes      | All      | Yes               |
|  accessibilityLabel     | Accessibility label for the button. This is read by the screen reader when the user taps the button.  |  string  | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | Yes      | All      | Yes               |

**Drawer.Item**：A component used to show an action item with an icon and a label in a navigation drawer.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  label   | The label text of the item.  | string  | Yes      | All      | Yes               |
|  icon   | Icon to display for the DrawerItem.  | IconSource  | Yes      | All      | Yes               |
|  active   | Whether to highlight the drawer item as active.  | boolean  | Yes      | All      | Yes               |
|  disabled   | Whether the item is disabled.  | boolean  | Yes      | All      | Yes               |
|  onPress   | Function to execute on press.  | (e: GestureResponderEvent) => void  | Yes      | All      | Yes               |
|  background   | Type of background drawabale to display the feedback (Android).  | PressableAndroidRippleConfig  | Yes      | All      | Yes               |
|  accessibilityLabel   | Accessibility label for the button. This is read by the screen reader when the user taps the button.  | string  | Yes      | All      | Yes               |
|  right   | Callback which returns a React element to display on the right side. For instance a Badge.  |  (props: { color: string }) => React.ReactNode  | Yes      | All      | Yes               |
|  labelMaxFontSizeMultiplier   | Specifies the largest possible scale a label font can reach.  |  number  | Yes      | All      | Yes               |
|  rippleColor   | Color of the ripple effect.  |  ColorValue  | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |

**Drawer.Section**：A component to group content inside a navigation drawer.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title   | Title to show as the header for the section.  | string  | Yes      | All      | Yes               |
|  children (required)   | Content of the Drawer.Section.  | React.ReactNode  | Yes      | All      | Yes               |
|  showDivider  | Whether to show Divider at the end of the section. True by default.  | boolean  | Yes      | All      | Yes               |
|  titleMaxFontSizeMultiplier  | Specifies the largest possible scale a title font can reach. True by default.  | number  | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |

**FAB**：A floating action button represents the primary action on a screen. It appears in front of all screen content.

|            Name            |                         Description                          |                       Type                       | Required | Platform | HarmonyOS Support |
| :------------------------: | :----------------------------------------------------------: | :----------------------------------------------: | -------- | -------- | ----------------- |
|      icon (required)       |                 Icon to display for the FAB.                 |                    IconSource                    | Yes      | All      | Yes               |
|      label (required)      |                   Label for extended FAB.                    |                      string                      | Yes      | All      | Yes               |
|         uppercase          |               Make the label text uppercased.                |                     boolean                      | Yes      | All      | Yes               |
|         background         | Type of background drawabale to display the feedback (Android). |           PressableAndroidRippleConfig           | Yes      | All      | Yes               |
|     accessibilityLabel     | Accessibility label for the FAB. This is read by the screen reader when the user taps the FAB. |                      string                      | Yes      | All      | Yes               |
|     accessibilityState     | Accessibility state for the FAB. This is read by the screen reader when the user taps the FAB. |                AccessibilityState                | Yes      | All      | Yes               |
|          animated          |             Whether an icon change is animated.              |                     boolean                      | Yes      | All      | Yes               |
|           color            |       Custom color for the icon and label of the FAB.        |                      string                      | Yes      | All      | Yes               |
|        rippleColor         |                 Color of the ripple effect.                  |                    ColorValue                    | Yes      | All      | Yes               |
|          disabled          | Whether FAB is disabled. A disabled button is greyed out and onPress is not called on touch. |                     boolean                      | Yes      | All      | Yes               |
|          visible           |              Whether FAB is currently visible.               |                     boolean                      | Yes      | All      | Yes               |
|          loading           |             Whether to show a loading indicator.             |                     boolean                      | Yes      | All      | Yes               |
|          onPress           |                Function to execute on press.                 |        (e: GestureResponderEvent) => void        | Yes      | All      | Yes               |
|        onLongPress         |              Function to execute on long press.              |        (e: GestureResponderEvent) => void        | Yes      | All      | Yes               |
|       delayLongPress       | The number of milliseconds a user must touch the element before executing onLongPress |                      number                      | Yes      | All      | Yes               |
|            size            |                  Default value: `'medium'`                   |          'small' \| 'medium' \| 'large'          | Yes      | All      | Yes               |
|            mode            | Mode of the `FAB`. You can change the mode to adjust the the shadow: |               'flat' \| 'elevated'               | Yes      | All      | Yes               |
|          variant           | Color mappings variant for combinations of container and icon colors. | 'primary'\|'secondary'  \|'tertiary' \|'surface' | Yes      | All      | Yes               |
| labelMaxFontSizeMultiplier | Specifies the largest possible scale a label font can reach. |                      number                      | Yes      | All      | Yes               |
|           style            |                            style                             |               StyleProp<ViewStyle>               | Yes      | All      | Yes               |
|           theme            |                            theme                             |                    ThemeProp                     | Yes      | All      | Yes               |
|           testID           |               TestID used for testing purposes               |                      string                      | Yes      | All      | Yes               |
|            ref             |                             ref                              |              React.RefObject<View>               | Yes      | All      | Yes               |

**AnimatedFAB**：An animated, extending horizontally floating action button represents the primary action in an application.

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)   | Icon to display for the FAB.  | IconSource  | Yes      | All      | Yes               |
|  label (required)   | Label for extended FAB.  | string  | Yes      | All      | Yes               |
|  uppercase   | Make the label text uppercased.  | boolean  | Yes      | All      | Yes               |
|  background   | Type of background drawabale to display the feedback (Android).  | PressableAndroidRippleConfig  | Yes      | All      | Yes               |
|  accessibilityLabel   | Accessibility label for the FAB. This is read by the screen reader when the user taps the FAB.  | string  | Yes      | All      | Yes               |
|  accessibilityState   | Accessibility state for the FAB. This is read by the screen reader when the user taps the FAB.  | AccessibilityState  | Yes      | All      | Yes               |
|  color   | Custom color for the icon and label of the FAB.  | string  | Yes      | All      | Yes               |
|  rippleColor   | Color of the ripple effect.  | ColorValue  | Yes      | All      | Yes               |
|  disabled   | Whether FAB is disabled. A disabled button is greyed out and onPress is not called on touch.  | boolean  | Yes      | All      | Yes               |
|  visible   | Whether FAB is currently visible.  | boolean  | Yes      | All      | Yes               |
|  onPress   | Function to execute on press.  | (e: GestureResponderEvent) => void  | Yes      | All      | Yes               |
|  onLongPress   | Function to execute on long press.  | (e: GestureResponderEvent) => void  | Yes      | All      | Yes               |
|  delayLongPress   | The number of milliseconds a user must touch the element before executing onLongPress  | number  | Yes      | All      | Yes               |
|  iconMode   | Whether icon should be translated to the end of extended FAB or be static and stay in the same place. The default value is dynamic.  | static\| dynamic  | Yes      | All      | Yes               |
|  animateFrom   | Indicates from which direction animation should be performed. The default value is right.  | left\| right  | Yes      | All      | Yes               |
|  extended   | Whether FAB should start animation to extend.  | boolean  | Yes      | All      | Yes               |
|  labelMaxFontSizeMultiplier   | Specifies the largest possible scale a label font can reach.  | number  | Yes      | All      | Yes               |
|  variant    | Color mappings variant for combinations of container and icon colors.  | primary\| secondary \| tertiary \| surface | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | Yes      | All      | Yes               |

**FAB.Group**：A component to display a stack of FABs with related actions in a speed dial.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)   | Icon to display for the FAB.  | IconSource  | Yes      | All      | Yes               |
|  accessibilityLabel   | Accessibility label for the FAB. This is read by the screen reader when the user taps the FAB.  | string  | Yes      | All      | Yes               |
|  color   | Custom color for the FAB  | string  | Yes      | All      | Yes               |
|  backdropColor   | Custom backdrop color for opened speed dial background.  | string  | Yes      | All      | Yes               |
|  rippleColor   | Color of the ripple effect.  | ColorValue  | Yes      | All      | Yes               |
|  onPress   | Function to execute on pressing the FAB.  | (e: GestureResponderEvent) => void  | Yes      | All      | Yes               |
|  onLongPress   | Function to execute on long pressing the FAB.  | (e: GestureResponderEvent) => void  | Yes      | All      | Yes               |
|  toggleStackOnLongPress   | Makes actions stack appear on long press instead of on press.  | boolean  | Yes      | All      | Yes               |
|  delayLongPress   | Changes the delay for long press reaction.  | number  | Yes      | All      | Yes               |
|  enableLongPressWhenStackOpened   | Allows for onLongPress when stack is opened.  | boolean  | Yes      | All      | Yes               |
|  open (required)   | Whether the speed dial is open.  | boolean  | Yes      | All      | Yes               |
|  onStateChange (required)   | Callback which is called on opening and closing the speed dial. The open state needs to be updated when it's called, otherwise the change is dropped.  | (state: { open: boolean }) => void  | Yes      | All      | Yes               |
|  visible (required)   | Whether FAB is currently visible.  | boolean  | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | Yes      | All      | Yes               |

**HelperText**：Helper text is used in conjuction with input elements to provide additional hints for the user.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  type   | Type of the helper text.  | error\| info | Yes      | All      | Yes               |
|  children (required)   | Text content of the HelperText.  | React.ReactNode | Yes      | All      | Yes               |
|  visible   | Whether to display the helper text.  | boolean | Yes      | All      | Yes               |
|  padding   | Whether to apply padding to the helper text.  | none\| normal | Yes      | All      | Yes               |
|  disabled   | Whether the text input tied with helper text is disabled.  | boolean | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | Yes      | All      | Yes               |

**Icon**：An icon component which renders icon from vector library.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  size    | Size of icon.  | number | Yes      | All      | Yes               |
|  allowFontScaling    | allowFontScaling  | boolean | Yes      | All      | No               |
|  source (required)    | Icon to display.  | any | Yes      | All      | Yes               |
|  color    | Color of the icon.  | any | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | Yes      | All      | Yes               |

**IconButton**：An icon button is a button which displays only an icon without a label.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)    | Icon to display.  | IconSource | Yes      | All      | Yes               |
|  mode     | Mode of the icon button. By default there is no specified mode - only pressable icon will be rendered.  | outlined \| contained \| contained-tonal  | Yes      | All      | Yes               |
|  iconColor      | Color of the icon.  | string | contained-tonal  | Yes      | All      | Yes               |
|  containerColor      | Background color of the icon container.  | string | contained-tonal  | Yes      | All      | Yes               |
|  rippleColor      | Color of the ripple effect.  | ColorValue | contained-tonal  | Yes      | All      | Yes               |
|  selected       | Whether icon button is selected. A selected button receives alternative combination of icon and container colors.  | boolean | contained-tonal  | Yes      | All      | Yes               |
|  size       | Size of the icon.  | number | contained-tonal  | Yes      | All      | Yes               |
|  disabled       | Whether the button is disabled. A disabled button is greyed out and onPress is not called on touch.  | boolean | contained-tonal  | Yes      | All      | Yes               |
|  animated       | Whether an icon change is animated.  | boolean | contained-tonal  | Yes      | All      | Yes               |
|  accessibilityLabel       | Accessibility label for the button. This is read by the screen reader when the user taps the button.  | string | contained-tonal  | Yes      | All      | Yes               |
|  onPress       | Function to execute on press. | (e: GestureResponderEvent) => void  | Yes      | All      | Yes               |
|  ref  | ref  | React.RefObject<View>  | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |
|  testID  | TestID used for testing purposes  | string  | Yes      | All      | Yes               |
|  loading       | Whether to show a loading indicator. | boolean  | Yes      | All      | Yes               |

**List.Accordion**：A component used to display an expandable list item.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title (required)    | Title text for the list accordion.  | React.ReactNode | Yes      | All      | Yes               |
|  description    | Description text for the list accordion.  | React.ReactNode | Yes      | All      | Yes               |
|  left    | Callback which returns a React element to display on the left side.  | (props: { color: string; style: Style }) => React.ReactNode | Yes      | All      | Yes               |
|  right    | Callback which returns a React element to display on the right side.  | (props: { isExpanded: boolean }) => React.ReactNode | Yes      | All      | Yes               |
|  expanded    | Whether the accordion is expanded If this prop is provided, the accordion will behave as a "controlled component".  | boolean | Yes      | All      | Yes               |
|  onPress    | Function to execute on press.  | (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  onLongPress    | Function to execute on long press.  | (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  delayLongPress    | The number of milliseconds a user must touch the element before executing onLongPress.  | number | Yes      | All      | Yes               |
|  children (required)    | Content of the section.  | React.ReactNode | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |
|  background    | Type of background drawabale to display the feedback (Android). | PressableAndroidRippleConfig | Yes      | All      | Yes               |
|  style    | Style that is passed to the wrapping TouchableRipple element. | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  titleStyle    | Style that is passed to Title element. | StyleProp<TextStyle> | Yes      | All      | Yes               |
|  descriptionStyle    | Style that is passed to Description element. | StyleProp<TextStyle> | Yes      | All      | Yes               |
|  rippleColor    | Color of the ripple effect. | ColorValue | Yes      | All      | Yes               |
|  titleNumberOfLines    | Truncate Title text such that the total number of lines does not exceed this number. | number | Yes      | All      | Yes               |
|  descriptionNumberOfLines    | Truncate Description text such that the total number of lines does not exceed this number. | number | Yes      | All      | Yes               |
|  titleMaxFontSizeMultiplier    | Specifies the largest possible scale a description font can reach. | number | Yes      | All      | Yes               |
|  id    | Id is used for distinguishing specific accordion when using List. | string \| number | Yes      | All      | Yes               |
|  testID    | TestID used for testing purposes | string | Yes      | All      | Yes               |
|  accessibilityLabel    | Accessibility label for the TouchableRipple. This is read by the screen reader when the user taps the touchable. | string | Yes      | All      | Yes               |
|  pointerEvents    | pointerEvents passed to the View container | ViewProps['pointerEvents'] | Yes      | All      | Yes               |

**List.AccordionGroup**：List.AccordionGroup allows to control a group of List Accordions.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  onAccordionPress    | Function to execute on selection change. | (expandedId: string | number) => void | Yes      | All      | Yes               |
|  expandedId    | Id of the currently expanded list accordion | string \| number | Yes      | All      | Yes               |
|  children (required)    | React elements containing list accordions | React.ReactNode | Yes      | All      | Yes               |

**List.Icon**：List.AccordionGroup allows to control a group of List Accordions.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)    | Icon to show. | IconSource | Yes      | All      | Yes               |
|  color    | Color for the icon. | string | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |

**ListItem**：A component to show tiles inside a List.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title (required)    | Title text for the list item. |  React.ReactNode | Yes      | All      | Yes               |
|  description    | Description text for the list item or callback which returns a React element to display the description. | React.ReactNode | Yes      | All      | Yes               |
|  left    | Callback which returns a React element to display on the left side. | (props: { color: string; style: Style }) => React.ReactNode | Yes      | All      | Yes               |
|  right    | Callback which returns a React element to display on the right side. | (props: { color: string; style?: Style }) => React.ReactNode | Yes      | All      | Yes               |
|  onPress    | Function to execute on press. |  (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |
|  style    | Style that is passed to the wrapping TouchableRipple element. |  StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  contentStyle    | Style that is passed to the container wrapping title and descripton. |   StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  titleStyle    | Style that is passed to Title element. |   StyleProp<TextStyle> | Yes      | All      | Yes               |
|  descriptionStyle    | Style that is passed to Description element. |   StyleProp<TextStyle> | Yes      | All      | Yes               |
|  titleNumberOfLines    | Truncate Title text such that the total number of lines does not exceed this number. |   number | Yes      | All      | Yes               |
|  descriptionNumberOfLines    | Truncate Description text such that the total number of lines does not exceed this number. |   number | Yes      | All      | Yes               |
|  titleEllipsizeMode    | Ellipsize Mode for the Title. One of 'head', 'middle', 'tail', 'clip'. |   EllipsizeProp | Yes      | All      | Yes               |
|  titleMaxFontSizeMultiplier    | Specifies the largest possible scale a title font can reach. |   number | Yes      | All      | Yes               |
|  descriptionMaxFontSizeMultiplier    | Specifies the largest possible scale a description font can reach. |   number | Yes      | All      | Yes               |
|  descriptionEllipsizeMode    | Ellipsize Mode for the Description. One of 'head', 'middle', 'tail', 'clip'. |   'head' 'middle' 'tail' 'clip' | Yes      | All      | Yes               |
|  testID    | TestID used for testing purposes |   string | Yes      | All      | Yes               |

**List.Section**：A component used to group list items.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title    | Title text for the section. |  string | Yes      | All      | Yes               |
|  children (required)    | Content of the section. |  React.ReactNode | Yes      | All      | Yes               |
|  titleStyle    | Style that is passed to Title element. |  StyleProp<TextStyle> | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |

**List.Subheader**：A component used to display a header in lists.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |
|  style    | Style that is passed to Text element. |  StyleProp<TextStyle> | Yes      | All      | Yes               |
|  maxFontSizeMultiplier    | Specifies the largest possible scale a text font can reach. |  number | Yes      | All      | Yes               |

**Menu**：Menus display a list of choices on temporary elevated surfaces.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  visible (required)    | Whether the Menu is currently visible. |  boolean | Yes      | All      | Yes               |
|  anchor (required)    | The anchor to open the menu from. In most cases, it will be a button that opens the menu. |  React.ReactNode | { x: number; y: number } | Yes      | All      | Yes               |
|  anchorPosition    | Whether the menu should open at the top of the anchor or at its bottom. | top \| bottom | Yes      | All      | Yes               |
|  statusBarHeight    | Extra margin to add at the top of the menu to account for translucent status bar on Android. If you are using Expo, we assume translucent status bar and set a height for status bar automatically. | number | Yes      | Android      | false               |
|  onDismiss    | Callback called when Menu is dismissed.  |  fuction | Yes      | All      | Yes               |
|  overlayAccessibilityLabel    | Accessibility label for the overlay. This is read by the screen reader when the user taps outside the menu.  |  string | Yes      | All      | Yes               |
|  children (required)    | Content of the Menu  |  React.ReactNode | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  contentStyle    | Style of menu's inner content.  |  Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |
|  theme   | theme   | InternalTheme  | Yes      | All      | Yes               |
|  keyboardShouldPersistTaps    | Inner ScrollView prop  | crollViewProps['keyboardShouldPersistTaps'] | Yes      | All      | Yes               |
|  testID  | testID to be used on tests.  | string  | Yes      | All      | Yes               |

**Menu.Item**：A component to show a single list item inside a Menu.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  title (required)    | Title text for the MenuItem. |  React.ReactNode | Yes      | All      | Yes               |
|  leadingIcon    | Leading icon to display for the MenuItem. |  IconSource | Yes      | All      | Yes               |
|  trailingIcon(Available in v5.x with theme version 3)    | Trailing icon to display for the MenuItem. |  IconSource | Yes      | All      | Yes               |
|  disabled    | Whether the 'item' is disabled. A disabled 'item' is greyed out and onPress is not called on touch. |  boolean | Yes      | All      | Yes               |
|  dense (Available in v5.x with theme version 3)    | Sets min height with densed layout. |  boolean | Yes      | All      | Yes               |
|  background    | Type of background drawabale to display the feedback (Android). |  PressableAndroidRippleConfig | Yes      | All      | Yes               |
|  onPress    | Function to execute on press. |  (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  titleMaxFontSizeMultiplier    | Specifies the largest possible scale a title font can reach. |  number | Yes      | All      | Yes               |
|  style  | style  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  contentStyle  | contentStyle  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  titleStyle  | titleStyle  | StyleProp<ViewStyle>  | Yes      | All      | Yes               |
|  rippleColor  | titleStyle  | ColorValue  | Yes      | All      | Yes               |
|  theme   | Color of the ripple effect.   | InternalTheme  | Yes      | All      | Yes               |
|  testID    | TestID used for testing purposes|  string | Yes      | All      | Yes               |
|  accessibilityLabel    | Accessibility label for the Touchable. |  string | Yes      | All      | Yes               |
|  accessibilityState    | Accessibility state for the Touchable.  |  accessibilityState | Yes      | All      | Yes               |

**Modal**：The Modal component is a simple way to present content above an enclosing view. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  dismissable    | Determines whether clicking outside the modal dismiss it. |  boolean | Yes      | All      | Yes               |
|  dismissableBackButton    | Determines whether clicking Android hardware back button dismiss dialog. |  boolean | Yes      | All      | Yes               |
|  onDismiss    | Callback that is called when the user dismisses the modal.|  () => void | Yes      | All      | Yes               |
|  overlayAccessibilityLabel    | Callback that is called when the user dismisses the modal.|  () => void | Yes      | All      | Yes               |
|  visible    | Determines Whether the modal is visible. |  boolean | Yes      | All      | Yes               |
|  children (required)    | Content of the Modal. |  React.ReactNode | Yes      | All      | Yes               |
|  contentContainerStyle    | Style for the content of the modal |  Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |
|  theme  | theme  | ThemeProp  | Yes      | All      | Yes               |
|  style    | Style for the wrapper of the modal. Use this prop to change the default wrapper style or to override safe area insets with marginTop and marginBottom. |  StyleProp<TextStyle> | Yes      | All      |
|  testID    | testID to be used on tests. |  string | Yes      | All      | Yes               |

**Portal**：Portal allows rendering a component at a different place in the parent tree.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)    | Content of the Portal. |  React.ReactNode | Yes      | All      | Yes               |
|  theme (required)    | theme |  InternalTheme | Yes      | All      | Yes               |

**Portal.Host**：Portal host renders all of its children Portal elements. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)    | Content of the Portal. |  React.ReactNode | Yes      | All      | Yes               |

**ProgressBar**：Progress bar is an indicator used to present progress of some activity in the app.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  animatedValue    |Animated value (between 0 and 1). This tells the progress bar to rely on this value to animate it. Note: It should not be used in parallel with the progress prop. |  number | Yes      | All      | Yes               |
|  progress    | Progress value (between 0 and 1). Note: It should not be used in parallel with the animatedValue prop. |  number | Yes      | All      | Yes               |
|  color    | Color of the progress bar. The background color will be calculated based on this but you can change it by passing backgroundColor to style prop. |  string | Yes      | All      | Yes               |
|  indeterminate    | If the progress bar will show indeterminate progress. |  boolean | Yes      | All      | Yes               |
|  visible    | Whether to show the ProgressBar (true, the default) or hide it (false). |  boolean | Yes      | All      | Yes               |
|  fillStyle    | Style of filled part of the ProgresBar. |  Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |
|  style    | style |  StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme    | theme |  ThemeProp | Yes      | All      | Yes               |
|  testID    | testID to be used on tests. |  string | Yes      | All      | Yes               |

**RadioButton**：Radio buttons allow the selection a single option from a set.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  value (required)    | Value of the radio button |  string | Yes      | All      | Yes               |
|  status    | Status of radio button. |  checked \| unchecked | Yes      | All      | Yes               |
|  disabled    | Whether radio is disabled. |  boolean | Yes      | All      | Yes               |
|  onPress    | Function to execute on press. |  (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  uncheckedColor    | Custom color for unchecked radio. |  string | Yes      | All      | Yes               |
|  color    | Custom color for radio. |  string | Yes      | All      | Yes               |
|  theme    | theme |  ThemeProp | Yes      | All      | Yes               |
|  testID    | testID to be used on tests. |  string | Yes      | All      | Yes               |

**RadioButton.Group**：Radio button group allows to control a group of radio buttons.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  onValueChange (required)    | Function to execute on selection change. |  fuction | Yes      | All      | Yes               |
|  value (required)    | Value of the currently selected radio button. |  string | Yes      | All      | Yes               |
|  children (required) | React elements containing radio buttons.|  string | Yes      | All      | Yes               |

**RadioButton.Item**：RadioButton.Item allows you to press the whole row (item) instead of only the RadioButton.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  value (required)    | Value of the radio button. |  string | Yes      | All      | Yes               |
|  label (required)    | Label to be displayed on the item. |  string | Yes      | All      | Yes  |
|  disabled    | Whether radio is disabled. |  boolean | Yes      | All      | Yes               |
|  background    | Type of background drawabale to display the feedback (Android). https://reactnative.dev/docs/pressable#rippleconfig |  PressableAndroidRippleConfig | Yes      | All      | Yes               |
|  onPress    | Function to execute on press. |  Function | Yes      | All      | Yes               |
|  onLongPress    | Function to execute on long press. |  Function | Yes      | All      | Yes               |
|  accessibilityLabel    | Accessibility label for the touchable. This is read by the screen reader when the user taps the touchable. |  Function | Yes      | All      | Yes               |
|  uncheckedColor    | Custom color for unchecked radio. |  string | Yes      | All      | Yes               |
|  color    | Custom color for radio. |  string | Yes      | All      | Yes               |
|  rippleColor    | Color of the ripple effect. |  ColorValue | Yes      | All      | Yes               |
|  status    | Status of radio button. |  checked \| unchecked | Yes      | All      | Yes               |
|  style    | Additional styles for container View. |  StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  labelStyle    | Style that is passed to Label element. |  StyleProp<TextStyle> | Yes      | All      | Yes               |
|  labelVariant(Available in v5.x with theme version 3)   | Label text variant defines appropriate text styles for type role and its size. Available variants: |  unknown | Yes      | All      | Yes               |
|  labelMaxFontSizeMultiplier  | Specifies the largest possible scale a label font can reach. |  number | Yes      | All      | Yes               |
|  theme  | theme |  ThemeProp | Yes      | All      | Yes               |
|  testID  | testID to be used on tests. |  string | Yes      | All      | Yes               |
|  mode  | Whether <RadioButton.Android /> or <RadioButton.IOS /> should be used. Left undefined <RadioButton /> will be used. |  android \| ios | Yes      | All      | Yes               |
|  position  | Radio button control position. |  leading \| trailing | Yes      | All      | Yes               |

**Searchbar**：Searchbar is a simple input box where users can type search queries.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  placeholder    | Hint text shown when the input is empty. |  string | Yes      | All      | Yes               |
|  value (required)    | The value of the text input. |  string | Yes      | All      | Yes               |
|  onChangeText    | Callback that is called when the text input's text changes. |  (query: string) => void | Yes      | All      | Yes               |
|  mode(Available in v5.x with theme version 3)    | Search layout mode, the default value is "bar". |  bar \| view | Yes      | All      | Yes               |
|  icon    | Icon name for the left icon button (see onIconPress). |  (query: string) => void | Yes      | All      | Yes               |
|  onChangeText    | Callback that is called when the text input's text changes. |  IconSource | Yes      | All      | Yes               |
|  iconColor    | Custom color for icon, default will be derived from theme |  string | Yes      | All      | Yes               |
|  rippleColor    | Color of the ripple effect. |  ColorValue | Yes      | All      | Yes               |
|  onIconPress    | Callback to execute if we want the left icon to act as button. |  (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  onClearIconPress    | Callback to execute if we want to add custom behaviour to close icon button. |  (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  searchAccessibilityLabel    | Accessibility label for the button. This is read by the screen reader when the user taps the button. |  string | Yes      | All      | Yes               |
|  clearIcon    | Custom icon for clear button, default will be icon close. |  IconSource | Yes      | All      | Yes               |
|  clearAccessibilityLabel    | Accessibility label for the button. This is read by the screen reader when the user taps the button. |  string | Yes      | All      | Yes               |
|  traileringIcon    | Icon name for the right trailering icon button.  |  IconSource | Yes      | All      | Yes               |
|  traileringIconColor    | Custom color for the right trailering icon, default will be derived from theme  |  string | Yes      | All      | Yes               |
|  traileringRippleColor    | Color of the trailering icon ripple effect.  |  ColorValue | Yes      | All      | Yes               |
|  onTraileringIconPress    | Callback to execute on the right trailering icon button press.  |  (e: GestureResponderEvent) => void | Yes      | All      | Yes               |
|  traileringIconAccessibilityLabel    | Accessibility label for the right trailering icon button. This is read by the screen reader when the user taps the button.  |  string | Yes      | All      | Yes               |
|  right     | Callback which returns a React element to display on the right side. Works only when mode is set to "bar".  |   (props: { color: string; style: Style; testID: string; }) => React.ReactNode | Yes      | All      | Yes               |
|  showDivider    | Whether to show Divider at the bottom of the search. Works only when mode is set to "view". True by default. |  boolean | Yes      | All      | Yes               |
|  elevation     | Changes Searchbar shadow and background on iOS and Android. |  Animated.Value | Yes      | All      | Yes               |
|  inputStyle    | Set style of the TextInput component inside the searchbar | StyleProp<TextStyle> | Yes      | All      | Yes               |
|  style    | style | Animated.WithAnimatedValue<StyleProp<ViewStyle>> | Yes      | All      | Yes               |
|  loading    | Custom flag for replacing clear button with activity indicator. | Boolean | Yes      | All      | Yes               |
|  testID    | TestID used for testing purposes | string | Yes      | All      | Yes               |
|  theme    | theme | string | Yes      | All      | Yes               |

**SegmentedButtons**：Segmented buttons can be used to select options, switch views or sort elements.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  buttons (required)    | Buttons to display as options in toggle button. Button should contain the following properties: |  { value: string; icon?: IconSource; disabled?: boolean; accessibilityLabel?: string; checkedColor?: string; uncheckedColor?: string; onPress?: (event: GestureResponderEvent) => void; label?: string; showSelectedCheck?: boolean; style?: StyleProp<ViewStyle>; labelStyle?: StyleProp<TextStyle>; testID?: string; }[] | Yes      | All      | Yes               |
|  density    | Density is applied to the height, to allow usage in denser UIs |  regular | Yes      | All      | Yes               |
|  style    | style | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme    | theme | string | Yes      | All      | Yes               |

**Snackbar**：Snackbars provide brief feedback about an operation through a message rendered at the bottom of the container in which it's wrapped.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  visible (required)    | Whether the Snackbar is currently visible. |  boolean | Yes      | All      | Yes               |
|  action    | Label and press callback for the action button. It should contain the following properties: |  $RemoveChildren<typeof Button> & { label: string; } | Yes      | All      | Yes               |
|  icon    | Icon to display when onIconPress is defined. Default will be close icon. | IconSource | Yes      | All      | Yes               |
|  rippleColor    | Color of the ripple effect. | ColorValue | Yes      | All      | Yes               |
|  onIconPress    | Function to execute on icon button press. The icon button appears only when this prop is specified. | () => void | Yes      | All      | Yes               |
|  iconAccessibilityLabel    | Accessibility label for the icon button. This is read by the screen reader when the user taps the button. | string | Yes      | All      | Yes               |
|  duration    | The duration for which the Snackbar is shown. | number | Yes      | All      | Yes               |
|  onDismiss (required)    | Callback called when Snackbar is dismissed. The visible prop needs to be updated when this is called. | () => void | Yes      | All      | Yes               |
|  children (required)    | Text content of the Snackbar. | React.ReactNode | Yes      | All      | Yes               |
|  maxFontSizeMultiplier    | Specifies the largest possible scale a text font can reach. | number | Yes      | All      | Yes               |
|  wrapperStyle    | Style for the wrapper of the snackbar | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  style    | style | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme    | theme | string | Yes      | All      | Yes               |
|  ref    | ref | React.RefObject<View> | Yes      | All      | Yes               |
|  testID    | string | TestID used for testing purposes | Yes      | All      | Yes               |

**Surface**：Surface is a basic container that can give depth to an element with elevation shadow. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)    | Content of the Surface. |  React.ReactNode | Yes      | All      | Yes               |
|  elevation    | Changes shadows and background on iOS and Android. Used to create UI hierarchy between components. |  Animated.Value | Yes      | All      | Yes               |
|  mode    | Mode of the Surface. |  flat \| elevated | Yes      | All      | Yes               |
|  theme    | theme | string | Yes      | All      | Yes               |
|  ref    | ref | React.RefObject<View> | Yes      | All      | Yes               |
|  testID    | string | TestID used for testing purposes | Yes      | All      | Yes               |

**Switch**：Switch is a visual toggle between two mutually exclusive states — on and off.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  disabled    | Disable toggling the switch. |  React.ReactNode | Yes      | All      | Yes               |
|  value    | Value of the switch, true means 'on', false means 'off'. |  boolean | Yes      | All      | Yes               |
|  color    | Custom color for switch. |  string | Yes      | All      | Yes               |
|  onValueChange    | Callback called with the new value when it changes. |  Function | Yes      | All      | Yes               |
|  style    | style | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme    | theme | string | Yes      | All      | Yes               |

**Text**：Typography component showing styles complied with passed variant prop and supported by the type system.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  Text props    |  Extends: ...Text props |  props | Yes      | All      | Yes               |
|  variant    | Variant defines appropriate text styles for type role and its size. Available variants: |  VariantProp<T> | Yes      | All      | Yes               |
|  children (required)    |  Content of the Text. |  React.ReactNode | Yes      | All      | Yes               |
|  style    | style | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme    | theme | string | Yes      | All      | Yes               |

**TextInput**：A component to allow users to input text.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  mode    | Mode of the TextInput. |  flat \| outlined | Yes      | All      | Yes      |
|  left    | left | React.ReactNode | Yes      | All      | Yes      |
|  right    | right | React.ReactNode | Yes      | All      | Yes      |
|  disabled    | If true, user won't be able to interact with the component. |  boolean | Yes      | All      |  Yes      |
|  label    | The text or component to use for the floating label. |  TextInputLabelProp | Yes      | All      |  Yes      |
|  placeholder    | Placeholder for the input. |  string | Yes      | All      |  Yes      |
|  error    | Whether to style the TextInput with error style. |  boolean | Yes      | All      |  Yes      |
|  onChangeText    | Callback that is called when the text input's text changes. Changed text is passed as an argument to the callback handler. |  Function | Yes      | All      |  Yes      |
|  selectionColor    | Selection color of the input. On iOS, it sets both the selection color and cursor color. On Android, it sets only the selection color. |  string | Yes      | All      |  Yes      |
|  underlineColor    | Inactive underline color of the input. |  string | Yes      | All      |  Yes      |
|  activeUnderlineColor    | Active underline color of the input. |  string | Yes      | All      |  Yes      |
|  outlineColor    | Active outline color of the input. |  string | Yes      | All      ||
|  activeOutlineColor    | Active outline color of the input. |  string | Yes      | All      |  Yes      |
|  textColor    | Color of the text in the input. |  string | Yes      | All      |  Yes      |
|  dense    | Sets min height with densed layout.  |  boolean | Yes      | All      |  Yes      |
|  multiline    | Whether the input can have multiple lines.  |  boolean | Yes      | All      |  Yes      |
|  numberOfLines    | The number of lines to show in the input (Android only).  |  number | No    | Android |  No  |
|  onFocus    | Callback that is called when the text input is focused.  |   (args: any) => void | Yes      | All      |  Yes      |
|  onBlur    | Callback that is called when the text input is blurred.  |   (args: any) => void | Yes      | All      |  Yes      |
|  render    | Callback to render a custom input component such as react-native-text-input-mask instead of the default TextInput component from react-native.  |   (props: RenderProps) => React.ReactNode | Yes      | All      |  Yes      |
|  value    | Value of the text input.  | string | Yes      | All      |  Yes      |
|  style    | Pass fontSize prop to modify the font size inside TextInput  |  StyleProp<TextStyle> | Yes      | All      |  Yes      |
|  theme    | theme  |  ThemeProp | Yes      | All      |  Yes      |
|  testID    | testID to be used on tests.  |  string | Yes      | All      |  Yes      |
|  contentStyle    | Pass custom style directly to the input itself. Overrides input style Example: paddingLeft, backgroundColor  |  StyleProp<TextStyle> | Yes      | All      |  Yes      |
|  outlineStyle    | Pass style to override the default style of outlined wrapper. Overrides style when mode is set to outlined Example: borderRadius, borderColor  | StyleProp<ViewStyle> | Yes      | All      |  Yes      |
|  underlineStyle    | Pass style to override the default style of underlined wrapper. Overrides style when mode is set to flat Example: borderRadius, borderColor  | StyleProp<ViewStyle> | Yes      | All      |  Yes      |
|  editable    | editable  | boolean | Yes      | All      |  Yes      |

**TextInput.Affix**：A component to allow users to input text.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  text (required)    | Text to show. |  string | Yes      | All      |  Yes      |
|  accessibilityLabel    | Accessibility label for the affix. This is read by the screen reader when the user taps the affix. |  string | Yes      | All      | Yes      |
|  textStyle    | Style that is passed to the Text element. |  StyleProp<TextStyle> | Yes      | All      |  Yes      |
|  theme    | theme | string | Yes      | All      | Yes               |

**TextInput.Icon**：A component to render a leading / trailing icon in the TextInput
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)    | Icon to show. |   IconSource | Yes      | All      |  Yes      |
|  onPress   | Function to execute on press. |  (e: GestureResponderEvent) => void | Yes      | All      |  Yes      |
|  forceTextInputFocus    | Whether the TextInput will focus after onPress. |  boolean | Yes      | All      |  Yes      |
|  color    | Color of the icon or a function receiving a boolean indicating whether the TextInput is focused and returning the color. | (isTextInputFocused: boolean) => string  | Yes      | All      | Yes               |
|  rippleColor    | Color of the ripple effect. | ColorValue | Yes      | All      | Yes               |
|  style    | style | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme    | theme | string | Yes      | All      | Yes               |

**ToggleButton**：Toggle buttons can be used to group related options. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  icon (required)    | Icon to display for the ToggleButton. |   IconSource | Yes      | All      |  Yes      |
|  size    | Size of the icon. |   number | Yes      | All      |  Yes      |
|  iconColor    | Custom text color for button. |   string | Yes      | All      |  Yes      |
|  rippleColor    | Color of the ripple effect. |   string | Yes      | All      |  Yes      |
|  disabled    | Whether the button is disabled. |   boolean | Yes      | All      |  Yes      |
|  accessibilityLabel    | Accessibility label for the ToggleButton. This is read by the screen reader when the user taps the button. |   string | Yes      | All      |  Yes      |
|  onPress    | Function to execute on press. |  fuction  | Yes      | All      |  Yes      |
|  value    | Value of button. |   string | Yes      | All      |  Yes      |
|  status    | Status of button. |   checked \| unchecked | Yes      | All      |  Yes      |
|  style    | style | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme    | theme | string | Yes      | All      | Yes               |
|  ref    | ref | React.RefObject<View> | Yes      | All      | Yes               |
|  testID    | string | testID to be used on tests. | Yes      | All      | Yes               |

**ToggleButton.Group**：Toggle group allows to control a group of toggle buttons. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  onValueChange (required)    | Function to execute on selection change. |   (value: Value) => void | Yes      | All      |  Yes      |
|  value (required)    | Value of the currently selected toggle button. |   Value \| null | Yes      | All      |  Yes      |
|  children (required)    | React elements containing toggle buttons. |   React.ReactNode | Yes      | All      |  Yes      |

**ToggleButton.Row**：Toggle button row renders a group of toggle buttons in a row.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  onValueChange (required)    | Function to execute on selection change. |   (value: Value) => void | Yes      | All      |  Yes      |
|  value (required)    | Value of the currently selected toggle button. |   string | Yes      | All      |  Yes      |
|  children (required)    | React elements containing toggle buttons. |   React.ReactNode | Yes      | All      |  Yes      |
|  style    | style | StyleProp<ViewStyle> | Yes      | All      | Yes               |

**Tooltip**：Tooltips display informative text when users hover over, focus on, or tap an element.
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  children (required)   | Tooltip reference element. Needs to be able to hold a ref. |   React.ReactElement | Yes      | All      |  Yes      |
|  enterTouchDelay   | The number of milliseconds a user must touch the element before showing the tooltip. |   number | Yes      | All      |  Yes      |
|  leaveTouchDelay   | The number of milliseconds after the user stops touching an element before hiding the tooltip. |   number | Yes      | All      |  Yes      |
|  title (required)   | Tooltip title |   string | Yes      | All      |  Yes      |
|  titleMaxFontSizeMultiplier   | Specifies the largest possible scale a title font can reach. |   number | Yes      | All      |  Yes      |
|  theme    | theme | string | Yes      | All      | Yes               |

**TouchableRipple**：A wrapper for views that should respond to touches. 
|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  borderless   | Whether to render the ripple outside the view bounds. |   boolean | No     | Android |  No    |
|  background   | Type of background drawabale to display the feedback. |   Object | Yes      | All      |  Yes      |
|  centered   | Whether to start the ripple at the center (Web). |   boolean | No    | Web   |  No    |
|  disabled   | Whether to prevent interaction with the touchable. |   boolean | Yes      | All      |  Yes      |
|  onPress   | Function to execute on press. If not set, will cause the touchable to be disabled. |   (e: GestureResponderEvent) => void | Yes      | All      |  Yes      |
|  onLongPress   | Function to execute on long press. |   (e: GestureResponderEvent) => void | Yes      | All      |  Yes      |
|  onPressIn   | Function to execute immediately when a touch is engaged, before onPressOut and onPress. |   (e: GestureResponderEvent) => void | Yes      | All      |  Yes      |
|  onPressOut   | Function to execute when a touch is released. |   (e: GestureResponderEvent) => void | Yes      | All      |  Yes      |
|  rippleColor   | Color of the ripple effect. |   ColorValue | Yes      | All      |  Yes      |
|  underlayColor   | Color of the underlay for the highlight effect. |   string | Yes      | All      |  Yes      |
|  children (required)   | Content of the TouchableRipple. |   ((state: PressableStateCallbackType) => React.ReactNode) \| React.ReactNode | Yes      | All      |  Yes      |
|  style    | style | StyleProp<ViewStyle> | Yes      | All      | Yes               |
|  theme    | theme | string | Yes      | All      | Yes               |

## 遗留问题

## 其他
- Icon 组件allowFontScaling不生效, 参看源码传入的此属性并未传入内部icon组件 [源码位置](https://github.com/callstack/react-native-paper/blob/v5.12.3/src/components/Icon.tsx#L153) 
- Menu组件中的mode属性为[5.12.4版本新增](https://github.com/callstack/react-native-paper/releases/tag/v5.12.4)，当前版本为5.12.3 
- Menu statusBarHeight 无效果，此属性为Android平台独有 [源码位置](https://github.com/callstack/react-native-paper/blob/v5.12.3/src/components/Menu/Menu.tsx#L447)
- DataTableRow 组件使用 TouchableRipple 产生的涟漪效果，在Android上生效，iOS无效果 
- BottomNavigation safeAreaInset top属性无效果，因为在源码中未使用 [源码位置](https://github.com/callstack/react-native-paper/blob/v5.12.3/src/components/BottomNavigation/BottomNavigationBar.tsx#L580) 
- BottomNavigation.Bar组件 keyboardHidesNavigationBar属性为父组件BottomNavigation传入，请勿单独使用


## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-native-paper/blob/main/LICENSE.md) ，请自由地享受和参与开源。
