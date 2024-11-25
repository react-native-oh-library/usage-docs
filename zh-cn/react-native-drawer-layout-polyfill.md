> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-drawer-layout-polyfill</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/rnc-archive/react-native-drawer-layout-polyfill">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/rnc-archive/react-native-drawer-layout-polyfill)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-drawer-layout-polyfill@2.0.0
```

#### **yarn**

```bash
yarn add react-native-drawer-layout-polyfill@2.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useState, useRef } from "react";
import { Button, Text, StyleSheet, View, TextInput } from "react-native";
import DrawerLayout from "react-native-drawer-layout-polyfill";

const App = () => {
  const drawerLayoutRef = useRef(null);
  const [drawerPosition, setDrawerPosition] = useState("left");
  const [keyboardDismissMode, setKeyboardDismissMode] = useState("none");
  const [drawerLockMode, setDrawerLockMode] = useState("unlocked ");
  const [isOpen, setIsOpen] = useState("关闭 ");
  const [drawerSlideOutput, setDrawerSlideOutput] = useState("");
  const [drawerStateChangedOutput, setDrawerStateChangedOutput] = useState("");
  const [drawerWidth, setDrawerWidth] = useState(300);
  const [value, onChangeText] = useState("");

  const open = () => {
    drawerLayoutRef.current.openDrawer();
  };

  const close = () => {
    drawerLayoutRef.current.closeDrawer();
  };

  const changeDrawerPosition = () => {
    console.log("drawerPosition-修改弹框位置", drawerPosition);
    if (drawerPosition === "left") {
      setDrawerPosition("right");
    } else {
      setDrawerPosition("left");
    }
  };

  const changeDrawerHideKeyboard = () => {
    console.log("keyboardDismissMode-是否隐藏软键盘", keyboardDismissMode);
    if (keyboardDismissMode === "none") {
      setKeyboardDismissMode("on-drag");
    } else {
      setKeyboardDismissMode("none");
    }
  };

  const changeDrawerWidth = () => {
    console.log("drawerWidth-修改弹框宽度", drawerWidth);
    if (value && Number(value) >= 100) {
      setDrawerWidth(Number(value));
    }
  };

  const changeDrawerLockMode = (type) => {
    console.log("drawerLockMode-修改弹框锁定模式", type);
    setDrawerLockMode(type);
  };

  const handleDrawerOpen = (e) => {
    console.log("onDrawerOpen-打开弹框的回调");
    setIsOpen("打开");
  };

  const handleDrawerClose = (e) => {
    console.log("onDrawerClose-关闭弹框的回调");
    setIsOpen("关闭");
  };

  const handleDrawerSlide = (e) => {
    console.log("onDrawerSlide-导航视图发生交互时的回调函数");
    setDrawerSlideOutput(JSON.stringify(e.nativeEvent));
  };

  const handleDrawerStateChanged = (e) => {
    console.log("onDrawerStateChanged-导航视图的状态发生变化时的回调函数");
    setDrawerStateChangedOutput(JSON.stringify(e));
  };

  const navigationView = (
    <View style={styles.navigationContainer}>
      <Text style={styles.textCommon}>I'm in the Drawer!</Text>
      <Text style={styles.textCommon}>弹框状态:{isOpen}</Text>
      <Text style={styles.textCommon}>
        弹框打开关闭过程中触发:{drawerSlideOutput}
      </Text>
      <Text style={styles.textCommon}>
        弹框状态切换触发:{drawerStateChangedOutput}
      </Text>
      <Button
        style={styles.buttonMargin}
        title="关闭弹框"
        onPress={() => close()}
      />
    </View>
  );

  return (
    <DrawerLayout
      ref={drawerLayoutRef}
      drawerWidth={drawerWidth}
      drawerPosition={drawerPosition}
      renderNavigationView={() => navigationView}
      keyboardDismissMode={keyboardDismissMode}
      drawerLockMode={drawerLockMode}
      drawerBackgroundColor="red"
      statusBarBackgroundColor="blue"
      onDrawerOpen={handleDrawerOpen}
      onDrawerClose={handleDrawerClose}
      onDrawerSlide={handleDrawerSlide}
      onDrawerStateChanged={handleDrawerStateChanged}
    >
      <View style={styles.container}>
        <Text style={styles.textCommon}>
          设置导航视图的锁定模式:{drawerLockMode}
        </Text>
        <Text style={styles.textCommon}>
          是否隐藏软键盘:{keyboardDismissMode}
        </Text>
        <Text style={styles.textCommon}>弹框状态:{isOpen}</Text>
        <Text style={styles.textCommon}>
          弹框打开关闭过程中触发:{drawerSlideOutput}
        </Text>
        <Text style={styles.textCommon}>
          弹框状态切换触发:{drawerStateChangedOutput}
        </Text>
        <Button title="打开弹框" onPress={() => open()} />
        <View style={styles.buttonMargin}></View>
        <Button title="改变弹框位置" onPress={() => changeDrawerPosition()} />
        <View style={styles.buttonMargin}></View>
        <Button
          title="弹框动画过程中是否隐藏键盘"
          onPress={() => changeDrawerHideKeyboard()}
        />
        <View style={styles.buttonMargin}></View>
        <Button
          title="设置导航视图的锁定模式- unlocked "
          onPress={() => changeDrawerLockMode("unlocked")}
        />
        <View style={styles.buttonMargin}></View>
        <Button
          title="设置导航视图的锁定模式- locked-closed"
          onPress={() => changeDrawerLockMode("locked-closed")}
        />
        <View style={styles.buttonMargin}></View>
        <Button
          title="设置导航视图的锁定模式- locked-open"
          onPress={() => changeDrawerLockMode("locked-open")}
        />
        <View style={styles.buttonMargin}></View>
        <TextInput
          style={{
            height: 40,
            borderColor: "gray",
            borderWidth: 1,
            width: 300,
          }}
          onChangeText={(text) => onChangeText(text)}
          value={value}
        />
        <View style={styles.buttonMargin}></View>
        <Button title="修改弹框宽度" onPress={() => changeDrawerWidth()} />
      </View>
    </DrawerLayout>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
    paddingTop: 50,
    padding: 8,
  },
  navigationContainer: {
    flex: 1,
    paddingTop: 50,
    padding: 8,
  },
  textCommon: {
    marginBottom: 10,
    fontSize: 15,
  },
  buttonMargin: {
    marginBottom: 5,
  },
});

