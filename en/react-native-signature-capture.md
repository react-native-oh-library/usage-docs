> Template version: v0.2.2

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



> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-signature-capture)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-library/react-native-signature-capture Releases](https://github.com/react-native-oh-library/react-native-signature-capture/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



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

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

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

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1.Open `entry/oh-package.json5` file and add the following dependencies:

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

 

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-signature-capture": "file:../../node_modules/@react-native-oh-tpl/react-native-signature-capture/harmony/rnoh_signature_capture.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing SignatureCaptureArkView Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

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

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.  

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ SignatureCaptureArkView.NAME
  ];
```

### 4. Introducing SignatureCapturePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-signature-capture Releases](https://github.com/react-native-oh-library/react-native-signature-capture/releases)

   
## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


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

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name       | Description                                                                                         | Type     | Required | Platform    | HarmonyOS Support |
|------------|-----------------------------------------------------------------------------------------------------|----------|----------|-------------|-------------------|
| saveImage  | when called it will save the image and returns the base 64 encoded string on onSaveEvent() callback | function | no       | iOS/Android | yes               |
| resetImage | when called it will clear the image on the canvas                                                   | function | no       | iOS/Android | yes               |


## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/RepairShopr/react-native-signature-capture/blob/master/LICENSE).

