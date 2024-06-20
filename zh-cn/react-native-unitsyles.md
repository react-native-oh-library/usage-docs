> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-unistyles</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jpudysz/react-native-unistyles">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jpudysz/react-native-unistyles/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-unistyles)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-unistyles Releases](https://github.com/react-native-oh-library/react-native-unistyles/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-unistyles@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-unistyles@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

<!-- {% raw %} -->
```js
import {
  StatusBar,
  StyleSheet,
  Text,
  View,
  Button,
  ScrollView,
  PixelRatio,
} from "react-native";
import {
  UnistylesRuntime,
  createStyleSheet,
  useStyles,
  UnistylesRegistry,
  mq,
  UnistylesPlugin,
} from "react-native-unistyles";
import React, { useEffect } from "react";
const basic_styles = StyleSheet.create({
  consta: { backgroundColor: "#F5FCFF" },
  titleStyle: { fontSize: 16, fontWeight: "500" },
});

export function UnistylesExample() {
  let anti_shake = true;
  const hasSomeCoolFeatures = true;
  const { styles, theme } = useStyles(stylesheet, {
    colors: hasSomeCoolFeatures,
    sizes: !hasSomeCoolFeatures,
  });
  let status_color = true;
  const renderCount = React.useRef(1);
  useEffect(
    () => () => {
      UnistylesRuntime.removePlugin(autoGuidelinePlugin);
    },
    []
  );
  const isAutoGuidelinePluginEnabled = UnistylesRuntime.enabledPlugins.includes(
    autoGuidelinePlugin.name
  );

  return (
    <ScrollView>
      <View style={basic_styles.consta}>
        <StatusBar barStyle="light-content"></StatusBar>
        <Text style={basic_styles.titleStyle}>{"变更状态栏颜色:"}</Text>
        <Button
          title="status"
          onPress={() => {
            anti_shake = !anti_shake;
            if (anti_shake) {
              UnistylesRuntime.statusBar.setColor(
                status_color ? sharedColors.barbie : sharedColors.aloes
              );
              status_color = !status_color;
            }
          }}
        ></Button>

        <Text style={basic_styles.titleStyle}>{"变更主题对象:"}</Text>
        <View style={styles.container}>
          <Text style={styles.text}>
            {" "}
            当前主题:{UnistylesRuntime.themeName} 重新渲染的次数:{renderCount.current++}
          </Text>
          <Text style={styles.theme}>
            {" "}
            Colors: {JSON.stringify(theme.colors, null, 2)}{" "}
          </Text>
          <Button
            title="变更light主题"
            onPress={() => {
              anti_shake = !anti_shake;
              if (anti_shake) {
                UnistylesRuntime.setAdaptiveThemes(false);
                UnistylesRuntime.setTheme("light");
                UnistylesRuntime.updateTheme("light", (theme) => ({
                  ...theme,
                  colors: {
                    ...theme.colors,
                    typography:
                      theme.colors.typography === "#000000"
                        ? theme.colors.blood
                        : "#000000",
                  },
                }));
              }
            }}
          />
        </View>

        <Text style={basic_styles.titleStyle}>{"更改页面样式:"}</Text>
        <Text style={styles.text}>
          {" "}
          这个页面正在使用 {UnistylesRuntime.themeName} 主题.
        </Text>
        <Button
          title="更改页面主题"
          color={theme.colors.accent}
          onPress={() => {
            anti_shake = !anti_shake;
            if (anti_shake) {
              UnistylesRuntime.setAdaptiveThemes(false);
              UnistylesRuntime.setTheme(
                UnistylesRuntime.themeName === "light" ? "premium" : "light"
              );
            }
          }}
        />

        <Text style={basic_styles.titleStyle}>{"自适应主题:"}</Text>
        <Text style={styles.container}>
          {" 系统主题:" + UnistylesRuntime.colorScheme}
        </Text>
        <Button
          title="启用自适应主题"
          onPress={() => {
            anti_shake = !anti_shake;
            if (anti_shake) {
              UnistylesRuntime.setAdaptiveThemes(true);
            }
          }}
        />

        <Text style={basic_styles.titleStyle}>{"插件:"}</Text>
        <View style={styles.unscaledBox}></View>
        <Text>
          前缀为unscaled的样式会被插件跳过,已启用的插件
          {UnistylesRuntime.enabledPlugins}
        </Text>
        <Button
          title={isAutoGuidelinePluginEnabled ? "关闭插件" : "启用插件"}
          onPress={() => {
            anti_shake = !anti_shake;
            if (anti_shake) {
              isAutoGuidelinePluginEnabled
                ? UnistylesRuntime.removePlugin(autoGuidelinePlugin)
                : UnistylesRuntime.addPlugin(autoGuidelinePlugin);
            }
          }}
        />

        <Text style={basic_styles.titleStyle}>
          {"在StyleSheets中使用runtime:"}
        </Text>
        <View style={styles.box}>
          <Text>
            占据了屏幕一半大小的方块width:{styles.box.width} 861 height:
            {styles.box.height}
          </Text>
        </View>

        <Text style={basic_styles.titleStyle}>{"动态函数式样式表:"}</Text>
        <View style={styles.dynamicFunction(2)}>
          <Text>accent</Text>
        </View>
        <View style={styles.dynamicFunction(1)}>
          <Text>barbie</Text>
        </View>

        <Text style={basic_styles.titleStyle}>{"媒体查询:"}</Text>
        <View style={styles.container1}>
          <Text>
            你的屏幕大小是:{UnistylesRuntime.screen.width}x
            {UnistylesRuntime.screen.height};当宽大于500时背景是
            {theme.colors.backgroundColor}，宽大于900时背景为
            {theme.colors.aloes}
          </Text>
        </View>

        <Text style={basic_styles.titleStyle}>
          {"在StyleSheets中使用variants:"}
        </Text>
        <View style={styles.box_variants}></View>
        <Text style={basic_styles.titleStyle}>{":"}</Text>

        <Text style={basic_styles.titleStyle}>{"字体大小偏好:"}</Text>
        <Text>
          {"现在的字体大小偏好设置为:" + UnistylesRuntime.contentSizeCategory}
        </Text>
      </View>
    </ScrollView>
  );
}

const stylesheet = createStyleSheet((theme, runtime) => ({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    paddingHorizontal: 20,
    backgroundColor: theme.colors.backgroundColor,
    rowGap: 20,
  },
  text: {
    textAlign: "center",
    color: theme.colors.typography,
    fontSize: 14,
  },
  bold: {
    fontWeight: "bold",
  },
  container1: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    paddingHorizontal: 20,
    backgroundColor: {
      [mq.width(undefined, 500).and.height(undefined, 1000)]:
        theme.colors.backgroundColor,
      [mq.only.width(932)]: theme.colors.aloes,
    },
    rowGap: 20,
  },
  theme: {
    color: theme.colors.typography,
  },
  box: {
    justifyContent: "center",
    alignItems: "center",
    padding: 20,
    marginTop: 50,
    width: runtime.screen.width / 2,
    height: runtime.screen.height / 2,
    backgroundColor:
      runtime.orientation === "portrait"
        ? theme.colors.accent
        : theme.colors.oak,
  },
  dynamicFunction: (index: number) => ({
    backgroundColor:
      index % 2 === 0 ? theme.colors.accent : theme.colors.barbie,
  }),
  box_variants: {
    borderRadius: 10,
    variants: {
      colors: {
        true: { backgroundColor: theme.colors.barbie },
        false: { backgroundColor: theme.colors.blood },
        default: { backgroundColor: theme.colors.sky },
        other: { backgroundColor: theme.colors.typography },
      },
      sizes: {
        true: { width: 200, height: 200 },
        false: { width: 50, height: 50 },
        default: { width: 100, height: 100 },
        other: { width: 150, height: 150 },
      },
    },
  },
  unscaledBox: { width: 100, height: 100, backgroundColor: theme.colors.blood },
}));

const sharedColors = {
  barbie: "#ff9ff3",
  oak: "#1dd1a1",
  sky: "#48dbfb",
  fog: "#c8d6e5",
  aloes: "#00d2d3",
  blood: "#ff6b6b",
};
const lightTheme = {
  colors: {
    ...sharedColors,
    backgroundColor: "#ffffff",
    typography: "#000000",
    accent: sharedColors.blood,
  },
};
const darkTheme = {
  colors: {
    ...sharedColors,
    backgroundColor: "#000000",
    typography: "#ffffff",
    accent: sharedColors.barbie,
  },
};
const premiumTheme = {
  colors: {
    ...sharedColors,
    backgroundColor: sharedColors.barbie,
    typography: "#76278f",
    accent: "#000000",
  },
};
const breakpoints = { xs: 0, sm: 300, md: 500, lg: 800, xl: 1200 };
UnistylesRegistry.addThemes({
  light: lightTheme,
  dark: darkTheme,
  premium: premiumTheme,
})
  .addBreakpoints(breakpoints)
  .addConfig({ adaptiveThemes: true, initialTheme: "light" });

const REFERENCE_WIDTH = 300;
const REFERENCE_HEIGHT = 800;

const autoGuidelinePlugin: UnistylesPlugin = {
  name: "autoGuideline",
  onParsedStyle: (styleKey, style, runtime) => {
    const pairs = Object.entries(style).map(([key, value]) => {
      if (styleKey.includes("unscaled")) {
        return [key, value];
      }

      const isNumber = typeof value === "number";

      if (!isNumber || key === "flex") {
        return [key, value];
      }

      if (key === "height") {
        const percentage = value / REFERENCE_HEIGHT;
        return [
          key,
          PixelRatio.roundToNearestPixel(runtime.screen.height * percentage),
        ];
      }
      const percentage = value / REFERENCE_WIDTH;
      return [
        key,
        PixelRatio.roundToNearestPixel(runtime.screen.width * percentage),
      ];
    });

    return Object.fromEntries(pairs);
  },
};
```
<!-- {% endraw %} -->

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides 字段

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
    "@react-native-oh-tpl/react-native-unistyles": "file:../../node_modules/@react-native-oh-tpl/react-native-unistyles/harmony/unistyles.har"
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

