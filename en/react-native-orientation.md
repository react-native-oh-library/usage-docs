> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-orientation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/yamill/react-native-orientation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-orientation/blob/sig/LICENSE.md">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-orientation)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-library/react-native-orientation Releases](https://github.com/react-native-oh-library/react-native-orientation/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-orientation
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-orientation
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import Orientation from "react-native-orientation";
import { Alert, StyleSheet, Text, TouchableOpacity, View } from "react-native";
import { useEffect, useState } from "react";

export default function OrientationDemo() {
  const [orientation, setOrientation] = useState<string>();
  const [SpecificOrientation, setSpecificOrientation] = useState<string>();
  const updateOrientation = (orientation: string) => {
    console.info("orientation", orientation);
    setOrientation(orientation);
  };
  const UpdateSpecificOrientation = (SpecificOrientation: string) => {
    console.info("SpecificOrientation", SpecificOrientation);
    setSpecificOrientation(SpecificOrientation);
  };
  useEffect(() => {
    Orientation.addOrientationListener(updateOrientation);
    Orientation.addSpecificOrientationListener(UpdateSpecificOrientation);
    return () => {
      Orientation.removeOrientationListener(updateOrientation);
      Orientation.removeSpecificOrientationListener(UpdateSpecificOrientation);
    };
  }, []);
  const getOrientationInt = () => {
    Orientation.getOrientation((err: string, orientation: string) => {
      if (orientation) {
        Alert.alert(`The current screen orientation is${orientation}`);
      } else {
        Alert.alert(err);
      }
    });
  };
  const getSpecificOrientationInt = () => {
    Orientation.getSpecificOrientation((err: string, orientation: string) => {
      if (orientation) {
        Alert.alert(`The current screen orientation is${orientation}`);
      } else {
        Alert.alert(err);
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
  return (
    <View style={styles.container}>
      <Text>{`Current Orientation: ${orientation}`}</Text>
      <Text>{`Current SpecificOrientation: ${SpecificOrientation}`}</Text>
      <TouchableOpacity onPress={getOrientationInt} style={styles.button}>
        <Text style={styles.instructions}>
          Get the current screen orientation
        </Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={getSpecificOrientationInt}
        style={styles.button}
      >
        <Text style={styles.instructions}>
          Get the specific direction of the current screen
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

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

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
    "@react-native-oh-tpl/rnoh-orientation": "file:../../node_modules/@react-native-oh-tpl/react-native-orientation/harmony/rn_orientation.har"
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

run the following instruction on the terminal:

```bash
cd entry
ohpm install --no-link
```

### 3. Introducing RNOrientationPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNOrientationPackage } from '@react-native-oh-tpl/rnoh-orientation/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNOrientationPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-orientation Releases](https://github.com/react-native-oh-library/react-native-orientation/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-orientation](https://github.com/react-native-oh-library/react-native-orientation)

| Name                   | Description                                                              | Type     | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| lockToPortrait         | Lock the orientation of the application to portrait (portrait)           | function | No       | IOS/Android | yes               |
| lockToLandscape        | Lock the orientation of the application to landscape (landscape)         | function | No       | IOS/Android | yes               |
| lockToLandscapeLeft    | Lock the orientation of the app to landscape and rotated to the left     | function | No       | IOS/Android | yes               |
| lockToLandscapeRight   | Lock the orientation of the app to landscape and rotated to the right    | function | No       | IOS/Android | yes               |
| unlockAllOrientations  | Unlocks the orientation of the app, allowing the device to rotate freely | function | No       | IOS/Android | yes               |
| getOrientation         | Get the direction of the current device                                  | callback | No       | IOS/Android | yes               |
| getSpecificOrientation | Obtains the direction of the current device                              | callback | No       | IOS/Android | yes               |

## Events

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-orientation](https://github.com/react-native-oh-library/react-native-orientation)

| Name                              | Description                                       | Type     | Required | Platform    | HarmonyOS Support |
| --------------------------------- | ------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| addOrientationListener            | Enable monitoring of screen orientation changes   | callback | No       | IOS/Android | yes               |
| addSpecificOrientationListener    | Start to monitor the change of screen orientation | callback | No       | IOS/Android | yes               |
| removeOrientationListener         | Remove Listen Screen Orientation Change           | callback | No       | IOS/Android | yes               |
| removeSpecificOrientationListener | Remove Monitor Screen Specific Orientation Change | callback | No       | IOS/Android | yes               |

## Others

## License

This project is licensed under [ISC License](https://github.com/react-native-oh-library/react-native-orientation/blob/master/LICENSE).
