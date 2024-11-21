> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>nativewind</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/nativewind/nativewind">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/nativewind/nativewind/blob/main/packages/nativewind/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/nativewind)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/nativewind Releases](https://github.com/react-native-oh-library/nativewind/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/nativewind
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/nativewind
```

#### **tailwind.config.js**

```bash
npx tailwindcss init
```

#### **Add the paths of all component files to your tailwind.config.js file.**

```diff
module.exports = {
- content: [],
+ content: ["./App.{js,jsx,ts,tsx}", "./screens/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

#### **Modify your babel.config.js.**

```diff
module.exports = {
- plugins: [],
+ plugins: ["@react-native-oh-tpl/nativewind/babel"],
};
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import React from 'react';
import { Text, View, ScrollView } from 'react-native';
import { styled } from 'nativewind';

const StyledView = styled(View)
const StyledText = styled(Text)
const NativewindDemo = () => {
    return (
        <StyledView className="flex-1 items-center justify-center">
            <StyledText className="font-bold">
                Hello,World.
            </StyledText>
        </StyledView>
    )
}

export default NativewindDemo
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/nativewind Releases](https://github.com/react-native-oh-library/nativewind/releases)

## API
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                                  | Type                                                         | Required | Platform | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| styled()             | can be used similar to Styled Components,and provide base styling. | (ComponentName:JSX.Element,StyleName?:String) => JSX.Element | no       | All      | yes               |
| StyledComponent      | StyledComponent is the component version of styled accepts your component as prop. | component                                                    | no       | All      | yes               |
| useColorScheme()     | provides access to the devices color scheme.                 | () =>{colorScheme,setColorScheme}                            | no       | All      | yes               |
| NativeWindStyleSheet | A StyleSheet is an abstraction similar to CSS StyleSheets and React Native's StyleSheet | component                                                    | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/nativewind/nativewind/blob/main/packages/nativewind/LICENSE).