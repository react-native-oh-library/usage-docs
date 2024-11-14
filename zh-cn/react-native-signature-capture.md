> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-signature-capture</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/RepairShopr/react-native-signature-capture">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/RepairShopr/react-native-signature-capture/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-signature-capture)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-signature-capture Releases](https://github.com/react-native-oh-library/react-native-signature-capture/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：


<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-signature-capture
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-signature-capture
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
var React = require('react');
var ReactNative = require('react-native');

var {Component} = React;

var {
    AppRegistry,
    StyleSheet,
    Text,
    View, TouchableHighlight
} = ReactNative;

import SignatureCapture from 'react-native-signature-capture';

class RNSignatureExample extends Component {
    render() {
        return (
            <View style={{ flex: 1, flexDirection: "column" }}>
                <Text style={{alignItems:"center",justifyContent:"center"}}>Signature Capture Extended </Text>
                <SignatureCapture
                    style={[{flex:1},styles.signature]}
                    ref="sign"
                    onSaveEvent={this._onSaveEvent}
                    onDragEvent={this._onDragEvent}
                    saveImageFileInExtStorage={false}
                    showNativeButtons={false}
                    showTitleLabel={false}
                    backgroundColor="#ff00ff"
                    strokeColor="#ffffff"
                    minStrokeWidth={4}
                    maxStrokeWidth={4}
                    viewMode={"portrait"}/>

                <View style={{ flex: 1, flexDirection: "row" }}>
                    <TouchableHighlight style={styles.buttonStyle}
                        onPress={() => { this.saveSign() } } >
                        <Text>Save</Text>
                    </TouchableHighlight>

                    <TouchableHighlight style={styles.buttonStyle}
                        onPress={() => { this.resetSign() } } >
                        <Text>Reset</Text>
                    </TouchableHighlight>

                </View>

            </View>
        );
    }

    saveSign() {
        this.refs["sign"].saveImage();
    }

    resetSign() {
        this.refs["sign"].resetImage();
    }

    _onSaveEvent(result) {
        //result.encoded - for the base64 encoded png
        //result.pathName - for the file path name
        console.log(result);
    }
    _onDragEvent() {
         // This callback will be called when the user enters signature
        console.log("dragged");
    }
}

const styles = StyleSheet.create({
    signature: {
        flex: 1,
        borderColor: '#000033',
        borderWidth: 1,
    },
    buttonStyle: {
        flex: 1, justifyContent: "center", alignItems: "center", height: 50,
        backgroundColor: "#eeeeee",
        margin: 10
    }
});

AppRegistry.registerComponent('RNSignatureExample', () => RNSignatureExample);


```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入 (推荐)

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-signature-capture": "file:../../node_modules/@react-native-oh-tpl/react-native-signature-capture/harmony/rnoh_signature_capture.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.在 ArkTs 侧引入 SignatureCaptureArkView 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { SignatureCaptureArkView } from '@react-native-oh-tpl/react-native-signature-capture'

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+    if (ctx.componentName === SignatureCaptureArkView.NAME) {
+      SignatureCaptureArkView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ SignatureCaptureArkView.NAME
  ];
```

### 4.在 ArkTs 侧引入 SignatureCapturePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { SignatureCapturePackage } from '@react-native-oh-tpl/react-native-signature-capture/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SignatureCapturePackage(ctx)
  ];
}
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-signature-capture Releases](https://github.com/react-native-oh-library/react-native-signature-capture/releases)

   
## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name                                                              | Description                                                                                                                                                                     | Type                      | Required | Platform    | HarmonyOS Support |
|-------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------|----------|-------------|-------------------|
| showBorder                                                        | If this props is made to false, it will hide the dashed border.                                                                                                                 | boolean                   | no       | iOS         | yes               |
| showNativeButtons                                                 | If this props is made to true, it will display the native buttons "Save" and "Reset"..                                                                                          | boolean                   | no       | iOS/Android | yes               |
| showTitleLabel                                                    | If this props is made to true, it will display the "x_ _ _ _ _ _ _ _ _ _ _" placeholder indicating where to sign.                                                               | boolean                   | no       | iOS         | yes               |
| viewMode                                                          | "portrait" or "landscape" change the screen orientation based on boolean value                                                                                                  | "portrait" \| "landscape" | no       | iOS/Android | yes               |
| maxSize                                                           | sets the max size of the image maintains aspect ratio, default is 500                                                                                                           | number                    | no       | iOS/Android | yes               |
| minStrokeWidth                                                    | sets the min stroke line width                                                                                                                                                  | number                    | no       | Android     | yes               |
| maxStrokeWidth                                                    | sets the max stroke line width                                                                                                                                                  | number                    | no       | Android     | yes               |
| backgroundColor                                                   | Sets the background color of the component. Defaults to white. May be 'transparent'.                                                                                            | color                     | no       | iOS/Android | yes               |
| strokeColor                                                       | Sets the color of the signature. Defaults to black.                                                                                                                             | color                     | no       | iOS/Android | yes               |
| saveImageFileInExtStorage                                         | Make this props true, if you want to save the image file in external storage. Default is false. Warning: Image file will be visible in gallery or any other image browsing app. | boolean                   | no       | Android     | no                |
| onSaveEvent: (event: {pathName: string, encoded: string}) => void | Triggered when saveImage() is called, which return Base64 Encoded String and image file path.                                                                                   | function                  | no       | iOS/Android | yes               |
| onDragEvent: (event: boolean) => void                             | Triggered when user marks his signature on the canvas. This will not be called when the user does not perform any action on canvas.                                             | function                  | no       | iOS/Android | yes               |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name       | Description                                                                                         | Type     | Required | Platform    | HarmonyOS Support |
|------------|-----------------------------------------------------------------------------------------------------|----------|----------|-------------|-------------------|
| saveImage  | when called it will save the image and returns the base 64 encoded string on onSaveEvent() callback | function | no       | iOS/Android | yes               |
| resetImage | when called it will clear the image on the canvas                                                   | function | no       | iOS/Android | yes               |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/RepairShopr/react-native-signature-capture/blob/master/LICENSE) ，请自由地享受和参与开源。

