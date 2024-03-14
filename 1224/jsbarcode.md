> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>JsBarCode</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lindell/JsBarcode/blob/master/MIT-LICENSE.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/lindell/JsBarcode)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install jsbarcode --save@3.11.6
```

#### **yarn**

```bash
yarn add jsbarcode@3.11.6
```

<!-- tabs:end -->

快速使用：

```bash
import JsBarCode from 'jsbarcode';
```

>[!WARNING] 使用时 import 的库名不变。

下面的代码展示了这个库的基本使用示例：

### **With canvas:**
```js
var JsBarcode = require('jsbarcode');

// Canvas v1
var Canvas = require("canvas");
// Canvas v2
var { createCanvas } = require("canvas");

// Canvas v1
var canvas = new Canvas();
// Canvas v2
var canvas = createCanvas();

JsBarcode(canvas, "Hello");
```

### **With svg:**

```js
const { DOMImplementation, XMLSerializer } = require('xmldom');
const xmlSerializer = new XMLSerializer();
const document = new DOMImplementation().createDocument('http://www.w3.org/1999/xhtml', 'html', null);
const svgNode = document.createElementNS('http://www.w3.org/2000/svg', 'svg');

JsBarcode(svgNode, 'test', {
    xmlDocument: document,
});

const svgText = xmlSerializer.serializeToString(svgNode);
```

如下是Options示例展示:

```js
// format
JsBarcode("#barcode", "123456789012", {
  format: "EAN13"
});
JsBarcode("#barcode", "123456789012", {
  format: "CODE39"
});

// width
JsBarcode("#barcode", "Wider barcode", {
  width: 3
});

// height
JsBarcode("#barcode", "Tall barcode", {
  height: 150
});

// Text
JsBarcode("#barcode", "Hello", {
  text: "Hi!"
});

// fontOptions
JsBarcode("#barcode", "Bold text", {
  fontOptions: "bold"
});

JsBarcode("#barcode", "Italic text", {
  fontOptions: "italic"
});

JsBarcode("#barcode", "Both options", {
  fontOptions: "bold italic"
});

// font
JsBarcode("#barcode", "Fantasy font", {
  font: "fantasy"
});

 // textAlign
 JsBarcode("#barcode", "Left text", {
  textAlign: "left"
});

 // textPosition
 JsBarcode("#barcode", "Top text", {
  textPosition: "top"
});

// textMargin
JsBarcode("#barcode", "Text margin", {
  textMargin: 25
});

// fontSize
JsBarcode("#barcode", "Bigger text", {
  fontSize: 40
});

// background
JsBarcode("#barcode", "Blue background", {
  background: "#ccffff"
});

// lineColor
JsBarcode("#barcode", "Red lines", {
  lineColor: "#990000"
});

// margins
JsBarcode("#barcode", "Bigger margins", {
  margin: 30,
  background: "#dddddd"
});

JsBarcode("#barcode", "Left/Top margin", {
  marginLeft: 30,
  marginTop: 50,
  background: "#dddddd"
});

// flat
JsBarcode("#barcode", "29012343", {
  format: "EAN8",
  flat: false
});

JsBarcode("#barcode", "29012343", {
  format: "EAN8",
  flat: true
});

```
#### **Options**

| **Option**   | **Default value** | **Type**           |
| ------------ | ----------------- | ------------------ |
| format       | "auto" (CODE128)  | String             |
| width        | 2                 | Number             |
| height       | 100               | Number             |
| displayValue | true              | Boolean            |
| text         | undefined         | String             |
| fontOptions  | ""                | String             |
| font         | "monospace"       | String             |
| textAlign    | "center"          | String             |
| textPosition | "bottom"          | String             |
| textMargin   | 2                 | Number             |
| fontSize     | 20                | Number             |
| background   | "#ffffff"         | String (CSS color) |
| lineColor    | "#000000"         | String (CSS color) |
| margin       | 10                | Number             |
| marginTop    | undefined         | Number             |
| marginBottom | undefined         | Number             |
| marginLeft   | undefined         | Number             |
| marginRight  | undefined         | Number             |
| flat         | false             | Boolean            |
| valid        | function(valid){} | Function           |


## 其他

## 开源协议