> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@callstack/react-theme-provider</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-theme-provider">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/react-theme-provider/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/callstack/react-theme-provider)

## Installation and Usage

#### **npm**

```bash
npm install @callstack/react-theme-provider@3.0.9
```

#### **yarn**

```bash
yarn add @callstack/react-theme-provider@3.0.9
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { StyleSheet, Text, Button, View } from "react-native";

import { createTheming } from "@callstack/react-theme-provider";

const theme = {
  lightTheme: {
    background: "#ffffff",
    text: "#000000",
  },
  darkTheme: {
    background: "#000000",
    text: "#ffffff",
  },
};

const { ThemeProvider, useTheme } = createTheming(theme);

const RNThemeProvider = () => {
  const theme = useTheme();

  const [ptheme, setTheme] = React.useState(theme.lightTheme);

  const toggleTheme = () => {
    setTheme((ptheme) =>
      ptheme === theme.lightTheme ? theme.darkTheme : theme.lightTheme
    );
  };

  const ThemedView = () => {
    return (
      <View style={[styles.container, { backgroundColor: ptheme.background }]}>
        <Text style={[styles.text, { color: ptheme.text }]}>
          Hello, Themed World!
        </Text>
      </View>
    );
  };
  return (
    <ThemeProvider theme={theme}>
      <ThemedView />
      <View style={styles.buttonContainer}>
        <Button title="Toggle Theme" onPress={toggleTheme} />
      </View>
    </ThemeProvider>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  text: {
    fontSize: 20,
  },
  buttonContainer: {
    position: "absolute",
    justifyContent: "center",
    alignItems: "center",
    bottom: 30,
    left: 0,
    right: 0,
  },
});

export default RNThemeProvider;
```

This document is verified based on the following versions:

1. RNOH: 0.72.26; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.300; ROM: 3.0.0.22;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Components

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name          | Description                                        | Type      | Required | Platform | HarmonyOS Support |
| ------------- | -------------------------------------------------- | --------- | -------- | -------- | ----------------- |
| ThemeProvider | 接收一个主题对象作为属性，并将该主题提供给其子组件 | component | no       | all      | yes               |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name          | Description                                     | Type     | Required | Platform | HarmonyOS Support |
| ------------- | ----------------------------------------------- | -------- | -------- | -------- | ----------------- |
| createTheming | 从库中导入以创建主题对象                        | function | yes      | all      | yes               |
| useTheme      | 用于在函数组件中访问当前主题,它返回当前主题对象 | function | no       | all      | yes               |
| withTheme     | 用于将当前主题作为属性传递给包装组件            | function | yes      | all      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/callstack/react-theme-provider/blob/master/LICENSE).


