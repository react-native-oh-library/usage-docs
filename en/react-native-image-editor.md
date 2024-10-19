<!-- {% raw %} -->
> Template version: V0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/image-editor</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-native-image-editor">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/react-native-image-editor/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [Github address](https://github.com/react-native-oh-library/react-native-image-editor)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package:[@react-native-oh-tpl/image-editor Releases](https://github.com/react-native-oh-library/react-native-image-editor/releases).

#### **npm**

```bash
npm install @react-native-oh-tpl/image-editor@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/image-editor@file:#
```

@react-native-community/image-editor is used as an example.

> [!TIP] The library name imported during use remains unchanged.

```js
import React, { Component } from "react";
import {
  Image,
  ScrollView,
  Text,
  View,
  StyleSheet,
  Button,
  Alert,
  KeyboardAvoidingView,
} from "react-native";

import ImageEditor from "@react-native-community/image-editor";

export interface Props {
  // noop
}

interface Size {
  width: number;
  height: number;
}

interface State {
  photoUri: any;
  photoWidth: number;
  photoHeight: number;
  croppedImageURI: string | null;
  targetSize?: Size;
  cropHorizontal: boolean;
}

export default class ImageEditor extends Component<Props, State> {
  constructor(props: Props) {
    super(props);
    this.state = {
      photoUri: "https://octodex.github.com/images/OctoAsians_dex_Full.png",
      photoWidth: 896,
      photoHeight: 896,
      croppedImageURI: null,
      targetSize: {
        width: 0,
        height: 0,
      },
      cropHorizontal: false,
    };
  }

  _crop = async () => {
    let cropData = {
      offset: { x: 100, y: 100 },
      size: { width: 300, height: 300 },
      quality: 1,
      format: "jpeg",
    };
    if (
      cropData.size.width + cropData.offset.x > this.state.photoWidth ||
      cropData.size.height + cropData.offset.y > this.state.photoHeight
    ) {
      Alert.alert("The cropped size exceeds the original size");
      return;
    }
    const croppedImageURI = await ImageEditor.cropImage(
      this.state.photoUri,
      cropData
    );
    if (croppedImageURI) {
      this.setState({
        croppedImageURI,
        targetSize: {
          width: cropData.size.width,
          height: cropData.size.height,
        },
      });

      if (this.state.targetSize.width >= this.state.targetSize.height) {
        this.setState({
          cropHorizontal: true,
        });
      } else {
        this.setState({
          cropHorizontal: false,
        });
      }
    }
  };

  render() {
    const {
      photoUri,
      photoWidth,
      photoHeight,
      croppedImageURI,
      targetSize,
      cropHorizontal,
    } = this.state;
    return (
      <KeyboardAvoidingView behavior="position">
        <ScrollView>
          <ScrollView style={{ height: photoHeight }} horizontal={true}>
            <Image
              source={{ uri: photoUri }}
              style={{ width: photoWidth, height: photoHeight }}
            />
          </ScrollView>
          {croppedImageURI ? (
            <ScrollView
              style={{ height: targetSize?.height }}
              horizontal={cropHorizontal}
            >
              <Image
                source={{ uri: croppedImageURI }}
                style={{ width: targetSize?.width, height: targetSize?.height }}
              />
            </ScrollView>
          ) : (
            <Text>No image generated</Text>
          )}
          <View style={styles.button}>
            <Text>{croppedImageURI}</Text>
            <Button title="OK" onPress={() => this._crop()} />
          </View>
        </ScrollView>
      </KeyboardAvoidingView>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  button: {
    padding: 10,
  },
  flex: {
    display: "flex",
    flexDirection: "row",
    justifyContent: "flex-start",
    alignItems: "center",
  },
});
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

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
    "@react-native-oh-tpl/image-editor": "file:../../node_modules/@react-native-oh-tpl/image-editor/harmony/image_editor.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

### 3.Introducing ImageEditorPackage Component to ArkTS


Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {ImageEditorPackage} from "@react-native-oh-tpl/image-editor/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImageEditorPackage(ctx)
  ];
}
```

### 4.Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-image-editor Releases](https://github.com/react-native-oh-library/react-native-image-editor/releases)


## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip]  If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name      | Type    | Description                                                  | Platform    | HarmonyOS Support |
| --------- | -------- | ------------------------------------------------------------ | ----------- | ----------------- |
| cropImage | function | Crop the image specified by the URI param. If URI points to a remote image, it will be downloaded automatically. If the image cannot be loaded/downloaded, the promise will be rejected.<br/><br/>If the cropping process is successful, the resultant cropped image will be stored in the cache path, and the CropResult returned in the promise will point to the image in the cache path. ⚠️ Remember to delete the cropped image from the cache path when you are done with it. | ios/Android | yes               |

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**cropData**

| Name          | Value                             | Type   | Description                                                                                                                                                                                               | Required | Platform | HarmonyOS Support |
| ------------- | --------------------------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| `offset`      | { x: number, y: number }          | object | The top-left corner of the cropped image, specified in the original image's coordinate space                                                                                                              | yes      | All      | yes               |
| `size`        | { width: number, height: number } | object | Size (dimensions) of the cropped image                                                                                                                                                                    | yes      | All      | yes               |
| `displaySize` | { width: number, height: number } | object | Size to which you want to scale the cropped image                                                                                                                                                         | no       | All      | yes               |
| `resizeMode`  | 'contain' \| 'cover' \| 'stretch' | string | Resizing mode to use when scaling the image**Default value**: `'cover'`                                                                                                                                   | no       | All      | yes               |
| `quality`     | 0.0 - 1.0                         | number | A value in range `0.0` - `1.0` specifying compression level of the result image. `1` means no compression (highest quality) and `0` the highest compression (lowest quality)<br/>**Default value**: `0.9` | no       | All      | yes               |
| `format`      | 'jpeg' \| 'png' \| 'webp'         | string | The format of the resulting image.<br/>**Default value**: based on the provided image;<br/>if value determination is not possible, `'jpeg'` will be used as a fallback.                                   | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under  [ [The MIT License (MIT)]](https://github.com/callstack/react-native-image-editor/blob/master/LICENSE), Please enjoy and participate freely in open source.
<!-- {% endraw %} -->