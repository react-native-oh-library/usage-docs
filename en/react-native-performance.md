> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-performance</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/oblador/react-native-performance">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/oblador/react-native-performance/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-performance)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-performance Releases](https://github.com/react-native-oh-library/react-native-performance/releases). For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-performance
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-performance
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useEffect } from "react";
import {
  ScrollView,
  StyleSheet,
  View,
  Text,
  Button,
  Alert,
  FlatList,
  SafeAreaView,
  StatusBar,
  TouchableOpacity,
} from "react-native";
import performance, {
  PerformanceObserver,
  setResourceLoggingEnabled,
} from "@react-native-oh-tpl/react-native-performance";
export function TestNativePerformance() {
  const [result1, setResult1] = React.useState(0);
  const [result2, setResult2] = React.useState("");
  const [result3, setResult3] = React.useState("");
  const [result4, setResult4] = React.useState("");
  const [result5, setResult5] = React.useState("");
  const [result6, setResult6] = React.useState("");
  const [result7, setResult7] = React.useState("");
  const handleTimeStampClick1 = () => {
    performance.mark("entry");
    let entry = performance.getEntriesByName("entry")[0];
    const timestamp = Date.now() - performance.timeOrigin + entry.startTime;
    setResult1(timestamp);
  };
  const handleTimeStampClick2 = () => {
    performance.mark("myMark");
    performance.measure("myMeasure2", "myMark");
    let ms = performance.getEntriesByName("myMeasure2");
    setResult2(JSON.stringify(ms));
  };
  const handleTimeStampClick3 = () => {
    performance.mark("myMark", {
      detail: {
        screen: "settings",
      },
    });
    performance.measure("myMeasure3", {
      start: "myMark",
      detail: {
        category: "render",
      },
    });
    let ms = performance.getEntriesByName("myMeasure3");
    setResult3(JSON.stringify(ms));
  };
  const handleTimeStampClick4 = () => {
    performance.mark("newTimeMark");
    performance.measure("newTime", "newTimeMark");
    const measureObserver = new PerformanceObserver((list, observer) => {
      let res = [];
      list.getEntries().forEach((entry) => {
        res.push(JSON.stringify(entry));
      });
      setResult4(res.join(","));
    });
    measureObserver.observe({ type: "measure", buffered: true });
  };
  const handleTimeStampClick5 = async () => {
    setResourceLoggingEnabled(true);
    await fetch("https://www.baidu.com");
    let res = performance.getEntriesByType("resource");
    setResult5(JSON.stringify(res));
  };
  const handleTimeStampClick6 = () => {
    performance.metric("myMetric", 123);
    let res = performance.getEntriesByType("metric");
    setResult6(JSON.stringify(res));
  };
  const handleTimeStampClick7 = () => {
    let res = performance.getEntriesByType("react-native-mark");
    setResult7(JSON.stringify(res));
  };

  return (
    <View style={styles.container}>
      <ScrollView style={{ flex: 1 }}>
        <View style={styles.rowStyle}>
          <Button
            onPress={handleTimeStampClick1}
            title="Convert a performance timestamp"
          />
          <Text style={styles.fontstyle}>
            {"Exhibition result1: " + result1}
          </Text>
        </View>
        <View style={styles.rowStyle}>
          <Button
            onPress={handleTimeStampClick2}
            title="Basic measure example"
          />
          <Text style={styles.fontstyle}>
            {"Exhibition result2: " + result2}
          </Text>
        </View>
        <View style={styles.rowStyle}>
          <Button onPress={handleTimeStampClick3} title="Meta data" />
          <Text style={styles.fontstyle}>
            {"Exhibition result3: " + result3}
          </Text>
        </View>
        <View style={styles.rowStyle}>
          <Button
            onPress={handleTimeStampClick4}
            title="Subscribing to entries"
          />
          <Text style={styles.fontstyle}>
            {"Exhibition result4: " + result4}
          </Text>
        </View>
        <View style={styles.rowStyle}>
          <Button onPress={handleTimeStampClick5} title="Network resources" />
          <Text style={styles.fontstyle}>
            {"Exhibition result5: " + result5}
          </Text>
        </View>
        <View style={styles.rowStyle}>
          <Button onPress={handleTimeStampClick6} title="Custom metrics" />
          <Text style={styles.fontstyle}>
            {"Exhibition result6: " + result6}
          </Text>
        </View>
        <View style={styles.rowStyle}>
          <Button onPress={handleTimeStampClick7} title="React Native Marks" />
          <Text style={styles.fontstyle}>
            {"Exhibition result7: " + result7}
          </Text>
        </View>
      </ScrollView>
    </View>
  );
}

