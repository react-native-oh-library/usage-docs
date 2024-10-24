> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-render-html</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/meliorence/react-native-render-html">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/meliorence/react-native-render-html/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-BSD-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/meliorence/react-native-render-html)

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE：DevEco Studio 5.0.3.403; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**RenderHtml**

| Name                                   | Description                                                                                                                                                                                                       | Type                                               | Required | Platform    | HarmonyOS Support |
|----------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------|----------|-------------|-------------------|
| allowedStyles                          | Whitelist specific inline CSS style properties and ignore the others.                                                                                                                                             | CSSPropertyNameList                                | NO       | Android iOS | Yes               |
| baseStyle                              | The default style for the document (root). Inheritable styles will be transferred to children. That works also for textual styles.                                                                                | MixedStyleDeclaration                              | NO       | Android iOS | Yes               |
| classesStyles                          | Provide mixed styles to target elements selected by CSS classes.                                                                                                                                                  | Readonly<Record<string, MixedStyleDeclaration>>    | NO       | Android iOS | Yes               |
| computeEmbeddedMaxWidth                | A function which takes contentWidth and tagName as arguments and returns a new width. Can return Infinity to denote unconstrained widths.                                                                         | (contentWidth: number, tagName: string) => number  | NO       | Android iOS | Yes               |
| contentWidth                           | The width of the HTML content to display. The recommended practice is to pass useWindowDimensions().width minus any padding or margins.                                                                           | number                                             | NO       | Android iOS | Yes               |
| customHTMLElementModels                | Customize element models for target tags.                                                                                                                                                                         | HTMLElementModelRecord                             | NO       | Android iOS | Yes               |
| dangerouslyDisableHoisting             | Disable hoisting. Especially useful for rendering with react-native-web.Note that your layout might break in native!                                                                                              | boolean                                            | NO       | Android iOS | Yes               |
| dangerouslyDisableWhitespaceCollapsing | Disable whitespace collapsing. Especially useful if your html is being pre-processed server-side with a minifier.                                                                                                 | boolean                                            | NO       | Android iOS | Yes               |
| debug                                  | Log to the console a snapshot of the rendered TDocument after each transient render tree invalidation.                                                                                                            | boolean                                            | NO       | Android iOS | Yes               |
| defaultTextProps                       | Default props for Text elements in the render tree.                                                                                                                                                               | TextProps                                          | NO       | Android iOS | Yes               |
| defaultViewProps                       | Default props for View elements in the render tree.                                                                                                                                                               | ViewProps                                          | NO       | Android iOS | Yes               |
| domVisitors                            | An object which callbacks will be invoked when a DOM element or text node has been parsed and its children attached. This is great to tamper the dom, remove children, insert nodes, change text nodes data... etc. | DomVisitorCallbacks                                | NO       | Android iOS | Yes               |
| emSize                                 | The default value in pixels for 1em.                                                                                                                                                                              | number                                             | NO       | Android iOS | Yes               |
| enableCSSInlineProcessing              | Enable or disable inline CSS processing of inline styles.                                                                                                                                                         | boolean                                            | NO       | Android iOS | Yes               |
| enableExperimentalBRCollapsing         | Recommended value is `true` on non-web platforms. Also note that this is an experimental feature, thus subject to behavioral instability.                                                                         | boolean                                            | NO       | Android iOS | Yes               |
| enableExperimentalMarginCollapsing     | Enable or disable margin collapsing CSS behavior (experimental!).                                                                                                                                                 | boolean                                            | NO       | Android iOS | Yes               |
| idsStyles                              | Enable or disable margin collapsing CSS behavior (experimental!).                                                                                                                                                 | boolean                                            | NO       | Android iOS | Yes               |
| ignoreDomNode                          | Ignore specific DOM nodes.                                                                                                                                                                                        | (node: Node, parent: NodeWithChildren) => unknown  | NO       | Android iOS | Yes               |
| ignoredDomTags                         | A list of lowercase tags which should not be included in the DOM.                                                                                                                                                 | Array<string>                                      | NO       | Android iOS | Yes               |
| ignoredStyles                          | Blacklist specific inline CSS style properties and allow the others.                                                                                                                                              | CSSPropertyNameList                                | NO       | Android iOS | Yes               |
| bypassAnonymousTPhrasingNodes          | The most simple one is that itsimplifies the render tree                                                                                                                                                          | boolean                                            | NO       | Android iOS | Yes               |
| onDocumentMetadataLoaded               | Handler invoked when the document metadata is available. It will re-trigger on HTML content changes.                                                                                                              | (documentMetadata: DocumentMetadata) => void       | NO       | Android iOS | Yes               |
| onHTMLLoaded                           | Triggered when HTML is available to the RenderHTML component.                                                                                                                                                     | (html: string) => void                             | NO       | Android iOS | Yes               |
| onTTreeChange                          | Triggered when the transient render tree changes. Useful for debugging.                                                                                                                                           | (ttree: TDocument) => void                         | NO       | Android iOS | Yes               |
| renderers                              | Your custom renderers.                                                                                                                                                                                            | CustomTagRendererRecor                             | NO       | Android iOS | Yes               |
| selectDomRoot                          | Select the DOM root before TTree generation. For example, you could iterate over children until you reach an article element and return this element.                                                             | TRenderEngineOptions                               | NO       | Android iOS | Yes               |
| setMarkersForTNode                     | Set custom markers from a TNode and all its descendants. Markers will be accessible in custom renderers via `tnode.markers` prop.                                                                                 | SetMarkersForTNode                                 | NO       | Android iOS | Yes               |
| source                                 | The object source to render (either { uri }, { html } or { dom }).                                                                                                                                                | HTMLSource                                         | Yes      | Android iOS | Yes               |
| renderersProps                         | Props to use in custom renderers with useRendererProps.                                                                                                                                                           | Partial<RenderersProps>                            | NO       | Android iOS | Yes               |
| systemFonts                            | A list of fonts available in the current platform. These fonts will be used to select the first match in CSS `fontFamily` property, which supports a comma-separated list of fonts. By default, a handful of fonts are selected per platform. | Array<string>                                      | No       | Android iOS | Yes               |
| tagsStyles                             | Provide mixed styles to target HTML tag names.                                                                                                                                                                    | Readonly<Record<string, MixedStyleDeclaration>>    | NO       | Android iOS | Yes               |

## Known Issues

## Others

- [ ] img 的宽度不会随着 contentWidth 的动态修改而更改,接口属性原库本身不支持（与iOS/Android表现一致）（由 RN 基座引起，RNImage 组件更新状态时 this.descriptorWrapper 没有重新赋值） [issue#638](https://github.com/meliorence/react-native-render-html/issues/638)

## License

This project is licensed under [The MIT License (MIT)](https://github.com/meliorence/react-native-render-html/blob/master/LICENSE).
