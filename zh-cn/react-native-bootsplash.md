<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-bootsplash</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/zoontek/react-native-bootsplash">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/zoontek/react-native-bootsplash/blob/expo-plugin/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-bootsplash)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-bootsplash Releases](https://github.com/react-native-oh-library/react-native-bootsplash/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-bootsplash@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-bootsplash@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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
    manifest: require("../assets/bootsplash_manifest.json"),
    logo: require("../assets/bootsplash_logo.png"),
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
    // set transparent status bar
    StatusBar.setBarStyle("dark-content");
    if (Platform.OS !== "android") {
      StatusBar.setBackgroundColor("transparent");
      StatusBar.setTranslucent(true);
    }
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

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 引入原生端代码

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

### 在 ArkTs 侧引入 RNBootSplashPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {RNBootSplashPackage} from '@react-native-oh-tpl/react-native-bootsplash/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNBootSplashPackage(ctx)
  ];
}
```

### 运行

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

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name             | Description                                                  | Type     | Required | Platform     | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------- | -------- | ------------ | ----------------- |
| getConstants     | Obtaining the Default Configuration                          | function | no       | Android、IOS | yes               |
| hide             | Hide the splash screen                                       | function | no       | Android、IOS | yes               |
| isVisible        | Return the current visibility status of the native splash screen | function | no       | Android、IOS | yes               |
| useHideAnimation | A hook to easily creation a hide custom hide animation, by animating all splash screen elements using Animated | function | yes      | Android、IOS | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/zoontek/react-native-bootsplash/blob/expo-plugin/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->