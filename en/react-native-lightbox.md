> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-lightbox</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/cbbfcd/react-native-lightbox">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/cbbfcd/react-native-lightbox/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/cbbfcd/react-native-lightbox)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-lightbox-v2@0.9.0
```

#### **yarn**

```bash
yarn add react-native-lightbox-v2@0.9.0
```

<!-- tabs:end -->

> [!WARNING] The name of the imported repository remains unchanged.

```ts
import React, { useState } from "react";
import {
  Image,
  ScrollView,
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
  SafeAreaView,
  Alert,
} from "react-native";

import Lightbox from "react-native-lightbox-v2";

const BASE_PADDING = 10;

export const ReactNativeLightBoxExample = () => {
  let [info, setInfo] = useState("");

  const callBack = (type: any) => {
    setInfo(type);
    Alert.alert(type);
  };

  let eventObject = {
    willClose: () => callBack("willClose"),
    onClose: () => callBack("onClose"),
    onOpen: () => callBack("onOpen"),
    didOpen: () => callBack("didOpen"),
    onLongPress: () => callBack("onLongPress"),
    onLayout: () => callBack("onLayout"),
    doubleTapCallback: () => callBack("doubleTapCallback"),
    longPressCallback: () => callBack("longPressCallback"),
  };

  return (
    <View style={styles.container}>
      <View>
        <Text>eventCallBack {info}</Text>
      </View>
      <View style={styles.text}>
        <Text>eventCallBack </Text>
      </View>
      <Lightbox {...eventObject}>
        <View style={styles.customHeaderBox}>
          <Text>I have eventCallBack</Text>
        </View>
      </Lightbox>

      <View style={styles.text}>
        <Text>renderHeader </Text>
      </View>
      <Lightbox
        renderHeader={(close) => (
          <TouchableOpacity onPress={close}>
            <Text style={styles.closeButton}>Close</Text>
          </TouchableOpacity>
        )}
      >
        <View style={styles.customHeaderBox}>
          <Text>I have a custom header</Text>
        </View>
      </Lightbox>
      <View style={styles.text}>
        <Text>renderContent </Text>
      </View>
      <Lightbox
        renderContent={() => (
          <View style={styles.customHeaderBox}>
            <Text style={{ color: "red" }}>renderContent</Text>
          </View>
        )}
      >
        <View style={styles.customHeaderBox}>
          <Text>I have a custom renderContent</Text>
        </View>
      </Lightbox>
    </View>
  );
};
const styles = StyleSheet.create({
  container: {
    paddingHorizontal: BASE_PADDING,
    backgroundColor: "white",
  },
  closeButton: {
    color: "white",
    borderWidth: 1,
    borderColor: "white",
    padding: 8,
    borderRadius: 3,
    textAlign: "center",
    margin: 10,
    alignSelf: "flex-end",
  },
  customHeaderBox: {
    height: 150,
    backgroundColor: "#6C7A89",
    justifyContent: "center",
    alignItems: "center",
  },

  row: {
    flexDirection: "row",
    marginLeft: -BASE_PADDING,
    marginRight: -BASE_PADDING,
  },
  col: {
    flex: 1,
  },

  contain: {
    flex: 1,
    height: 150,
  },
  text: {
    marginVertical: BASE_PADDING * 2,
  },
});
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71 (API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

This library is a UI component library. You can configure properties to implement corresponding functionalities.

| Name                        | Description                                                  | Type       | Required | Platform | HarmonyOS Support |
| --------------------------- | ------------------------------------------------------------ | ---------- | -------- | -------- | ----------------- |
| **`activeProps`**           | (Optional) Applies to the content component in lightbox mode. It can be used to apply a custom style or a higher-resolution image source.| `object`   | no       | all      | yes               |
| **`renderHeader(close)`**   | Sets the custom header, which is used to replace the default X button.                        | `function` | no       | all      | yes               |
| **`renderContent`**         | Sets the custom lightbox content, which is used to replace the default subcontent.                  | `function` | no       | all      | yes               |
| **`willClose`**             | Triggered before the lightbox is closed.                                         | `function` | no       | all      | yes               |
| **`onClose`**               | Triggered when the lightbox is closed.                                         | `function` | no       | all      | yes               |
| **`onOpen`**                | Triggered when the lightbox is opened.                                         | `function` | no       | all      | yes               |
| **`didOpen`**               | Triggered after the lightbox is opened.                                         | `function` | no       | all      | yes               |
| **`onLongPress`**           | Triggered when the lightbox is long pressed.                                         | `function` | no       | all      | yes               |
| **`onLayout`**              | Triggered after the lightbox layout is complete.                                     | `function` | no       | all      | yes               |
| **`doubleTapCallback`**     | Triggered when the lightbox is double-tapped.                                         | `function` | no       | all      | yes               |
| **`doubleTapZoomEnabled`**  | Sets whether to enable zooming through double-tap. The default value is `true`.                            | `boolean`  | no       | all      | yes               |
| **`doubleTapGapTimer`**     | Sets the double-tap time gap. The default value is `500 ms`.                          | `number`   | no       | all      | yes               |
| **`longPressGapTimer`**     | Sets the time gap for long press. The default value is `2000 ms`.                       | `number`   | no       | all      | yes               |
| **`longPressCallback`**     | Triggered after the content is long pressed.                                              | `function` | no       | all      | yes               |
| **`doubleTapZoomToCenter`** | Zooms in the view to the center through double-tap.                                            | `boolean`  | no       | all      | yes               |
| **`doubleTapMaxZoom`**      | The maximum amplification coefficient. The default value is `2`.                                    | `number`   | no       | all      | yes               |
| **`doubleTapZoomStep`**     | Zoom ratio of each double-tap. The default value is `0.5`.                            | `number`   | no       | all      | yes               |
| **`underlayColor`**         | Touchable background color. The default value is `black`.                            | `string`   | no       | all      | yes               |
| **`backgroundColor`**       | The lightbox background color. The default value is `black`.                           | `string`   | no       | all      | yes               |
| **`swipeToDismiss`**        | Enables gestures to cancel full-screen mode by swiping up or down. The default value is `true`.   | `bool`     | no       | all      | yes               |
| **`disabled`**              | Disables lightbox. The default value is `false`.                               | `bool`     | no       | all      | yes               |
| **`style`**                 | Style of the lightbox view wrapper.                                   | `object`   | no       | all      | yes               |
| **`dragDismissThreshold`**  | Threshold distance for swiping to exit. The default value is `150`.                            | `number`   | no       | all      | yes               |
| **`modalProps`**            | Modal property. The default value is `{}`.                    | `object`   | no       | all      | yes               |
| **`useNativeDriver`**       | Whether to use the local driver. The default value is `false`.                        | `bool`     | no       | all      | yes               |
| **`springConfig`**          | [`Animated.spring`](https://facebook.github.io/react-native/docs/animations.html) configuration. The default value is `{ tension: 30, friction: 7 }`.| `object`   | no       | all      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/cbbfcd/react-native-lightbox/blob/master/LICENSE).
