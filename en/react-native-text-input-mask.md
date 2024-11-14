> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-text-input-mask</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-text-input-mask/react-native-text-input-mask">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-text-input-mask/react-native-text-input-mask/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-text-input-mask)

## 安装与使用

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-text-input-mask Releases](https://github.com/react-native-oh-library/react-native-text-input-mask/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-text-input-mask
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-text-input-mask
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useState, useRef } from "react";
import { StyleSheet, Text, View, ScrollView, Button, TextInput } from "react-native";
import TextInputMask, { mask, unmask, setMask } from 'react-native-text-input-mask'
import { Colors } from "react-native/Libraries/NewAppScreen";
export const TextInputTest = () => {
    const [maskTest, maskValue] = useState('');
    const maskDemo = () => {
        mask("+1 ([000]) [000] [00] [00]", "13343469915", true).then(res => {
            maskValue(res)
        }).catch(err => {
            console.log('error', err)
        })
    }

    const [unmaskTest, unmaskValue] = useState('');
    const unmaskDemo = () => {
        unmask("+1 ([000]) [000] [00] [00]", "13343469915", true).then(res => {
            unmaskValue(res)
        }).catch(err => {
            console.log('error', err)
        })
    }
    const customNotations = [{ "character": 's', "characterSet": "$€", "isOptional": true }]
    const [onChangeTextTest_formatted, setonChangeTextValue_formatted] = useState('');
    const [onChangeTextTest_extracted, setonChangeTextValue_extracted] = useState('');
    const componentDemo = (formatted: string, extracted: string | undefined) => {
        console.log("formatted", formatted)
        setonChangeTextValue_formatted(formatted)
        console.log("extracted", extracted)
        if (extracted) {
            setonChangeTextValue_extracted(extracted)
        }
    }
    return (
        <ScrollView style={{ flex: 1 }}>
            <View style={styles.container}>
                <TextInputMask
                    rightToLeft= {true}
                    onChangeText={componentDemo}
                    affinityCalculationStrategy="CAPACITY"
                    style={styles.input}
                    autocomplete={true}
                    customNotations={customNotations}
                    mask={"[s][9999]"}
                    placeholder="Enter phone number"
                />
                <Text style={styles.input}>{onChangeTextTest_formatted}</Text>
                <Text style={styles.input}>{onChangeTextTest_extracted}</Text>
            </View>
            <View style={styles.container}>
                <Text style={styles.label}>Phone Number:</Text>
                <Button
                    title="mask"
                    onPress={maskDemo}
                />
                <Text style={styles.input}>
                    {maskTest}
                </Text>
            </View>
            <View style={styles.container}>
                <Text style={styles.label}>Phone Number:</Text>
                <Button
                    title="unmask"
                    onPress={unmaskDemo}
                />
                <Text style={styles.input}>
                    {unmaskTest}
                </Text>
            </View> 
        </ScrollView>
    );
}
const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        padding: 16,
    },
    label: {
        color: Colors.white,
        fontSize: 16,
        marginBottom: 8,
    },
    input: {
        height: 40,
        color: Colors.white,
        borderColor: '#ccc',
        borderWidth: 1,
        paddingHorizontal: 8,
    },
});

```


## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json` 添加 overrides 字段

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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
  "dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-text-input-mask": "file:../../node_modules/@react-native-oh-tpl/react-native-text-input-mask/harmony/text_input_mask.har"
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

### 3.配置 CMakeLists 和引入 RNTextInputMaskPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

 ```	diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(RNOH_CPP_DIR "${OH_MODULE_DIR}/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")

file(GLOB GENERATED_CPP_FILES "${CMAKE_CURRENT_SOURCE_DIR}/generated/*.cpp")

set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
add_compile_definitions(WITH_HITRACE_SYSTRACE)
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use

add_subdirectory("${RNOH_CPP_DIR}" ./rn)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-text-input-mask/src/main/cpp" ./RNTextInputMask)

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)


target_link_libraries(rnoh_app PUBLIC rnoh)
+ target_link_libraries(rnoh_app PUBLIC text_input_mask)
 ```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```	diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "RNTextInputMaskPackage.h"
 using namespace rnoh;

 std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
     return {std::make_shared<RNOHGeneratedPackage>(ctx),
+            std::make_shared<RNTextInputMaskPackage>(ctx)
     };
 }
```

