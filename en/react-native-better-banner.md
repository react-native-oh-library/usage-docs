> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-better-banner</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/better-banner">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.isc.org/licenses/>">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/better-banner)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-better-banner Releases](https://github.com/react-native-oh-library/better-banner/releases). For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-better-banner
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-better-banner
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { StyleSheet, View, Text } from "react-native";

import BetterBanner from "react-native-better-banner";

const App = () => {
  return (
    <View style={styles.container}>
      <BetterBanner
        bannerComponents={[
          <View
            style={{
              width: "100%",
              height: "100%",
              backgroundColor: "#1997fc",
              alignItems: "center",
              justifyContent: "center",
            }}
          >
            <Text style={{ fontSize: 35, color: "#fff", marginBottom: 10 }}>
              Page 01
            </Text>
            <Text style={{ fontSize: 15, color: "#fff" }}>
              Welcome! have a good time
            </Text>
          </View>,
          <View
            style={{
              width: "100%",
              height: "100%",
              backgroundColor: "#da578f",
              alignItems: "center",
              justifyContent: "center",
            }}
          >
            <Text style={{ fontSize: 35, color: "#fff", marginBottom: 10 }}>
              Page 02
            </Text>
            <Text style={{ fontSize: 15, color: "#fff" }}>
              Welcome! have a good time
            </Text>
          </View>,
          <View
            style={{
              width: "100%",
              height: "100%",
              backgroundColor: "#7c3fe4",
              alignItems: "center",
              justifyContent: "center",
            }}
          >
            <Text style={{ fontSize: 35, color: "#fff", marginBottom: 10 }}>
              Page 03
            </Text>
            <Text style={{ fontSize: 15, color: "#fff" }}>
              Welcome! have a good time
            </Text>
          </View>,
        ]}
        bannerTitles={[
          "Page 01 Page 01 Page 01 Page 01 Page 01 Page 01 Page 01 ",
          "Page 02",
          "Page 03",
        ]}
        onPress={(index) => alert("you pressed index is : " + index)}
        indicatorContainerBackgroundColor={"rgba(0,0,0,0.3)"}
        isSeamlessScroll={true}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
});

export default App;
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-better-banner Releases](https://github.com/react-native-oh-library/better-banner/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                              | Description                                                  | Type     | Default               | Platform | HarmonyOS Support |
| --------------------------------- | ------------------------------------------------------------ | -------- | --------------------- | -------- | ----------------- |
| bannerImages                      | Displays banner images. Either this API or `bannerComponents` can be called.                | Array    | []                    | All      | Yes               |
| bannerComponents                  | Displays custom banner components. Either this API or `bannerImages` can be called.              | Array    | []                    | All      | Yes               |
| bannerHeight                      | Default height of the banner.                                           | Number   | 250                   | All      | Yes               |
| bannerTitles                      | Title of each image or component.                                    | Array    | []                    | All      | Yes               |
| bannerTitleTextColor              | Title text color of each image or component.                          | String   | #fff                  | All      | Yes               |
| bannerTitleTextSize               | Title text size of each image or component.                          | Number   | 2000                  | All      | Yes               |
| isAutoScroll                      | Whether to enable auto scroll.                                            | Boolean  | true                  | All      | Yes               |
| isSeamlessScroll                  | Whether to enable seamless scroll. (This value is normal on iOS devices but abnormal on some Android devices.)  | Boolean  | false                 | All      | Yes               |
| adaptSeamlessScrollValue          | If seamless scroll is abnormal on some models, you can set this value to `true` or `false`. This value specifies whether to display the scrolling animation through `scrollTo` of `ScrollView`.| Boolean  | false                 | All      | Yes               |
| indicatorWidth                    | Indicator width.                                                  | Number   | 10                    | All      | Yes               |
| indicatorHeight                   | Indicator height.                                                  | Number   | 6                     | All      | Yes               |
| indicatorColor                    | Indicator color.                                                  | String   | rgba(255,255,255,0.6) | All      | Yes               |
| indicatorStyle                    | Indicator style. You can also use this property to set the width, height, color, and rounded corner of the indicator at a time. This property covers `indicatorWidth`, `indicatorHeight`, and `indicatorColor`.| Object   | {}                    | All      | Yes               |
| indicatorGap                      | Indicator gap.                                            | Number   | 6                     | All      | Yes               |
| activeIndicatorColor              | Active indicator color.                                              | String   | #fff                  | All      | Yes               |
| indicatorGroupPosition            | Position of the indicator group. It can be set to `left`, `center`, and `right`. If `bannerTitles` has been set, this property can only be `right`.| String   | right                 | All      | Yes               |
| indicatorGroupSideOffset          | Side offset of the indicator group.                                          | Number   | 10                    | All      | Yes               |
| indicatorContainerHeight          | Height of the indicator container.                                              | Number   | 32                    | All      | Yes               |
| indicatorContainerBackgroundColor | Background color of the indicator container.                                            | String   | transparent           | All      | Yes               |
| onPress()                         | Callback function called when the banner image is touched. It returns the banner `index`.             | Function | ()=>{}                | All      | Yes               |
| onScrollEnd()                     | Callback function called when the scrolling of each banner image ends. It is equivalent to `onMomentumScrollEnd` of `ScrollView`.| Function | ()=>{}                | All      | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The ISC License (ISC)](https://www.isc.org/licenses/).
