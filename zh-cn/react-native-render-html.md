<!-- {% raw %} -->
> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-render-html</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/meliorence/react-native-render-html">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/meliorence/react-native-render-html/blob/master/README.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/meliorence/react-native-render-html)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-render-html@6.3.4
```

#### **yarn**

```bash
yarn add react-native-render-html@6.3.4
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React from "react";
import { useWindowDimensions } from "react-native";
import RenderHtml from "react-native-render-html";

const source = {
  html: `
<p style='text-align:center;'>
  Hello World!
</p>`,
};

export default function App() {
  const { width } = useWindowDimensions();
  return <RenderHtml contentWidth={width} source={source} />;
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，详情见 [react-native-render-html 源库地址](https://github.com/meliorence/react-native-render-html)

**组件 RenderHtml**

| Name                               | Description                                                                                                                                                                                                         | Type                                              | Required | Platform | HarmonyOS Support                                                 |
| ---------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- | -------- | -------- | ----------------------------------------------------------------- |
| allowedStyles                      | Whitelist specific inline CSS style properties and ignore the others.                                                                                                                                               | CSSPropertyNameList                               | NO       | All      | Yes                                                               |
| baseStyle                          | The default style for the document (root). Inheritable styles will be transferred to children. That works also for textual styles.                                                                                  | MixedStyleDeclaration                             | NO       | All      | Yes                                                               |
| classesStyles                      | Provide mixed styles to target elements selected by CSS classes.                                                                                                                                                    | Readonly<Record<string, MixedStyleDeclaration>>   | NO       | All      | Yes                                                               |
| computeEmbeddedMaxWidth            | A function which takes contentWidth and tagName as arguments and returns a new width. Can return Infinity to denote unconstrained widths.                                                                           | (contentWidth: number, tagName: string) => number | NO       | All      | Yes                                                               |
| contentWidth                       | The width of the HTML content to display. The recommended practice is to pass useWindowDimensions().width minus any padding or margins.                                                                             | number                                            | NO       | All      | Yes                                                               |
| customHTMLElementModels            | Customize element models for target tags.                                                                                                                                                                           | HTMLElementModelRecord                            | NO       | All      | Yes                                                               |
| defaultTextProps                   | Default props for Text elements in the render tree.                                                                                                                                                                 | TextProps                                         | NO       | All      | Yes                                                               |
| defaultViewProps                   | Default props for View elements in the render tree.                                                                                                                                                                 | ViewProps                                         | NO       | All      | Yes                                                               |
| domVisitors                        | An object which callbacks will be invoked when a DOM element or text node has been parsed and its children attached. This is great to tamper the dom, remove children, insert nodes, change text nodes data... etc. | DomVisitorCallbacks                               | NO       | All      | Yes                                                               |
| emSize                             | The default value in pixels for 1em.                                                                                                                                                                                | number                                            | NO       | All      | Yes                                                               |
| enableCSSInlineProcessing          | Enable or disable inline CSS processing of inline styles.                                                                                                                                                           | boolean                                           | NO       | All      | Yes                                                               |
| enableExperimentalMarginCollapsing | Enable or disable margin collapsing CSS behavior (experimental!).                                                                                                                                                   | boolean                                           | NO       | All      | Yes                                                               |
| idsStyles                          | Enable or disable margin collapsing CSS behavior (experimental!).                                                                                                                                                   | boolean                                           | NO       | All      | Yes                                                               |
| ignoreDomNode                      | Ignore specific DOM nodes.                                                                                                                                                                                          | (node: Node, parent: NodeWithChildren) => unknown | NO       | All      | Yes                                                               |
| ignoredDomTags                     | A list of lowercase tags which should not be included in the DOM.                                                                                                                                                   | Array<string>                                     | NO       | All      | Yes                                                               |
| ignoredStyles                      | Blacklist specific inline CSS style properties and allow the others.                                                                                                                                                | CSSPropertyNameList                               | NO       | All      | Yes                                                               |
| onDocumentMetadataLoaded           | Handler invoked when the document metadata is available. It will re-trigger on HTML content changes.                                                                                                                | (documentMetadata: DocumentMetadata) => void      | NO       | All      | Yes                                                               |
| onHTMLLoaded                       | Triggered when HTML is available to the RenderHTML component.                                                                                                                                                       | (html: string) => void                            | NO       | All      | Yes                                                               |
| onTTreeChange                      | Triggered when the transient render tree changes. Useful for debugging.                                                                                                                                             | (ttree: TDocument) => void                        | NO       | All      | Yes                                                               |
| renderers                          | Your custom renderers.                                                                                                                                                                                              | CustomTagRendererRecor                            | NO       | All      | Yes                                                               |
| source                             | The object source to render (either { uri }, { html } or { dom }).                                                                                                                                                  | HTMLSource                                        | Yes      | All      | partially(已验证 html)                                            |
| renderersProps                     | Props to use in custom renderers with useRendererProps.                                                                                                                                                             | Partial<RenderersProps>                           | NO       | All      | partially(已验证 img 的百分比属性 enableExperimentalPercentWidth) |
| tagsStyles                         | Provide mixed styles to target HTML tag names.                                                                                                                                                                      | Readonly<Record<string, MixedStyleDeclaration>>   | NO       | All      | Yes                                                               |

## 遗留问题

- [ ] img 的宽度不会随着 contentWidth 的动态修改而更改（由 RN 基座引起，RNImage 组件更新状态时 this.descriptorWrapper 没有重新赋值）

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/meliorence/react-native-render-html/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->