> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-fast-image</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/DylanVann/react-native-fast-image">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-fast-image/blob/harmony/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-fast-image)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-fast-image Releases](https://github.com/react-native-oh-library/react-native-fast-image/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

>[! Warning] The reactive fast image component will enable app.setImangeCacheCount by default when running to request memory. You can use globalThis IsSetImageRawDataCacheSize is closed by assigning a value. After closing, the decoding speed will be affected when there are many pictures. You can improve the decoding speed by customizing the app. setImangeCacheCount memory application in the business logic, [Reference Connection](https://github.com/react-native-oh-library/react-native-fast-image/blob/sig/harmony/fast_image/src/main/ets/FastImagePackage.ts)。

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-fast-image
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-fast-image
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { StyleSheet, View, ScrollView } from "react-native";
import FastImage, {
  ResizeMode,
  OnLoadEvent,
  OnProgressEvent,
} from "react-native-fast-image";

export const FastImageDemo = () => {
  return (
    <ScrollView>
      <View>
        <FastImage
          style={styles.image}
          source={{
            uri: "https://res8.vmallres.com/pimages/uomcdn/CN/pms/202205/gbom/6941487259298/428_428_D7BFF22D4678EB68440F914B352214C4mp_tds.png",
          }}
          resizeMode={FastImage.resizeMode.contain}
          onLoadStart={() => {
            console.log("onLoadStart: success");
          }}
          onProgress={(e: OnProgressEvent) => {
            console.log(
              "onProgress: success loaded=" +
                e.nativeEvent.loaded +
                " total=" +
                e.nativeEvent.total
            );
          }}
          onLoad={(e: OnLoadEvent) => {
            console.log(
              "onLoad: success width=" +
                e.nativeEvent.width +
                " height=" +
                e.nativeEvent.height
            );
          }}
          onError={() => {
            console.log("onError: success");
          }}
          onLoadEnd={() => {
            console.log("onLoadEnd: success");
          }}
        />
      </View>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  image: {
    width: 200,
    height: 200,
    margin: 20,
  },
});
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

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-fast-image": "file:../../node_modules/@react-native-oh-tpl/react-native-fast-image/harmony/fast_image.har"
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

### 3. Configuring CMakeLists and Introducing FastImagePackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-fast-image/src/main/cpp" ./fast-image)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_fast_image)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "FastImagePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<FastImagePackage>(ctx),
    };
}
```

### 4. Introducing FastImagePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {FastImagePackage} from '@react-native-oh-tpl/react-native-fast-image/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new FastImagePackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-fast-image Releases](https://github.com/react-native-oh-library/react-native-fast-image/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                                                                               | Type             | Required | Platform | HarmonyOS Support |
| ------------------ | ----------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| `source.uri`       | Source for the remote image to load.                                                      | string           | yes      | All      | yes               |
| `source.headers?`  | Headers to load the image with. e.g. { Authorization: 'someAuthToken' }.                  | object           | yes      | All      | yes               |
| `source.priority?` | loading url priority                                                                      | enum             | no       | All      | no                |
| `source.cache?`    | setting loading url cache mode                                                            | enum             | no       | All      | no                |
| `defaultSource?`   | An asset loaded with require(...).                                                        | number           | yes      | All      | yes               |
| `resizeMode?`      | loading image for scale mode                                                              | enum             | yes      | All      | yes               |
| `onLoadStart`      | Called when the image starts to load.                                                     | function         | yes      | All      | yes               |
| `onProgress`       | Called when the image is loading.                                                         | function         | yes      | All      | yes               |
| `onLoad`           | Called on a successful image fetch. Called with the width and height of the loaded image. | function         | yes      | All      | yes               |
| `onError`          | Called on an image fetching error.                                                        | function         | yes      | All      | yes               |
| `onLoadEnd`        | Called when the image finishes loading, whether it was successful or an error.            | function         | yes      | All      | yes               |
| `tintColor?`       | If supplied, changes the color of all the non-transparent pixels to the given color.      | number \| string | yes      | All      | yes               |

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                         | Description                                | Type     | Required | Platform | HarmonyOS Support |
| ---------------------------- | ------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `FastImage.preload`          | Preload images to display later. e.g.      | function | no       | All      | yes               |
| `FastImage.clearMemoryCache` | Clear all images from memory cache.        | function | no       | All      | yes               |
| `FastImage.clearDiskCache`   | Clear all images from disk cache. priority | function | no       | All      | yes               |

## Known Issues

- [ ] 不支持 Properties source.cache. [issue#57](https://github.com/react-native-oh-library/react-native-fast-image/issues/57)
- [ ] 不支持 Properties source.priority. [issue#56](https://github.com/react-native-oh-library/react-native-fast-image/issues/56)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/DylanVann/react-native-fast-image/blob/main/LICENSE).

