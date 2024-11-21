> Template version: v0.2.2
<p align="center">
  <h1 align="center"> <code>@react-navigation/native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/native">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/native/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-navigation/react-navigation/tree/6.x/packages/native)


## Installation and Usage

Go to the project directory and execute the following instruction:
<!-- tabs:start -->

#### **npm**

```bash
npm install @react-navigation/native@6.1.17
```
#### **yarn**

```bash
yarn add @react-navigation/native@6.1.17
```


<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.
```js
import * as React from 'react';
import { Text, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';

const Tab = createBottomTabNavigator();

function HomeScreen({ navigation }) {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Home screen</Text>
        </View>
    );
}

function DetailsScreen({ navigation }) {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Details!</Text>
        </View>
    );
}

export default function App() {
    return (
        <NavigationContainer>
            <Tab.Navigator>
                <Tab.Screen name="Home" component={HomeScreen} />
                <Tab.Screen name="Details" component={DetailsScreen} />
            </Tab.Navigator>
        </NavigationContainer>
    );
}

export {App}
```

## Constraints
### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.11; SDK: OpenHarmony(api11) 4.1.0.53; IDE: DevEco Studio 4.1.3.412; ROM: 2.0.0.52;
2. RNOH: 0.72.13; SDK: HarmonyOS NEXT Developer Preview1; IDE: DevEco Studio 4.1.3.500; ROM: 2.0.0.58;
3. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1 B.0.18; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
4. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**NavigationContainer**：

| Name                      | Description                                                                                                          | Type     | Required | Platform | HarmonyOS Support |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| useNavigationContainerRef | A ref link to navigation                                                                                             | function | no       | all      | yes               |
| onStateChange             | Function that gets called every time navigation state changes. It receives the new navigation state as the argument. | function | no       | all      | yes               |
| onReady                   | Function which is called after the navigation container and all its children finish mounting for the first time.     | function | no       | all      | yes               |

**Hooks**
| Name           | Description                                                                                                                                                                                    | Type     | Required | Platform | HarmonyOS Support |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| useScrollToTop | The expected native behavior of scrollable components is to respond to events from navigation that will scroll to top when tapping on the active tab as you would expect from native tab bars. | function | no       | all      | yes               |

## Known Issues

## Others

This repository depends on the following libraries, please refer to the corresponding documentation:
+ [@react-navigation/bottom-tabs](/zh-cn/react-navigation-bottom-tabs.md)
+ [@react-native-oh-tpl/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)
+ [@react-native-oh-library/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)


## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/native/LICENSE).
