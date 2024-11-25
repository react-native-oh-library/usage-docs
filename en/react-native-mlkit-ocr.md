> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-mlkit-ocr</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/agoldis/react-native-mlkit-ocr">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/agoldis/react-native-mlkit-ocr/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-mlkit-ocr)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-mlkit-ocr Releases](https://github.com/react-native-oh-library/react-native-mlkit-ocr/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-mlkit-ocr
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-mlkit-ocr
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from 'react';
import {
    StyleSheet,
    View,
    Button,
    SafeAreaView,
    ScrollView,
    Text,
    Dimensions,
    ActivityIndicator,
} from 'react-native';
import MlkitOcr, { MlkitOcrResult } from 'react-native-mlkit-ocr';
const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
    },
    scroll: {
        flex: 1,
        width: '100%',
        borderColor: '#ccc',
        borderWidth: 2,
    },
});
export const OcrTest = () => {
    const [loading, setLoading] = React.useState<boolean>(false);
    const [result, setResult] = React.useState<MlkitOcrResult | undefined>();

    if (loading) {
        return (
            <SafeAreaView style={styles.container}>
                <ActivityIndicator />
            </SafeAreaView>
        );
    }
    return (
        <SafeAreaView style={styles.container}>
            {Array.isArray(result) && result?.length && (
                <ScrollView
                    contentContainerStyle={{
                        alignItems: 'stretch',
                        padding: 20,
                        height: Dimensions.get('window').height,
                    }}
                    showsVerticalScrollIndicator
                    style={styles.scroll}
                >
                    {result?.map((block) => {
                        return block.lines.map((line) => {
                            return (
                                <View
                                    key={line.text}
                                    style={{
                                        backgroundColor: '#ccccccaf',
                                    }}
                                >
                                    <Text style={{ fontSize: 10 }}>{line.text}</Text>
                                </View>
                            );
                        });
                    })}
                </ScrollView>
            )}

            <Button
                title="Recognize online photos"
                onPress={() => {
                    MlkitOcr.detectFromUri('https://res.vmallres.com//uomcdn/CN/pms/202407/E3B48F7290631FAF341FDB09CF907F03.jpg').then(res => {
                        setTimeout(() => {
                            setResult(res)
                            console.log("================uri=res", JSON.stringify(res))
                        }, 1000)
                    }).catch(err => {
                        console.log("=========err", err);
                    })
                }}
            />
            <Button
                title="Recognize local photos"
                onPress={() => {
                    MlkitOcr.detectFromFile('file://docs/storage/Users/currentUser/test/1.jpg').then(res => {
                        setTimeout(() => {
                            setResult(res)
                            console.log("================file=res", JSON.stringify(res))
                        }, 1000)
                    }).catch(err => {
                        console.log("=========err", err);
                    })
                }}
            />
        </SafeAreaView>
    );
}
```

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

### 2.Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-mlkit-ocr": "file:../../node_modules/@react-native-oh-tpl/react-native-mlkit-ocr/harmony/rn_mlkit_ocr.har"
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

### 3. Configuring CMakeLists and Introducing RNMlkitOcrPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/@react-native-oh-tpl/react-native-mlkit-ocr/src/main/cpp" ./rn_mlkit_ocr)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_mlkit_ocr)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNMlkitOcrPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNMlkitOcrPackage>(ctx)
    };
}
```

### 4. Introducing RNMlkitOcrPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import { RNMlkitOcrPackage } from '@react-native-oh-tpl/react-native-mlkit-ocr/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNMlkitOcrPackage(ctx),
  ];
}
```

### 5. Permission Requirements

> [!TIP] "ohos.permission.INTERNET"权限等级为<B>normal</B>，授权方式为<B>system_grant</B>，[使用 ACL 签名的配置指导](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/signing-0000001587684945-V3#section157591551175916)

Add configuration to `YourProject/entry/src/main/module.json5`

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

    "requestPermissions": [
+    {
+        "name": "ohos.permission.INTERNET",
+     },
    ]
  }
}
```

### 6. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-mlkit-ocr Releases](https://github.com/react-native-oh-library/react-native-mlkit-ocr/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| NAME                 | Description      | TYPE     | Required | Platform | HarmonyOS Support |
| -------------------- | ---------------- | -------- | -------- | -------- | ----------------- |
| detectFromUri(uri)   | 传入网络图片地址 | Function | Yes      | All      | Yes               |
| detectFromFile(path) | 传入本地图片地址 | Function | Yes      | All      | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/agoldis/react-native-mlkit-ocr/blob/main/LICENSE).
