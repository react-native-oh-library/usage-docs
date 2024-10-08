> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-markdown-renderer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mientjan/react-native-markdown-renderer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20iOS%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mientjan/react-native-markdown-renderer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-markdown-renderer)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-markdown-renderer Releases](https://github.com/react-native-oh-library/react-native-markdown-renderer/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-markdown-renderer@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-markdown-renderer@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import react from "react";
import { PureComponent } from "react-native";
import Markdown from "react-native-markdown-renderer";

const copy = `# h1 Heading 8-)

| Option | Description |
| ------ | ----------- |
| data   | path to data files to supply the data that will be passed into templates. |
| engine | engine to be used for processing templates. Handlebars is the default. |
| ext    | extension to be used for dest files. |
`;

export default class Page extends PureComponent {
  static propTypes = {};
  static defaultProps = {};

  render() {
    return <Markdown>{copy}</Markdown>;
  }
}
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-markdown-renderer Releases](https://github.com/react-native-oh-library/react-native-markdown-renderer/releases)，并下载适用版本的 tgz 包。

## Markdown 组件

默认导出 Markdown 组件

Markdown 组件核心功能就是支持 Markdowm 语法格式的渲染，语法格式为（说明:`copy`为符合 Markdown 语法的字符串）：`<Markdown>{copy}</Markdown>`。
说明：`copy`为组件支持的满足 Markdown 语法格式的字符串，具体支持的语法格式，详见：[Syntax Support](https://github.com/mientjan/react-native-markdown-renderer/blob/master/README.md)

### 组件属性

Markdown 组件的 Props

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name       | Description                                                                                      | Type     | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| style      | Overrides the built-in style of the original Markdown component                                  | object   | no       | iOS/Android | yes               |
| rules      | Rendering rule of the markdowm syntax tag in the Markdown component.                             | function | yes      | iOS/Android | yes               |
| markdownit | MarkdownIt 类的 md 实例，用于覆盖默认的 MarkdownIt 实例（默认：MarkdownIt({typographer: true})） | object   | yes      | iOS/Android | yes               |

## 库相关变量、封装类及工具函数

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

改库导出了一系列内部定义的常量、封装类及工具函数

### 内部定义的常量

| Name        | Description            | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | ---------------------- | ------ | -------- | ----------- | ----------------- |
| renderRules | 内部定义的渲染规则对象 | object | no       | iOS/Android | yes               |
| styles      | 内部定义的样式对象     | object | no       | iOS/Android | yes               |

### 封装类

| Name            | Description                           | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------- | ------ | -------- | ----------- | ----------------- |
| AstRenderer     | 内部封装的 AST 抽象树渲染类           | object | no       | iOS/Android | yes               |
| PluginContainer | 内部定义的 blockPlugin 插件容器类     | object | no       | iOS/Android | yes               |
| MarkdownIt      | 内部依赖库 markdown-it 默认导出的对象 | object | no       | iOS/Android | yes               |

### 工具函数

| Name           | Description                                                                                    | Type     | Required | Platform    | HarmonyOS Support |
| -------------- | ---------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| applyStyle     | 用于将给指定的 displayName 组件转换为 Text 组件并应用 style 样式                               | function | no       | iOS/Android | yes               |
| getUniqueID    | 获取 uuid 时间戳字符串作为唯一标识                                                             | function | yes      | iOS/Android | yes               |
| openUrl        | 打开默认应用，跳转指定链接地址                                                                 | function | yes      | iOS/Android | yes               |
| hasParents     | 判断指定 parents 数组中是否存在指定 type 的元素 （内部方法，不应直接调用）                     | function | yes      | iOS/Android | yes               |
| parser         | 将指定的 source 通过 renderer 方法及 MarkdownIt 对象转换为 View 组件（内部方法，不应直接调用） | function | yes      | iOS/Android | yes               |
| stringToTokens | 将指定的 source 通过 MarkdownIt 对象的 parse 方法转换为 token 数组（内部方法，不应直接调用）   | function | yes      | iOS/Android | yes               |
| tokensToAST    | 将 token 数组转换为 AST 抽象树（内部方法，不应直接调用）                                       | function | yes      | iOS/Android | yes               |
| blockPlugin    | js 插件方法,用于提供对 Markdown 中 Blockquotes 语法的支持                                      | function | yes      | iOS/Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/killserver/react-native-markdown-renderer/blob/main/LICENSE) ，请自由地享受和参与开源。
