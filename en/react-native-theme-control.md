> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-theme-control</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vonovak/react-native-theme-control">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vonovak/react-native-theme-control/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-theme-control)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-theme-control/Releases](https://github.com/react-native-oh-library/react-native-theme-control/releases).

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-theme-control
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-theme-control
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from 'react';
import { Text, useColorScheme, View } from 'react-native';
import {
    setThemePreference,
    SystemBars,
    ThemePreference,
    useThemePreference,
} from '@vonovak/react-native-theme-control';
// @ts-ignore
import SegmentedControl from '@react-native-segmented-control/segmented-control/js/SegmentedControl.js';

export function SimpleScreen() {
    const colorScheme = useColorScheme();
    const isDarkMode = colorScheme === 'dark';
    const themePreference = useThemePreference();
    const bgColor = isDarkMode ? '#2A2550' : '#FFF6EA';
    const textColor = isDarkMode ? 'white' : 'black';
    const barsBackground = isDarkMode ? '#9900F0' : '#A0BCC2';
    const dividerColor = textColor;
    const textColorStyle = { color: textColor };
    const values: Array<ThemePreference> = ['light', 'dark', 'system'];
    return (
        <View
    style={{
        backgroundColor: bgColor,
        flexGrow: 1,
        flexShrink: 1,
        alignItems: 'center',
        justifyContent: 'space-evenly',
    }}
>
<SystemBars
backgroundColor={barsBackground}
dividerColor={dividerColor}
/>
    <SegmentedControl
style={{ width: '100%' }}
values={values}
selectedIndex={values.indexOf(themePreference)}
onChange={({ nativeEvent }: { nativeEvent: any }) => {
    setThemePreference(nativeEvent.value as ThemePreference);
}}
/>
    <Text style={textColorStyle}>useColorScheme(): {colorScheme}</Text>
    <Text style={textColorStyle}>
useThemePreference(): {themePreference}
</Text>
    </View>
);
}
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
    "@react-native-oh-tpl/react-native-theme-control": "file:../../node_modules/@react-native-oh-tpl/react-native-theme-control/harmony/themecontrol.har",

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

### 3. Introducing RNThemeControlPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNThemeControlPackage } from '@react-native-oh-tpl/react-native-theme-control/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNThemeControlPackage(ctx)
  ];
}
```

### 4. Add the `MyAbilityStage.ets` in `entry/src/main/ets/abilityStage`

Open the `entry/src/main/ets/abilityStage/MyAbilityStage.ets` file and add the following code:

```diff
import appRecovery from '@ohos.app.ability.appRecovery';
import AbilityStage from '@ohos.app.ability.AbilityStage';
import { Want } from '@kit.AbilityKit';

export default class MyAbilityStage extends AbilityStage {
  onCreate() {
      appRecovery.enableAppRecovery(
      appRecovery.RestartFlag.ALWAYS_RESTART,
      appRecovery.SaveOccasionFlag.SAVE_WHEN_ERROR,
      appRecovery.SaveModeFlag.SAVE_WITH_FILE
    );

    let wantObj: Want = {
      bundleName: 'com.rnoh.tester',
      abilityName: 'EntryAbility'
    };

    appRecovery.setRestartWant(wantObj)
  }
}
```

### 5. Open the `entry/src/main/ets/entryability/EntryAbility.ets` file and add the following code:

Open the `entry/src/main/ets/abilityStage/MyAbilityStage.ets` file and add the following code:

```diff
+ import {RNAbility} from 'rnoh';
+ import Want from '@ohos.app.ability.Want';
+ import { RNThemeControlModule } from '@react-native-oh-tpl/react-native-theme-control';
    .....
+  export default class EntryAbility extends RNAbility {
+    onCreate(want: Want): void {
+    super.onCreate(want);
+    RNThemeControlModule.recoverApplicationTheme(this.context);
+   }
  getPagePath() {
    return 'pages/Index';
  }
}
```

Open the `entry/src/main/module.json5` file and add the following code：

```diff
"module": {
    "name": "entry",
+   "srcEntry": "./ets/abilityStage/MyAbilityStage.ets",
    "type": "entry",
    .....

"abilities": [
  {
    "name": "EntryAbility",
     .....
     "visible": true,
+    "recoverable": true,
     .....
```

### 6. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-theme-control Releases](https://github.com/react-native-oh-library/react-native-theme-control/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                                                                                                                                               | Type       | Required | Platform    | HarmonyOS Support |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | -------- | ----------- | ----------------- |
| SystemBars          | Setting the System Status Bar                                                                                                                             | Components | No       | IOS/Android | Yes               |
| NavigationBar       | Setting the Navigation Bar                                                                                                                                | Components | No       | Android     | No                |
| AppBackground       | Sets the background color of the UIApplication window (iOS) or the current Activity (Android).                                                            | Components | No       | IOS/Android | Yes               |
| setNavbarAppearance | Set the appearance of the navigation bar imperatively                                                                                                     | Function   | No       | Android     | No                |
| setAppBackground    | Set background color                                                                                                                                      | Function   | No       | IOS/Android | Yes               |
| setThemePreference  | Set the theme                                                                                                                                             | Function   | No       | IOS/Android | Yes               |
| getThemePreference  | Get Subject                                                                                                                                               | Function   | No       | IOS/Android | Yes               |
| useThemePreference  | A React hook that returns the current theme preference, which might be dark, light (if you have set the theme before by calling setAppearance) or system. | Function   | No       | IOS/Android | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/vonovak/react-native-theme-control/blob/main/LICENSE).
