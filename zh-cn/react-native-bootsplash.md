> 模板版本：v0.2.2

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



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-bootsplash)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-bootsplash Releases](https://github.com/react-native-oh-library/react-native-bootsplash/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

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
为了加快设置速度，我们提供了一个CLI来自动生成配置、创建Android Drawable XML文件、iOS Storyboard文件和HarmonyOS Resources文件

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

编辑您的启动Ability文件, 它通常是配置在entry模块module.json5中abilities属性中配置的第一个abilitie:

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> [!TIP] 示例中logo参数使用了本地图片资源，可以到[react-native-boot-splash demo](https://github.com/react-native-oh-library/RNOHDCS/tree/main/react-native-boot-splash/source)获取该图片

```js
import { useState , useEffect} from "react";
import { Animated, View, Text, Dimensions, Platform, StatusBar, StyleSheet } from "react-native";
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
  onAnimationEnd: () => void;
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
              console.log("--------++++AnimationEnd")
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

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-bootsplash": "file:../../node_modules/@react-native-oh-tpl/react-native-bootsplash/harmony/boot_splash.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.在 ArkTs 侧引入 RNBootSplashPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

### 4.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-bootsplash Releases](https://github.com/react-native-oh-library/react-native-bootsplash/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name             | Description                                                  | Type     | Required | Platform     | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------- | -------- | ------------ | ----------------- |
| hide             | Hide the splash screen.                            | function | no       | Android、IOS | yes               |
| isVisible        | Return the current visibility status of the native splash screen. | function | no       | Android、IOS | yes               |
| useHideAnimation     | A hook to easily create a custom hide animation by animating all splash screen elements using Animated, react-native-reanimated or else (similar as the video on top of this documentation).                          | function | no       | Android、IOS | yes               |

### hide

```js
type hide = (config?: { fade?: boolean }) => Promise<void>;
```

| Name  | Description                                                | Type             | Required | Platform    | HarmonyOS Support |
| ----- | ---------------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| fade | Hide the splash screen (immediately, or with a fade out). | boolean | No      | iOS/Android | partially               |

### useHideAnimation

```js
useHideAnimation(config: {UseHideAnimationConfig}) => {container: ContainerProps;logo: LogoProps;brand: BrandProps;};
```

| Name  | Description                                                | Type             | Required | Platform    | HarmonyOS Support |
| ----- | ---------------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| ready | a boolean flag to delay the animate execution (default: true) | boolean | No      | iOS/Android | partially               |
| manifest | the manifest file is generated in your assets directory | Manifest | Yes      | iOS/Android | partially               |
| logo | logo image in animation | ImageRequireSource | No      | iOS/Android | partially               |
| darkLogo | logo image in animation in dark mode | ImageRequireSource | No      | iOS/Android | partially               |
| brand | brand image in animation | ImageRequireSource | No      | iOS/Android | partially               |
| darkBrand | brand image in animation in dark mode | ImageRequireSource | No      | iOS/Android | partially               |
| statusBarTranslucent | sets whether the status bar is transparent | boolean | No      | iOS/Android | partially               |
| navigationBarTranslucent | sets whether the navigation bar is transparent | boolean | No      | iOS/Android | partially               |
| animate | custom hide animation | function | Yes      | iOS/Android | partially               |

## 遗留问题

- [ ] HarmonyOS的window窗口上不支持设置动画属性，hide接口fade参数设置true没有效果 问题: [issue#13](https://github.com/react-native-oh-library/react-native-bootsplash/issues/13)

## 其他
- 执行generate-bootsplash命令行时，由于 `--brand, --brand-width 和 --dark-*` 选项需要购买license才能使用，涉及功能未开源，HarmonyOS平台不支持使用

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/zoontek/react-native-bootsplash/blob/master/LICENSE) ，请自由地享受和参与开源。