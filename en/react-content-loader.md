> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-content-loader</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/danilowoz/react-content-loader">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/danilowoz/react-content-loader/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-content-loader)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-content-loader Releases](https://github.com/react-native-oh-library/react-content-loader/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-content-loader@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-content-loader@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import ContentLoader, {
  Facebook,
  Code,
  List,
  BulletList,
  Instagram,
  Rect,
  Circle,
} from "react-content-loader/native";
import { View, ScrollView } from "react-native";

export function AppExample() {
  return (
    <View style={{ flex: 1, backgroundColor: "white" }}>
      <ScrollView>
        <ContentLoader
          width={"100%"}
          height={80}
          animate={false}
          viewBox="0 0 380 70"
        >
          <Circle cx="30" cy="30" r="30" />
          <Rect x="80" y="17" rx="4" ry="4" width="300" height="13" />
          <Rect x="80" y="40" rx="3" ry="3" width="250" height="10" />
        </ContentLoader>
        <Facebook></Facebook>
        <Code></Code>
        <List></List>
        <BulletList></BulletList>
        <Instagram></Instagram>
      </ScrollView>
    </View>
  );
}
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-svg](/en/react-native-svg-capi.md) to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-content-loader Releases](https://github.com/react-native-oh-library/react-content-loader/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### Options

| Name              | Description                                                                                                                                                                                                                                                                               | Type                | Required | Platform       | HarmonyOS Support |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- | -------- | -------------- | ----------------- |
| animate           | Opt-out of animations with false                                                                                                                                                                                                                                                          | boolean             | no       | all            | yes               |
| speed             | Animation speed in seconds                                                                                                                                                                                                                                                                | number              | no       | all            | yes               |
| rtl               | Content right-to-left                                                                                                                                                                                                                                                                     | boolean             | no       | all            | yes               |
| backgroundColor   | Used as background of animation                                                                                                                                                                                                                                                           | string              | no       | all            | yes               |
| viewBox           | Use viewBox props to set a custom viewBox value,for more information about how to use it,read the article [How to Scale SVG](https://css-tricks.com/scale-svg/)                                                                                                                           | string              | no       | all            | yes               |
| foregroundColor   | Used as the foreground of animation                                                                                                                                                                                                                                                       | string              | no       | all            | yes               |
| interval          | Animation interval in seconds                                                                                                                                                                                                                                                             | number              | no       | all            | yes               |
| beforeMask        | Define custom shapes before content                                                                                                                                                                                                                                                       | JSX.Element         | no       | all            | partially         |
| uniqueKey         | Use the same value of prop key, that will solve inconsistency on the SSR                                                                                                                                                                                                                  | string              | no       | React DOM only | no                |
| title             | It's used to describe what element it is. Use '' (empty string) to remove.                                                                                                                                                                                                                | string              | no       | React DOM only | no                |
| baseUrl           | Required if you're using `<base url="/" />` document `<head/>`. This prop is common used as: `<ContentLoader baseUrl={window.location.pathname} />` which will fill the SVG attribute with the relative path. Related [#93](https://github.com/danilowoz/react-content-loader/issues/93). | string              | no       | React DOM only | no                |
| backgroundOpacity | Background opacity (0 = transparent, 1 = opaque)used to solve an issue in [Safari](#safari--ios)                                                                                                                                                                                          | number              | no       | React DOM only | no                |
| foregroundOpacity | Animation opacity (0 = transparent, 1 = opaque)used to solve an issue in [Safari](#safari--ios)                                                                                                                                                                                           | number              | no       | React DOM only | no                |
| style             | css style                                                                                                                                                                                                                                                                                 | React.CSSProperties | no       | React DOM only | no                |

## Known Issues

- [ ] beforeMaskProperties 设置非 svg 暴露出来的组件时无效: [issue#256](https://github.com/react-native-oh-library/react-native-harmony-svg/issues/256)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/danilowoz/react-content-loader/blob/master/LICENSE).
