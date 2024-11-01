> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-markdown-display</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-markdown-display">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20macos%20|%20web%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/iamacup/react-native-markdown-display/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [GitHub address](https://github.com/react-native-oh-library/react-native-markdown-display/tree/sig)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-markdown-display Releases](https://github.com/react-native-oh-library/react-native-markdown-display/releases).

Go to the project directory and execute the following instruction：

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-markdown-display@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-markdown-display@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository：

> [!WARNING] The name of the imported repository remains unchanged.

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

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

## Constraints

### Compatibility

This document is verified based on the following versions

- RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;
- RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


Please check for details [react-native-markdown-display](https://github.com/iamacup/react-native-markdown-display/blob/master/README.md)

The following are the HarmonyOS properties：

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/iamacup/react-native-markdown-display/blob/master/LICENSE).
