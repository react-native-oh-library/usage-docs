> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-navigation/drawer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/drawer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/drawer/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/drawer)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-navigation Releases](https://github.com/react-native-oh-library/react-navigation/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/drawer
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/drawer
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import { View, Text, Button } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import {
    createDrawerNavigator,
    DrawerContentScrollView,
    DrawerItemList,
    DrawerItem,
} from '@react-navigation/drawer';

function Feed({ navigation }) {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Feed Screen</Text>
            <Button title="Open drawer" onPress={() => navigation.openDrawer()} />
            <Button title="Toggle drawer" onPress={() => navigation.toggleDrawer()} />
        </View>
    );
}

function Notifications() {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Notifications Screen</Text>
        </View>
    );
}

function CustomDrawerContent(props) {
    return (
        <DrawerContentScrollView {...props}>
            <DrawerItemList {...props} />
            <DrawerItem
                label="Close drawer"
                onPress={() => props.navigation.closeDrawer()}
            />
            <DrawerItem
                label="Toggle drawer"
                onPress={() => props.navigation.toggleDrawer()}
            />
        </DrawerContentScrollView>
    );
}

const Drawer = createDrawerNavigator();

function MyDrawer() {
    return (
        <Drawer.Navigator
            drawerContent={(props) => <CustomDrawerContent {...props} />}
            initialRouteName='Feed'
        >
            <Drawer.Screen name="Feed" component={Feed} />
            <Drawer.Screen name="Notifications" component={Notifications} />
        </Drawer.Navigator>
    );
}

export default function NavigationDrawer() {
    return (
        <NavigationContainer>
            <MyDrawer />
        </NavigationContainer>
    );
}

