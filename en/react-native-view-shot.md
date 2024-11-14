> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-view-shot</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gre/react-native-view-shot">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/gre/react-native-view-shot/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-view-shot)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-view-shot Releases](https://github.com/react-native-oh-library/react-native-view-shot/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-view-shot
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-view-shot
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { View, Text, Button } from "react-native";
import ViewShot, { captureRef, captureScreen } from "react-native-view-shot";

export function ViewShotDemo() {
  const view = React.useRef < View > (null);
  const ref = React.useRef(null);
  const onCapture = (res) => {
    console.info("onCapture callback");
  };
  const onCaptureFailure = (err) => {
    console.info("onCaptureFailure " + JSON.stringify(err));
  };

  return (
    <View>
      <View
        ref={view}
        collapsable={false}
        style={{ backgroundColor: "#ffffff" }}
      >
        <Text style={{ color: "#000", marginBottom: 30 }}>
          Hello OpenHarmony
        </Text>
        <Text style={{ color: "#000", marginBottom: 30 }}>Hello HarmonyOS</Text>
        <Text style={{ color: "#000", marginBottom: 30 }}>
          Hello HarmonyOS Next.
        </Text>

        <ViewShot
          ref={ref}
          style={{ backgroundColor: "#ffffff" }}
          onCapture={onCapture}
          onCaptureFailure={onCaptureFailure}
          captureMode="mount"
        >
          <Text style={{ color: "#000", marginBottom: 30 }}>Hello World</Text>
        </ViewShot>

      </View>
      <Button
        title="captureRef"
        onPress={() => {
          captureRef(view).then((res) => {
            console.info(`captureRef: ${JSON.stringify(res)}`);
          });
        }}
      />
      <Button
        title="ViewShot capture"
        onPress={() => {
          captureRef(ref).then((res) => {
            console.info(`captureRef: ${res}`);
          });
        }}
      />
      <Button
        title="captureScreen"
        onPress={() => {
          captureScreen().then((res) => {
            console.info(`captureScreen success: ${res}`);
          });
        }}
      />
    </View>
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

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-view-shot": "file:../../node_modules/@react-native-oh-tpl/react-native-view-shot/harmony/view_shot.har"
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

### 3. Configuring CMakeLists and Introducing ViewShotPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-view-shot/src/main/cpp" ./view-shot)
# RNOH_BEGIN: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_view_shot)
# RNOH_BEGIN: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ViewShotPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ViewShotPackage>(ctx)
    };
}
```

### 4.Introducing ViewShotPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { ViewShotPackage } from '@react-native-oh-tpl/react-native-view-shot/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ViewShotPackage(ctx),
  ];
}
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/view-shot Releases](https://github.com/react-native-oh-library/react-native-view-shot/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Type                                   | Required | Platform     | HarmonyOS Support |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- | -------- | ------------ | ----------------- |
| captureMode      | if not defined (default). the capture is not automatic and you need to use the ref and call `capture()` yourself<br>`"mount"`. Capture the view once at mount. (It is important to understand image loading won't be waited, in such case you want to use "none" with viewShotRef.capture() after Image#onLoad.) <br>`"continuous"` EXPERIMENTAL, this will capture A LOT of images continuously. For very specific use-cases.<br> `"update"` EXPERIMENTAL, this will capture images each time React redraw (on did update). For very specific use-cases. | ( 'mount' \| 'continuous' \| 'update') | no       | Android, iOS | yes               |
| onCapture        | when a `captureMode` is defined, this callback will be called with the capture result.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | function                               | no       | Android, iOS | yes               |
| onCaptureFailure | when a `captureMode` is defined, this callback will be called when a capture fails.                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | function                               | no       | Android, iOS | yes               |
| options | view shot configuration. | object                         | no       | Android, iOS | partially     |
| children | the actual content to rasterize. | ReactNode | no | Android, iOS | yes |

#### options属性详情

| Name                     | Description                                                  | Type                                 | Required | Platform     | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------ | -------- | ------------ | ----------------- |
| fileName                 | the file name of the file. Must be at least 3 characters long. | string                               | no       | Android, iOS | yes               |
| width / height           | the width and height of the final image (resized from the View bound. don't provide it if you want the original pixel size). | number                               | no       | Android, iOS | yes               |
| quality                  | the quality. 0.0 - 1.0 (default). (only available on lossy formats like jpg) | number                               | no       | Android, iOS | yes               |
| format                   | either png or jpg. Defaults to png.                          | string                               | no       | Android, iOS | yes               |
| result                   | the method you want to use to save the snapshot, one of:<br/>"tmpfile" (default): save to a temporary file (that will only exist for as long as the app is running).<br/>"base64": encode as base64 and returns the raw string. Use only with small images as this may result of lags (the string is sent over the bridge). N.B. This is not a data uri, use data-uri instead.<br/>"data-uri": same as base64 but also includes the Data URI scheme header. | ( 'tmpfile' \|'base64' \|'data-uri') | no       | Android, iOS | yes               |
| snapshotContentContainer | if true and when view is a ScrollView, the "content container" height will be evaluated instead of the container height. | boolean                              | no       | Android, iOS | no                |
| useRenderInContext       | change the iOS snapshot strategy to use method renderInContext instead of drawViewHierarchyInRect which may help for some use cases. | boolean                              | no       | Android, iOS | no                |

## APIs

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name             | Description | Type     | Required | Platform     | HarmonyOS Support |
| ---------------- | ----------- | -------- | -------- | ------------ | ----------------- |
| `captureRef`     | 组件截图    | function | no       | Android, iOS | yes               |
| `captureScreen`  | 屏幕截图    | function | no       | Android, iOS | yes               |
| `releaseCapture` | 资源释放    | function | no       | Android, iOS | yes               |

## Known Issues

- [x] HarmonyOS 资源释放接口验证未通过 [issues#2](https://github.com/react-native-oh-library/react-native-view-shot/issues/2)。
- [ ] 被截图组件需要设置背景色，否则截图效果全黑 [issues#3](https://github.com/react-native-oh-library/react-native-view-shot/issues/3)。
- [ ] 截图配置项 snapshotContentContainer 与 useRenderInContext 暂未实现 [issues#34](https://github.com/react-native-oh-library/react-native-view-shot/issues/34)。

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/gre/react-native-view-shot/blob/master/LICENSE).