### 在 ArkTs 侧引入 RNUnistylesPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {RNUnistylesPackage} from '@react-native-oh-tpl/react-native-unistyles/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNUnistylesPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-unistyles Releases](https://github.com/react-native-oh-library/react-native-unistyles/releases)


## Runtime
### UnistylesRuntime

UnistylesRuntime 是 Unitstyles 库 的一个Host Object。它始终保持最新状态，并允许您与Unistyles的原生层进行交互

#### UnistylesRuntime 属性

| Name                 | Description                                                                  | Type                 | Required | Platform        | HarmonyOS Support |
| -------------------- | ---------------------------------------------------------------------------- | -------------------- | -------- | --------------- | ----------------- |
| screenWidth          | Screen dimensions Width                                                      | number               | no       | All             | yes               |
| screenHeight         | Screen dimensions Height                                                     | number               | no       | All             | yes               |
| enabledPlugins       | Names of currently enabled plugins                                           | boolean              | no       | All             | yes               |
| hasAdaptiveThemes    | Indicates if you have enabled adaptive themes                                | boolean              | no       | All             | yes               |
| themeName            | Name of the selected theme or an empty string if you don’t use themes        | string               | no       | All             | yes               |
| breakpoint           | Current breakpoint or always undefined if you don’t use breakpoints          | UnistylesBreakpoints | no       | All             | yes               |
| colorScheme          | Get your device’s color scheme. Available options dark, light or unspecified | string               | no       | All             | yes               |
| contentSizeCategory  | Your device’s content size category                                          | string               | no       | All             | yes               |
| insets               | Device insets which are safe to put content into                             | inset                | no       | All             | yes               |
| statusBar.width      | Status bar dimensions width                                                  | number               | no       | All             | yes               |
| statusBar.height     | Status bar dimensions height                                                 | number               | no       | All             | yes               |
| navigationBar.height | Navigation bar dimensions height                                             | number               | no       | Android 		  | yes               |
| navigationBar.width  | Navigation bar dimensions width                                              | number               | no       | Android 		  | yes               |
| ScreenOrientation    | Your device’s orientation                                                    | ScreenOrientation    | no       | All             | yes               |

