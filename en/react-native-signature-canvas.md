> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-signature-canvas</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/YanYuanFE/react-native-signature-canvas">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/YanYuanFE/react-native-signature-canvas/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/YanYuanFE/react-native-signature-canvas)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install --save react-native-signature-canvas@4.7.2
```

#### **yarn**

```bash
yarn add react-native-signature-canvas@4.7.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { StyleSheet, Text, View, Image } from "react-native";
import Signature from "react-native-signature-canvas";

export const SignatureScreen = () => {
  const [signature, setSign] = useState(null);

  const handleOK = (signature) => {
    console.log(signature);
    setSign(signature);
  };

  const handleEmpty = () => {
    console.log("Empty");
  };

  const style = `.m-signature-pad--footer
    .button {
      background-color: red;
      color: #FFF;
    }`;
  return (
    <View style={{ flex: 1 }}>
      <View style={styles.preview}>
        {signature ? (
          <Image
            resizeMode={"contain"}
            style={{ width: 335, height: 114 }}
            source={{ uri: signature }}
          />
        ) : null}
      </View>
      <Signature
        onOK={handleOK}
        onEmpty={handleEmpty}
        descriptionText="Sign"
        clearText="Clear"
        confirmText="Save"
        webStyle={style}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  preview: {
    width: 335,
    height: 114,
    backgroundColor: "#F8F8F8",
    justifyContent: "center",
    alignItems: "center",
    marginTop: 15,
  },
  previewText: {
    color: "#FFF",
    fontSize: 14,
    height: 40,
    lineHeight: 40,
    paddingLeft: 10,
    paddingRight: 10,
    backgroundColor: "#69B2FF",
    width: 120,
    textAlign: "center",
    marginTop: 10,
  },
});
```
## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-webview的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-webview 文档](/zh-cn/react-native-webview.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM:3.0.0.25;

## 属性

### SignatureScreen 

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。



| Name            | Description     | Type                                                                                                                     | Required | Platform | HarmonyOS Support    | 
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | 
| autoClear  | should auto clear the signature after clicking the Confirm button  |boolean| no   | iOS/Android       | yes | 
| backgroundColor            | default is "rgba(255,255,255,0)" (transparent), background color of the canvas |string| no   | iOS/Android       | yes | 
| bgHeight            | 	height of the background image  |number| no   | iOS/Android       | yes | 
| bgWidth            |width of the background image |number| no   | iOS/Android       | yes | 
| bgSrc            |	background image source uri (url) |string| no   | iOS/Android       | yes | 
| clearText            |clear button text|string| no   | iOS/Android       | yes | 
| confirmText            |save button text |string| no   | iOS/Android       | yes | 
| customHtml            |html string that lets you modify things like the layout or elements |(injectedJavaScript: string) => string| no   | iOS/Android       | yes | 
| dataURL            |default is "", Base64 string, draws saved signature from dataURL. |string| no   | iOS/Android       | yes | 
| descriptionText            |description text for signature |string| no   | iOS/Android       | yes | 
| dotSize            |radius of a single dot (not stroke width) |number| no   | iOS/Android       | yes | 
| imageType            |"image/png" (default), "image/jpeg"、"image/svg+xml", imageType of exported signature|string| no   | iOS/Android       | yes | 
| minWidth            |minimum width of a line. Defaults to 0.5 |number| no   | iOS/Android       | yes | 
| maxWidth            |maximum width of a line. Defaults to 2.5 |number| no   | iOS/Android       | yes | 
| onOK            |callback function after saving non-empty signature|function| no   | iOS/Android       | yes | 
| onEmpty            |callback function after trying to save an empty signature|function| no   | iOS/Android       | yes | 
| onClear            |callback function after clearing the signature|function| no   | iOS/Android       | yes | 
| onGetData            |callback function when getData() is called |function| no   | iOS/Android       | yes | 
| onBegin            |callback function when a new stroke is started |function| no   | iOS/Android       | yes | 
| onEnd            |callback function when the stroke has ended |function| no   | iOS/Android       | yes | 
| onLoadEnd            |callback function when the webview canvas load ended |function| no   | iOS/Android       | yes | 
| onUndo            |callback function when undo() is called |function| no   | iOS/Android       | yes | 
| onRedo	            |callback function when redo() is called |function| no   | iOS/Android       | yes | 
| onDraw            |callback function when drawing is enabled |function| no   | iOS/Android       | yes | 
| onErase            |callback function when erasing is enabled |function| no   | iOS/Android       | yes | 
| onChangePenColor            |callback function after changing the pen color|function| no   | iOS/Android       | yes | 
| onChangePenSize            |callback function after changing the pen size |function| no   | iOS/Android       | yes | 
| overlayHeight            |height of the overlay image |number| no   | iOS/Android       | yes | 
| overlayWidth            |width of the overlay image |number| no   | iOS/Android       | yes | 
| overlaySrc            |overlay image source uri (url) must be .png with a transparent background |string| no   | iOS/Android       | yes | 
| penColor            |default is "black", color of pen|string| no   | iOS/Android       | yes | 
| rotated            |rotate signature pad 90 degrees |boolean| no   | iOS/Android       | yes | 
| style            |style of wrapper view|object| no   | iOS/Android       | yes | 
| trimWhitespace           |trim image whitespace|boolean| no   | iOS/Android       | yes | 
| webStyle            |webview style for overwrite default style, all style: https://github.com/YanYuanFE/react-native-signature-canvas/blob/master/h5/css/signature-pad.css |string| no   | iOS/Android       | yes | 
| androidLayerType            |Sets the android webview layerType |none、software、hardware| no   | Android       | no | 
| androidHardwareAccelerationDisabled           |androidHardwareAccelerationDisabled for react-native-webview. Default is false |boolean| no   | Android       | no | 
| showsVerticalScrollIndicator            |Boolean value that determines whether a vertical scroll indicator is shown in the WebView, The default value is true.|boolean| no   | iOS/Android       | no | 
| nestedScrollEnabled            |enable nested scrolling for use inside of a scrollview|boolean| no   | no      | no | 




## 静态方法


> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。



| Name            | Description     | Type                                                                                                                     | Required | Platform | HarmonyOS Support    | 
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | 
| clearSignature  |Clear the current signature  |function| no   | iOS/Android       | yes | 
| changePenColor  |Change pen color |function| no   | iOS/Android       | yes | 
| changePenSize |Change pen size  |function| no   | iOS/Android       | yes | 
| draw  |Enable drawing signature  |function| no   | iOS/Android       | yes | 
| erase  |Enable erasing signature  |function| no   | iOS/Android       | yes | 
| getData  |riggers the onGetData callback with a single data JSON string  |function| no   | iOS/Android       | yes | 
| readSignature  |Reads the current signature on the canvas and triggers either the onOK or onEmpty callbacks  |function| no   | iOS/Android       | yes | 
| undo  |Undo last stroke  |function| no   | iOS/Android       | yes | 
| redo  |Redo last stroke |function| no   | iOS/Android       | yes | 



## 遗留问题
- [ ] showsVerticalScrollIndicator属性不生效: [issue#137](https://github.com/react-native-oh-library/react-native-webview/issues/137)

## 其他

 1、minDistance属性版本问题: 此属性在4.7.3版本生效，npm包最新版本为4.7.2，如需使用，请从[Github](https://github.com/YanYuanFE/react-native-signature-canvas)下载最新代码使用；

 2、nestedScrollEnabled属性在 iOS,Android 不生效，harmonyOS与其表现一致；[issue#363](https://github.com/YanYuanFE/react-native-signature-canvas/issues/363)


## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/YanYuanFE/react-native-signature-canvas/blob/master/LICENSE) ，请自由地享受和参与开源。
