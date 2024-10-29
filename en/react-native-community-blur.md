> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/blur</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Kureev/react-native-blur">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Kureev/react-native-blur/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-blur)

## Installation and Usage

本库已经适配`C-API版本`从版本`4.4.0-0.1.0`开始的版本为`C-API版本`，`C-API版本`在性能和速度上都优于`ArkTS版本`。

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-community-blur Releases](https://github.com/react-native-oh-library/react-native-blur/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/blur@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/blur@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState} from 'react';
import {
  Image,
  StyleSheet,
  Platform,
  Switch,
  Text,
  View,
  SafeAreaView,
  Dimensions,
} from 'react-native';

import {
  BlurView,
  BlurViewProps,
} from '@react-native-community/blur';

export const Blurs = () => {
  const [blurBlurType, setBlurBlurType] = useState<BlurViewProps['blurType']>('dark');
  const [blurAmount, setBlurAmount] = useState<number>(100);
  useState<BlurViewProps['blurType']>('dark');
  const tintColor = blurBlurType === 'dark' ? 'white' : 'black';

  return (
    <View style={styles.container}>
      <View style={styles.blurContainer}>
        <BlurView
          blurType={blurBlurType}
          blurAmount={blurAmount}
          reducedTransparencyFallbackColor='red'
          style={[styles.blurView]}
        />
        <Text style={[styles.text, { color: tintColor }]}>
          Blur component ({Platform.OS})
        </Text>

        <View style={styles.row}>
          <Text onPress={() => {
            setBlurBlurType('light')
          }}>light</Text>

          <Text onPress={() => {
            setBlurBlurType('dark')
          }}>dark</Text>

          <Text onPress={() => {
            setBlurBlurType('chromeMaterialLight')
          }}>chromeMaterialLight click will crash</Text>
        </View>
        <View style={styles.row}>
          <Text onPress={() => {
            setBlurAmount(20)
          }}>20</Text>

          <Text onPress={() => {
            setBlurAmount(40)
          }}>40</Text>

          <Text onPress={() => {
            setBlurAmount(60)
          }}>60</Text>
          <Text onPress={() => {
            setBlurAmount(80)
          }}>80</Text>

          <Text onPress={() => {
            setBlurAmount(100)
          }}>100</Text>
        </View>
      </View>
    </View>
  );
};

export const BlurDemo = () => {
  const [showBlurs, setShowBlurs] = React.useState(false);
    //'../assets/bgimage.jpeg' 此路径的图片为本地图片，在使用demo时将此图片的路径换为自己本地图片路径
  return (
    <View style={styles.container}>
      <Image
      
        source={require('../assets/bgimage.jpeg')}
        resizeMode="cover"
        style={styles.img}
      />
      {showBlurs ? <Blurs /> : null}

      <SafeAreaView style={styles.blurToggle}>
        <Switch
          onValueChange={(value) => setShowBlurs(value)}
          value={showBlurs}
        />
      </SafeAreaView>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: 'transparent',
  },
  blurContainer: {
    flex: 1,
    backgroundColor: 'transparent',
    justifyContent: 'center',
    alignItems: 'stretch',
  },
  row: {
    marginTop: 50,
    flex: 1,
    width: '100%',
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'stretch',
  },
  blurView: {
    position: 'absolute',
    left: 0,
    right: 0,
    top: 0,
    bottom: 0,
    width: Dimensions.get('window').width,
  },

  blurView2: {
    position: 'absolute',
    left: 0,
    right: 0,
    top: 0,
    bottom: 0,
  },
  img: {
    position: 'absolute',
    left: 0,
    right: 0,
    top: 0,
    bottom: 0,
    height: Dimensions.get('window').height,
    width: Dimensions.get('window').width,
  },
  text: {
    fontSize: 20,
    fontWeight: 'bold',
    textAlign: 'center',
    margin: 10,
    color: 'white',
  },
  blurToggle: {
    position: 'absolute',
    top: 30,
    right: 10,
    alignItems: 'flex-end',
  },
});
```

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```js
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

    "@react-native-oh-tpl/blur": "file:../../node_modules/@react-native-oh-tpl/blur/harmony/blur.har"
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

### 3. Configuring CMakeLists and Introducing BlurPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/blur/src/main/cpp" ./blur)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_blur)
# RNOH_END: link_packages
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:


```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "BlurPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<BlurPackage>(ctx)
    };
}
```

### 4.Introducing BlurView Component to ArkTS (使用4.4.0-0.1.0及之后的版本忽略这步配置)

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
+ import {  BlurView, BLUR_TYPE } from "@react-native-oh-tpl/blur"

@Builder
function buildCustomRNComponent(ctx: ComponentBuilderContext) {
 ...
+  if (ctx.componentName === BLUR_TYPE) {
+   BlurView({
+     ctx: ctx.rnohContext,
+     tag: ctx.tag,
+   })
+ }
 ...
}
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ BLUR_TYPE
  ];
