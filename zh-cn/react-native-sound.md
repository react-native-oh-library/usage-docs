> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-sound</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/zmxv/react-native-sound">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-sound/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-sound)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-library/react-native-sound> Releases](https://github.com/react-native-oh-library/react-native-sound/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-sound@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-sound@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useState } from "react";
import type { PropsWithChildren } from "react";
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  useColorScheme,
  View,
  Button,
} from "react-native";

import {
  Colors,
  DebugInstructions,
  Header,
  LearnMoreLinks,
  ReloadInstructions,
} from "react-native/Libraries/NewAppScreen";

import Sound from "react-native-sound";

type SectionProps = PropsWithChildren<{
  title: string;
  func: () => void;
}>;

type SliderSectionProps = PropsWithChildren<{
  duration: number;
  value: number;
  func: () => void;
}>;

function Section({ title, func }: SectionProps): JSX.Element {
  const isDarkMode = useColorScheme() === "dark";
  return (
    <View style={styles.sectionContainer}>
      <Button
        onPress={func}
        title={title}
        color="#2196f3"
        accessibilityLabel="Learn more about this purple button"
      />
    </View>
  );
}

function SoundDemo(): JSX.Element {
  const isDarkMode = useColorScheme() === "dark";
  const backgroundStyle = {
    backgroundColor: isDarkMode ? Colors.darker : Colors.lighter,
  };

  const navigationOptions = (props: {
    navigation: { state: { params: { title: any } } };
  }) => ({
    title: props.navigation.state.params.title,
  });

  let sound = new Sound("whoosh.mp3");

  const onPlay = () => {
    sound.play();
  };

  return (
    <SafeAreaView style={backgroundStyle}>
      <StatusBar
        barStyle={isDarkMode ? "light-content" : "dark-content"}
        backgroundColor={backgroundStyle.backgroundColor}
      />
      <ScrollView
        contentInsetAdjustmentBehavior="automatic"
        style={backgroundStyle}
      >
        <Header />

        <View
          style={{
            backgroundColor: isDarkMode ? Colors.black : Colors.white,
          }}
        >
          <Section title="play" func={onPlay}></Section>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  sectionContainer: {
    marginTop: 12,
    paddingHorizontal: 24,
  },
  sectionTitle: {
    fontSize: 24,
    fontWeight: "600",
  },
  sectionDescription: {
    marginTop: 8,
    fontSize: 18,
    fontWeight: "400",
  },
  highlight: {
    fontWeight: "700",
  },
});

export default SoundDemo;
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

    "rnoh-sound": "file:../../node_modules/@react-native-oh-tpl/react-native-sound/harmony/sound.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 配置 CMakeLists 和引入 SoundPackge

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
txtproject(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-sound/src/main/cpp" ./sound)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_sound)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "SoundPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SoundPackage>(ctx),
    };
}
```

### 在 ArkTs 侧引入 SoundPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { SoundPackage } from 'rnoh-sound/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SoundPackage(ctx)
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

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[<@react-native-oh-library/react-native-sound> Releases](https://github.com/react-native-oh-library/react-native-sound/releases)

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-sound](https://github.com/react-native-oh-library/react-native-sound)

| Name      | Description                      | Type   | Required | Platform    | HarmonyOS Support |
| --------- | -------------------------------- | ------ | -------- | ----------- | ----------------- |
| setActive | Set the device activation status | string | No       | IOS/Android | yes               |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-sound](https://github.com/react-native-oh-library/react-native-sound)

| Name           | Description                              | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ---------------------------------------- | ------ | -------- | ----------- | ----------------- |
| play           | Start playing audio.                     | string | No       | IOS/Android | yes               |
| pause          | Pause audio playback.                    | string | No       | IOS/Android | yes               |
| stop           | Stop playing audio.                      | string | No       | IOS/Android | yes               |
| reset          | Reset Audio Status.                      | string | No       | Android     | yes               |
| release        | Releasing audio resources.               | string | No       | IOS/Android | yes               |
| getVolume      | Obtains the audio volume.                | string | No       | IOS/Android | yes               |
| setVolume      | Setting the Relative Audio Volume.       | string | No       | IOS/Android | yes               |
| getCurrentTime | Obtains the current playback time point. | string | No       | IOS/Android | yes               |
| setCurrentTime | Sets the playback time point.            | string | No       | IOS/Android | yes               |
| getSpeed       | Obtains the playback speed.              | string | No       | IOS/Android | yes               |
| setSpeed       | Setting the Playback Speed               | string | No       | IOS/Android | yes               |
| isPlaying      | Whether the audio is being played        | string | No       | IOS/Android | yes               |

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/zmxv/react-native-sound/blob/master/LICENSE) ，请自由地享受和参与开源。
