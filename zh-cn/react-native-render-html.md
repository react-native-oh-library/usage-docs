> 模板版本：v0.1.2

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

>[!tip] [Github 地址](https://github.com/meliorence/react-native-render-html)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add react-native-render-html
```
#### **npm**

```bash
npm install react-native-render-html
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React from 'react';
import { useWindowDimensions } from 'react-native';
import RenderHtml from 'react-native-render-html';

const source = {
  html: `
<p style='text-align:center;'>
  Hello World!
</p>`
};

export default function App() {
  const { width } = useWindowDimensions();
  return (
    <RenderHtml
      contentWidth={width}
      source={source}
    />
  );
}
```

## 约束与限制

### 兼容性

 在下述版本验证通过：

 1. IDE：DevEco Studio 4.1.3.313;SDK：OpenHarmony(api11) 4.1.0.52;测试设备：Mate40 Pro(NOH-AN00);ROM：2.0.0.52(C00E52R1P17log);RNOH：0.72.11

## 属性

以下属性已验证，详情见 [react-native-render-html源库地址](https://github.com/meliorence/react-native-render-html)

**组件 RenderHtml**

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |
| allowedStyles | Whitelist specific inline CSS style properties and ignore the others. | CSSPropertyNameList  | NO | / | Yes |
| baseStyle | The default style for the document (root). Inheritable styles will be transferred to children. That works also for textual styles. | MixedStyleDeclaration  | NO | / | Yes |
| classesStyles | Provide mixed styles to target elements selected by CSS classes. | Readonly<Record<string, MixedStyleDeclaration>>  | NO | / | Yes |
| computeEmbeddedMaxWidth | A function which takes contentWidth and tagName as arguments and returns a new width. Can return Infinity to denote unconstrained widths. | (contentWidth: number, tagName: string) => number  | NO | / | Yes |
| contentWidth | The width of the HTML content to display. The recommended practice is to pass useWindowDimensions().width minus any padding or margins. | number  | NO | / | Yes |
| customHTMLElementModels | Customize element models for target tags. | HTMLElementModelRecord  | NO | / | Yes |
| defaultTextProps | Default props for Text elements in the render tree. | TextProps | NO | / | Yes |
| defaultViewProps | Default props for View elements in the render tree. | ViewProps | NO | / | Yes |
| domVisitors | An object which callbacks will be invoked when a DOM element or text node has been parsed and its children attached. This is great to tamper the dom, remove children, insert nodes, change text nodes data... etc. | DomVisitorCallbacks | NO | / | Yes |
| emSize | The default value in pixels for 1em. | number | NO | / | Yes |
| enableCSSInlineProcessing | Enable or disable inline CSS processing of inline styles. | boolean | NO | / | Yes |
| enableExperimentalMarginCollapsing | Enable or disable margin collapsing CSS behavior (experimental!). | boolean | NO | / | Yes |
| idsStyles | Enable or disable margin collapsing CSS behavior (experimental!). | boolean | NO | / | Yes |
| ignoreDomNode | Ignore specific DOM nodes. | (node: Node, parent: NodeWithChildren) => unknown | NO | / | Yes |
| ignoredDomTags | A list of lowercase tags which should not be included in the DOM. | Array<string> | NO | / | Yes |
| ignoredStyles | Blacklist specific inline CSS style properties and allow the others. | CSSPropertyNameList | NO | / | Yes |
| onDocumentMetadataLoaded | Handler invoked when the document metadata is available. It will re-trigger on HTML content changes. | (documentMetadata: DocumentMetadata) => void | NO | / | Yes |
| onHTMLLoaded | Triggered when HTML is available to the RenderHTML component. | (html: string) => void | NO | / | Yes |
| onTTreeChange | Triggered when the transient render tree changes. Useful for debugging. | (ttree: TDocument) => void | NO | / | Yes |
| renderers | Your custom renderers. | CustomTagRendererRecor | NO | / | Yes |
| source | The object source to render (either { uri }, { html } or { dom }). | HTMLSource  | Yes | / | Yes(已验证html) |
| renderersProps | Props to use in custom renderers with useRendererProps. | Partial<RenderersProps>| NO | / | Yes |
| tagsStyles | Provide mixed styles to target HTML tag names. | Readonly<Record<string, MixedStyleDeclaration>>| NO | / | Yes |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/meliorence/react-native-render-html/blob/master/LICENSE) ，请自由地享受和参与开源。
