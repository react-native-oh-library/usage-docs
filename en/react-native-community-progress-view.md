> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/progress-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-progress-view/progress-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20macos%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-progress-view/progress-view/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/progress-view)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/progress-view Releases](https://github.com/react-native-oh-library/progress-view/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/progress-view
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/progress-view
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { ProgressView } from "@react-native-community/progress-view";

export default function ProgressViewExample() {
  return (
    <ProgressView
      progressTintColor="orange"
      trackTintColor="blue"
      progress={0.7}
    />
  )
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
    "@react-native-oh-tpl/progress-view": "file:../../node_modules/@react-native-oh-tpl/progress-view/harmony/progress_view.har"
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

### 3. Configuring CMakeLists and Introducing ProgressViewPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/progress-view/src/main/cpp" ./progress-view)
# RNOH_BEGIN: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_progress_view)
# RNOH_BEGIN: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ProgressViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ProgressViewPackage>(ctx)
    };
}
```

### 4. Introducing ProgressViewPackage Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
...
import { SampleView, SAMPLE_VIEW_TYPE, PropsDisplayer } from "rnoh-sample-package"
+ import { RNCProgressView, PROGRESS_VIEW_TYPE } from "@react-native-oh-tpl/progress-view"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...  
+ if (ctx.componentName === PROGRESS_VIEW_TYPE) {
+   RNCProgressView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ PROGRESS_VIEW_TYPE
  ];
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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/progress-view Releases](https://github.com/react-native-oh-library/progress-view/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                                | Type   | Required | Platform | HarmonyOS Support |
| ------------------- | ------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `progress`          | The progress value (between 0 and 1).      | number | No       | All      | Yes               |
| `progressTintColor` | The tint color of the progress bar itself. | string | No       | All      | Yes               |
| `trackTintColor`    | The tint color of the progress bar track.  | string | No       | All      | Yes               |
| `progressImage`     | A stretchable image to display as the progress bar.      | Image.propTypes.source | No       | All      | No               |
| `trackImage` | A stretchable image to display behind the progress bar. Network images only work on Windows.| Image.propTypes.source | No       | All      | No               |
| `progressViewStyle`    | The progress bar style. Network images only work on Windows.  | enum('default', 'bar') | No       | All      | No               |
| `isIndeterminate`    | Turns progress bar into an indeterminate progress bar.  | bool | No       | Windows      | Partially               |

## Known Issues

- [ ] 原库部分接口在 HarmonyOS 中没有对应属性及接口处理相关逻辑，问题: [issue#1](https://github.com/react-native-oh-library/progress-view/issues/5)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/progress-view/blob/harmony/LICENSE).
