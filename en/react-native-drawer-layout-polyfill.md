<!-- {% raw %} -->
Template version: v0.2.2

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


> [!TIP] [GitHub address](https://github.com/rnc-archive/react-native-drawer-layout-polyfill)

## Installation and Usage

Go to the project directory and execute the following instruction：

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

The following code shows the basic use scenario of the repository：

```tsx
import React, { useState, useRef } from "react";
import { Button, Text, StyleSheet, View, TextInput } from "react-native";
import DrawerLayout from "react-native-drawer-layout-polyfill";

const App = () => {
  const drawerLayoutRef = useRef(null);
  const [drawerPosition, setDrawerPosition] = useState("left");
  const [keyboardDismissMode, setKeyboardDismissMode] = useState("none");
  const [drawerLockMode, setDrawerLockMode] = useState("unlocked ");
  const [isOpen, setIsOpen] = useState("closure ");
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
    console.log("drawerPosition-Modify the bomb frame position", drawerPosition);
    if (drawerPosition === "left") {
      setDrawerPosition("right");
    } else {
      setDrawerPosition("left");
    }
  };

  const changeDrawerHideKeyboard = () => {
    console.log("keyboardDismissMode-Whether to hide the soft keyboard", keyboardDismissMode);
    if (keyboardDismissMode === "none") {
      setKeyboardDismissMode("on-drag");
    } else {
      setKeyboardDismissMode("none");
    }
  };

  const changeDrawerWidth = () => {
    console.log("drawerWidth-Modify the width of the bullet box", drawerWidth);
    if (value && Number(value) >= 100) {
      setDrawerWidth(Number(value));
    }
  };

  const changeDrawerLockMode = (type) => {
    console.log("drawerLockMode-Modify the lock mode of the pop-up box", type);
    setDrawerLockMode(type);
  };

  const handleDrawerOpen = (e) => {
    console.log("onDrawerOpen-Open the callback in the pop-up box");
    setIsOpen("Open");
  };

  const handleDrawerClose = (e) => {
    console.log("onDrawerClose-Turn off the bomb frame");
    setIsOpen("closure");
  };

  const handleDrawerSlide = (e) => {
    console.log("onDrawerSlide-The callback function when navigation view occurs when interacting");
    setDrawerSlideOutput(JSON.stringify(e.nativeEvent));
  };

  const handleDrawerStateChanged = (e) => {
    console.log("onDrawerStateChanged-The recovery function when the state of the navigation view changes");
    setDrawerStateChangedOutput(JSON.stringify(e));
  };

  const navigationView = (
    <View style={styles.navigationContainer}>
      <Text style={styles.textCommon}>I'm in the Drawer!</Text>
      <Text style={styles.textCommon}>Bomb state:{isOpen}</Text>
      <Text style={styles.textCommon}>
        Triggered during the bomb frame opening and closing process:{drawerSlideOutput}
      </Text>
      <Text style={styles.textCommon}>
        Bullet frame state switch trigger:{drawerStateChangedOutput}
      </Text>
      <Button
        style={styles.buttonMargin}
        title="Turn off the bomb frame"
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
          Set the lock mode of the navigation view:{drawerLockMode}
        </Text>
        <Text style={styles.textCommon}>
          Whether to hide the soft service:{keyboardDismissMode}
        </Text>
        <Text style={styles.textCommon}>弹框状态:{isOpen}</Text>
        <Text style={styles.textCommon}>
          Triggered during the bomb frame opening and closing process:{drawerSlideOutput}
        </Text>
        <Text style={styles.textCommon}>
          Bullet frame state switch trigger:{drawerStateChangedOutput}
        </Text>
        <Button title="Open the bomb frame" onPress={() => open()} />
        <View style={styles.buttonMargin}></View>
        <Button title="Change the bomb frame position" onPress={() => changeDrawerPosition()} />
        <View style={styles.buttonMargin}></View>
        <Button
          title="Whether the keyboard is hidden during the bomb frame animation process"
          onPress={() => changeDrawerHideKeyboard()}
        />
        <View style={styles.buttonMargin}></View>
        <Button
          title="Set the lock mode of the navigation view- unlocked "
          onPress={() => changeDrawerLockMode("unlocked")}
        />
        <View style={styles.buttonMargin}></View>
        <Button
          title="Set the lock mode of the navigation view- locked-closed"
          onPress={() => changeDrawerLockMode("locked-closed")}
        />
        <View style={styles.buttonMargin}></View>
        <Button
          title="Set the lock mode of the navigation view- locked-open"
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
        <Button title="Modify the width of the bullet box" onPress={() => changeDrawerWidth()} />
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

## Constraints

### Compatibility

This document is verified based on the following versions

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


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

## API

| Name        | Description        | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------ | -------- | ----------- | ----------------- |
| openDrawer  | Closes the drawer. | NO       | Android IOS | YES               |
| closeDrawer | Opens the drawer.  | NO       | Android IOS | YES               |

## Known Issues

- [ ] The property statusbarbackgroundcolor is temporarily not supported by HarmonyOS. [issue#10](https://github.com/rnc-archive/react-native-drawer-layout-polyfill/issues/10)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://www.mit-license.org/).

<!-- {% endraw %} -->