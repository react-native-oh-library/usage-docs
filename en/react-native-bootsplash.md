> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-bootsplash</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/zoontek/react-native-bootsplash">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/zoontek/react-native-bootsplash/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-bootsplash)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-bootsplash Releases](https://github.com/react-native-oh-library/react-native-bootsplash/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-bootsplash
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-bootsplash
```

#### 生成配置文件

为了加快设置速度，我们提供了一个 CLI 来自动生成配置、创建 Android Drawable XML 文件、iOS Storyboard 文件和 HarmonyOS Resources 文件

```bash
$ npx react-native generate-bootsplash --help
# --- or ---
$ yarn react-native generate-bootsplash --help
```

该命令可以使用多个参数:

```js
Usage: react-native generate-bootsplash [options] <logo>

Generate a launch screen using a logo file path (PNG or SVG)

Options:
  --project-type <string>     Project type ("detect", "bare" or "expo") (default: "detect")
  --platforms <list>          Platforms to generate for, separated by a comma (default: "android,ios,web,harmony")
  --background <string>       Background color (in hexadecimal format) (default: "#fff")
  --logo-width <number>       Logo width at @1x (in dp - we recommend approximately ~100) (default: 100)
  --assets-output <string>    Assets output directory path (default: "assets/bootsplash")
  --flavor <string>           Android flavor build variant (where your resource directory is) (default: "main")
  --html <string>             HTML template file path (your web app entry point) (default: "public/index.html")
  --license-key <string>      License key to enable brand and dark mode assets generation
  --brand <string>            Brand file path (PNG or SVG)
  --brand-width <number>      Brand width at @1x (in dp - we recommend approximately ~80) (default: 80)
  --dark-background <string>  [dark mode] Background color (in hexadecimal format)
  --dark-logo <string>        [dark mode] Logo file path (PNG or SVG)
  --dark-brand <string>       [dark mode] Brand file path (PNG or SVG)
  -h, --help                  display help for command
```

命令用法示例:

```bash
# Without license key
npx react-native generate-bootsplash svgs/light-logo.svg
```

命令执行后将创建以下文件:

```js
# Without license key
android/app/src/main/res/drawable-mdpi/bootsplash_logo.png
android/app/src/main/res/drawable-hdpi/bootsplash_logo.png
android/app/src/main/res/drawable-xhdpi/bootsplash_logo.png
android/app/src/main/res/drawable-xxhdpi/bootsplash_logo.png
android/app/src/main/res/drawable-xxxhdpi/bootsplash_logo.png
android/app/src/main/AndroidManifest.xml
android/app/src/main/res/values/colors.xml
android/app/src/main/res/values/styles.xml

ios/YourApp/BootSplash.storyboard
ios/YourApp/Colors.xcassets/BootSplashBackground-<hash>.colorset/Contents.json
ios/YourApp/Images.xcassets/BootSplashLogo-<hash>.imageset/Contents.json
ios/YourApp/Images.xcassets/BootSplashLogo-<hash>.imageset/logo-<hash>.png
ios/YourApp/Images.xcassets/BootSplashLogo-<hash>.imageset/logo-<hash>@2x.png
ios/YourApp/Images.xcassets/BootSplashLogo-<hash>.imageset/logo-<hash>@3x.png
ios/YourApp/Info.plist
ios/YourApp.xcodeproj/project.pbxproj

harmony/entry/src/main/resources/base/media/bootsplash_logo.png
harmony/entry/src/main/resources/base/element/color.json
harmony/entry/src/main/module.json5

public/index.html

assets/bootsplash/manifest.json
assets/bootsplash/logo.png
assets/bootsplash/logo@1,5x.png
assets/bootsplash/logo@2x.png
assets/bootsplash/logo@3x.png
assets/bootsplash/logo@4x.png
```

编辑您的启动 Ability 文件, 它通常是配置在 entry 模块 module.json5 中 abilities 属性中配置的第一个 abilitie:

```diff
+ import { window } from '@kit.ArkUI';
+ import { RNBootSplashScreen } from '@react-native-oh-tpl/react-native-bootsplash/src/main/ets/RNBootSplashScreen';

export default class EntryAbility extends RNAbility {
+  onWindowStageCreate(windowStage: window.WindowStage) {
+     RNBootSplashScreen.init(this.context, windowStage).then(() => {
+       super.onWindowStageCreate(windowStage);
+     })
+  }

  ...
}
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