const styles = StyleSheet.create({
  rowStyle: {
    marginBottom: 20,
  },
  fontstyle: {
    fontSize: 32,
    fontWeight: 600,
  },
  container: {
    width: "100%",
    height: "100%",
    backgroundColor: "#fffafa",
  },
});
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

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
    "@react-native-oh-tpl/react-native-performance": "file:../../node_modules/@react-native-oh-tpl/react-native-performance/harmony/react_native_performance.har"
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

### 3. Introducing RNPerformancePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNPerformancePackage} from '@react-native-oh-tpl/react-native-performance/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNPerformancePackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-performance Releases](https://github.com/react-native-oh-library/react-native-performance/releases)

## Performance

Exports the **Performance** object by default.

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### Performance property

| Name       | Description                                             | Type   | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| timeOrigin | Returns the high-resolution timestamp used by **Performance** as the performance-related baseline timestamp.| number | yes      | IOS/Android | yes               |

#### Performance method

| Name             | Description                                                                                                                                                                                                                                                                                                                        | Type     | Required | Platform    | HarmonyOS Support |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| now              | Returns a high-resolution timestamp, in milliseconds.                                                                                                                                                                                                                                                                                            | function | yes      | IOS/Android | yes               |
| mark             | Creates a timestamp in the performance input buffer based on the given **markName** value.                                                                                                                                                                                                                                                                | function | yes      | IOS/Android | yes               |
| measure          | Creates a measure record in the performance record cache. If only the measure name is specified, the start timestamp is set to zero, and the end timestamp (used to calculate the duration) is the value returned by **Performance.now()**. You can use a string to set the **PerformanceMark** object to a start tag and an end tag. If only the **endMark** is provided, you need to set an empty measure option object: **performance.Measure("myMeasure", {}, "myEndMarker")**.| function | yes      | IOS/Android | yes               |
| metric           | Generates entries of the **metric** type if you want to collect custom metrics that are not time-based. This function is an extension of the Performance API.                                                                                                                                                                                                        | function | yes      | IOS/Android | yes               |
| getEntries       | Returns a **PerformanceEntry** object array if a **filter** is specified; returns all entries if no parameter is specified.                                                                                                                                                                                                                                       | function | yes      | IOS/Android | yes               |
| getEntriesByName | Returns an array of **PerformanceEntry** objects with the given **name** and **type**.                                                                                                                                                                                                                                                                  | function | yes      | IOS/Android | yes               |
| getEntriesByType | Returns a **PerformanceEntry** object array with the given **type**.                                                                                                                                                                                                                                                                                | function | yes      | IOS/Android | yes               |
| clearMarks       | Removes the declared marks from the cache. If no parameter is passed, all performance entries with the **entry type** mark are removed from the performance entry cache.                                                                                                                                                                              | function | yes      | IOS/Android | yes               |
| clearMeasures    | Removes the declared measure records from the cache. If no parameter is passed, all performance entities whose **entry type** is **measure** are removed from the performance entry cache.                                                                                                                                                                                        | function | yes      | IOS/Android | yes               |

## PerformanceObserver

Generates a **PerformanceObserver** object based on the specified observer callback, which is called when the performance entry event of the **entry type** registered through **observe()** is recorded.

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### PerformanceObserver method

| Name    | Description                                                                                                                           | Type     | Required | Platform    | HarmonyOS Support |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| observe | Specifies the performance entry type for the **PerformanceObserver** object. When a performance entry of a specified type is recorded, the callback of the performance observer object is called.| function | yes      | IOS/Android | yes               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                      | Description                                                                         | Type     | Required | Platform    | HarmonyOS Support |
| ------------------------- | ----------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| setResourceLoggingEnabled | Enables resource logging, which is disabled by default and is used only by **fetch** and **XMLHttpRequest**.| function | yes      | IOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [MIT License](https://github.com/oblador/react-native-performance/blob/master/LICENSE).
