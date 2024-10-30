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

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-performance Releases](https://github.com/react-native-oh-library/react-native-performance/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-performance@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-performance@file:#
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

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

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

默认导出 Performance 对象

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### Performance property

| Name       | Description                                             | Type   | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| timeOrigin | 返回 Performance 用作性能相关时间戳基线的高分辨率时间戳 | number | yes      | IOS/Android | yes               |

#### Performance method

| Name             | Description                                                                                                                                                                                                                                                                                                                        | Type     | Required | Platform    | HarmonyOS Support |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- | --- | -------- | --- | ----------- | --- |
| now              | 返回一个高分辨率时间戳（以毫秒为单位）                                                                                                                                                                                                                                                                                             | function | yes      | IOS/Android | yes               |
| mark             | 根据给出 markName 值，在性能输入缓冲区中创建一个 timestamp(时间戳)                                                                                                                                                                                                                                                                 | function | yes      | IOS/Android | yes               |
| measure          | 性能记录缓存中使用 measure()创建一个新的测量记录如果仅指定了测量名称，则开始时间戳设置为零，结束时间戳（用于计算持续时间）是 Performance.now()返回的值。可以使用字符串将 PerformanceMark 对象标识为开始标记和结束标记。要只提供一个 endMark，您需要提供一个空的测量选项对象: performance.Measure（“myMeasure”，{}，“myEndMarker”） | function | yes      | IOS/Android | yes               |
| metric           | 如果您希望收集不基于时间的自定义度量，此模块将提供名为.metric（）的 Performance API 扩展，该扩展将生成类型为 metric 的条目                                                                                                                                                                                                         | function | yes      | IOS/Android | yes               |
| getEntries       | 对于给定的 filter，此方法返回 PerformanceEntry 对象数组，如果不带任何参数，返回全部 entries                                                                                                                                                                                                                                        | function | yes      | IOS/Android | yes               |
| getEntriesByName | 返回一个给定名称和 name 和 type 属性的 PerformanceEntry 对象数组                                                                                                                                                                                                                                                                   | function | yes      | IOS/Android | yes               |
| getEntriesByType | 返回一个给定 type 属性的 PerformanceEntry 对象数组                                                                                                                                                                                                                                                                                 | function | yes      | IOS/Android | yes               |
| clearMarks       | 从缓存中移除声明的标记。如果调用这个方法时没有传递参数，则所有带有 entry type 这类标记的 performance entries 将从 performance entry 缓存区中被移除。                                                                                                                                                                               | function | yes      | IOS/Android | yes               |
| clearMeasures    | 从缓存区中移除声明的测量记录。如果这个方法被调用时没有传入参数，则所有 entry type 标记值为"measure" 的性能实体将被从性能入口缓存区中移除。                                                                                                                                                                                         | function | yes      | IOS/Android | yes               |     | function | yes | IOS/Android | yes |

## PerformanceObserver

给定的观察者 callback 生成一个新的 PerformanceObserver 对象。当通过 observe() 方法注册的 条目类型 的 性能条目事件 被记录下来时，调用该观察者回调。

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### PerformanceObserver method

| Name    | Description                                                                                                                           | Type     | Required | Platform    | HarmonyOS Support |
| ------- | ------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| observe | observe() 方法用于指定 PerformanceObserver 对象观察的性能条目类型。当记录一个指定类型的性能条目时，性能监测对象的回调函数将会被调用。 | function | yes      | IOS/Android | yes               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                      | Description                                                                         | Type     | Required | Platform    | HarmonyOS Support |
| ------------------------- | ----------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| setResourceLoggingEnabled | 默认情况下禁用资源日志记录，并且当前仅 fetch/XMLHttpRequest 使用,使用时需设置开启。 | function | yes      | IOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/oblador/react-native-performance/blob/master/LICENSE).
