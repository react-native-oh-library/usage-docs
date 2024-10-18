> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@shopify/restyle</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Shopify/restyle">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Shopify/restyle/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/Shopify/restyle)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @shopify/restyle@2.4.4
```

#### **yarn**

```bash
yarn add @shopify/restyle@2.4.4
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { createTheme } from "@shopify/restyle";

const palette = {
  purpleLight: "#8C6FF7",
  purplePrimary: "#5A31F4",
  purpleDark: "#3F22AB",

  greenLight: "#56DCBA",
  greenPrimary: "#0ECD9D",
  greenDark: "#0A906E",

  black: "#0B0B0B",
  white: "#F0F2F3",
};

const theme = createTheme({
  colors: {
    mainBackground: palette.white,
    cardPrimaryBackground: palette.purplePrimary,
  },
  spacing: {
    s: 8,
    m: 16,
    l: 24,
    xl: 40,
  },
  textVariants: {
    header: {
      fontWeight: "bold",
      fontSize: 34,
    },
    body: {
      fontSize: 16,
      lineHeight: 24,
    },
    defaults: {
      // We can define a default text variant here.
    },
  },
});
export type Theme = typeof theme;
export default theme;

```

```js
import { ThemeProvider } from "@shopify/restyle";
import theme from "./theme";

export const App = () => (
  <ThemeProvider theme={theme}>{/* Rest of the app */}</ThemeProvider>
);

```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Hooks

详细请查看 [restyle 的文档介绍](https://shopify.github.io/restyle/)

以下为目前已支持的 Hooks：

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|       Name        |                                           Description                                           |   Type   | Required | Platform | HarmonyOS Support |
|:-----------------:|:-----------------------------------------------------------------------------------------------:|:--------:|:--------:|:--------:|:-----------------:|
|     useTheme      |                            Retrieve attribute objects from the theme                            | function |    No    |   All    |        Yes        |
|    useRestyle     | Dynamically styles reaction components based on a theme and a set of rules for resetting styles | function |    No    |   All    |        Yes        |
| useResponsiveProp |                  Fetching the value of a responsive prop in a custom component                  | function |    No    |   All    |        Yes        |

## 方法

详细请查看 [restyle 的文档介绍](https://shopify.github.io/restyle/)

以下为目前已支持的方法：

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|          Name          |                                  Description                                   |   Type   | Required | Platform | HarmonyOS Support |
|:----------------------:|:------------------------------------------------------------------------------:|:--------:|:--------:|:--------:|:-----------------:|
|      createTheme       |                                Defining a Theme                                | function |    No    |   All    |        Yes        |
|     createVariant      |           Provides a flexible way to handle style changes in a theme           | function |    No    |   All    |        Yes        |
| createRestyleFunction  |                         Creating a Predefined Restyle                          | function |    No    |   All    |        Yes        |
| createRestyleComponent | To create a custom component, you need to set the predefined Restyle function. | function |    No    |   All    |        Yes        |

## 预定义组件

详细请查看 [restyle 的文档介绍](https://shopify.github.io/restyle/)

以下为目前已支持的预定义组件：

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|     Name      |                  Description                   |   Type   | Required | Platform | HarmonyOS Support |
|:-------------:|:----------------------------------------------:|:--------:|:--------:|:--------:|:-----------------:|
|  createText   |           Predefined Text component            | function |    No    |   All    |        Yes        |
|   createBox   |            Predefined Box component            | function |    No    |   All    |        Yes        |
| ThemeProvider | Set the theme to the outermost React component | function |    No    |   All    |        Yes        |

## 预定义 Restyle 函数

详细请查看 [restyle 的文档介绍](https://shopify.github.io/restyle/fundamentals/restyle-functions)

以下为目前已支持的预定义 Restyle 函数：

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|              Name              |                                                                                                                                                                                    Props                                                                                                                                                                                     |   Type   | Required | Platform | HarmonyOS Support |
|:------------------------------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------:|:--------:|:--------:|:-----------------:|
| backgbackgroundColorroundColor |                                                                                                                                                                   backgroundColor [bg]backgroundColor [bg]                                                                                                                                                                   | function |    No    |   All    |        Yes        |
|           colorcolor           |                                                                                                                                                                                 color color                                                                                                                                                                                  | function |    No    |   All    |        Yes        |
|         opacityopacity         |                                                                                                                                                                                opacityopacity                                                                                                                                                                                | function |    No    |   All    |        Yes        |
|         visiblevisible         |                                                                                                                                     display (maps `true` / `false` to `flex` / `none`)display (maps `true` / `false` to `flex` / `none`)                                                                                                                                     | function |    No    |   All    |        Yes        |
|            spacing             | margin [m], marginTop [mt], marginRight [mr], marginBottom [mb], marginLeft [ml], marginStart [ms], marginEnd[me], marginHorizontal [mx], marginVertical [my], padding [p], paddingTop [pt], paddingRight [pr], paddingBottom [pb], paddingLeft [pl], paddingStart [ps], paddingEnd [pe], paddingHorizontal [px], paddingVertical [py], gap [g], rowGap [rG], columnGap [cG] | function |    No    |   All    |        Yes        |
|             layout             |                                                                                     width, height, minWidth, maxWidth, minHeight, maxHeight, overflow, aspectRatio, alignContent, alignItems, alignSelf, justifyContent, flex, flexBasis, flexDirection, flexGrow, flexShrink, flexWrap                                                                                      | function |    No    |   All    |        Yes        |
|            position            |                                                                                                                                                                position, top, right, bottom, left, start, end                                                                                                                                                                | function |    No    |   All    |        Yes        |
|            position            |                                                                                                                                                                                    zIndex                                                                                                                                                                                    | function |    No    |   All    |        Yes        |
|             border             |                                                                                                                       borderBottomWidth, borderLeftWidth, borderRightWidth, borderStartWidth, borderEndWidth, borderStyle, borderTopWidth, borderWidth                                                                                                                       | function |    No    |   All    |        Yes        |
|             border             |                                                                                                                             borderColor, borderTopColor, borderRightColor, borderLeftColor, borderStartColor, borderEndColor, borderBottomColor                                                                                                                              | function |    No    |   All    |        Yes        |
|             border             |                                                                                      borderRadius, borderBottomLeftRadius, borderBottomRightRadius, borderBottomStartRadius, borderBottomEndRadius, borderTopLeftRadius, borderTopRightRadius, borderTopStartRadius, borderTopEndRadius                                                                                      | function |    No    |   All    |        Yes        |
|             shadow             |                                                                                                                                                             shadowOpacity, shadowOffset, shadowRadius, elevation                                                                                                                                                             | function |    No    |   All    |        Yes        |
|             shadow             |                                                                                                                                                                                 shadowColor                                                                                                                                                                                  | function |    No    |   All    |        Yes        |
|           textShadow           |                                                                                                                                                                      textShadowOffset, textShadowRadius                                                                                                                                                                      | function |    No    |   All    |        NO         |
|           textShadow           |                                                                                                                                                                               textShadowColor                                                                                                                                                                                | function |    No    |   All    |        NO         |

## 遗留问题

## 其他

 - 预函数textShadow在Android和iOS不生效， HarmonyOS与Android,iOS表现一致 [原库 issue](https://github.com/Shopify/restyle/issues/307)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/Shopify/restyle/blob/master/LICENSE.md)，请自由地享受和参与开源。