export { NavigationDrawer }
```

## Link
本库依赖以下三方库，请查看对应文档：
+ [@react-navigation/native](/zh-cn/react-navigation-native.md)
+ [@react-native-oh-tpl/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)
+ [@react-native-oh-tpl/react-native-reanimated](/zh-cn/react-native-reanimated.md)
+ [@react-native-oh-library/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-gesture-handler、@react-native-oh-tpl/react-native-reanimated、@react-native-oh-library/react-native-safe-area-context 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档的 Link 章节](/zh-cn/react-native-gesture-handler.md#link)、[@react-native-oh-tpl/react-native-reanimated 文档的 Link 章节](/zh-cn/react-native-reanimated.md#link)、[@react-native-oh-library/react-native-safe-area-context 文档的 Link 章节](/zh-cn/react-native-safe-area-context.md#link)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-navigation Releases](https://github.com/react-native-oh-library/react-navigation/releases)
  
## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多使用详情请查看 [@react-navigation/drawer 的文档介绍](https://reactnavigation.org/docs/drawer-navigator)

**Props**

| Name                    | Description                                                                                                                                                                                                           | Type                                                                    | Required | Platform    | HarmonyOS Support |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|----------|-------------|-------------------|
| id                      | Optional unique ID for the navigator. This can be used with navigation.getParent to refer to this navigator in a child navigator.                                                                                     | string                                                                  | no       | all         | yes               |
| initialRouteName        | The name of the route to render on the first load of the navigator.                                                                                                                                                   | string                                                                  | no       | all         | yes               |
| screenOptions           | Default options to use for the screens in the navigator.                                                                                                                                                              | object                                                                  | no       | all         | yes               |
| backBehavior            | This controls what happens when goBack is called in the navigator. This includes pressing the device's back button or back gesture on Android.                                                                        | 'firstRoute'&#124;'initialRoute'&#124;'order'&#124;'history'&#124;'none' | no       | all         | yes               |
| defaultStatus           | The default status of the drawer                                                                                                                                                                                      | 'open'&#124;'close'                                                      | no       | all         | yes               |
| detachInactiveScreens   | Boolean used to indicate whether inactive screens should be detached from the view hierarchy to save memory. This enables integration with react-native-screens. Defaults to true.                                    | boolean                                                                 | no       | Android，iOS | no                |
| useLegacyImplementation | Whether to use the legacy implementation based on Reanimated 1. The new implementation based on Reanimated 2 will perform better, but you need additional configuration and need to use Hermes with Flipper to debug. | boolean                                                                 | no       | all         | no                |
| drawerContent           | Function that returns React element to render as the content of the drawer, for example, navigation items                                                                                                             | function                                                                | no       | all         | yes               |

**Options & screenOptions**
| Name                          | Description                                                                                                                                                                                               | Type                                             | Required | Platform    | HarmonyOS Support |
|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------|----------|-------------|-------------------|
| title                         | A generic title that can be used as a fallback for headerTitle and drawerLabel.                                                                                                                           | string                                           | no       | all         | yes               |
| lazy                          | Whether this screen should render the first time it's accessed. Defaults to true. Set it to false if you want to render the screen on initial render.                                                     | boolean                                          | no       | all         | yes               |
| drawerLabel                   | String or a function that given { focused: boolean, color: string } returns a React.Node, to display in drawer sidebar. When undefined, scene title is used.                                              | string&#124;function                             | no       | all         | yes               |
| drawerIcon                    | React.Node to display in drawer sidebar.                                                                                                                                                                  | function                                         | no       | all         | yes               |
| drawerActiveTintColor         | Color for the icon and label in the active item in the drawer.                                                                                                                                            | string                                           | no       | all         | yes               |
| drawerActiveBackgroundColor   | Background color for the active item in the drawer.                                                                                                                                                       | string                                           | no       | all         | yes               |
| drawerInactiveTintColor       | Color for the icon and label in the inactive items in the drawer.                                                                                                                                         | string                                           | no       | all         | yes               |
| drawerInactiveBackgroundColor | Background color for the inactive items in the drawer.                                                                                                                                                    | string                                           | no       | all         | yes               |
| drawerItemStyle               | Style object for the single item, which can contain an icon and/or a label.                                                                                                                               | object                                           | no       | all         | yes               |
| drawerLabelStyle              | Style object to apply to the Text style inside content section which renders a label.                                                                                                                     | object                                           | no       | all         | yes               |
| drawerContentContainerStyle   | Style object for the content section inside the ScrollView.                                                                                                                                               | object                                           | no       | all         | yes               |
| drawerContentStyle            | Style object for the wrapper view.                                                                                                                                                                        | object                                           | no       | all         | yes               |
| drawerStyle                   | Style object for the drawer component. You can pass a custom background color for a drawer or a custom width here.                                                                                        | object                                           | no       | all         | yes               |
| drawerPosition                | Options are left or right. Defaults to left for LTR languages and right for RTL languages.                                                                                                                | 'left'&#124;'right'                               | no       | all         | yes               |
| drawerType                    | Type of the drawer. It determines how the drawer looks and animates.                                                                                                                                      | 'front'&#124;'back'&#124;'slide'&#124;'permanent' | no       | all         | yes               |
| drawerHideStatusBarOnOpen     | When set to true, Drawer will hide the OS status bar whenever the drawer is pulled or when it's in an "open" state.                                                                                       | boolean                                          | no       | all         | yes               |
| drawerStatusBarAnimation      | Animation of the statusbar when hiding it. use in combination with hideStatusBar.                                                                                                                         | 'slide'&#124;'fade'&#124;'none'                  | no       | iOS         | no                |
| overlayColor                  | Color overlay to be displayed on top of the content view when drawer gets open. The opacity is animated from 0 to 1 when the drawer opens.                                                                | string                                           | no       | all         | yes               |
| sceneContainerStyle           | Style object for the component wrapping the screen content.                                                                                                                                               | string                                           | no       | all         | yes               |
| gestureHandlerProps           | Props to pass to the underlying pan gesture handler.                                                                                                                                                      | object                                           | no       | Android，iOS | no               |
| swipeEnabled                  | Whether you can use swipe gestures to open or close the drawer. Defaults to true.                                                                                                                         | boolean                                          | no       | Android，iOS | no               |
| swipeEdgeWidth                | Allows for defining how far from the edge of the content view the swipe gesture should activate.                                                                                                          | number                                           | no       | Android，iOS | no               |
| swipeMinDistance              | Minimum swipe distance threshold that should activate opening the drawer.                                                                                                                                 | number                                           | no       | Android，iOS | no               |
| keyboardDismissMode           | Whether the keyboard should be dismissed when the swipe gesture begins. Defaults to 'on-drag'. Set to 'none' to disable keyboard handling.                                                                | 'on-drag'&#124;'none'                             | no       | all         | no               |
| unmountOnBlur                 | Whether this screen should be unmounted when navigating away from it. Unmounting a screen resets any local state in the screen as well as state of nested navigators in the screen. Defaults to false.    |                boolean                                  | no       | all         | yes               |
| freezeOnBlur                  | Boolean indicating whether to prevent inactive screens from re-rendering. Defaults to false. Defaults to true when enableFreeze() from react-native-screens package is run at the top of the application. | boolean                                          | no       | Android，iOS | no                |

**Events**
| Name            | Description                                                                         | Type     | Required | Platform | HarmonyOS Support |
|-----------------|-------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| drawerItemPress | This event is fired when the user presses the button for the screen in the drawer.  | function | no       | all      | yes               |


## 遗留问题

 - [ ] swipeEnabled等手势相关属性不生效，因为依赖的手势库有问题，待修复：[issue #12](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler/issues/12)
  
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/drawer/LICENSE) ，请自由地享受和参与开源。