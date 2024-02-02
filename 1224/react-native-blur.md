> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-blur</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Kureev/react-native-blur">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-blur/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-blur)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-blur Releases](https://github.com/react-native-oh-library/react-native-blur/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

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

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

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

const Blurs = () => {
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

export default const BlurDemo = () => {
  const [showBlurs, setShowBlurs] = React.useState(true);
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
    "rnoh": "file:../rnoh",
    "rnoh-blur": "file:../../node_modules/@react-native-oh-tpl/blur/harmony/blur.har"
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
    "rnoh-blur": "file:../../node_modules/@react-native-oh-tpl/blur/harmony/blur"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 BlurPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-blur/src/main/cpp" ./blur)
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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 在 ArkTs 侧引入 BlurView 组件

打开 `entry/src/main/ets/pages/index.ets`，添加：

```diff
...
+ import {  BlurView, BLUR_TYPE } from "rnoh-blur"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.componentName === BLUR_TYPE) {
+   BlurView({
+     ctx: ctx.rnohContext,
+     tag: ctx.tag,
+     buildCustomComponent: CustomComponentBuilder
+   })
+ }
 ...
}
...

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl Releases](https://github.com/react-native-oh-library/react-native-blur/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                           | Description                                                                               | Type             | Required | Platform | HarmonyOS Support |
| ------------------------------ | ----------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| `blurType`                   | blur type                                                      | enum            | yes      | All      | yes               |
| `blurAmount?`              | 0 - 100 (The maximum blurAmount on Android is 32, so higher values will be clamped to 32)                  | number           | No      | All      | yes               |
| `reducedTransparencyFallbackColor?`             | Reduce transparency fallback color                                                                      | Any color             | No       | iOS only      | no                |
| `blurRadius?`                | Matches iOS blurAmount                                                            | number             | No       | Android only      | no                |
| `downsampleFactor?`               | Matches iOS blurAmount                                                        | number           | No      | Android only      | no               |
| `overlayColor?`                  | Default color based on iOS blurType                                                              | Any color             | No      | Android only      | no

#### blurType

> [!tip] "Platform"列表示该组件在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该组件；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                           | Description                                                                                          | Platform | HarmonyOS Support |
| ------------------------------ | ----------------------------------------------------------------------------------------- |  -------- | ----------------- |
| `xlight`|extra light blur type| All| no 
| `light`|light blur type| All| yes 
| `dark`|dark blur type| All| yes 
| `extraDark`|extra dark blur type (tvOS only)| tvOS only| no
| `regular`|regular blur type (iOS 10+ and tvOS only)| iOS 10+ and tvOS only| yes
| `prominent`|prominent blur type (iOS 10+ and tvOS only)| iOS 10+ and tvOS only| no
| `chromeMaterial`|An adaptable blur effect that creates the appearance of a material with normal thickness| iOS 13 only| no
| `material`|An adaptable blur effect that creates the appearance of a material with normal thickness| iOS 13 only| no
| `thickMaterial`|An adaptable blur effect that creates the appearance of a material that is thicker than normal| iOS 13 only| no
| `thinMaterial`|An adaptable blur effect that creates the appearance of an ultra-thin material|  iOS 13 only| no
| `ultraThinMaterial`|An adaptable blur effect that creates the appearance of an ultra-thin material|  iOS 13 only| no
| `chromeMaterialDark`|A blur effect that creates the appearance of an ultra-thin material and is always dark|  iOS 13 only| no
| `materialDark`|A blur effect that creates the appearance of a thin material and is always dark|  iOS 13 only| no
| `thickMaterialDark`|A blur effect that creates the appearance of a material with normal thickness and is always dark|  iOS 13 only| yes
| `thinMaterialDark`|A blur effect that creates the appearance of a material that is thicker than normal and is always dark| iOS 13 only| yes
| `ultraThinMaterialDark`|A blur effect that creates the appearance of the system chrome and is always dark| i iOS 13 only| no
| `chromeMaterialLight`|An adaptable blur effect that creates the appearance of the system chrome|  iOS 13 only| no
| `materialLight`|An adaptable blur effect that creates the appearance of a material with normal thickness|  iOS 13 only| no
| `thickMaterialLight`|An adaptable blur effect that creates the appearance of a thin material|  iOS 13 only| yes
| `thinMaterialLight`|An adaptable blur effect that creates the appearance of a thin material|  iOS 13 only| yes
| `ultraThinMaterialLight`|An adaptable blur effect that creates the appearance of an ultra-thin material|  iOS 13 only| no

## 组件

> [!tip] "Platform"列表示该组件在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该组件；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name| Description| Type  | Platform | HarmonyOS Support |
|------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `BlurView`           | Preload images to display later. e.g.      | component       | All                | yes
| `VibrancyView`   | The vibrancy effect lets the content underneath a blurred view show through more vibrantly | component | IOS      | no

## 遗留问题

- [ ] blurTypes设置为ios/android平台定义枚举值，闪退[issue#755](https://gl.swmansion.com/rnoh/react-native-harmony/-/issues/755)
- [ ] harmony 暂不支持VibrancyView组件

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/Kureev/react-native-blur/blob/master/LICENSE) ，请自由地享受和参与开源。