目前 UnistylesRuntime 支持：

* `statusBar.setColor`
Update statusBar color at runtime

* `navigationBar.setColor`
Update navigationBar color at runtime

* `setAdaptiveThemes`
Toggle adaptive themes 

* `setTheme`
Change the current theme    

* `updateTheme`
Update the theme at runtime

* `removePlugin`
Disable a plugin 

* `addPlugin`
Enable a plugin 


## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。
> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### global

| Name             | Description                                                                  | Type     | Required | Platform | HarmonyOS Support |
| ---------------- | ---------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| useInitialTheme  | using multiple themes and need to determine the initial theme during runtime | function | no       | All      | yes               |
| useStyles        | set current styles                                                           | function | no       | All      | yes               |
| createStyleSheet | create unistyles StyleSheet                                                  | function | no       | All      | yes               |

#### mq

| Name   | Description                   | Type     | Required | Platform | HarmonyOS Support |
| ------ | ----------------------------- | -------- | -------- | -------- | ----------------- |
| width  | width from xx onwards         | function | no       | All      | yes               |
| height | heigh from xx onwards         | function | no       | All      | yes               |
| and    | and                           | function | no       | All      | yes               |
| only   | width or height from xx to xx | function | no       | All      | yes               |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。
> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### UnistylesRegistry

| Name           | Description          | Type     | Required | Platform | HarmonyOS Support |
| -------------- | -------------------- | -------- | -------- | -------- | ----------------- |
| addThemes      | register themes      | function | no       | All      | yes               |
| addBreakpoints | register breakpoints | function | no       | All      | yes               |
| addConfig      | register config      | function | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/jpudysz/react-native-unistyles/blob/main/LICENSE) ，请自由地享受和参与开源。