> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>rn-placeholder</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mfrachet/rn-placeholder">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mfrachet/rn-placeholder/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/rn-placeholder)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/rn-placeholder Releases](https://github.com/react-native-oh-library/rn-placeholder/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/rn-placeholder@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/rn-placeholder@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import {
  Placeholder,
  PlaceholderMedia,
  PlaceholderLine,
  Fade,
} from "@react-native-oh-tpl/rn-placeholder";

const App = () => (
  <Placeholder
    Animation={Fade}
    Left={PlaceholderMedia}
    Right={PlaceholderMedia}
  >
    <PlaceholderLine width={80} />
    <PlaceholderLine />
    <PlaceholderLine width={30} />
  </Placeholder>
);
export default App;
```

## Constraints

### Compatibility

This document is verified based on the following versions:

RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1) ; IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

详情见 [rn-placeholder 源库地址](https://github.com/mfrachet/rn-placeholder)

**组件 Placeholder**

It's the wrapper around all of the other components. Using alone will not produce anything interesting. You have put some line or media inside to make it powerful.It accepts all the props of a React Native View plus:

| Name      | Description                                         | Type          | Required | Platform | HarmonyOS Support |
| --------- | --------------------------------------------------- | ------------- | -------- | -------- | ----------------- |
| Animation | An optional component that animates the placeholder | Animations    | no       | All      | Yes               |
| Left      | An optional component to display on the left        | ComponentType | no       | All      | Yes               |
| Right     | An optional component to display on the right       | ComponentType | no       | All      | Yes               |

**_Animations_**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| --------- | -------------------------------------------------- | ------------- | -------- | -------- | -------- |
| Fade | This is the base animation that makes the placeholder become clearer on a specified interval| ComponentType | no | All | Yes |
| ShineOverlay | This applies a tiny overlay from left to right of the placeholder. It's pretty neat but it has the drawback to only work without style customization: only on white background with gray lines |ComponentType| no | All | Yes |
| Shine | The shine animation is an attempt to overcome the overlay problem of the ShineOverlay animation by animating only the differnt part of the placeholder | ComponentType | no | All | Yes |
| Loader | A simple placeholder animation based on the standard loader (ActivityIndicator) of each platforms | ComponentType | no | All | Yes |
| Progressive | A progressive loading animation effect | ComponentType | no | All | Yes |
| Tweaking existing animations | It's possible to tweak a specific animation by passing it additional props. However keep in mind that it's important to spread the props from the Animation render function. Else you will be in strange behaviors| ComponentType | no | All | Yes |

**组件 PlaceholderLine**

A PlaceholderLine is one of the two basic and visual components of a placeholder.

| Name     | Description                                                            | Type    | Required | Platform | HarmonyOS Support |
| -------- | ---------------------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| height   | The line height, default is 12                                         | number  | no       | All      | Yes               |
| color    | The line color, default is #efefef                                     | string  | no       | All      | Yes               |
| width    | The line width in percent, default is 100(%)                           | number  | no       | All      | Yes               |
| noMargin | Defines if a line should have a margin bottom or not, default is false | boolean | no       | All      | Yes               |
| style    | Customize the style of the underlying View component                   | object  | no       | All      | Yes               |

**组件 PlaceholderMedia**

A PlaceholderMedia is the second of the two basic and visual components of a placeholder. It can be used a single placeholder like following:

| Name    | Description                                              | Type    | Required | Platform | HarmonyOS Support |
| ------- | -------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| size    | The media size (height / width), default is 40           | number  | no       | All      | Yes               |
| isRound | Defines if the media is rounded or not, default is false | boolean | no       | All      | Yes               |
| color   | The media color, default is #efefef                      | string  | no       | All      | Yes               |
| style   | Customize the style of the underlying View component     | object  | no       | All      | Yes               |

## Known Issues

- [ ] package.json 中 peerDependencies 依赖 react 版本与项目 react 版本不一致会产生依赖冲突，此问题只会导致 npm 安装依赖报错，不对组件功能造成影响。源库此问题 issues: [issue#226](https://github.com/mfrachet/rn-placeholder/issues/226)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mfrachet/rn-placeholder/blob/master/LICENSE.md).
