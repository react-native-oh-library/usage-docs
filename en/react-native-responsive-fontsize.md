> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-responsive-fontsize</code> </h1>
</p>
<p align="center">
    <a href="https://https://github.com/heyman333/react-native-responsive-fontsize">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/heyman333/react-native-responsive-fontSize/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/heyman333/react-native-responsive-fontSize)

## Installation and Usage

<!-- tabs:start -->

Go to the project directory and execute the following instruction:

#### **npm**

```bash
$ npm install react-native-responsive-fontsize@0.5.1 --save
```

#### **yarn**

```bash
$ yarn add react-native-responsive-fontsize@0.5.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import { RFPercentage, RFValue } from "react-native-responsive-fontsize";
import { View, Text, StyleSheet } from "react-native";

const styles = StyleSheet.create({
  welcome: {
    fontSize: RFValue(24, 580),
    textAlign: "center",
    margin: 10,
  },
  instructions: {
    textAlign: "center",
    margin: 10,
    fontSize: RFPercentage(5),
  },
});
const App = () => {
  return (
    <View
      style={{
        height: "100%",
        width: "100%",
        backgroundColor: "#ffffff",
        marginTop: 50,
      }}
    >
      <View style={{ height: 200 }}>
        <Text>fontSize used RFValue(24, 580):</Text>
        <Text style={styles.welcome}>Hello World1</Text>
      </View>
      <View style={{ height: 200 }}>
        <Text>fontSize used RFPercentage(5):</Text>
        <Text style={styles.instructions}>Hello World2</Text>
      </View>
    </View>
  );
};

export default App;
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.27; SDK：HarmonyOS-NEXT-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.。

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name         | Description                                                                                         | Type     | Required | Platform    | HarmonyOS Support |
| ------------ | --------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| RFPercentage | The font size is calculated as a percentage of the height(`width` in landscape mode) of the device. | function | no       | Android/iOS | yes               |
| RFValue      | The font size is calculated based on standardScreenHeight and passed value                          | function | no       | Android/iOS | yes               |

**RFPercentage parameter**

| Name    | Description | Type   | Required | Platform    | HarmonyOS Support |
| ------- | ----------- | ------ | -------- | ----------- | ----------------- |
| percent | font size   | number | yes      | Android/iOS | yes               |

**RFValue parameter**

| Name                 | Description            | Type   | Required | Platform    | HarmonyOS Support |
| -------------------- | ---------------------- | ------ | -------- | ----------- | ----------------- |
| value                | font size              | number | yes      | Android/iOS | yes               |
| standardScreenHeight | standard screen height | number | no       | Android/iOS | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/heyman333/react-native-responsive-fontSize/blob/master/LICENSE).
