> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-tab-navigator</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ptomasroos/react-native-tab-navigator">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ptomasroos/react-native-tab-navigator/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-tab-navigator)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-tab-navigator Releases](https://github.com/react-native-oh-library/react-native-tab-navigator/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-tab-navigator
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-tab-navigator
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```ts
import React, { useState } from "react";
import { View, StyleSheet, Text, Image } from "react-native";
import TabNavigator from "react-native-tab-navigator";

const HOME_IMAGE = [
  require("../assets/tab-navigator/home_unselected.svg"),
  require("../assets/tab-navigator/home_selected.svg"),
];
const PROFILE_IMAGE = [
  require("../assets/tab-navigator/profile_unselected.svg"),
  require("../assets/tab-navigator/profile_selected.svg"),
];

const App = () => {
  const [selectedTab, setSelectedTab] = useState("home");
  return (
    <View style={styles.container}>
      <TabNavigator style={styles.tabContainer}>
        <TabNavigator.Item
          selected={selectedTab === "home"}
          title="Home"
          selectedTitleStyle={{ color: "#3496f0" }}
          renderIcon={() => (
            <Image source={HOME_IMAGE[0]} style={styles.iconSize} />
          )}
          renderSelectedIcon={() => (
            <Image source={HOME_IMAGE[1]} style={styles.iconSize} />
          )}
          onPress={() => setSelectedTab("home")}
        >
          <Home />
        </TabNavigator.Item>
        <TabNavigator.Item
          selected={selectedTab === "profile"}
          title="Profile"
          selectedTitleStyle={{ color: "#3496f0" }}
          renderIcon={() => (
            <Image source={PROFILE_IMAGE[0]} style={styles.iconSize} />
          )}
          renderSelectedIcon={() => (
            <Image source={PROFILE_IMAGE[1]} style={styles.iconSize} />
          )}
          onPress={() => setSelectedTab("profile")}
        >
          <Profile />
        </TabNavigator.Item>
      </TabNavigator>
    </View>
  );
};

function Home() {
  return (
    <View style={styles.tabContainer}>
      <Text style={styles.welcome}>Home</Text>
    </View>
  );
}

function Profile() {
  return (
    <View style={styles.tabContainer}>
      <Text style={styles.welcome}>Profile</Text>
    </View>
  );
}

export default App;
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-tab-navigator Releases](https://github.com/react-native-oh-library/react-native-tab-navigator/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### TabNavigator props

| Name              | Description                     | Type           | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------- | -------------- | -------- | ----------- | ----------------- |
| sceneStyle        | define for rendered scene       | object (style) | No       | iOS/Android | Yes               |
| tabBarStyle       | define style for TabBar         | object (style) | No       | iOS/Android | Yes               |
| tabBarShadowStyle | define shadow style for tabBar  | object (style) | No       | iOS/Android | Yes               |
| hidesTabTouch     | disable onPress opacity for Tab | boolean        | No       | iOS/Android | Yes               |

### TabNavigator.Item props

| Name               | Description                                        | Type             | Required | Platform    | HarmonyOS Support |
| ------------------ | -------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| renderIcon         | returns Item icon                                  | function         | No       | iOS/Android | Yes               |
| renderSelectedIcon | returns selected Item icon                         | function         | No       | iOS/Android | Yes               |
| badgeText          | text for Item badge                                | string or number | No       | iOS/Android | Yes               |
| renderBadge        | returns Item badge                                 | function         | No       | iOS/Android | Yes               |
| title              | Item title                                         | string           | No       | iOS/Android | Yes               |
| titleStyle         | styling for Item title                             | style            | No       | iOS/Android | Yes               |
| selectedTitleStyle | styling for selected Item title                    | style            | No       | iOS/Android | Yes               |
| tabStyle           | styling for tab                                    | style            | No       | iOS/Android | Yes               |
| selected           | return whether the item is selected                | boolean          | No       | iOS/Android | Yes               |
| onPress            | onPress method for Item                            | function         | No       | iOS/Android | Yes               |
| allowFontScaling   | allow font scaling for title                       | boolean          | No       | iOS/Android | Yes               |
| accessible         | indicates if this item is an accessibility element | boolean          | No       | iOS/Android | Yes               |
| accessibilityLabel | override text for screen readers                   | string           | No       | iOS/Android | Yes               |
| testID             | used to locate this item in end-to-end-tests       | string           | No       | iOS/Android | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ptomasroos/react-native-tab-navigator/blob/master/LICENSE).
