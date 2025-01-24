> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>JsBarCode</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lindell/JsBarcode/blob/master/MIT-LICENSE.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/lindell/JsBarcode)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install jsbarcode@3.11.6 --save
```

#### **yarn**

```bash
yarn add jsbarcode@3.11.6
```

<!-- tabs:end -->

quick-access：

```bash
import JsBarCode from 'jsbarcode';
```

> [!WARNING] The name of the imported repository remains unchanged.

The following code shows the basic use scenario of the repository:

### **With svg**

> [!TIP] The jsbarcode library depends on the react-native-svg library to display barcodes. Currently, only some properties of the svg library are supported on HarmonyOS. For details, see the [react-native-svg](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-svg.md) library.

```tsx
import {ScrollView, StyleSheet, View, Text} from 'react-native';
import {Barcode} from './component/SvgComponent';
import {useState} from 'react';

export default function JsbarcodeSvgDemo() {

  return (
    <ScrollView>
      <View style={styles.container}>
        <Text style={styles.testStyle}>format和background：'red'</Text>
        <Barcode
          value="123456789999"
          options={{format: 'UPC', background: 'red'}}
        />
        <Text style={styles.testStyle}>
          format: 'EAN13', background: 'yellow'
        </Text>
        <Barcode
          value="9501101530003"
          options={{format: 'EAN13', background: 'yellow'}}
        />
        <Text style={styles.testStyle}>
          format: 'CODE128', background: 'pink'
        </Text>
        <Barcode
          value="7895641245"
          options={{format: 'CODE128', background: 'pink'}}
        />
        <Text style={styles.testStyle}>width和height</Text>
        <Barcode
          value="1234568999999"
          options={{format: 'CODE128', width: 1, height: 150}}
        />
        <Barcode
          value="7895641245"
          options={{format: 'CODE128', width: 3, height: 30}}
        />
        <Text style={styles.testStyle}>Text</Text>
        <Barcode
          value="1234568999999"
          options={{format: 'CODE128', text: 'hello!'}}
        />
        <Text style={styles.testStyle}>fontOptions:bold</Text>
        <Barcode
          value="9501101530003"
          options={{format: 'EAN13', fontOptions: 'bold'}}
        />
        <Text style={styles.testStyle}>fontOptions:'bold italic'</Text>
        <Barcode
          value="9501101530003"
          options={{format: 'EAN13', fontOptions: 'bold italic'}}
        />
        <Text style={styles.testStyle}>fontOptions:'italic'</Text>
        <Barcode
          value="9501101530003"
          options={{format: 'EAN13', fontOptions: 'italic'}}
        />
        <Text style={styles.testStyle}>font</Text>
        <Barcode value="Fantasy font" options={{format: 'CODE128', font: 'fantasy'}} />
        <Text style={styles.testStyle}>displayValue</Text>
        <Barcode
          value="1234568999999"
          options={{format: 'CODE128', displayValue: false}}
        />
        <Text style={styles.testStyle}>textAlign</Text>
        <Barcode
          value="1234568999999"
          options={{format: 'CODE128', textAlign: 'left'}}
        />
        <Text style={styles.testStyle}>textPosition</Text>
        <Barcode
          value="1234568999999"
          options={{format: 'CODE128', textPosition: 'top'}}
        />
        <Text style={styles.testStyle}>textMargin</Text>
        <Barcode
          value="1234568999999"
          options={{format: 'CODE128', textMargin: 10}}
        />
        <Text style={styles.testStyle}>fontSize</Text>
        <Barcode
          value="1234568999999"
          options={{format: 'CODE128', fontSize: 40}}
        />
        <Text style={styles.testStyle}>lineColor</Text>
        <Barcode
          value="1234568999999"
          options={{format: 'CODE128', lineColor: '#990000'}}
        />
        <Text style={styles.testStyle}>margins</Text>
        <Barcode
          value="1234568956999"
          options={{format: 'CODE128', marginLeft: 30, marginTop: 50}}
        />
        <Text style={styles.testStyle}>flat: false</Text>
        <Barcode
          value="29012343"
          options={{format: 'EAN8', flat: false}}
        />
        <Text style={styles.testStyle}>flat: true</Text>
        <Barcode
          value="29012343"
          options={{format: 'EAN8', flat: true}}
        />
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'column',
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  testStyle: {
    fontWeight: '600',
  },
});
```

### **With Canvas**

> [!TIP] The react-native-canvas library is not supported on HarmonyOS yet and cannot be rendered using **Canvas**. The following usage is for reference only.

```js
var JsBarcode = require("jsbarcode");

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

