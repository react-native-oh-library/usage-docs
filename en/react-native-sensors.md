> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-sensors</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-sensors/react-native-sensors">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-sensors/react-native-sensors/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-sensors)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-sensors Releases](https://github.com/react-native-oh-library/react-native-sensors/releases).


Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-sensors@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-sensors@file:#
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

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

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
    "@react-native-oh-tpl/react-native-sensors": "file:../../node_modules/@react-native-oh-tpl/react-native-sensors/harmony/sensors.har"
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

### 3. Introducing SensorsPackage Component to ArkTS


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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-sensors Releases](https://github.com/react-native-oh-library/react-native-sensors/releases)


This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

### Permission Requirements (If Any)

Configure the required permissions in module. json 5

accelerometer Required permissions: ohos.permission.ACCELEROMETER

gyroscope Required permissions: ohos.permission.GYROSCOPE

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-sensors/react-native-sensors/blob/master/LICENSE), Please enjoy and participate freely in open source.
