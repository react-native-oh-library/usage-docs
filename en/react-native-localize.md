> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-localize</code></h1>
</p>
<p align="center">
    <a href="https://github.com/zoontek/react-native-localize">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/zoontek/react-native-localize/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-localize)


## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-localize Releases](https://github.com/react-native-oh-library/react-native-localize/releases)

Go to the project directory and execute the following instruction:

>[!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-localize@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-localize@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```jsx
import * as React from "react";
import {
  I18nManager,
  Platform,
  SafeAreaView,
  ScrollView,
  StyleSheet,
  Text,
  View,
} from "react-native";
import * as RNLocalize from "react-native-localize";

const styles = StyleSheet.create({
  safeArea: {
    backgroundColor: "white",
    flex: 1,
  },
  container: {
    padding: 16,
    alignItems: "flex-start",
  },
  block: {
    marginBottom: 16,
    alignItems: "flex-start",
  },
  name: {
    textDecorationLine: "underline",
    fontWeight: "500",
    marginBottom: 8,
    color: "black",
  },
  value: {
    textAlign: "left",
    color: "black",
  },
});

const Line = ({ name, value }: { name: string; value: unknown }) => (
  <View style={styles.block}>
    <Text style={styles.name}>{name}</Text>
    <Text style={styles.value}>{JSON.stringify(value, null, 2)}</Text>
  </View>
);
function LocalizeDemo() {
  return (
    <SafeAreaView style={styles.safeArea}>
      <ScrollView contentContainerStyle={styles.container}>
        <Line name="RNLocalize.getLocales()" value={RNLocalize.getLocales()} />

        <Line name="RNLocalize.getCurrencies()" value={RNLocalize.getCurrencies()} />

        <Line name="RNLocalize.getCountry()" value={RNLocalize.getCountry()} />

        <Line name="RNLocalize.getCalendar()" value={RNLocalize.getCalendar()} />

        <Line name="RNLocalize.getTimeZone()" value={RNLocalize.getTimeZone()} />

        <Line name="RNLocalize.uses24HourClock()" value={RNLocalize.uses24HourClock()} />

        <Line
          name="RNLocalize.findBestLanguageTag(['en-US', 'en', 'fr', 'zh'])"
          value={RNLocalize.findBestLanguageTag(["en-US", "en", "fr", 'zh'])}
        />
      </ScrollView>
    </SafeAreaView>
  );
}
export default LocalizeDemo;
```

## Use Codegen

this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:


Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-localize": "file:../../node_modules/@react-native-oh-tpl/react-native-localize/harmony/rn_localize.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing RNLocalizePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
  
+ import { RNLocalizePackage } from '@react-native-oh-tpl/react-native-localize/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNLocalizePackage(ctx)
  ];
}
```

### 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-localize Releases](https://github.com/react-native-oh-library/react-native-localize/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name                      | Description                                    | Required | Platform | HarmonyOS Support |
|---------------------------| ---------------------------------------------- | -------- |----------|-------------------|
| getLocales()              | Returns the user preferred locales, in order.             | No       | All      | yes               |
| getNumberFormatSettings() | Returns number formatting settings. | No       | All      | yes               |
| getCurrencies()           | Returns the user preferred currency codes, in order. | No       | All      | yes               |
| getCountry()              | Returns the user current country code (based on its device locale, not on its position).                                  | No       | All      | yes               |
| getCalendar()             | Returns the user preferred calendar format. | No       | All      | yes               |
| getTemperatureUnit()      | Returns the user preferred temperature unit. | No       | All      | No                |
| getTimeZone()             | Returns the user preferred timezone (based on its device settings, not on its position).             | No       | All      | yes               |
| uses24HourClock()         | Returns true if the user prefers 24h clock format, false if they prefer 12h clock format. | No       | All      | yes               |
| usesMetricSystem()        | Returns true if the user prefers metric measure system, false if they prefer imperial. | No       | All      | No                |
| usesAutoDateAndTime()     | Tells if the automatic date & time setting is enabled on the phone. Android only                                 | No       | Android  | No                |
| usesAutoTimeZone()        | Tells if the automatic time zone setting is enabled on the phone. Android only | No       | Android  | No                |
| findBestLanguageTag()     | Returns the best language tag possible and its reading direction | No       | All      | yes               |

## Known Issues
- [ ]  Temperature and length units cannot be obtained in HarmonyOS  [issue#2](https://github.com/react-native-oh-library/react-native-localize/issues/2)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/zoontek/react-native-localize/blob/master/LICENSE).