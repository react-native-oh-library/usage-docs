> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-mask-text</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/akinncar/react-native-mask-text">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/akinncar/react-native-mask-text/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/akinncar/react-native-mask-text)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-mask-text@0.14.2
```

#### **yarn**

```bash
yarn add react-native-mask-text@0.14.2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import { StyleSheet, Text, View } from "react-native";
import { MaskedTextInput, MaskedText } from "react-native-mask-text";

export default function App() {
  const [maskedValue, setMaskedValue] = useState("");
  const [unMaskedValue, setUnmaskedValue] = useState("");

  const [currencyMaskedValue, setCurrencyMaskedValue] = useState("");
  const [currencyUnMaskedValue, setCurrencyUnmaskedValue] = useState("");

  return (
    <View style={styles.container}>
      <Text style={styles.title}>MaskedTextInput Component:</Text>
      <MaskedTextInput
        mask="AAA-999"
        onChangeText={(text, rawText) => {
          setMaskedValue(text);
          setUnmaskedValue(rawText);
        }}
        style={styles.input}
        keyboardType="numeric"
      />
      <Text style={styles.paragraph}>Raw Text: {unMaskedValue}</Text>
      <Text style={styles.paragraph}>Masked Text: {maskedValue}</Text>

      <Text style={styles.title}>MaskedTextInput Component with Currency:</Text>
      <MaskedTextInput
        type="currency"
        options={{
          prefix: "$",
          decimalSeparator: ".",
          groupSeparator: ",",
          precision: 2,
        }}
        onChangeText={(text, rawText) => {
          setCurrencyMaskedValue(text);
          setCurrencyUnmaskedValue(rawText);
        }}
        style={styles.input}
        keyboardType="numeric"
      />
      <Text style={styles.paragraph}>Raw Text: {currencyUnMaskedValue}</Text>
      <Text style={styles.paragraph}>Masked Text: {currencyMaskedValue}</Text>

      <Text style={styles.title}>MaskedText Component:</Text>
      <MaskedText mask="99/99/9999" style={styles.paragraph}>
        30081990
      </MaskedText>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    backgroundColor: "#ecf0f1",
    padding: 8,
  },
  title: {
    margin: 24,
    fontSize: 24,
    textAlign: "center",
    fontWeight: "bold",
  },
  paragraph: {
    margin: 24,
    fontSize: 18,
    textAlign: "center",
  },
  input: {
    height: 40,
    margin: 12,
    borderWidth: 1,
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

| Name | Description                                    | Type                                                               | Default | Required | Platform | HarmonyOS Support |
| ---- | ---------------------------------------------- | ------------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| type | Show type                                      | String (enum) `custom`, `date`, `time`,`currency`                  | custom  | no       | All      | yes               |
| mask | Custom Mask. Pattern used in masked components | `9` - accept digit. `A` - accept alpha. `S` - accept alphanumeric. | null    | no       | All      | yes               |

### Date Mask

These options only are used if you use prop `type="date"` in your component:

| Name       | Description | Type   | Default    | Required | Platform | HarmonyOS Support |
| ---------- | ----------- | ------ | ---------- | -------- | -------- | ----------------- |
| dateFormat | Date Format | string | yyyy/mm/dd | no       | All      | yes               |

### Time Mask

These options only are used if you use prop `type="time"` in your component:

| Name       | Description | Type   | Default  | Required | Platform | HarmonyOS Support |
| ---------- | ----------- | ------ | -------- | -------- | -------- | ----------------- |
| timeFormat | Time Format | string | HH:mm:ss | no       | All      | yes               |

### Currency Mask

These options only are used if you use prop `type="currency"` in your component:

| Name                   | Description                                 | Type   | Default | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------------------------------------- | ------ | ------- | -------- | -------- | ----------------- |
| prefix                 | String to prepend                           | string | null    | No       | All      | yes               |
| decimalSeparator       | Separation for decimals                     | string | null    | No       | All      | yes               |
| groupSeparator         | Grouping separator of the integer part      | string | null    | No       | All      | yes               |
| precision              | Precision for fraction part (cents)         | number | 0       | No       | All      | yes               |
| groupSize              | Primary grouping size of the integer part   | number | 3       | No       | All      | yes               |
| secondaryGroupSize     | Secondary grouping size of the integer part | number | null    | No       | All      | yes               |
| fractionGroupSeparator | Grouping separator of the fraction part     | string | null    | No       | All      | yes               |
| fractionGroupSize      | Grouping size of the fraction part          | number | null    | No       | All      | yes               |
| suffix                 | String to append                            | string | null    | No       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/akinncar/react-native-mask-text/blob/main/LICENSE).