Here is an example of using Options:

```js
// format
JsBarcode("#barcode", "123456789012", {
  format: "EAN13",
});
JsBarcode("#barcode", "123456789012", {
  format: "CODE39",
});

// width
JsBarcode("#barcode", "Wider barcode", {
  width: 3,
});

// height
JsBarcode("#barcode", "Tall barcode", {
  height: 150,
});

// Text
JsBarcode("#barcode", "Hello", {
  text: "Hi!",
});

// fontOptions
JsBarcode("#barcode", "Bold text", {
  fontOptions: "bold",
});

// font
JsBarcode("#barcode", "Fantasy font", {
  font: "fantasy",
});

// textAlign
JsBarcode("#barcode", "Left text", {
  textAlign: "left",
});

// textPosition
JsBarcode("#barcode", "Top text", {
  textPosition: "top",
});

// textMargin
JsBarcode("#barcode", "Text margin", {
  textMargin: 25,
});

// fontSize
JsBarcode("#barcode", "Bigger text", {
  fontSize: 40,
});

// background
JsBarcode("#barcode", "Blue background", {
  background: "#ccffff",
});

// lineColor
JsBarcode("#barcode", "Red lines", {
  lineColor: "#990000",
});

// margins
JsBarcode("#barcode", "Bigger margins", {
  margin: 30,
  background: "#dddddd",
});

JsBarcode("#barcode", "Left/Top margin", {
  marginLeft: 30,
  marginTop: 50,
  background: "#dddddd",
});

// flat
JsBarcode("#barcode", "29012343", {
  format: "EAN8",
  flat: false,
});

JsBarcode("#barcode", "29012343", {
  format: "EAN8",
  flat: true,
});
```
## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## **All Options**

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name         | Description       | Type               | Required | HarmonyOS Support | Remark                                                       |
| ------------ | ----------------- | ------------------ | -------- | ----------------- | ------------------------------------------------------------ |
| format       | "auto" (CODE128)  | String             | no       | yes               |                                                              |
| width        | 2                 | Number             | no       | yes               |                                                              |
| height       | 100               | Number             | no       | yes               |                                                              |
| displayValue | true              | Boolean            | no       | yes               |                                                              |
| text         | undefined         | String             | no       | yes               |                                                              |
| fontOptions  | ""                | String             | no       | yes               | Currently, the react-native-svg library does not support **fontOptions: 'italic'**. As a result, the barcode effect does not take effect. |
| font         | "monospace"       | String             | no       | yes               | Currently, the react-native-svg library does not support **font**. As a result, the barcode effect does not take effect. |
| textAlign    | "center"          | String             | no       | yes               |                                                              |
| textPosition | "bottom"          | String             | no       | yes               |                                                              |
| textMargin   | 2                 | Number             | no       | yes               |                                                              |
| fontSize     | 20                | Number             | no       | yes               |                                                              |
| background   | "#ffffff"         | String (CSS color) | no       | yes               |                                                              |
| lineColor    | "#000000"         | String (CSS color) | no       | yes               |                                                              |
| margin       | 10                | Number             | no       | yes               |                                                              |
| marginTop    | undefined         | Number             | no       | yes               |                                                              |
| marginBottom | undefined         | Number             | no       | yes               |                                                              |
| marginLeft   | undefined         | Number             | no       | yes               |                                                              |
| marginRight  | undefined         | Number             | no       | yes               |                                                              |
| flat         | false             | Boolean            | no       | yes               | Only the EAN8 or EAN13 format is supported.                  |
| valid        | function(valid){} | Function           | no       | yes               |                                                              |

## Known Issues

The jsbarcode library depends on the react-native-svg library to display barcodes. Currently, only some properties of the svg library are supported on HarmonyOS. Therefore, the barcode position displayed on HarmonyOS is incorrect, and the font size is small.

## Others

## License

This project is licensed under [MIT License](https://github.com/lindell/JsBarcode/blob/master/MIT-LICENSE.txt).