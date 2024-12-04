> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-sensors</code> </h1>
</p>

This project is based on [react-native-sensors@7.2.1-rc.2](https://github.com/react-native-sensors/react-native-sensors).

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-sensors`, The version correspondence details are as follows:

| Version                        | Package Name                             | Repository                                                   | Release                                                      |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <= 7.2.1-rc.2-0.0.1@deprecated | @react-native-oh-library/react-native-sensors  | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-sensors) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-sensors/releases) |
| > 7.2.1                        | @react-native-ohos/react-native-sensors | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-sensors) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-sensors/releases) |


## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-sensors
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-sensors
```

<!-- tabs:end -->

react-native-sensors is used as an example.

> [!WARNING] The name of the imported repository remains unchanged.

```js
import {
  accelerometer,
  gyroscope,
  setUpdateIntervalForType,
  magnetometer,
  barometer,
  orientation,
  gravity,
} from "react-native-sensors";

//accelerometer  accelerometer: Observable<{x: number, y: number, z: number, timestamp: string}>
accelerometer.subscribe(({ x, y, z, timestamp }) =>
  console.log("accelerometer", { x, y, z, timestamp })
);

//gyroscope  gyroscope: Observable<{x: number, y: number, z: number, timestamp: string}>
gyroscope
  .pipe(filter((speed) => speed.x > 1))
  .subscribe(({ x, y, z, timestamp }) =>
    console.log("gyroscope", { x, y, z, timestamp })
  );

//magnetometer magnetometer: Observable<{x: number, y: number, z: number, timestamp: string}>
magnetometer.subscribe(({ x, y, z, timestamp }) =>
  console.log("magnetometer", { x, y, z, timestamp })
);

//barometer barometer: Observable<{pressure: number}>
barometer.subscribe(({ pressure }) => console.log("barometer", { pressure }));

//orientation orientation: Observable<{x: number, y: number, z: number, timestamp: string}>
orientation.subscribe(({ x, y, z, timestamp }) =>
  console.log("orientation", { x, y, z, timestamp })
);

//gravity gravity: Observable<{x: number, y: number, z: number, timestamp: string}>
gravity.subscribe(({ x, y, z, timestamp }) =>
  console.log("gravity", { x, y, z, timestamp })
);
// setUpdateIntervalForType(type: string, interval: number)
setUpdateIntervalForType(SensorTypes.accelerometer, 100);
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
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-sensors": "file:../../node_modules/@react-native-ohos/react-native-sensors/harmony/sensors.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

### 2.3 Configuring CMakeLists and Introducing SensorsPackage Package

> **[!TIP] Version 7.2.2 and above requires.**

Open entry/src/main/cpp/CMakeLists.txt and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-sensors/src/main/cpp" ./sensors)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_sensors)
# RNOH_END: manual_package_linking_2
```

Open entry/src/main/cpp/PackageProvider.cpp and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "SensorsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<SensorsPackage>(ctx)
    };
}
```

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {SensorsPackage} from '@react-native-oh-tpl/react-native-sensors/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SensorsPackage(ctx)
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

Check the release version information in the release address of the third-party library:[@react-native-ohos/react-native-sensors Releases](https://gitee.com/openharmony-sig/rntpc_react-native-sensors/releases)

### 3.2 Permission Requirements (If Any)

Configure the required permissions in module. json 5

accelerometer Required permissions: ohos.permission.ACCELEROMETER

gyroscope Required permissions: ohos.permission.GYROSCOPE

## 4. API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                     | Description  | Type       | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------ | ---------- | -------- | ----------- | ----------------- |
| accelerometer            | accelerometer     | Observable | no       | ios/Android | yes               |
| gyroscope                | gyroscope       | Observable | no       | ios/Android | yes               |
| magnetometer             | magnetometer       | Observable | no       | ios/Android | yes               |
| barometer                | barometer       | Observable | no       | ios/Android | yes               |
| orientation              | orientation         | Observable | no       | ios/Android | yes               |
| gravity                  | gravity         | Observable | no       | ios/Android | yes               |
| setUpdateIntervalForType | setUpdateIntervalForType     | function   | no       | ios/Android | yes               |
| setLogLevelForType       | setLogLevelForType | function   | no       | ios/Android | yes               |

## 5. Known Issues


## 6. License

This project is licensed under [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-sensors/blob/master/LICENSE), Please enjoy and participate freely in open source.