```

### 5.Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-community-blur Releases](https://github.com/react-native-oh-library/react-native-blur/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                | Description                                                                               | Type      | Required | Platform | HarmonyOS Support |
| ----------------------------------- | ----------------------------------------------------------------------------------------- | --------- |----------| ------- | ----------------- |
| `blurType`                          | blur type                                                                                 | enum      | yes      | iOS,Android     | yes               |
| `blurAmount?`                       | 0 - 100 (The maximum blurAmount on Android is 32, so higher values will be clamped to 32) | number    | no       | iOS,Android     | yes               |
| `reducedTransparencyFallbackColor?` | Reduce transparency fallback color                                                        | Any color | no       | iOS     | no                |
| `blurRadius?`                       | Matches iOS blurAmount                                                                    | number    | no       | Android | no                |
| `downsampleFactor?`                 | Matches iOS blurAmount                                                                    | number    | no       | Android | no                |
| `overlayColor?`                     | Default color based on iOS blurType                                                       | Any color | no       | Android | no                |

#### blurType

> [!TIP] 如果要使用自适应模糊效果需要配置深色模式[配置文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/arkts-light-dark-color-adaptation-V5#section1421172621111)如果不配置深色模式则自适应模糊效果将没有深色模式，只有浅色模式。

| Name                     | Description                                                                                            | Platform              | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------------------------------------------------ |-----------------------| ----------------- |
| `xlight`                 | extra light blur type                                                                                  | iOS,Android                   | yes                |
| `light`                  | light blur type                                                                                        | iOS,Android                   | yes               |
| `dark`                   | dark blur type                                                                                         | iOS,Android                   | yes               |
| `extraDark`              | extra dark blur type (tvOS only)                                                                       | iOS                   | yes                |
| `regular`                | regular blur type (iOS 10+ and tvOS only)                                                              | iOS  | yes               |
| `prominent`              | prominent blur type (iOS 10+ and tvOS only)                                                            | iOS  | yes                |
| `chromeMaterial`         | An adaptable blur effect that creates the appearance of a material with normal thickness               | iOS 13 only           | yes                |
| `material`               | An adaptable blur effect that creates the appearance of a material with normal thickness               | iOS 13 only           | yes                |
| `thickMaterial`          | An adaptable blur effect that creates the appearance of a material that is thicker than normal         | iOS 13 only           | yes                |
| `thinMaterial`           | An adaptable blur effect that creates the appearance of an ultra-thin material                         | iOS 13 only           | yes                |
| `ultraThinMaterial`      | An adaptable blur effect that creates the appearance of an ultra-thin material                         | iOS 13 only           | yes                |
| `chromeMaterialDark`     | A blur effect that creates the appearance of an ultra-thin material and is always dark                 | iOS 13 only           | yes                |
| `materialDark`           | A blur effect that creates the appearance of a thin material and is always dark                        | iOS 13 only           | yes                |
| `thickMaterialDark`      | A blur effect that creates the appearance of a material with normal thickness and is always dark       | iOS 13 only           | yes               |
| `thinMaterialDark`       | A blur effect that creates the appearance of a material that is thicker than normal and is always dark | iOS 13 only           | yes               |
| `ultraThinMaterialDark`  | A blur effect that creates the appearance of the system chrome and is always dark                      | iOS 13 only           | yes                |
| `chromeMaterialLight`    | An adaptable blur effect that creates the appearance of the system chrome                              | iOS 13 only           | yes                |
| `materialLight`          | An adaptable blur effect that creates the appearance of a material with normal thickness               | iOS 13 only           | yes                |
| `thickMaterialLight`     | An adaptable blur effect that creates the appearance of a thin material                                | iOS 13 only           | yes               |
| `thinMaterialLight`      | An adaptable blur effect that creates the appearance of a thin material                                | iOS 13 only           | yes               |
| `ultraThinMaterialLight` | An adaptable blur effect that creates the appearance of an ultra-thin material                         | iOS 13 only           | yes                |

## APIs

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name           | Description                                                                                | Type |Required     | Platform | HarmonyOS Support |
| -------------- | ------------------------------------------------------------------------------------------ | ----|----- |----------| ----------------- |
| `BlurView`     | Preload images to display later. e.g.                                                      | component|no | iOS,Android      | yes               |
| `VibrancyView` | The vibrancy effect lets the content underneath a blurred view show through more vibrantly | component|no | iOS      | no                |

## Known Issues

- [ ] @react-native-community/blur的 VibrancyView组件未实现HarmonyOS化 [issue#7](https://github.com/react-native-oh-library/react-native-blur/issues/7)
- [ ] @react-native-community/blur的reducedTransparencyFallbackColor属性未实现 HarmonyOS化[issue#8](https://github.com/react-native-oh-library/react-native-blur/issues/8)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/Kureev/react-native-blur/blob/master/LICENSE).
