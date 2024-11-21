> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-qr-decode-image-camera</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/deepanrajkumar/react-native-qr-decode-image-camera">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/deepanrajkumar/react-native-qr-decode-image-camera/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-qr-decode-image-camera Releases](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-qr-decode-image-camera
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-qr-decode-image-camera
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

> In the example: The launchImageLibrary method requires the introduction of the react-native-image-picker library for Harmony OS,Navigate to [react-native-image-picker](/zh-cn/react-native-image-picker.md)to view the usage instructions.

QRreader

```js
import React, {useState} from 'react';
import {Button, View, Text} from 'react-native';
import {QRreader} from 'react-native-qr-decode-image-camera';
import {launchImageLibrary} from 'react-native-image-picker';

export const qrExample = () => {
  const [reader, setReader] = useState<any>('');
  return (
    <View style={{flex: 1, justifyContent: 'center', alignItems: 'center'}}>
      <Button
        onPress={() => {
          launchImageLibrary({mediaType: 'photo', selectionLimit: 1}, data => {
            if (data.assets?.length) {
              const path = {
                uri: data.assets[0].originalPath,
              };
              QRreader(path)
                .then(res => {
                  setReader(res?.[0]?.originalValue);
                })
                .catch(error => {
                  console.log(error);
                });
            }
          });
        }}
        title="Click to select a QR code photo"
      />
      <Text style={{fontSize: 20}}>{reader}</Text>
    </View>
  );
};
```
QRscanner

```json
import React, {useState} from 'react';
import { View, Text, TouchableOpacity, StyleSheet} from 'react-native';
import { QRscanner} from 'react-native-qr-decode-image-camera';


export const qrExample = () => {

  const [flashMode, setflashMode] = useState(false);
  const onRead = res => {
    console.log(res);
  };
  return (
    <View style={styles.container}>
      <QRscanner
        onRead={onRead}
        renderBottomView={() => {
          return (
            <View
              style={{
                flex: 1,
                flexDirection: 'row',
                backgroundColor: '#0000004D',
              }}>
              <TouchableOpacity
                style={{
                  flex: 1,
                  alignItems: 'center',
                  justifyContent: 'center',
                }}
                onPress={() => {
                  if (flashMode) {
                    setflashMode(false);
                  } else {
                    setflashMode(true);
                  }
                }}>
                <Text style={{color: '#fff'}}>flashMode</Text>
              </TouchableOpacity>
            </View>
          );
        }}
        flashMode={flashMode}
        finderY={50}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#000',
  },
});
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-vision-camera. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in @react-native-oh-tpl/react-native-vision-camera to add it to your project.

## 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

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
    "@react-native-oh-tpl/react-native-qr-decode-image-camera": "file:../../node_modules/@react-native-oh-tpl/react-native-qr-decode-image-camera/harmony/qr_decode_image_camera.har"
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

### 3. Introducing RNQrDecodeImageCameraPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:


```diff
  ...
+ import {RNQrDecodeImageCameraPackage} from '@react-native-oh-tpl/react-native-qr-decode-image-camera/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNQrDecodeImageCameraPackage(ctx)
  ];
}
```

### 4. Introducing NativeScan Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { NativeScan } from "@react-native-oh-tpl/react-native-qr-decode-image-camera"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === NativeScan.NAME) {
+   NativeScan({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-qr-decode-image-camera](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera/releases)


## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

 | Name | Description | Type | Required | Platform | HarmonyOS Support |
 | ----------------------------- | ---------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
 | QRreader | Invoke this method to invoke the gallery, select the QR code image for image decoding, and asynchronously return the result. | funtion | no | iOS/Android | yes |

## Properties

### QRscanner

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                                      | Type    | Required | Platform    | HarmonyOS Support |
| ------------------ | ------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| isRepeatScan       | whether to allow repeated scanning               | boolean | no       | iOS/Android | yes               |
| zoom               | Camera focal length range 0-1                    | number  | no       | iOS/Android | no                |
| flashMode          | Turn on the flashlight                           | boolean | no       | iOS/Android | yes               |
| onRead             | scan callback                                    | funtion | yes      | iOS/Android | yes               |
| maskColor          | mask layer color                                 | string  | no       | iOS/Android | yes               |
| borderColor        | border color                                     | string  | no       | iOS/Android | yes               |
| cornerColor        | Color of corner of scan frame                    | string  | no       | iOS/Android | yes               |
| borderWidth        | border width of scan frame                       | number  | no       | iOS/Android | yes               |
| cornerBorderWidth  | border width of scan frame corner                | number  | no       | iOS/Android | yes               |
| cornerBorderLength | width and height of the corner of the scan frame | number  | no       | iOS/Android | yes               |
| rectHeight         | Scan frame height                                | number  | no       | iOS/Android | yes               |
| rectWidth          | Scan Frame Width                                 | number  | no       | iOS/Android | yes               |
| finderX            | scan frame X axis offset                         | number  | no       | iOS/Android | yes               |
| finderY            | scan frame Y axis offset                         | number  | no       | iOS/Android | yes               |
| isCornerOffset     | whether the corners are offset                   | boolean | no       | iOS/Android | yes               |
| cornerOffsetSize   | offset                                           | number  | no       | iOS/Android | yes               |
| bottomHeight       | Reserved height at the bottom                    | number  | no       | iOS/Android | yes               |
| scanBarAnimateTime | scan line time                                   | number  | no       | iOS/Android | yes               |
| scanBarColor       | scan line color                                  | string  | no       | iOS/Android | yes               |
| scanBarImage       | scan line image                                  | any     | no       | iOS/Android | yes               |
| scanBarHeight      | scan line height                                 | number  | no       | iOS/Android | yes               |
| scanBarMargin      | scanline left and right margin                   | number  | no       | IOS/Android | yes               |
| hintText           | hintText                                         | string  | no       | IOS/Android | yes               |
| hintTextStyle      | hint string style                                | object  | no       | iOS/Android | yes               |
| hintTextPosition   | hintTextPosition                                 | number  | no       | iOS/Android | yes               |
| renderTopView      | render top View                                  | funtion | no       | iOS/Android | yes               |
| renderBottomView   | render bottom View                               | funtion | no       | iOS/Android | yes               |
| isShowScanBar      | whether to show scan lines                       | boolean | no       | iOS/Android | yes               |
| topViewStyle       | render top container style                       | object  | no       | iOS/Android | yes               |
| bottomViewStyle    | render bottom container style                    | object  | no       | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/deepanrajkumar/react-native-qr-decode-image-camera/blob/master/LICENSE).
