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

### **With svg:**
> [!tip] [jsbarcode库依赖react-native-svg库进行条形码展示, svg 当前仅实现部分属性，其余还未实现鸿蒙化]
> [!tip] [详见react-native-svg](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg.md)
```js
import { useMemo } from 'react';
import JsBarcode from 'jsbarcode';
import { SvgXml } from 'react-native-svg';
import { DOMImplementation, XMLSerializer } from 'xmldom';

export const Barcode = (props: Props) => {
  const [jsbarcodeInfo, setJsbarcodeInfo] = useState('');
  const {
    width ,
    height,
    format,
    ... // options
  } = props.options;

  const svgText = useMemo(() => {
    const document = new DOMImplementation().createDocument(null, 'html');
    const svgNode = document.createElementNS(null, 'svg');

    JsBarcode(svgNode, props.value, {
      xmlDocument: document,
      width,
      height,
      format,
      ... // options
    });

    svgNode.removeAttribute('style')
    setJsbarcodeInfo(new XMLSerializer().serializeToString(svgNode));

    return new XMLSerializer().serializeToString(svgNode);
  }, [props]);

  return <SvgXml xml={svgText} />;
};

// 页面展示条形码
import { Barcode } from 'XXXX';
function JsbarcodeSvgDemo() {
  return (
    <Barcode
      value="9501101530003"
      options={{format: 'EAN13', background: 'yellow'}}
    />
  )
}
```

### **With canvas:**
> [!tip] [react-native-canvas库暂未鸿蒙化，当前无法使用canvas渲染，下面用法仅供参考]

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

如下是Options使用示例展示:

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
#### **All Options**
> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name         | Description       | Type               | Required | HarmonyOS Support | Remark                                                                |
| ------------ | ----------------- | ------------------ | -------- | ----------------- | --------------------------------------------------------------------- |
| format       | "auto" (CODE128)  | String             | no       | yes               |                                                                       |
| width        | 2                 | Number             | no       | yes               |                                                                       |
| height       | 100               | Number             | no       | yes               |                                                                       |
| displayValue | true              | Boolean            | no       | yes               |                                                                       |
| text         | undefined         | String             | no       | yes               |                                                                       |
| fontOptions  | ""                | String             | no       | yes               | react-native-svg目前不支持fontOptions: 'italic'，导致条形码效果不生效    |
| font         | "monospace"       | String             | no       | yes               | react-native-svg目前不支持font设置，导致条形码效果不生效                 |
| textAlign    | "center"          | String             | no       | yes               |                                                                       |
| textPosition | "bottom"          | String             | no       | yes               |                                                                       |
| textMargin   | 2                 | Number             | no       | yes               |                                                                       |
| fontSize     | 20                | Number             | no       | yes               |                                                                       |
| background   | "#ffffff"         | String (CSS color) | no       | yes               |                                                                       |
| lineColor    | "#000000"         | String (CSS color) | no       | yes               |                                                                       |
| margin       | 10                | Number             | no       | yes               |                                                                       |
| marginTop    | undefined         | Number             | no       | yes               |                                                                       |
| marginBottom | undefined         | Number             | no       | yes               |                                                                       |
| marginLeft   | undefined         | Number             | no       | yes               |                                                                       |
| marginRight  | undefined         | Number             | no       | yes               |                                                                       |
| flat         | false             | Boolean            | no       | yes               | 仅支持format：EAN8/EAN13                                               |
| valid        | function(valid){} | Function           | no       | yes               |                                                                       |

## 遗留问题
jsbarcode库依赖react-native-svg库进行条形码展示, 因svg 当前仅实现部分属性，其余还未实现鸿蒙化，目前在HarmonyOS上条形码的文本位置效果不对，fontSize显示比较小。

## 其他

## 开源协议