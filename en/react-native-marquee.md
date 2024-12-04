> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-marquee</code> </h1>
</p>

This project is based on [react-native-marquee@0.5.0](https://github.com/kyo504/react-native-marquee)。

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-marquee`, The version correspondence details are as follows:

| Version                   | Package Name                                      | Repository         | Release                    |
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |
| <= 0.5.0-0.0.1@deprecated | @react-native-oh-tpl/react-native-marquee | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-marquee) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-marquee/releases) |
| > 0.5.1                  | @react-native-ohos/react-native-marquee   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-marquee) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-marquee/releases) |


## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-marquee
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-marquee
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { Component } from "react";
import { StyleSheet, View } from "react-native";
import MarqueeText from "react-native-marquee";

export default class MarqueeTextSample extends Component {
  render() {
    return (
      <View style={styles.container}>
        <MarqueeText
          style={{ fontSize: 24 }}
          speed={1}
          marqueeOnStart={true}
          loop={true}
          delay={1000}
        >
          Lorem Ipsum is simply dummy text of the printing and typesetting
          industry and typesetting industry.
        </MarqueeText>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
  },
});
```

## 2. Constraints

### 2.1 Compatibility

Check the release version information in the release address of the third-party library: [@react-native-ohos/react-native-marquee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-marquee/releases)

## 3. Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

MarqueeText component basically inherits [TextProps](https://reactnative.dev/docs/text) and the followings are additional ones:

| Name              | Description                                                               | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| marqueeOnStart    | A flag whether to start marquee animation right after render              | boolean  | no     | All      | yes               |
| speed             | Speed calculated as pixels/second                                         | number   | no      | All      | yes               |
| loop              | 	A flag whether to loop marquee animation or not                         | boolean  | no     | All      | yes               |
| delay             | Duration to delay the animation after render, in milliseconds             | number   | no      | All      | yes               |
| onMarqueeComplete | A callback for when the marquee finishes animation and stops              | function | no      | All      | yes               |
| consecutive       | A flag to enable consecutive mode that imitates the default behavior of HTML marquee element. Does not take effect if loop is false | boolean  | no      | All      | yes               |

## 4. Known Issues

## 5. Others

## 6. License

This project is licensed under [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-marquee/blob/master/LICENSE).

