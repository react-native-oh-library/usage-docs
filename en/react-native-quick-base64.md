> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-quick-base64</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/craftzdog/react-native-quick-base64">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/craftzdog/react-native-quick-base64/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/react-native-oh-library/react-native-quick-base64)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-quick-base64 Releases](https://github.com/react-native-oh-library/react-native-quick-base64/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-quick-base64@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-quick-base64@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from 'react';
import { Text, View, TextInput, ScrollView, StyleSheet, Button } from 'react-native';
import { byteLength, btoa, atob, toByteArray, fromByteArray, getNative, trimBase64Padding, shim } from '@react-native-oh-tpl/react-native-quick-base64';

type FuncBase64ToArrayBuffer = (
  data: string,
  removeLinebreaks?: boolean
) => ArrayBuffer
type FuncBase64FromArrayBuffer = (
  data: string | ArrayBuffer,
  urlSafe?: boolean
) => string


interface NativeModule {
  base64FromArrayBuffer: FuncBase64FromArrayBuffer | undefined;
  base64ToArrayBuffer: FuncBase64ToArrayBuffer | undefined;
}

const PALETTE = {
  REACT_CYAN_LIGHT: 'hsl(193, 95%, 68%)',
  REACT_CYAN_DARK: 'hsl(193, 95%, 30%)',
};

