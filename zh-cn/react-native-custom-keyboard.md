
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-custom-keyboard</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/reactnativecn/react-native-custom-keyboard">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-custom-keyboard)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-custom-keyboard Releases](https://github.com/react-native-oh-library/react-native-custom-keyboard/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-custom-keyboard
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-custom-keyboard
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';  
import {  
  StyleSheet,  
  Text,  
  View,  
  TouchableOpacity,  
} from 'react-native';  

import {  
  CustomTextInput,  
  register,  
  insertText,  
  backSpace,  
} from 'react-native-custom-keyboard';  

/**  
 * Custom Keyboard Component  
 */  
const MyKeyboard = ({ tag }) => {  
  const onPress = (value) => {  
    insertText(tag, value);  
  };  

  return (  
    <View style={styles.keyboard}>  
      {[[1, 2, 3], [4, 5, 6], [7, 8, 9]].map((row, rowIndex) => (  
        <View style={styles.row} key={`row-${rowIndex}`}>  
          {row.map((num) => (  
            <View style={styles.button} key={num}>  
              <TouchableOpacity onPress={() => onPress(num.toString())}>  
                <Text style={styles.buttonLabel}>{num}</Text>  
              </TouchableOpacity>  
            </View>  
          ))}  
        </View>  
      ))}  
      <View style={styles.row}>  
        <View style={styles.button}>  
          <TouchableOpacity onPress={() => onPress('0')}>  
            <Text style={styles.buttonLabel}>0</Text>  
          </TouchableOpacity>  
        </View>  
        <View style={styles.button}>  
          <TouchableOpacity onPress={() => onPress('.')}>  
            <Text style={styles.buttonLabel}>.</Text>  
          </TouchableOpacity>  
        </View>  
        <View style={styles.button}>  
          <TouchableOpacity onPress={() => backSpace(tag)}>  
            <Text style={styles.buttonLabel}>←</Text>  
          </TouchableOpacity>  
        </View>  
      </View>  
    </View>  
  );  
};  

register('price', () => MyKeyboard);  

/**  
 * Main Application Component  
 */  
const App = () => {  
  return (  
    <View style={styles.container}>  
      <CustomTextInput  
        customKeyboardType="price"  
        style={styles.input}  
      />  
    </View>  
  );  
};  

export default App;  

/**  
 * Style Definition  
 */  
const styles = StyleSheet.create({  
  container: {  
    flex: 1,  
    justifyContent: 'center',  
    alignItems: 'center',  
    backgroundColor: '#F5FCFF',  
  },  
  input: {  
    backgroundColor: '#ffffff',  
    borderWidth: 1,  
    borderColor: 'grey',  
    width: 270,  
    fontSize: 19,  
  },  
  keyboard: {  
    backgroundColor: 'white',  
  },  
  row: {  
    flexDirection: 'row',  
  },  
  button: {  
    width: '33.3333%',  
  },  
  buttonLabel: {  
    borderWidth: 0.5,  
    borderColor: '#d6d7da',  
    paddingVertical: 13,  
    textAlign: 'center',  
    fontSize: 20,  
  },  
});   
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
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
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-custom-keyboard": "file:../../node_modules/@react-native-oh-tpl/react-native-custom-keyboard/harmony/custom_keyboard.har"
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

### 3.配置 CMakeLists 和引入 rnoh_custom_keyboard_package

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-custom-keyboard/src/main/cpp" ./custom-keyboard)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_custom_keyboard_package)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "CustomKeyboardPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<CustomKeyboardPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 RNCustomKeyboardPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';
+import {RNCustomKeyboardPackage}  from '@react-native-oh-tpl/react-native-custom-keyboard/ts';


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new RNCustomKeyboardPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-custom-keyboard Releases](https://github.com/react-native-oh-library/react-native-custom-keyboard/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                       | Type   | Required | Platform | HarmonyOS Support |
| ------------------ | --------------------------------- | ------ | -------- | -------- | ----------------- |
| customKeyboardType | Use a registered custom keyboard. | string | no       | All      | yes               |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                 | Description                                                                                                                                                                                   | Type     | Required | Platform | HarmonyOS Support |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| register             | Register a custom keyboard type.                                                                                                                                                              | function | no       | All      | yes               |
| install              | Install custom keyboard to a TextInput.  Generally you can use CustomTextInput instead of this. But you can use this API to install/change custom keyboard dynamically.                       | function | no       | All      | yes               |
| uninstall            | Uninstall custom keyboard from a TextInput dynamically.                                                                                                                                       | function | no       | All      | yes               |
| insertText           | Use in a custom keyboard, insert text to TextInput.                                                                                                                                           | function | no       | All      | yes               |
| backSpace            | Use in a custom keyboard, delete selected text or the charactor before cursor.                                                                                                                | function | no       | All      | yes               |
| doDelete             | Use in a custom keyboard, delete selected text or the charactor after cursor.                                                                                                                 | function | no       | All      | yes               |
| moveLeft             | Use in a custom keyboard, move cursor to selection start or move cursor left.                                                                                                                 | function | no       | All      | yes               |
| moveRight            | Use in a custom keyboard, move cursor to selection end or move cursor right.                                                                                                                  | function | no       | All      | yes               |
| switchSystemKeyboard | Use in a custom keyboard. Switch to system keyboard.Next time user press or focus on the TextInput, custom keyboard will appear again. To keep using system keyboard, call uninstall instead. | function | no       | All      | yes               |

## 其他

## 遗留问题

## 开源协议

本项目基于 [The MIT License (MIT)](https://www.mit-license.org) ，请自由地享受和参与开源。