> [!TIP] 示例中 logo 参数使用了本地图片资源，可以到[react-native-boot-splash demo](https://github.com/react-native-oh-library/RNOHDCS/tree/main/react-native-boot-splash/source)获取该图片

```js
import { useState, useEffect } from "react";
import {
  Animated,
  View,
  Text,
  Dimensions,
  Platform,
  StatusBar,
  StyleSheet,
} from "react-native";
import BootSplash from "react-native-bootsplash";

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
  },
  text: {
    fontSize: 30,
    fontWeight: "700",
    margin: 20,
    lineHeight: 30,
    color: "#333",
    textAlign: "center",
  },
});

type Props = {
  onAnimationEnd: () => void,
};

export const AnimatedBootSplash = ({ onAnimationEnd }: Props) => {
  const [opacity] = useState(() => new Animated.Value(1));
  const [translateY] = useState(() => new Animated.Value(0));

  const { container, logo /*, brand */ } = BootSplash.useHideAnimation({
    manifest: require("../source/bootsplash_manifest.json"),
    logo: require("../source/bootsplash_logo.png"),
    statusBarTranslucent: true,
    navigationBarTranslucent: false,

    animate: () => {
      const { height } = Dimensions.get("window");
      Animated.stagger(250, [
        Animated.spring(translateY, {
          useNativeDriver: true,
          toValue: -50,
        }),
        Animated.spring(translateY, {
          useNativeDriver: true,
          toValue: height,
        }),
      ]).start();
      Animated.timing(opacity, {
        useNativeDriver: true,
        toValue: 0,
        duration: 150,
        delay: 350,
      }).start(() => {
        onAnimationEnd();
      });
    },
  });

  return (
    <Animated.View {...container} style={[container.style, { opacity }]}>
      <Animated.Image
        {...logo}
        style={[logo.style, { transform: [{ translateY }] }]}
      />
    </Animated.View>
  );
};

const App = () => {
  const [visible, setVisible] = useState(true);

  useEffect(() => {
    StatusBar.setBarStyle("dark-content");
  }, []);

  return (
    <>
      <View style={styles.container}>
        <Text style={styles.text}>Hello World</Text>
        {visible && (
          <AnimatedBootSplash
            onAnimationEnd={() => {
              BootSplash.isVisible();
              console.log("--------++++AnimationEnd");
              setVisible(false);
            }}
          />
        )}
      </View>
    </>
  );
};

export default App;
```

```json
// bootsplash_manifest.json
{
  "background": "#F5FCFF",
  "logo": {
    "width": 300,
    "height": 89
  }
}
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
    "@react-native-oh-tpl/react-native-bootsplash": "file:../../node_modules/@react-native-oh-tpl/react-native-bootsplash/harmony/boot_splash.har"
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

### 3. Introducing RNBootSplashPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNBootSplashPackage } from '@react-native-oh-tpl/react-native-bootsplash/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNBootSplashPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-bootsplash Releases](https://github.com/react-native-oh-library/react-native-bootsplash/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name             | Description                                                                                                                                                                                  | Type     | Required | Platform     | HarmonyOS Support |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ------------ | ----------------- |
| hide             | Hide the splash screen.                                                                                                                                                                      | function | no       | Android、IOS | yes               |
| isVisible        | Return the current visibility status of the native splash screen.                                                                                                                            | function | no       | Android、IOS | yes               |
| useHideAnimation | A hook to easily create a custom hide animation by animating all splash screen elements using Animated, react-native-reanimated or else (similar as the video on top of this documentation). | function | no       | Android、IOS | yes               |

### hide

```js
type hide = (config?: { fade?: boolean }) => Promise<void>;
```

| Name | Description                                               | Type    | Required | Platform    | HarmonyOS Support |
| ---- | --------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| fade | Hide the splash screen (immediately, or with a fade out). | boolean | No       | iOS/Android | partially         |

### useHideAnimation

```js
useHideAnimation(config: {UseHideAnimationConfig}) => {container: ContainerProps;logo: LogoProps;brand: BrandProps;};
```

| Name                     | Description                                                   | Type               | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------- | ------------------ | -------- | ----------- | ----------------- |
| ready                    | a boolean flag to delay the animate execution (default: true) | boolean            | No       | iOS/Android | partially         |
| manifest                 | the manifest file is generated in your assets directory       | Manifest           | Yes      | iOS/Android | partially         |
| logo                     | logo image in animation                                       | ImageRequireSource | No       | iOS/Android | partially         |
| darkLogo                 | logo image in animation in dark mode                          | ImageRequireSource | No       | iOS/Android | partially         |
| brand                    | brand image in animation                                      | ImageRequireSource | No       | iOS/Android | partially         |
| darkBrand                | brand image in animation in dark mode                         | ImageRequireSource | No       | iOS/Android | partially         |
| statusBarTranslucent     | sets whether the status bar is transparent                    | boolean            | No       | iOS/Android | partially         |
| navigationBarTranslucent | sets whether the navigation bar is transparent                | boolean            | No       | iOS/Android | partially         |
| animate                  | custom hide animation                                         | function           | Yes      | iOS/Android | partially         |

## Known Issues

- [ ] HarmonyOS 的 window 窗口上不支持设置动画属性，hide 接口 fade 参数设置 true 没有效果 问题: [issue#13](https://github.com/react-native-oh-library/react-native-bootsplash/issues/13)

## Others

- 执行 generate-bootsplash 命令行时，由于 `--brand, --brand-width 和 --dark-*` 选项需要购买 license 才能使用，涉及功能未开源，HarmonyOS 平台不支持使用

## License

This project is licensed under [The MIT License (MIT)](https://github.com/zoontek/react-native-bootsplash/blob/master/LICENSE).
