> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-markdown-display</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-markdown-display">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20macos%20|%20web%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-markdown-display/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-markdown-display/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-markdown-display Releases](https://github.com/react-native-oh-library/react-native-markdown-display/releases/tag/7.0.2-0.0.1)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-markdown-display
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-markdown-display
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { SafeAreaView, ScrollView, StatusBar } from 'react-native';

import Markdown from 'react-native-markdown-display';

const copy = `# h1 Heading 8-)

**This is some bold text!**

This is normal text
`;

const App: () => React$Node = () => {
  return (
    <>
      <StatusBar barStyle="dark-content" />
      <SafeAreaView>
        <ScrollView
          contentInsetAdjustmentBehavior="automatic"
          style={{height: '100%'}}
        >
          <Markdown>
            {copy}
          </Markdown>
        </ScrollView>
      </SafeAreaView>
    </>
  );
};

export default App;
```

## Link

目前鸿蒙暂不支持` AutoLink`，所以` Link` 步骤需要手动配置。

首先需要使用 `DevEco Studio` 打开项目里的鸿蒙工程 `harmony`

## 约束与限制

### 兼容性

在以下版本验证通过

- RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;

### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请查看[react-native-markdown-display](https://github.com/iamacup/react-native-markdown-display/blob/master/README.md)

如下是已经鸿蒙化的属性：

> [!tip] "鸿蒙支持"列为 yes 的属性表示支持鸿蒙平台，并且效果对标"原库平台"列中的 ios 或 android 的效果。

| Name                      | Description                                                                                                                                                                                           | Default                                                                                                                    | Required | Platform | HarmonyOS Support |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| `children`                | The markdown string to render, or the [pre-processed tree](https://github.com/react-native-oh-library/react-native-markdown-display/tree/sig#pre-processing)                                          | N/A                                                                                                                        | Yes      | All      | yes               |
| `style`                   | An object to override the styling for the various rules, [see style section below](https://github.com/react-native-oh-library/react-native-markdown-display/tree/sig#rules-and-styles) for more info  | [source](https://github.com/react-native-oh-library/react-native-markdown-display/blob/7.0.2-0.0.1/src/lib/styles.js)      | No       | All      | yes               |
| `mergeStyle`              | If true, when a style is supplied, the individual items are merged with the default styles instead of overwriting them                                                                                | `true`                                                                                                                     | No       | All      | yes               |
| `rules`                   | An object of rules that specify how to render each markdown item, [see rules section below](https://github.com/react-native-oh-library/react-native-markdown-display/tree/sig#rules) for more info    | [source](https://github.com/react-native-oh-library/react-native-markdown-display/blob/7.0.2-0.0.1/src/lib/renderRules.js) | No       | All      | yes               |
| `onLinkPress`             | A handler function to change click behaviour, [see handling links section below](https://github.com/react-native-oh-library/react-native-markdown-display/tree/sig#handling-links) for more info      | `import { Linking } from 'react-native';` and `Linking.openURL(url);`                                                      | No       | All      | yes               |
| `debugPrintTree`          | Will print the AST tree to the console to help you see what the markdown is being translated to                                                                                                       | `false`                                                                                                                    | No       | All      | yes               |
| `renderer`                | Used to specify a custom renderer, you can not use the rules or styles props with a custom renderer.                                                                                                  | `instanceOf(AstRenderer)`                                                                                                  | No       | All      | yes               |
| `markdownit`              | A custom markdownit instance with your configuration, default is `MarkdownIt({typographer: true})`                                                                                                    | `instanceOf(MarkdownIt)`                                                                                                   | No       | All      | yes               |
| `maxTopLevelChildren`     | If defined as a number will only render out first `n` many top level children, then will try to render out `topLevelMaxExceededItem`                                                                  | `null`                                                                                                                     | No       | All      | yes               |
| `topLevelMaxExceededItem` | Will render when `maxTopLevelChildren` is hit. Make sure to give it a key!                                                                                                                            | `<Text key="dotdotdot">...</Text>`                                                                                         | No       | All      | yes               |
| `allowedImageHandlers`    | Any image that does not start with one of these will have the `defaultImageHandler` value prepended to it (unless `defaultImageHandler` is null in which case it won't try to render anything)        | `['data:image/png;base64', 'data:image/gif;base64', 'data:image/jpeg;base64', 'https://', 'http://']`                      | No       | All      | yes               |
| `defaultImageHandler`     | Will be prepended to an image url if it does not start with something in the `allowedImageHandlers` array, if this is set to null, it won't try to recover but will just not render anything instead. | `http://`                                                                                                                  | No       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-markdown-display/blob/sig/LICENSE) ，请自由地享受和参与开源。
