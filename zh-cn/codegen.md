# Codegen 使用

### 简介

`CodeGen` 是 React Native 中的一项工具，用于简化和自动化代码生成。它可以帮助开发者生成桥接代码，使得 React Native 应用能够更方便地与原生代码进行交互。

在 Harmony OS RN 中已支持 codegen，并且大部分 Arkts 三方库已支持，因此在使用这些三方库之前需要通过 codegen 生成桥接代码，否则可能会出现如下报错：

```
cannot find module '@rnoh/react-native-openharmony/generated/ts' or its corresponding type declarations.
```

### 使用方式

在 Harmony OS RN 中已支持 codegen，并且大部分 Arkts 三方库已支持，因此在使用这些三方库之前，需要在 RN 工程中执行如下代码，才能生成桥接代码。

```
// src为HarmonyOS工程中react-native-openharmony路径
// 示例：react-native codegen-harmony --rnoh-module-path ./harmony/oh_modules/@rnoh/react-native-openharmony
react-native codegen-harmony --rnoh-module-path src
```

执行后，会在`src`目录下生成 generated 目录和桥接代码。
