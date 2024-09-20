> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-text-size</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/aMarCruz/react-native-text-size">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/aMarCruz/react-native-text-size/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-BSD-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-text-size)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-text-size Releases](https://github.com/react-native-oh-library/react-native-text-size/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-text-size@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-text-size@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState, useEffect } from 'react';
import {
  ScrollView,
  Text,
  View,
  Dimensions,
  TextInput
} from 'react-native';

import RTNTextSize, { TSFontSpecs, TSFontInfo } from 'react-native-text-size'

export default function TextSizeExample() {
  const [res, setRes] = useState<string[]>([])
  const [res2, setRes2] = useState<string[]>([])
  const fontFamily = 'HarmonyOS Sans SC'
  const [texts, setTexts] = useState<string>('I rnTextSize ❤️')
  const [texts3, setTexts3] = useState<string>('')
  const [width, setWidth] = useState<number>();
  const [height, setHeight] = useState<number>();
  const fontSpecs: TSFontSpecs = {
    fontFamily: undefined,
    fontSize: 20,
    fontStyle: 'normal',
    fontWeight: '700',
  }
  type State = { heights2: number[] }
  const [texts2, setTexts2] = useState(['I ❤️ rnTextSize', 'I ❤️ rnTextSize using flatHeights', 'Thx for flatHeights', 'test123',])
  const [heights2, setHeights2] = useState<number[]>([]);
  const fontSpecs2: TSFontSpecs = {
    fontFamily: undefined,
    fontSize: 20,
    fontStyle: 'italic',
    fontWeight: 'bold',
  }
  const [key, setKey] = useState({})
  const [info, setInfo] = useState<TSFontInfo>()
  const fontSpecs3: TSFontSpecs = {
    fontFamily: 'harmony',
    textBreakStrategy: 'balanced',
  }

  useEffect(() => {
    const myFun = async () => {
      const resp = await RTNTextSize.fontFamilyNames();
      setRes(resp)

      const resp2 = await RTNTextSize.fontNamesForFamilyName(fontFamily);
      setRes2(resp2)

      setTexts(texts)
      const width = Dimensions.get('window').width * 0.8
      const newHeights = await RTNTextSize.measure({
        text: texts,      // array of texts to measure, can include symbols
        width: width,            // max-width of the "virtual" container
        ...fontSpecs,     // RN font specification
      })
      setHeight(newHeights.height);
      setWidth(newHeights.width)

      setTexts2(texts2)
      const width2 = Dimensions.get('window').width * 0.8
      const newHeights2 = await RTNTextSize.flatHeights({
        text: texts2,      // array of texts to measure, can include symbols
        width: width2,            // max-width of the "virtual" container
        ...fontSpecs2,     // RN font specification
      })
      setHeights2(newHeights2);

      const keyp = await RTNTextSize.specsForTextStyles();
      setKey(keyp)

      const infos = await RTNTextSize.fontFromSpecs(fontSpecs3);
      setInfo(infos)
    }
    myFun()
  }, [])

  return (
    <ScrollView style={{ flexGrow: 1 }}>
      <View style={{ paddingLeft: 12, paddingRight: 12 }}>
        <Text>
         measure:[fontFamily: undefined,fontSize: 20,fontStyle: 'normal', 正斜fontWeight: '700']
        </Text>
        <Text style={{
          width: width,
          height: height,
          ...fontSpecs
        }}>
          {texts}
        </Text>
        <TextInput
          value={texts}
          onChangeText={value => { setTexts(value) }}
          style={{ width: '100%', height: 28, borderWidth: 2, borderColor: 'black' }}
        />

        <Text>
          flatHeights:[fontFamily: undefined,fontSize: 20,fontStyle: 'italic', fontWeight: 'bold']
        </Text>
        {texts2.map(
          (texts2, index) => (
            <Text key = {index} style={{ height: heights2[index], ...fontSpecs2 }}>
              {texts2}
            </Text>
          )
        )}
        <TextInput
          value = {texts3}
          onChangeText={value => {
            let value2 =value.split(",");
            setTexts3(value)
            setTexts2(value2)
          }}
          style={{ width: '100%', height: 28, borderWidth: 2, borderColor: 'black' }}
        />
        <Text>
          specsForTextStyles:获取系统默认配置的字体的具体信息
        </Text>
        <Text>
          {JSON.stringify(key)}
        </Text>
        <Text>
          fontFamilyNames:获取系统默认配置的字体
        </Text>
        <Text>
          {res}
        </Text>
        <Text>
          fontNamesForFamilyName:获取系统字体的属性
        </Text>
        <Text>
          {res2}
        </Text>
        <Text>
          fontFromSpecs:返回从给定规范中获得的字体特征
        </Text>
        <Text>
          {JSON.stringify(info)}
        </Text>
      </View>
    </ScrollView>
  )
}
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-text-size": "file:../../node_modules/@react-native-oh-tpl/react-native-text-size/harmony/text_size.har"
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

### 3.配置 CMakeLists 和引入 RNTextSizePackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-text-size/src/main/cpp" ./text-size)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_text_size)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
...
+ #include "RNTextSizePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      ...
+     std::make_shared<RNTextSizePackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNTextSizePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNTextSizePackage } from '@react-native-oh-tpl/react-native-text-size/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    ...
+   new RNTextSizePackage(ctx)
  ];
}
```

### 5.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-text-size Releases](https://github.com/react-native-oh-library/react-native-text-size/releases)


## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> [!tip] 参数信息查看 [Github 地址](https://github.com/react-native-oh-library/react-native-text-size)

| Name                   | Description                                                                     | Type                            | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------------------------- | ------------------------------- | -------- | -------- | ----------------- |
| measure                | Measurement Text                                                                | TSMeasureResult                 | No       | All      | partially               |
| flatHeights            | Measurement Text                                                                | number[]                        | No       | All      | yes               |
| specsForTextStyles     | Get system font information for the running OS                                  | {[key: string]: TSFontForStyle} | No       | All      | yes               |
| fontFromSpecs          | Returns the characteristics of the font obtained from the given specifications. | TSFontInfo                      | No       | All      | yes               |
| fontFamilyNames        | Returns a Promise for an array of font family names available on the system     | string[]                        | No       | All      | yes               |
| fontNamesForFamilyName | Return the data of the corresponding font according to the name                 | string[]                        | No       | All      | yes               |


## 遗留问题

- [ ] fontFamilyNames&fontNamesForFamilyName 问题:需要依赖手机文件 font 目录下的 json 文件，该文件目前没有预置在手机目录下，会导致该接口调用为空。后续底层框架侧修复该问题 [issue#1](https://github.com/react-native-oh-library/react-native-text-size/issues/1)
- [ ] measure方法缺少lineInfo的返回处理 [issue#2](https://github.com/react-native-oh-library/react-native-text-size/issues/8)

## 其他

## 开源协议

本项目基于 [The BSD 2-Clause License（BSD）](https://github.com/aMarCruz/react-native-text-size/blob/master/LICENSE) ，请自由地享受和参与开源。