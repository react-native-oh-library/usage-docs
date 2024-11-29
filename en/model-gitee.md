# 文档模板(删除)

> [!ATTENTION] When using this template, delete the statements that end with "(Delete)". (Delete)

> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>原库 npm 包名</code> </h1>
</p>

This project is based on [原库 npm 名称@x.x.x](原库仓库连接)。

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-linear-gradient`, The version correspondence details are as follows:

| Version                   | Package Name                                      | Repository         | Release                    |
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |
| <= 3.0.0-0.5.0@deprecated | @react-native-oh-tpl/react-native-linear-gradient | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-linear-gradient) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-linear-gradient/releases) |
| > 3.0.0                   | @react-native-ohos/react-native-linear-gradient   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/releases) |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/库名
```

#### **yarn**

```bash
yarn add @react-native-ohos/库名
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
// react-native-safe-area-context is used as an example.
import React from "react";
import { Text, View } from "react-native";
import {
  SafeAreaProvider,
  SafeAreaView,
  initialWindowMetrics,
} from "react-native-safe-area-context";

const App = () => {
  return (
    <SafeAreaProvider initialMetrics={initialWindowMetrics}>
      <SafeAreaView style={{ flex: 1, backgroundColor: "red" }}>
        <View style={{ flex: 1 }}>
          <Text>hello</Text>
        </View>
      </SafeAreaView>
    </SafeAreaProvider>
  );
};

export default App;
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

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/Package_Name": "file:../../node_modules/@react-native-ohos/Package_Name/harmony/xxx.har"
    // NOTE: "@react-native-ohos/react-native-safe-area-context": "file:../../node_modules/@react-native-ohos/react-native-safe-area-context/harmony/safe_area.har"(Delete)
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

### 2.3 Configuring CMakeLists and Introducing xxx Package

**若涉及接入 codegen-lib 导致的配置项新增，需要在配置项前明确声明：> [!TIP] Version vx.x.x and above requires.**(Delete)

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-safe-area-context/src/main/cpp" ./safe-area)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_safe_area)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "SafeAreaViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<SafeAreaViewPackage>(ctx),
    };
}
```

### 2.4. Introducing xxx Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { SAFE_AREA_VIEW_TYPE, SafeAreaView, SAFE_AREA_PROVIDER_TYPE, SafeAreaProvider } from "@react-native-ohos/react-native-safe-area-context"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === SAFE_AREA_VIEW_TYPE) {
+   SafeAreaView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
+ RNC_VIDEO_TYPE
  ];
```

**提示：TurboModule**(Delete)

### 2.5 Introducing xxx Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {SafeAreaViewPackage} from '@react-native-ohos/react-native-safe-area-context/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new SafeAreaViewPackage(ctx)
  ];
}
```

### 2.6 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

**修改了原库代码的库使用下述描述**(Delete)

Check the release version information in the release address of the third-party library: [\<HarmonyOS npm package name> Releases](https://github.com/<repository address>/releases)

Example: [@react-native-ohos/react-native-safe-area-context Releases](https://github.com/react-native-oh-library/react-native-safe-area-context/releases) (Delete)

**未修改原库代码的库使用下述描述**(Delete)

This document is verified based on the following versions:

(Example)

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); IDE: DevEco Studio 5.0.3.906; ROM: NEXT.0.0.71;

### 3.2 Permission Requirements (If Any)

(Enter the related permission configuration.)

## 4. Properties (If Any)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| XXX  | XXX         | XXX  | (yes/no) | xxx      | (yes/no/partially) |

## 5. Static Methods (If Any)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| XXX  | XXX         | XXX  | (yes/no) | xxx      | (yes/no/partially) |

## 6. APIs (TurboModules, If Any)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| XXX  | XXX         | XXX  | (yes/no) | xxx      | (yes/no/partially) |

## 7. Known Issues

- [ ] xxx issue: [issue#\*\*\*](issue address 1)
- [ ] yyy issue: [issue#\*\*\*](issue address 2)

## 8. Others

**其他补充说明（删除）**

## 9. License

This project is licensed under [XXX License (XXX)](gitee仓库的LICENSE链接).

Example: This project is licensed under [MIT License](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/blob/master/LICENSE). (Delete)
