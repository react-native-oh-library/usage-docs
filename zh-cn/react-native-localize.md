<!-- {% raw %} -->
> 模板版本：v0.2.0

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-localize)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-localize Releases](https://github.com/react-native-oh-library/react-native-localize/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

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

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
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

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-localize": "file:../../node_modules/@react-native-oh-tpl/react-native-localize/harmony/rn_localize.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-localize": "file:../../node_modules/@react-native-oh-tpl/react-native-localize/harmony/rn_localize"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 在 ArkTs 侧引入 RNLocalizePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { RNLocalizePackage } from "@react-native-oh-tpl/react-native-localize/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNLocalizePackage(ctx)
  ];
}
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性
要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机ROM。

本文档内容基于以下版本验证通过：

RNOH：0.72.23; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.19

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name                   | Description                                    | Required | Platform | HarmonyOS Support |
| ---------------------- | ---------------------------------------------- | -------- |----------|-------------------|
| getLocales()        | Returns the user preferred locales, in order.             | No       | All      | yes               |
| etNumberFormatSettings()   | Returns number formatting settings. | No       | All      | yes               |
| getCurrencies() | Returns the user preferred currency codes, in order. | No       | All      | yes               |
| getCountry()         | Returns the user current country code (based on its device locale, not on its position).                                  | No       | All      | yes               |
| getCalendar()    | Returns the user preferred calendar format. | No       | All      | yes               |
| getTemperatureUnit()  | Returns the user preferred temperature unit. | No       | All      | No                |
| getTimeZone()         | Returns the user preferred timezone (based on its device settings, not on its position).             | No       | All      | yes               |
| uses24HourClock()   | Returns true if the user prefers 24h clock format, false if they prefer 12h clock format. | No       | All      | yes               |
| usesMetricSystem() | Returns true if the user prefers metric measure system, false if they prefer imperial. | No       | All      | No                |
| usesAutoDateAndTime()         | Tells if the automatic date & time setting is enabled on the phone. Android only                                 | No       | Android  | No                |
| usesAutoTimeZone()    | Tells if the automatic time zone setting is enabled on the phone. Android only | No       | Android  | No                |
| findBestLanguageTag()    | Returns the best language tag possible and its reading direction | No       | All      | yes               |

## 遗留问题
- [ ]  HarmonyOS 侧无法获取温度及长度单位[issue#2](https://github.com/react-native-oh-library/react-native-localize/issues/2)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/zoontek/react-native-localize/blob/master/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->