### 4.在 ArkTs 侧引入 RNTextInputMaskPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNTextInputMaskPackage } from '@react-native-oh-tpl/react-native-text-input-mask/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+    new RNTextInputMaskPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-text-input-mask Releases](https://github.com/react-native-oh-library/react-native-text-input-mask/releases)




##  API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name    | Description            | Type     | Platform    | HarmonyOS Support |
| ------- | ---------------------- | -------- | ----------- | ----------------- |
| mask   | 字符串格式化，返回格式化后的字符串 | function | Android/iOS | yes               |
| unmask | 将格式化后的字符串还原，返回还原后的字符串 | function | Android/iOS | yes               |
| setMask | 给组件设置监听，对输入框内容进行格式化，配合TextInputMask组件使用 | function | Android/iOS | yes |
| TextInputMask | 输入框组件 | component | Android/iOS | yes |

#### mask参数说明

```js
mask(mask: string, value: string, autocomplete: boolean) : Promise<string>
```

| Name        | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| mask | 字符串格式化的格式 | string | yes      | iOS/Android | yes               |
| value | 需要格式化的字符 | string | yes   | iOS/Android | yes               |
| autocomplete | 字符自动补全 | boolean | no     | iOS/Android | yes               |

#### unmask参数说明

```json
unmask(mask: string, value: string, autocomplete: boolean) : Promise<string>
```

| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| mask         | 字符串格式化的格式 | string  | yes      | iOS/Android | yes               |
| value        | 需要还原的字符     | string  | yes      | iOS/Android | yes               |
| autocomplete | 字符自动补全       | boolean | no       | iOS/Android | yes               |

#### setMask参数说明

```
setMask (reactNode: number, primaryFormat: string, options?: MaskOptions) : void
```


| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| :-------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| reactNode | 组件id | string | yes      | iOS/Android | yes               |
| primaryFormat | 格式化的格式 | string | yes | iOS/Android | yes               |
| options | 格式化相关属性 | MaskOptions | no   | iOS/Android | yes               |

##### MaskOptions

| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| affineFormats | 备用格式 | string[] | no    | iOS/Android | yes               |
| customNotations | 自定义转义字符 | Natation[] | no      | iOS/Android | yes            |
| affinityCalculationStrategy | 亲和度计算策略 | AffinityCalculationStrategy 枚举 | no      | iOS/Android | yes               |
| autocomplete | 是否自动补全       | boolean                          | no      | iOS/Android | yes               |
| autoskip | 是否自动跳过 | boolean | no      | iOS/Android | yes               |
| rightToLeft | 是否从右到左格式化 | boolean | no      | iOS/Android | yes               |

##### Natation

| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| character | 格式字符串中的符号。 | string | yes      | iOS/Android | yes               |
| characterSet | 可接受输入字符的关联字符集。 | string | yes      | iOS/Android | yes               |
| isOptional |是可选符号还是必选符号      | boolean | yes      | iOS/Android | yes               |

##### AffinityCalculationStrategy
| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| WHOLE_STRING             | 默认的计算策略                                               | string | no       | iOS/Android | yes               |
| PREFIX                   | 查找原始文本和相同文本之间的最长公共前缀                     | string | no       | iOS/Android | yes               |
| CAPACITY                 | 亲和性是输入的长度和当前掩码可以容纳的文本总量之间的容差。   | string | no       | iOS/Android | yes               |
| EXTRACTED_VALUE_CAPACITY | 亲和性是提取值的长度与当前掩码可以容纳的总提取值长度之间的容差。 | string | no       | iOS/Android | yes               |

## 其他

## 开源协议

本项目基于[The MIT License(MIT)](https://github.com/react-native-text-input-mask/react-native-text-input-mask/blob/master/LICENSE) ，请自由地享受和参与开源。



