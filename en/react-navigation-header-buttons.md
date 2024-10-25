> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-navigation-header-buttons</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vonovak/react-navigation-header-buttons">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vonovak/react-navigation-header-buttons/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/vonovak/react-navigation-header-buttons)

## Installation and Usage

<!-- tabs:start -->

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm i react-navigation-header-buttons@12.0.0
```

#### **yarn**

```bash
yarn add react-navigation-header-buttons@12.0.0
```

在 tsconfig.json 文件中添加如下代码:

```json
"compilerOptions": {
  ...
    "paths": {
    ...
      "react-navigation-header-buttons":[
        "./node_modules/react-navigation-header-buttons/lib/module/index.js"
      ]
    },
  }

```

在 metro.config.js 文件中添加如下代码:

```js
const config = {
...
  resolver: {
    unstable_enablePackageExports: true,
  },
};
module.exports = mergeConfig(
  ...
  config,
);

```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from "react";
import MaterialIcons from "@expo/vector-icons/MaterialIcons";
import {
  HeaderButtons,
  Item,
  HiddenItem,
  OverflowMenu,
  Divider,
  ItemProps,
  HiddenItemProps,
  HeaderButtonProps,
  HeaderButton,
} from "react-navigation-header-buttons";
import { Text } from "react-native";

const MaterialHeaderButton = (props: HeaderButtonProps) => (
  <HeaderButton IconComponent={MaterialIcons} iconSize={23} {...props} />
);

const EditItem = ({ onPress }: Pick<ItemProps, "onPress">) => {
  return <Item title="edit" onPress={onPress} />;
};

const ReusableHiddenItem = ({ onPress }: Pick<HiddenItemProps, "onPress">) => (
  <HiddenItem title="hidden2" onPress={onPress} disabled />
);

export function UsageWithIcons({ navigation }) {
  React.useLayoutEffect(() => {
    navigation.setOptions({
      title: "Demo",
      headerRight: () => (
        <HeaderButtons HeaderButtonComponent={MaterialHeaderButton}>
          <Item
            title="search"
            iconName="search"
            onPress={() => alert("search")}
          />
          <EditItem onPress={() => alert("Edit")} />
          <OverflowMenu
            OverflowIcon={({ color }) => (
              <MaterialIcons name="more-horiz" size={23} color={color} />
            )}
          >
            <HiddenItem title="hidden1" onPress={() => alert("hidden1")} />
            <Divider />
            <ReusableHiddenItem onPress={() => alert("hidden2")} />
          </OverflowMenu>
        </HeaderButtons>
      ),
    });
  }, [navigation]);

  return <Text>demo!</Text>;
}
```

## LINK

This repository depends on the following libraries, please refer to the corresponding documentation: 

- [@react-navigation/native](/en/react-navigation-native.md)
- [@react-navigation/elements](/en/react-navigation-elements.md)
- [@react-native-oh-library/react-native-safe-area-context](/en/react-native-safe-area-context.md)

If the library has been imported to the Harmony project, you do not need to import it again. If the library has not been imported, see @react-navigation/native Document、@react-navigation/elements Document、@react-native-oh-library/react-native-safe-area-context Document. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.26; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.300SP2; ROM:3.0.0.24(Canary3);
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

### HeaderButtons

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.。

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                                                                                                                                     | Type                        | Required | Platform    | HarmonyOS Support |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------- | -------- | ----------- | ----------------- |
| HeaderButtonComponent | component that renders the buttons, HeaderButton by default                                                                                                     | `ComponentType`             | no       | iOS/Android | yes               |
| children              | whatever you want to render inside                                                                                                                              | `ReactNode`                 | yes      | iOS/Android | yes               |
| left                  | whether the HeaderButtons are on the left from header title                                                                                                     | boolean                     | no       | iOS/Android | yes               |
| preset                | headers are typically rendered in Stack Navigator, however, you can also render them in a Tab Navigator header. Pass 'tabHeader' if button margins are missing. | `’tabHeader’/‘stackHeader’` | no       | iOS/Android | yes               |

### Item

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.。

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name        | Description                                                   | Type         | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------- | ------------ | -------- | ----------- | ----------------- |
| title       | title for the button, required                                | string       | no       | iOS/Android | yes               |
| onPress     | function to call on press                                     | function     | no       | iOS/Android | yes               |
| iconName    | icon name, used together with the IconComponent prop          | string       | no       | iOS/Android | yes               |
| style       | style to apply to the touchable element that wraps the button | ` ViewStyle` | no       | iOS/Android | yes               |
| buttonStyle | style to apply to the text / icon                             | ` ViewStyle` | no       | iOS/Android | yes               |

### OverflowMenu

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.。

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name         | Description                                                                                                                                                     | Type                            | Required | Platform    | HarmonyOS Support |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- | -------- | ----------- | ----------------- |
| OverflowIcon | React element or component for the overflow icon                                                                                                                | ` ReactElement / ComponentType` | no       | iOS/Android | yes               |
| style        | optional styles for overflow button                                                                                                                             | `ViewStyle`                     | no       | iOS/Android | yes               |
| onPress      | function that is called when overflow menu is pressed.                                                                                                          | function                        | no       | iOS/Android | yes               |
| left         | whether the OverflowMenu is on the left from header title                                                                                                       | boolean                         | no       | iOS/Android | yes               |
| children     | the overflow items                                                                                                                                              | `ReactNode`                     | yes      | iOS/Android | yes               |
| preset       | headers are typically rendered in Stack Navigator, however, you can also render them in a Tab Navigator header. Pass 'tabHeader' if button margins are missing. | ` 'tabHeader' / 'stackHeader'`  | no       | iOS/Android | yes               |

### HiddenItem

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.。

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name       | Description                                                      | Type        | Required | Platform    | HarmonyOS Support |
| ---------- | ---------------------------------------------------------------- | ----------- | -------- | ----------- | ----------------- |
| title      | title for the button, required                                   | string      | no       | iOS/Android | yes               |
| style      | style to apply to the touchable element that wraps the text      | `ViewStyle` | no       | iOS/Android | yes               |
| titleStyle | style to apply to the text                                       | `TextStyle` | no       | iOS/Android | yes               |
| onPress    | function to call on press                                        | function    | no       | iOS/Android | yes               |
| disabled   | disabled 'item' is greyed out and onPress is not called on touch | boolean     | no       | iOS/Android | yes               |

### HeaderButton

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.。

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name         | Description                                                                                    | Type        | Required | Platform    | HarmonyOS Support |
| ------------ | ---------------------------------------------------------------------------------------------- | ----------- | -------- | ----------- | ----------------- |
| title        | title for the button, required                                                                 | string      | no       | iOS/Android | yes               |
| style        | style to apply to the touchable element that wraps the text                                    | `ViewStyle` | no       | iOS/Android | yes               |
| onPress      | function to call on press                                                                      | function    | no       | iOS/Android | yes               |
| renderButton | You can fully customize what it renders inside of the PlatformPressable using the renderButton | ReactNode   | no       | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/vonovak/react-navigation-header-buttons/blob/master/LICENSE).
