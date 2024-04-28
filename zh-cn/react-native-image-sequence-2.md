> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-image-sequence</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-image-sequence">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-image-sequence/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-image-sequence)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[react-native-image-sequence Releases](https://github.com/react-native-oh-library/react-native-image-sequence/releases)，并下载适用版本的 tgz 包

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-sequence-2@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-sequence-2@file:#
```

<!-- tabs:end -->

快速使用：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { SafeAreaView, StyleSheet } from "react-native-harmony";
import { View, Text, Switch, TextInput, Button } from "react-native";
import TestDemo2 from "./TestDemo2";

const images = [
  { uri: "https://octodex.github.com/images/stormtroopocat.jpg" },
  require("../../assets/2.jpg"),
  require("../../assets/3.jpg"),
  require("../../assets/4.jpg"),
  require("../../assets/5.jpg"),
  require("../../assets/6.jpg"),
];

export interface sequenceType {
  images: NodeRequire[];
  loop: boolean;
  startFrameIndex: number;
  framesPerSecond: number;
  downsampleWidth: number;
  downsampleHeight: number;
}

const ImageSequenceDemo = (props: any) => {
  const [loopData, setLoopData] = useState(false);
  const [isShow, setIsShow] = useState(false);
  const [winWidth, setWinWidth] = useState(300);
  const [winHeight, setWinHeight] = useState(200);
  const [downsampleWidth, setDownSampleWidth] = useState(-1);
  const [downsampleHeight, setDownSampleHeight] = useState(-1);

  // 设置采样宽度
  const inputSampleWidth = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setDownSampleWidth(Number(value));
  };

  // 设置采样高度
  const inputSampleGeight = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setDownSampleHeight(Number(value));
  };

  // 设置起始位置
  const [startFrameIndex, setFrameIndex] = useState(0);
  const inputStartFrameIndex = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    let _value = Number(value);
    if (Number(value) > images.length) {
      _value = 0;
    }
    setFrameIndex(_value);
  };

  // 设置速率
  const [framesPerSecond, setFramesPerSecond] = useState(24);
  const inputFramesPerSecond = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    let _value = Number(value);
    if (Number(value) <= 0) {
      _value = 24;
    }
    setFramesPerSecond(_value);
  };

  const buttonIsShow = () => {
    setIsShow(!isShow);
  };

  const inputSetWinWidth = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setWinWidth(Number(value));
  };

  const inputSetWinHeight = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setWinHeight(Number(value));
  };

  return (
    <SafeAreaView>
      <View>
        <View>
          <Text>
            Current view size:width: {winWidth}, height:{winHeight}
          </Text>
          <Text>
            开启循环：<Switch onValueChange={(value) => setLoopData(value)}></Switch>
          </Text>
          <View>
            <Text>图片宽度/高度：</Text>
            <View style={styles.box}>
              <TextInput
                style={[styles.input, styles.input1]}
                onChangeText={(value) => inputSetWinWidth(value)}
                defaultValue="300"
                keyboardType="numeric"
              />
              <TextInput
                style={[styles.input, styles.input1]}
                onChangeText={(value) => inputSetWinHeight(value)}
                defaultValue="200"
                keyboardType="numeric"
              />
            </View>
          </View>
          <Text>开始位置：</Text>
          <TextInput
            style={styles.input}
            onChangeText={(value) => inputStartFrameIndex(value)}
            defaultValue="0"
            keyboardType="numeric"
          />
          <Text>播放速度：</Text>
          <TextInput
            style={styles.input}
            onChangeText={(value) => inputFramesPerSecond(value)}
            defaultValue="24"
            keyboardType="numeric"
          />
          <Text>采样宽度：</Text>
          <TextInput
            style={styles.input}
            onChangeText={(value) => inputSampleWidth(value)}
            defaultValue="-1"
            keyboardType="default"
          />
          <Text>采样高度：</Text>
          <TextInput
            style={styles.input}
            onChangeText={(value) => inputSetWinHeight(value)}
            defaultValue="-1"
            keyboardType="default"
          />
        </View>
        {!isShow ? (
          <Button title="显示" onPress={() => buttonIsShow()} />
        ) : (
          <Button title="返回" onPress={() => buttonIsShow()} />
        )}
        {isShow ? (
          <TestDemo2
            loop={loopData}
            images={images}
            width={winWidth}
            height={winHeight}
            startFrameIndex={startFrameIndex}
            framesPerSecond={framesPerSecond}
            downsampleWidth={downsampleWidth}
            downsampleHeight={downsampleHeight}
          />
        ) : null}
      </View>
    </SafeAreaView>
  );
};
const styles = StyleSheet.create({
  continer: {
    flex: 1,
    justifyContent: "center",
    width: "100%",
    height: "100%",
  },
  title: {
    textAlign: "center",
    marginVertical: 8,
  },
  fixToText: {
    flexDirection: "row",
    justifyContent: "space-between",
  },
  separator: {
    marginVertical: 8,
    borderBottomColor: "#737373",
    borderBottomWidth: StyleSheet.hairlineWidth,
  },
  input: {
    height: 40,
    margin: 12,
    borderWidth: 1,
    borderColor: "red",
    padding: 10,
    width: 200,
  },
  box: {
    flexDirection: "row",
    justifyContent: "flex-start",
  },
  input1: {
    width: 100,
  },
});

export default ImageSequenceDemo;
```

