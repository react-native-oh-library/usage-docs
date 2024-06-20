> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>parse5</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/TehShrike/deepmerge/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/inikulin/parse5)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install parse5@7.1.2
```

#### **yarn**

```bash
yarn add parse5@7.1.2
```

<!-- tabs:end -->

直接使用：

<!-- {% raw %} -->
```js
const parse5 = require("parse5");

// parse
const document = parse5.parse(
  "<!DOCTYPE html><html><head></head><body>Hi there!</body></html>",
);
console.log(document.childNodes[1].tagName); //> 'html'

// parseFragment
const documentFragment = parse5.parseFragment("<table></table>");
console.log(documentFragment.childNodes[0].tagName); //> 'table'
const trFragment = parse5.parseFragment(
  documentFragment.childNodes[0],
  "<tr><td>Shake it, baby</td></tr>",
);
console.log(trFragment.childNodes[0].childNodes[0].tagName); //> 'td'

// serialize
const document = parse5.parse(
  "<!DOCTYPE html><html><head></head><body>Hi there!</body></html>",
);
// Serializes a document.
const html = parse5.serialize(document);
// Serializes the <html> element content.
const str = parse5.serialize(document.childNodes[1]);
console.log(str); //> '<head></head><body>Hi there!</body>'

// serializeOuter
const document = parse5.parseFragment("<div>Hello, <b>world</b>!</div>");
// Serializes the <div> element.
const str = parse5.serializeOuter(document.childNodes[0]);
console.log(str); //> '<div>Hello, <b>world</b>!</div>'
```
<!-- {% endraw %} -->

## 约束与限制

### 兼容性

在下述版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [parse5文档地址](https://parse5.js.org/index.html)

| Name                                           | Description                                                                   | Type     | Required | HarmonyOS Support |
| ---------------------------------------------- | ----------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| parse(html, options?)                          | Parses an HTML string.                                                        | function | no       | yes               |
| parseFragment(fragmentContext, html, options?) | Parses an HTML fragment.                                                      | function | no       | yes               |
| serialize(node, options?)                      | Serializes an AST node to an HTML string.                                     | function | no       | yes               |
| serializeOuter(node, options?)                 | Serializes an AST element node to an HTML string, including the element node. | function | no       | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/inikulin/parse5/blob/master/LICENSE) ，请自由地享受和参与开源。
