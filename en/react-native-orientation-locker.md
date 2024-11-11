> Template version: v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-orientation-locker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wonday/react-native-orientation-locker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wonday/react-native-orientation-locker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-orientation-locker)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-library/react-native-orientation-locker Releases](https://github.com/react-native-oh-library/react-native-orientation-locker/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-orientation-locker@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-orientation-locker@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import {
  Alert,
  Button,
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
} from "react-native";
import { useCallback, useEffect, useState } from "react";
import Orientation, {
  OrientationLocker,
  PORTRAIT,
  LANDSCAPE,
  useOrientationChange,
  useDeviceOrientationChange,
  useLockListener,
} from "react-native-orientation-locker";

export function OrientationLockerExample() {
  const [showVideo, setShowVideo] = useState(true);
  const [orientation, setOrientation] = useState<string>();
  const [isLock, setIsLock] = useState<boolean>(false);
  const updateOrientation = (orientation: string) => {
    console.info("---orientation-----22222", orientation);
    setOrientation(orientation);
  };

  const updateDeviceOrientation = (orientation: string) => {
    console.info("---updateDeviceOrientation-----1111111", orientation);
    setOrientation(orientation);
  };

  const updateLock = (orientation: string) => {
    console.info("---updateLock-----", orientation);
  };

  useEffect(() => {
    getOrientationInt();
  }, []);

  const getOrientationInt = () => {
    Orientation.getOrientation((orientation: string) => {
      updateOrientation(orientation);
      if (orientation) {
        Alert.alert(`The current screen orientation is${orientation}`);
      } else {
        Alert.alert("Failed to obtain the current screen orientation");
      }
    });
  };

  const setLockToPortrait = () => {
    Orientation.lockToPortrait();
  };
  const setLockToLandscape = () => {
    Orientation.lockToLandscape();
  };
  const setLockToLandscapeLeft = () => {
    Orientation.lockToLandscapeLeft();
  };
  const setLockToLandscapeRight = () => {
    Orientation.lockToLandscapeRight();
  };
  const unlockAllOrientations = () => {
    Orientation.unlockAllOrientations();
  };
  const lockToPortraitUpsideDown = () => {
    Orientation.lockToPortraitUpsideDown();
  };
  const lockToAllOrientationsButUpsideDown = () => {
    Orientation.lockToAllOrientationsButUpsideDown();
  };
  const addTisten = () => {
    Orientation.addDeviceOrientationListener(updateDeviceOrientation);
  };
  const cancelAddTisten = () => {
    Orientation.removeDeviceOrientationListener(updateDeviceOrientation);
  };

  return (
    <View style={styles.container}>
      <Text>{`Current Orientation----: ${orientation}`}</Text>
      <TouchableOpacity
        onPress={lockToPortraitUpsideDown}
        style={styles.button}
      >
        <Text style={styles.instructions}>Lock the up and down direction</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={lockToAllOrientationsButUpsideDown}
        style={styles.button}
      >
        <Text style={styles.instructions}>
          Lock all directions except for up and down
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToPortrait} style={styles.button}>
        <Text style={styles.instructions}>
          Lock the current screen to portrait mode
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscape} style={styles.button}>
        <Text style={styles.instructions}>
          Lock the current screen to landscape mode
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscapeLeft} style={styles.button}>
        <Text style={styles.instructions}>
          Lock the current screen to landscape and rotate it to the left
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscapeRight} style={styles.button}>
        <Text style={styles.instructions}>
          Lock the current screen to landscape and rotate it to the right
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={unlockAllOrientations} style={styles.button}>
        <Text style={styles.instructions}>
          Unlock the current screen rotation lock
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={addTisten} style={styles.button}>
        <Text style={styles.instructions}>Add monitoring</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={cancelAddTisten} style={styles.button}>
        <Text style={styles.instructions}>Cancel monitoring</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "flex-start",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
    marginTop: 20,
  },
  welcome: {
    fontSize: 20,
    textAlign: "center",
    margin: 10,
  },
  instructions: {
    textAlign: "center",
    color: "#eeeeee",
    marginBottom: 0,
  },
  buttonContainer: {
    flex: 0,
    flexDirection: "row",
    justifyContent: "space-around",
  },
  button: {
    padding: 5,
    margin: 5,
    borderWidth: 1,
    borderColor: "white",
    borderRadius: 3,
    backgroundColor: "grey",
  },
});
```

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

## Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

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
    "@react-native-oh-tpl/react-native-orientation-locker":"file:../../node_modules/@react-native-oh-tpl/react-native-orientation-locker/harmony/orientation_locker.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-orientation-locker":"file:../../node_modules/@react-native-oh-tpl/react-native-orientation-locker/harmony/orientation_locker"
  }
```

run the following instruction on the terminal:

```bash
cd entry
ohpm install --no-link
```

### 3. Introducing RNOrientationLockerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNOrientationLockerPackage } from '@react-native-oh-tpl/react-native-orientation-locker/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNOrientationLockerPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-orientation-locker Releases](https://github.com/react-native-oh-library/react-native-orientation-locker/releases)

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-orientation-locker](https://github.com/react-native-oh-library/react-native-orientation-locker)

| Name                  | Description                                                              | Type     | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| lockToPortrait        | Lock the orientation of the application to portrait (portrait)           | function | No       | IOS/Android | yes               |
| lockToLandscape       | Lock the orientation of the application to landscape (landscape)         | function | No       | IOS/Android | yes               |
| lockToLandscapeLeft   | Lock the orientation of the app to landscape and rotated to the left     | function | No       | IOS/Android | yes               |
| lockToLandscapeRight  | Lock the orientation of the app to landscape and rotated to the right    | function | No       | IOS/Android | yes               |
| unlockAllOrientations | Unlocks the orientation of the app, allowing the device to rotate freely | function | No       | IOS/Android | yes               |
| getOrientation        | Get the direction of the current device                                  | callback | No       | IOS/Android | yes               |
| getDeviceOrientation  | Obtains the direction of the current device                              | callback | No       | IOS/Android | yes               |

## Events

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-orientation-locker](https://github.com/react-native-oh-library/react-native-orientation-locker)

| Name                            | Description                                                                                                                                                                                                                                                                                                                                      | Type     | Required | Platform    | HarmonyOS Support |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| addOrientationListener          | When UI orientation changed, callback function will be called. But if lockToXXX is called , callback function will be not called untill unlockAllOrientations. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT PORTRAIT-UPSIDEDOWN UNKNOWN When lockToXXX/unlockAllOrientations, it will force resend UI orientation changed event. | callback | No       | IOS/Android | yes               |
| addDeviceOrientationListener    | When device orientation changed, callback function will be called. When lockToXXX is called, callback function also can be called. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT PORTRAIT-UPSIDEDOWN UNKNOWN                                                                                                                      | callback | No       | IOS/Android | yes               |
| removeOrientationListener       |                                                                                                                                                                                                                                                                                                                                                  | callback | No       | IOS/Android | yes               |
| removeDeviceOrientationListener |                                                                                                                                                                                                                                                                                                                                                  | callback | No       | IOS/Android | yes               |
| addLockListener                 | When call lockToXXX/unlockAllOrientations, callback function will be called. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT UNKNOWN UNKNOWN means not be locked.                                                                                                                                                                   | callback | No       | IOS/Android | yes               |
| removeLockListener              |                                                                                                                                                                                                                                                                                                                                                  | callback | No       | IOS/Android | yes               |
| removeAllListeners              |                                                                                                                                                                                                                                                                                                                                                  | callback | No       | IOS/Android | yes               |

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/wonday/react-native-orientation-locker/blob/master/LICENSE).