```
import { StyleSheet, View } from "react-native";
import ImageSequence from 'react-native-image-sequence-2'

const Separator = () => <View style={styles.separator}/>
const TestDemo2 = (props: any) => {
    return (
        <ImageSequence
        images={props.images}
        loop={props.loop}
        startFrameIndex={props.startFrameIndex}
        framesPerSecond={props.framesPerSecond}
        downsampleWidth={props.downsampleWidth}
        downsampleHeight={props.downsampleHeight}
        style={{width: props.width, height: props.height}}
        />
    )
}
const styles = StyleSheet.create({
    separator: {
        marginVertical: 8,
        borderBottomColor: '#737373',
        borderBottomWidth: StyleSheet.hairlineWidth
    }
})

export default TestDemo2
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react-native-openharmony",
    "@rnoh-image-sequence": "file:../../node_modules/@react-native-oh-tpl/react-native-image-sequence-2/harmony/image_sequence.har"
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
    "rnoh": "file:../rnoh",
    "@rnoh-image-sequence": "file:../../node_modules/@react-native-oh-tpl/react-native-image-sequence-2/harmony/image_sequence"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 ImageSequencePackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
# RNOH_END: add_package_subdirectories

+ file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
+   ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "generated/RNOHGeneratedPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNOHGeneratedPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 image sequence 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import { RNImageSequence } from "rnoh-image-sequence"

  @Builder
  function buildCustomComponent(ctx: ComponentBuilderContext) {
    if (ctx.componentName === SAMPLE_VIEW_TYPE) {
      SampleView({
        ctx: ctx.rnComponentContext,
        tag: ctx.tag,
        buildCustomComponent: buildCustomComponent
      })
    }
+  if (ctx.componentName === RNImageSequence.NAME) {
+     RNImageSequence({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag
+     })
+   }
    ...
  }
  ...
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name             | Description                                                                                                                                                     | Type    | Required | Platform | HarmonyOS Support |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| images           | An array of source images. Each element of the array should be the result of a call to require(imagePath)                                                       | any[]   | Yes      | All      | Yes               |
| startFrameIndex  | Which index of the images array should the sequence start at. Default: 0                                                                                        | number  | No       | All      | Yes               |
| framesPerSecond  | Playback speed of the image sequence. Default: 24                                                                                                               | number  | No       | All      | Yes               |
| loop             | Should the sequence loop. Default: true                                                                                                                         | boolean | No       | All      | Yes               |
| downsampleWidth  | The width to use for optional downsampling. Both `downsampleWidth` and `downsampleHeight` must be set to a positive number to enable downsampling. Default: -1  | number  | No       | All      | Yes               |
| downsampleHeight | The height to use for optional downsampling. Both `downsampleWidth` and `downsampleHeight` must be set to a positive number to enable downsampling. Default: -1 | number  | No       | All      | Yes               |

## 遗留问题

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-image-sequence/blob/0.9.1-0.0.1/LICENSE) ，请自由地享受和参与开源。
