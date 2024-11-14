> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@klarna/platform-colors</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/klarna-incubator/platform-colors">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/klarna-incubator/platform-colors/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/platform-colors)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/platform-colors Releases](https://github.com/react-native-oh-library/platform-colors/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/platform-colors
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/platform-colors
```

Generate resource files:

```bash
npx @react-native-oh-tpl/platform-colors
```

> [!TIP] The first time you run the command it will prompt you which platforms you want to generate files for which will create a file with the following format:

```js
// platform-colors.config.js
module.exports = {
  prefix: "rnpc_",
  colors: {
    background: {
      light: "#000000",
      dark: "#ffffff",
    },
    text: "#696969",
    accent: "pink",
    contrasted: "#FFF0F5",
  },
  javascript: {
    typescript: true,
    outputDirectory: "src/colors/",
  },
  ios: {
    outputDirectory: "ios/app_name/Images.xcassets/",
  },
  android: {
    outputDirectory: "android/app/src/main/res/",
  },
  harmony: {
    outputDirectory: "harmony/AppScope/resources/",
  },
};
```

Now go ahead and inspect your android, ios and web folders. You should have your color definitions on each platform.

You need to re-run the command after each change to the config to update the generated files.

```bash
npx @react-native-oh-tpl/platform-colors
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```ts
import React from "react";
import {
  View,
  Text,
  StyleSheet,
  ScrollView,
  Image,
  ColorValue,
} from "react-native";
import { resolveColor, resolveColorSync } from "@klarna/platform-colors";
import { PlatformColor } from "react-native";

const accent = PlatformColor("rnpc_accent");

export const PlatformColorsTest = () => {
  const [asyncColor, setAsyncColor] = React.useState<ColorValue | undefined>(
    undefined
  );
  const syncColor = resolveColorSync(accent);
  React.useEffect(() => {
    resolveColor(accent).then((color) => setAsyncColor(color));
  }, []);

  return (
    <View style={{ top: 48, flex: 1 }}>
      <ScrollView
        contentInsetAdjustmentBehavior="automatic"
        style={styles.scrollView}
      >
        <ColorRow
          label="show color of id: rnpc_background"
          color={PlatformColor("rnpc_background")}
        />
        <ColorRow
          label="get 'ohos_id_color_warning' color by resolveColor api"
          color={asyncColor}
        />
        <ColorRow
          label="get 'ohos_id_color_warning' color by resolveColorSync api"
          color={syncColor}
        />
      </ScrollView>
    </View>
  );
};
const ColorRow = ({ label, color }: { label: string; color?: ColorValue }) => (
  <View style={styles.colorRow}>
    <View
      style={[
        styles.colorSample,
        {
          backgroundColor: color,
        },
      ]}
    />
    <Text style={styles.colorLabel}>{label}</Text>
  </View>
);
const styles = StyleSheet.create({
  scrollView: {
    flex: 1,
    paddingHorizontal: 10,
  },
  colorRow: {
    paddingHorizontal: 10,
    marginVertical: 10,
    flexDirection: "row",
    alignItems: "center",
  },
  colorSample: {
    width: 50,
    height: 50,
    borderRadius: 25,
    marginRight: 10,
    shadowOpacity: 0.2,
    shadowColor: "#999",
    shadowRadius: 1,
    shadowOffset: { width: 0, height: 0 },
  },
});
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

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
    "@react-native-oh-tpl/platform-colors": "file:../../node_modules/@react-native-oh-tpl/platform-colors/harmony/platform_colors.har"
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

### 3. Introducing RNPlatformColorsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNPlatformColorsPackage } from '@react-native-oh-tpl/platform-colors/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNPlatformColorsPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/platform-colors Releases](https://github.com/react-native-oh-library/platform-colors/releases)

## Properties

### platform-colors.config.js configuration files Properties

> details [@klarna/platform-colors documentation](https://github.com/klarna-incubator/platform-colors)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name       | Description                                                                                                                                                                           | Type   | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| prefix     | We prefix all colors with rnpc\_ by default, you can override that with this option.                                                                                                  | String | No       | iOS/Android | Yes               |
| colors     | An object where the key is the color name, and the value is either a string or an object containing light and optionally highContrastLight, dark & highContrastDark properties.       | Object | Yes      | iOS/Android | Yes               |
| ios        | An object containing outputDirectory which should be an .xcassets directory.                                                                                                          | Object | No       | iOS/Android | Yes               |
| android    | An object containing outputDirectory which should be an Android res directory.                                                                                                        | Object | No       | iOS/Android | Yes               |
| harmony    | An object containing outputDirectory which should be an Harmony res directory.                                                                                                        | Object | No       | --          | Yes               |
| css        | An object containing outputDirectory and filename which should be a directory where you store CSS files and if you want to change the default filename from colors.css.               | Object | No       | iOS/Android | Yes               |
| javascript | An object containing outputDirectory which should be a directory where you store your Type/JavaScript files and typescript which is set to true if you want the output in TypeScript. | Object | No       | iOS/Android | Yes               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name             | Description                          | Type     | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------ | -------- | -------- | ----------- | ----------------- |
| resolveColorSync | Getting hex value from dynamic color | Function | No       | iOS/Android | Yes               |
| resolveColor     | Getting hex value from dynamic color | Function | No       | iOS/Android | Yes               |

### resolveColorSync

```js
resolveColorSync(color: ColorValue): string;
```

| Name  | Description                                                                                                        | Type             | Required | Platform    | HarmonyOS Support |
| ----- | ------------------------------------------------------------------------------------------------------------------ | ---------------- | -------- | ----------- | ----------------- |
| color | Color value obtained through the PlatformColor interface.<br>Example: resolveColorSync(PlatformColor('coloeName')) | React.ColorValue | Yes      | iOS/Android | Yes               |

### resolveColor

```js
resolveColor(color: ColorValue): Promise<string>;
```

| Name  | Description                                                                                                    | Type             | Required | Platform    | HarmonyOS Support |
| ----- | -------------------------------------------------------------------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| color | Color value obtained through the PlatformColor interface.<br>Example: resolveColor(PlatformColor('coloeName')) | React.ColorValue | Yes      | iOS/Android | Yes               |

## Known Issues

## Others

## License

This project is licensed under [Apache License 2.0](https://github.com/klarna-incubator/platform-colors/blob/master/LICENSE).
