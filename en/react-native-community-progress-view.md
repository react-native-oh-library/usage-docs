> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>@react-native-community/progress-view</code> </h1>
</p>

This project is based on [react-native-community/progress-view@1.4.2](https://github.com/react-native-progress-view/progress-view).

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-progress-view`, The version correspondence details are as follows:

| Version                        | Package Name                             | Repository                                                   | Release                                                      |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <= 1.4.2@deprecated | @react-native-oh-tpl/progress-view  | [Github(deprecated)](https://github.com/react-native-oh-library/progress-view) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/progress-view/releases) |
| > 1.4.2                        | @react-native-ohos/progress-view | [Gitee](https://gitee.com/openharmony-sig/rntpc_progress-view) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_progress-view/releases) |


## Installation and Usage

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/progress-view
```

#### **yarn**

```bash
yarn add @react-native-ohos/progress-view
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

## 2. Manual Link

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2 Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/progress-view": "file:../../node_modules/@react-native-ohos/progress-view/harmony/progress_view.har"
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

### 2.3 Configuring CMakeLists and Introducing ProgressViewPackage Package

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/progress-view/src/main/cpp" ./progress-view)
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

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
...
import { SampleView, SAMPLE_VIEW_TYPE, PropsDisplayer } from "rnoh-sample-package"
+ import { RNCProgressView, PROGRESS_VIEW_TYPE } from "@react-native-ohos/progress-view"

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

 > **[!TIP] Version 1.4.3 and above requires.**

Open the `entry/src/main/ets/RNPackagesFactory.ts`，file and add the following code:

```diff
  ...
+ import { ProgressViewPackage } from "@react-native-ohos/progress-view/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ProgressViewPackage(ctx), 
  ];
}
```

### 2.4 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-ohos/react-native-progress-view Releases](https://gitee.com/openharmony-sig/rntpc_progress-view/releases)

## 4. Properties

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

## 5. Known Issues

- [ ] 原库部分接口在 HarmonyOS 中没有对应属性及接口处理相关逻辑，问题: [issue#1](https://github.com/react-native-oh-library/progress-view/issues/5)

## 6. Others

## 7. License

This project is licensed under [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_progress-view/blob/master/LICENSE).
