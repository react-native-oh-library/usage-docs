> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-color-matrix-image-filters</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/iyegoroff/react-native-color-matrix-image-filters">
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
       <a href="https://github.com/iyegoroff/react-native-color-matrix-image-filters/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-color-matrix-image-filters)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-color-matrix-image-filters Releases](https://github.com/react-native-oh-library/react-native-color-matrix-image-filters/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-color-matrix-image-filters@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-color-matrix-image-filters@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import {
    Achromatomaly,
    Achromatopsia,
    Brightness
} from 'react-native-color-matrix-image-filters';

import { View, StyleSheet, Image } from 'react-native';

export const ColorMatrixImageFiltersTest = () => {

    return (<View>
        <Achromatomaly>
            <Image style={styles.image} source={require('./mini-parrot.jpg')} resizeMode={'stretch'} />
        </Achromatomaly>
        <Achromatopsia>
            <Image style={styles.image} source={require('./mini-parrot.jpg')} resizeMode={'stretch'} />
        </Achromatopsia>
        <Brightness>
            <Image style={styles.image} source={require('./mini-parrot.jpg')} resizeMode={'stretch'} />
        </Brightness>
    </View>)
}

const styles = StyleSheet.create({
    image: {
        width: 150,
        height: 100,
        justifyContent: 'center',
        alignItems: 'center'
    }
})
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
    "@react-native-oh-tpl/react-native-color-matrix-image-filters": "file:../../node_modules/@react-native-oh-tpl/react-native-color-matrix-image-filters/harmony/color_matrix_image_filters.har"
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

### 3. Configuring CMakeLists and Introducing ColorMatrixImageFiltersPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-color-matrix-image-filters/src/main/cpp" ./color_matrix_image_filters)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_color_matrix_image_filters )
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ColorMatrixImageFiltersPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ColorMatrixImageFiltersPackage>(ctx)
    };
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

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-color-matrix-image-filters Releases](https://github.com/react-native-oh-library/react-native-color-matrix-image-filters/releases)


## Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| matrix  | Matrix parameter transfer for image filter settings         | number[]  | yes | iOS/Android      | yes |


### Supported filters

| Component        | Additional props                                                                                                | function                                                                                                                           |
| ---------------- | --------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| ColorMatrix      | matrix: Matrix                                                                                                  | -                                                                                                                                  |
| Normal           | -                                                                                                               | normal(): Matrix                                                                                                                   |
| RGBA             | red: number = 1, green: number = 1, blue: number = 1, alpha: number = 1                                         | rgba(red: number = 1, green: number = 1, blue: number = 1, alpha: number = 1): Matrix                                              |
| Saturate         | amount: number = 1                                                                                              | saturate(amount: number = 1): Matrix                                                                                               |
| HueRotate        | amount: number = 0                                                                                              | hueRotate(amount: number = 0): Matrix                                                                                              |
| LuminanceToAlpha | -                                                                                                               | luminanceToAlpha(): Matrix                                                                                                         |
| Invert           | -                                                                                                               | invert(): Matrix                                                                                                                   |
| Grayscale        | amount: number = 1                                                                                              | grayscale(amount: number = 1): Matrix                                                                                              |
| Sepia            | amount: number = 1                                                                                              | sepia(amount: number = 1): Matrix                                                                                                  |
| Nightvision      | -                                                                                                               | nightvision(): Matrix                                                                                                              |
| Warm             | -                                                                                                               | warm(): Matrix                                                                                                                     |
| Cool             | -                                                                                                               | cool(): Matrix                                                                                                                     |
| Brightness       | amount: number = 1                                                                                              | brightness(amount: number = 1): Matrix                                                                                             |
| Contrast         | amount: number = 1                                                                                              | contrast(amount: number = 1): Matrix                                                                                               |
| Temperature      | amount: number = 1                                                                                              | temperature(amount: number = 1): Matrix                                                                                            |
| Tint             | amount: number = 0                                                                                              | tint(amount: number = 0): Matrix                                                                                                   |
| Threshold        | amount: number = 0                                                                                              | threshold(amount: number = 0): Matrix                                                                                              |
| Technicolor      | -                                                                                                               | technicolor(): Matrix                                                                                                              |
| Polaroid         | -                                                                                                               | polaroid(): Matrix                                                                                                                 |
| ToBGR            | -                                                                                                               | toBGR(): Matrix                                                                                                                    |
| Kodachrome       | -                                                                                                               | kodachrome(): Matrix                                                                                                               |
| Browni           | -                                                                                                               | browni(): Matrix                                                                                                                   |
| Vintage          | -                                                                                                               | vintage(): Matrix                                                                                                                  |
| Night            | amount: number = 0.1                                                                                            | night(amount: number = 0.1): Matrix                                                                                                |
| Predator         | amount: number = 1                                                                                              | predator(amount: number = 1): Matrix                                                                                               |
| Lsd              | -                                                                                                               | lsd(): Matrix                                                                                                                      |
| ColorTone        | desaturation: number = 0.2, toned: number = 0.15, lightColor: string = "#FFE580", darkColor: string = "#338000" | colorTone(desaturation: number = 0.2, toned: number = 0.15, lightColor: string = "#FFE580", darkColor: string = "#338000"): Matrix |
| DuoTone          | firstColor: string = "#FFE580", secondColor: string = "#338000"                                                 | duoTone(firstColor: string = "#FFE580", secondColor: string = "#338000"): Matrix                                                   |
| Protanomaly      | -                                                                                                               | protanomaly(): Matrix                                                                                                              |
| Deuteranomaly    | -                                                                                                               | deuteranomaly(): Matrix                                                                                                            |
| Tritanomaly      | -                                                                                                               | tritanomaly(): Matrix                                                                                                              |
| Protanopia       | -                                                                                                               | protanopia(): Matrix                                                                                                               |
| Deuteranopia     | -                                                                                                               | deuteranopia(): Matrix                                                                                                             |
| Tritanopia       | -                                                                                                               | tritanopia(): Matrix                                                                                                               |
| Achromatopsia    | -                                                                                                               | achromatopsia(): Matrix                                                                                                            |
| Achromatomaly    | -                                                                                                               | achromatomaly(): Matrix                          


## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-color-matrix-image-filters/blob/master/LICENSE).
