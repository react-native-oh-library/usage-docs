> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-loading-spinner-overlay</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ladjs/react-native-loading-spinner-overlay">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ladjs/react-native-loading-spinner-overlay/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/ladjs/react-native-loading-spinner-overlay)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-loading-spinner-overlay@3.0.1
```

#### **yarn**

```bash
yarn add react-native-loading-spinner-overlay@3.0.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import { StyleSheet, Text, View } from "react-native";
import Spinner from "react-native-loading-spinner-overlay";

type Props = {};
export default class App extends Component<Props> {
  state = {
    spinner: false,
  };

  componentDidMount() {
    setInterval(() => {
      this.setState({
        spinner: !this.state.spinner,
      });
    }, 3000);
  }

  render() {
    return (
      <View style={styles.container}>
        <Spinner
          visible={this.state.spinner}
          textContent={"Loading..."}
          textStyle={styles.spinnerTextStyle}
        />
      </View>
    );
  }
}

const styles = StyleSheet.create({
  spinnerTextStyle: {
    color: "#FFF",
  },
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
  },
});
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name            | Description                                                                                                                                                                        | Type                                     | Default               | Required | Platform | HarmonyOS Support |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------- | --------------------- | -------- | -------- | ----------------- |
| cancelable      | If set to false, it will prevent spinner from hiding when pressing the hardware back button. If set to true, it will allow spinner to hide if the hardware back button is pressed. | Boolean                                  | `false`               | no       | Android  | yes               |
| color           | Changes the spinner's color (example values are `red`, `#ff0000`, etc). For adjusting the contrast see `overlayColor` prop below.                                                  | String                                   | `"white"`             | no       | All      | yes               |
| animation       | Changes animation on show and hide spinner's view.                                                                                                                                 | String (enum) `none`, `slide`, `fade`    | `"none"`              | no       | All      | yes               |
| overlayColor    | Changes the color of the overlay.                                                                                                                                                  | String                                   | `rgba(0, 0, 0, 0.25)` | no       | All      | yes               |
| size            | Sets the spinner's size. No other cross-platform sizes are supported right now.                                                                                                    | String (enum) `small`, `normal`, `large` | `"large"`             | no       | All      | yes               |
| textContent     | Optional text field to be shown.                                                                                                                                                   | String                                   | `""`                  | no       | All      | yes               |
| textStyle       | The style to be applied to the `<Text>` that displays the `textContent`.                                                                                                           | StyleSheet                               | `-`                   | no       | All      | yes               |
| visible         | Controls the visibility of the spinner.                                                                                                                                            | Boolean                                  | `false`               | yes      | All      | yes               |
| indicatorStyle  | Additional styles for the [ActivityIndicator](https://facebook.github.io/react-native/docs/activityindicator) to inherit                                                           | StyleSheet                               | `undefined`           | no       | All      | yes               |
| customIndicator | An alternative, custom component to use instead of the default `<ActivityIndicator />`                                                                                             | Element                                  | `undefined`           | no       | All      | yes               |
| children        | Children element(s) to nest inside the spinner                                                                                                                                     | Element                                  | `undefined`           | no       | All      | yes               |

## Known Issues

- [ ] 在 RNOH 框架中引入 RN 组件`Modal`和`ActivityIndicator`嵌套使用(`ActivityIndicator`作为`Modal`的 children)时会出现`ActivityIndicator`无法正常运作，导致当前库也无法在 HarmonyOS 中正常 Running。

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ladjs/react-native-loading-spinner-overlay/blob/master/LICENSE).