export default App;
```

## 约束与限制

### 兼容性

在以下版本验证通过

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-drawer-layout-polyfill](https://reactnative.dev/docs/drawerlayoutandroid)

| Name                     | Description                                                                                                                                                                                                                                                                                                                                                                                                                        | Type     | Required | Platform    | HarmonyOS Support | note                                                   |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- | ------------------------------------------------------ |
| renderNavigationView     | The navigation view that will be rendered to the side of the screen and can be pulled in.                                                                                                                                                                                                                                                                                                                                          | function | YES      | Android IOS | YES               |                                                        |
| drawerPosition           | Specifies the side of the screen from which the drawer will slide in. By default it is set to left. enum('left', 'right')                                                                                                                                                                                                                                                                                                          | string   | NO       | Android IOS | YES               |                                                        |
| drawerWidth              | Specifies the width of the drawer, more precisely the width of the view that be pulled in from the edge of the window.                                                                                                                                                                                                                                                                                                             | number   | NO       | Android IOS | YES               |                                                        |
| keyboardDismissMode      | Determines whether the keyboard gets dismissed in response to a drag. 'none' (the default), drags do not dismiss the keyboard. 'on-drag', the keyboard is dismissed when a drag begins.                                                                                                                                                                                                                                            | string   | NO       | Android IOS | YES               |                                                        |
| drawerLockMode           | Specifies the lock mode of the drawer. The drawer can be locked in 3 states: unlocked (default), meaning that the drawer will respond (open/close) to touch gestures. locked-closed, meaning that the drawer will stay closed and not respond to gestures. locked-open, meaning that the drawer will stay opened and not respond to gestures. The drawer may still be opened and closed programmatically (openDrawer/closeDrawer). | string   | NO       | Android IOS | YES               |                                                        |
| drawerBackgroundColor    | Specifies the background color of the drawer. The default value is white. If you want to set the opacity of the drawer, use rgba.                                                                                                                                                                                                                                                                                                  | string   | NO       | Android IOS | YES               |                                                        |
| statusBarBackgroundColor | Make the drawer take the entire screen and draw the background of the status bar to allow it to open over the status bar. It will only have an effect on API 21+. IOS and harmony are not supported.                                                                                                                                                                                                                               | string   | NO       | Android     | NO                | The original library only does the function of Android |
| onDrawerOpen             | Function called whenever the navigation view has been opened.                                                                                                                                                                                                                                                                                                                                                                      | function | NO       | Android IOS | YES               |                                                        |
| onDrawerClose            | Function called whenever the navigation view has been closed.                                                                                                                                                                                                                                                                                                                                                                      | function | NO       | Android IOS | YES               |                                                        |
| onDrawerSlide            | Function called whenever there is an interaction with the navigation view.                                                                                                                                                                                                                                                                                                                                                         | function | NO       | Android IOS | YES               |                                                        |
| onDrawerStateChanged     | Function called when the drawer state has changed. The drawer can be in 3 states: idle, meaning there is no interaction with the navigation view happening at the time                                                                                                                                                                                                                                                             | function | NO       | Android IOS | YES               |                                                        |

## 方法

| Name        | Description        | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------ | -------- | ----------- | ----------------- |
| openDrawer  | Closes the drawer. | NO       | Android IOS | YES               |
| closeDrawer | Opens the drawer.  | NO       | Android IOS | YES               |

## 遗留问题

- [ ] 属性statusBarBackgroundColor 鸿蒙暂不支持。[issue#10](https://github.com/rnc-archive/react-native-drawer-layout-polyfill/issues/10)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://www.mit-license.org/) ，请自由地享受和参与开源。