export function QuickBase64Test() {
  // 测试字符串转base64
  const [textTobase64, onChangeTextToBase64] = useState('');

  const [base64ToTextLength, onChangeBase64TextLength] = useState(0);

  const [base64ToText, onChangeBase64Text] = useState('');

  const [byteArray, onChangeByteArray] = useState(new Uint8Array(0));

  const [byteArrayRemove, onChangeByteArrayRemove] = useState(new Uint8Array(0));

  const [fbArrayBase64Str, onChangeFbArrayBase64Str] = useState('');

  const [fbArrayBase64StrUrlSafe, onChangeFbArrayBase64StrUrlSafe] = useState('');

  const [testShimBtoA, onChangeTestShimBtoA] = useState(''); // 字符串转base64

  const [testShimAtoB, onChangeTestShimAtoB] = useState(''); // base64转字符串

  const [nativeModule, onChangeNativeModule] = useState<NativeModule>({
    base64FromArrayBuffer: undefined,
    base64ToArrayBuffer: undefined
  });

  const [nativeBFABText, onChangeNBFABText] = useState('');

  const [nativeBFABTextUrlSafe, onChangeNBFABTextUrlSafe] = useState('');

  const [nativeBTABText, onChangeNBTABText] = useState(new Uint8Array(0));

  const [nativeBTABTextRemoveLinebreaks, onChangeNBTABTextRemoveLinebreaks] = useState(new Uint8Array(0));

  const [trimBase64PaddingText, onChangeTrimBase64PaddingText] = useState('');

  const byArray = new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100, 33]);
  // 点击事件 字符串转base64
  const onPressBtoA = (text: string) => {
    let b64 = btoa(text);
    console.log(`字符串转base64 ${b64}`);
    onChangeTextToBase64(b64)
  }

  const [testText, onChangeTestText] = React.useState('');

  // 点击事件 base64转字符串
  const onPressAtoB = (text: string) => {
    let textA = atob(text);
    console.log(`base64转字符串 ${textA}`);
    onChangeBase64Text(textA)
  }

  // 打印base64转为Unit8Array字节数组的长度
  const onPressBase64Length = (text: string) => {
    console.log(`打印base64长度1 ${text}`);
    onChangeBase64TextLength(byteLength(text))
  }

  /* toByteArray 把base64字符串解码为Uint8Array */
  const onPressToByteArray = (text: string) => {
    let btArray = toByteArray(text);
    console.log(`toByteArray ${btArray}`);
    onChangeByteArray(btArray)
  }

  /* toByteArray 把base64字符串解码为Uint8Array  removeLinebreaks */
  const onPressToByteArrayRemove = (text: string, removeLinebreaks: boolean = false) => {
    let btArray = toByteArray(text, removeLinebreaks);
    console.log(`toByteArray ${btArray}`);
    onChangeByteArrayRemove(btArray)
  }

  /* fromByteArray 把Uint8Array编码为Base64字符串 */
  const onPressFromByteArray = (
    uint8: Uint8Array,
    urlSafe: boolean = false) => {
    let b64 = fromByteArray(uint8);
    console.log(`fromByteArray ${b64}`);
    onChangeFbArrayBase64Str(b64)
  }

  /* fromByteArray 把Uint8Array编码为Base64字符串  */
  const onPressFromByteArrayUrlSafe = (
    uint8: Uint8Array,
    urlSafe: boolean = false) => {
    let b64 = fromByteArray(uint8, urlSafe);
    console.log(`fromByteArray ${b64}`);
    onChangeFbArrayBase64StrUrlSafe(b64)
  }

  /* shim 给全局对象添加btoa和atob函数的shim实现 */
  const handleAddShimToGlobal = () => {
    shim();
    console.log(typeof global.btoa); // 应该输出 "function"
    console.log(typeof global.atob); // 同样应该输出 "function"
  }

  const onPressTestShimBtoA = (text: string) => {
    const encodeBase64 = global.btoa(text);
    console.log(`shim global btoa ${encodeBase64}`);
    onChangeTestShimBtoA(encodeBase64)
  }

  const onPressTestShimAtoB = (text: string) => {
    const decodeBase64 = global.atob(text);
    console.log(`shim global atob ${decodeBase64}`);
    onChangeTestShimAtoB(decodeBase64)
  }

  /* trimBase64Padding 清除Base64字符串的填充字符 */
  const onPressTrimBase64Padding = (text: string) => {
    let trimBase64 = trimBase64Padding(text);
    console.log(`shim global atob ${trimBase64}`);
    onChangeTrimBase64PaddingText(trimBase64)
  }

  /* getNative 返回包含base64FromArrayBuffer和base64ToArrayBuffer函数的对象 */
  const onPressGetNative = () => {
    const native = getNative() as NativeModule;
    onChangeNativeModule(native)
  }

  /**
   * @param text
   * base64FromArrayBuffer方法接受一个Base64编码的字符串或ArrayBuffer，
   * 以及一个可选的布尔值参数，该参数决定是否生成的Base64字符串是URL安全的。
   * 这个方法将ArrayBuffer对象转换为Base64编码的字符串。
   */
  const onPressNBFAB = (text: string | ArrayBuffer) => {
    if (nativeModule?.base64FromArrayBuffer) {
      let base64FromArrayBuffer = nativeModule.base64FromArrayBuffer(text);
      onChangeNBFABText(base64FromArrayBuffer)
    }
  }

  /**
  * @description base64转换Unit8Array 去除换行符
  * @param text
  * @param removeLinebreaks true
  *
  */
  const onPressNBFABUrlSafe = (text: string | ArrayBuffer, urlSafe: boolean = false) => {
    if (nativeModule?.base64FromArrayBuffer) {
      let base64FromArrayBuffer = nativeModule.base64FromArrayBuffer(text, urlSafe);
      onChangeNBFABTextUrlSafe(base64FromArrayBuffer)
    }
  }

  /**
   * @description base64转换Unit8Array
   * base64ToArrayBuffer方法接受一个Base64编码的字符串和一个可选的布尔值参数，
   * 该参数决定是否在转换过程中删除换行符。这个方法将Base64编码的字符串转换为ArrayBuffer对象。
   * @param text
   * @param removeLinebreaks 默认值 false
   *
   */
  const onPressNBTAB = (text: string) => {
    if (nativeModule?.base64ToArrayBuffer) {
      let base64ToArrayBuffer = new Uint8Array(nativeModule.base64ToArrayBuffer(text));
      onChangeNBTABText(base64ToArrayBuffer)
    }
  }

  /**
   * @description base64转换Unit8Array 去除换行符
   * @param text
   * @param removeLinebreaks true
   *
   */
  const onPressNBTABRemoveLinebreaks = (text: string, removeLinebreaks: boolean = false) => {
    if (nativeModule?.base64ToArrayBuffer) {
      let base64ToArrayBuffer = new Uint8Array(nativeModule.base64ToArrayBuffer(text, removeLinebreaks));
      onChangeNBTABTextRemoveLinebreaks(base64ToArrayBuffer)
    }
  }

  return (
    <ScrollView>
      <View style={styles.mainContainer}>
        <View>
          <TextInput
            style={{ height: 40, borderColor: '#978081', borderWidth: 1, width: 300, marginBottom: 20, backgroundColor: '#f5f5f5' }}
            onChangeText={(text) => onChangeTestText(text)}
            placeholder="please input test text"
            placeholderTextColor={'#674651'}
            value={testText}
          />
        </View>

        <View>BtoA Encodes a character string into a Base64 character string.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test string transform base64, testing the text: {testText}</Text>
          <Button
            title="BtoA"
            onPress={() => { onPressBtoA(testText) }}
          />
          <Text style={{ color: 'green' }}>{(textTobase64)}</Text>
        </View>

        <View>AtoB Convert base64 to character string.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test base64 transform string, testing the text: {textTobase64}</Text>
          <Button
            title="AtoB"
            onPress={() => { onPressAtoB(textTobase64) }}
          />
          <Text style={{ color: 'green' }}>{(base64ToText)}</Text>
        </View>

        <View>Decodes a base64 string into a Uint8Array.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test base64 transform Unit8Array, testing the text: {textTobase64}</Text>
          <Button
            title="onPressToByteArray"
            onPress={() => { onPressToByteArray(textTobase64) }}
          />
          <Text style={{ color: 'green' }}>{(byteArray.toString())}</Text>
        </View>



        <View>Decodes a base64 string into a Uint8Array. Whether to cancel line breaks.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test base64 transform Unit8Array add removeLinebreaks is true, testing the text: {textTobase64}</Text>
          <Button
            title="onPressToByteArrayRemove"
            onPress={() => { onPressToByteArrayRemove(textTobase64, true) }}
          />
          <Text style={{ color: 'green' }}>{(byteArrayRemove.toString())}</Text>
        </View>



        <View>Takes a base64 string and returns the length of the byte array."</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>get Unit8Array length form base64 transform, testing the text: {textTobase64}</Text>
          <Button
            title="base64ToTextLength"
            onPress={() => { onPressBase64Length(textTobase64) }}
          />
          <Text style={{ color: 'green' }}>{(base64ToTextLength)}</Text>
        </View>



        <View>Encodes a Uint8Array into a Base64 character string.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test Uint8Array transform base64 string, testing the text: {byteArray.toString()}</Text>
          <Button
            title="onPressFromByteArray"
            onPress={() => { onPressFromByteArray(byteArray) }}
          />
          <Text style={{ color: 'green' }}>{(fbArrayBase64Str)}</Text>
        </View>

        <View>Encodes a Uint8Array into a Base64 character string. The urlSafe parameter determines whether Base64 encoding uses the URL-safe variant.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test Uint8Array transform base64 string add urlSafe params, testing the text: {byteArray.toString()}</Text>
          <Button
            title="onPressFromByteArrayUrlSafe"
            onPress={() => { onPressFromByteArrayUrlSafe(byteArray) }}
          />
          <Text style={{ color: 'green' }}>{(fbArrayBase64StrUrlSafe)}</Text>
        </View>

        <View
          style={{ display: 'flex', flexDirection: 'column', backgroundColor: '#ffffff' }}>
          <Text>Add btoa and atob functions for global objects</Text>
          <Button title="shim set global" onPress={() => handleAddShimToGlobal()} />
        </View>


        {/* 测试shim 设置 btoa和atob函数 成功与否 */}
        <View>Test whether the shim sets the btoa function successfully.</View>

        <View style={{ marginTop: 20, display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test shim BtoA, testing the text: {testText}</Text>
          <Button title="test shim BtoA" onPress={() => { onPressTestShimBtoA(testText) }} />
          <Text style={{ color: 'green' }}>{testShimBtoA}</Text>
        </View>


        {/* 测试shim 设置 btoa和atob函数 成功与否 */}
        <View>Test whether the shim sets the atob function successfully.</View>

        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>test shim AtoB, testing the text: {textTobase64}</Text>
          <Button title="test shim AtoB" onPress={() => { onPressTestShimAtoB(textTobase64) }} />
          <Text style={{ color: 'green' }}>{testShimAtoB}</Text>
        </View>


        {/* trimBase64Padding 清除Base64字符串的填充字符 */}
        <View>trimBase64Padding.</View>

        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>trimBase64Padding clears the padding characters of a Base64 string, testing the text: {textTobase64}</Text>
          <Button title="test trimBase64Padding" onPress={() => { onPressTrimBase64Padding(textTobase64) }} />
          <Text style={{ color: 'green' }}>{trimBase64PaddingText}</Text>
        </View>

        <View style={{ backgroundColor: "#ffffff" }}>
          <Text>Click the button below to get native function for base64FromArrayBuffer and base64ToArrayBuffer</Text>
          <Button title="Get getNative function" onPress={() => { onPressGetNative() }} />
        </View>


        <View>Click the button below to get base64FromArrayBuffer transform text.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>base64 transform string text: {testText}</Text>
          <Button title="onPressNBFAB" onPress={() => { onPressNBFAB(testText) }} />
          <Text style={{ color: 'green' }}>{nativeBFABText}</Text>
        </View>

        <View>Click the button below to get base64FromArrayBuffer transform text, The urlSafe parameter determines whether Base64 encoding uses the URL-safe variant."</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>ArrayBuffer transform string text: {[72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100]}</Text>
          <Button title="onPressNBFABUrlSafe" onPress={() => { onPressNBFABUrlSafe(new Uint8Array([72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100]).buffer) }} />
          <Text style={{ color: 'green' }}>{nativeBFABTextUrlSafe}</Text>
        </View>

        <View>Click the button below to get base64ToArrayBuffer transform text.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>base64 transform ArrayBuffer text: {textTobase64}</Text>
          <Button title="onPressNBTAB" onPress={() => { onPressNBTAB(textTobase64) }} />
          <Text style={{ color: 'green' }}>{nativeBTABText.toString()}</Text>
        </View>

        <View>Click the button below to get base64ToArrayBuffer transform text, Remove Line Breaks.</View>
        <View style={{ display: 'flex', flexDirection: 'column', marginBottom: 10 }}>
          <Text>base64 transform ArrayBuffer text: {textTobase64}</Text>
          <Button title="onPressNBTABRemoveLinebreaks" onPress={() => { onPressNBTABRemoveLinebreaks(textTobase64) }} />
          <Text style={{ color: 'green' }}>{nativeBTABTextRemoveLinebreaks}</Text>
        </View>

      </View>
    </ScrollView>
  );
}


const styles = StyleSheet.create({
  mainContainer: {
    flex: 1,
    paddingTop: 20,
    paddingLeft: 20,
    paddingRight: 20,
    paddingBottom: 20,
    backgroundColor: '#f5f5f5',
    color: '#674651',
  },
});
```

## Use Codegen

本库未带 rc.x 的版本号是已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/en/codegen.md)。

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

    "@react-native-oh-tpl/react-native-quick-base64": "file:../../node_modules/@react-native-oh-tpl/react-native-quick-base64/harmony/rn_quick_base64.har"
 }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] or details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing GestureHandlerPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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
+ add_subdirectory("${OH_MODULE_DIR}/@react-native-oh-tpl/react-native-quick-base64/src/main/cpp" ./rn_quick_base64)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_quick_base64)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNQuickBase64Package.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNQuickBase64Package>(ctx)
    };
}
```

### 4. Introducing Gesture Handler Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import { RNQuickBase64Package } from '@react-native-oh-tpl/react-native-quick-base64/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNQuickBase64Package(ctx),
  ];
}
```

### 5. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-quick-base64 Releases](https://github.com/react-native-oh-library/react-native-quick-base64/releases)

> [!TIP] [Official Documenttation](https://github.com/craftzdog/react-native-quick-base64)

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| NAME              | Description                                                                                                                                                                                                                               | TYPE     | Required | Platform | HarmonyOS Support |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| btoa              | Encodes a string in base64.                                                                                                                                                                                                               | Function | no       | All      | yes               |
| atob              | Decodes a base64 encoded string.                                                                                                                                                                                                          | Function | no       | All      | yes               |
| toByteArray       | Takes a base64 string and returns a byte array. Optional `removeLinebreaks` removes all `\n` characters.                                                                                                                                  | Function | no       | All      | yes               |
| byteLength        | Takes a base64 string and returns length of byte array.                                                                                                                                                                                   | Function | no       | All      | yes               |
| fromByteArray     | Takes a byte array and returns a base64 string. Optional `urlSafe` flag `true` will use [the URL-safe dictionary](https://github.com/craftzdog/react-native-quick-base64/blob/9d02dfd02599ca104d2ed6c1e2d938ddd9d6cd15/cpp/base64.h#L75). | Function | no       | All      | yes               |
| shim              | Adds `btoa` and `atob` functions to `global`.                                                                                                                                                                                             | Function | no       | All      | yes               |
| trimBase64Padding | Trims the `=` padding character(s) off of the end of a base64 encoded string. Also, for base64url encoded strings, it will trim off the trailing `.` character(s).                                                                        | Function | no       | All      | yes               |
| getNative         | Obtain the native base64ToArrayBuffer and base64FromArrayBuffer functions.                                                                                                                                                                | Function | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-quick-base64/blob/sig/LICENSE).
