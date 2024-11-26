> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-marker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/JimmyDaddy/react-native-image-marker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/JimmyDaddy/react-native-image-marker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/react-native-oh-library/react-native-image-marker)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-image-marker Releases](https://github.com/react-native-oh-library/react-native-image-marker/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-marker@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-marker@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import Marker, {
  Position,
  ImageMarkOptions,
  TextMarkOptions,
} from "react-native-image-marker";
import React, { useState } from "react";
import {
  StyleSheet,
  ScrollView,
  Text,
  View,
  Button,
  Image,
} from "react-native";
import { Colors } from "react-native/Libraries/NewAppScreen";

export const ImageMarkerText = () => {
  const [texturl, setTextMarkUrl] = useState("");
  const [imageurl, setImageMarkUrl] = useState("");
  const text_options: TextMarkOptions = {
    backgroundImage: {
      src: "https://developer.huawei.com/allianceCmsResource/resource/HUAWEI_Developer_VUE/images/yuekan/xintexing00.jpg",
    },
    watermarkTexts: [
      {
        text: "hello world \n hello",
        position: {
          position: Position.topLeft,
        },
        style: {
          color: "#FFFF00",
          fontSize: 30,
          fontName: "Arial",
          rotate: 30,
          textBackgroundStyle: {
            padding: "10% 10%",
            color: "#02B96B",
          },
          shadowStyle: {
            dx: 10,
            dy: 10,
            radius: 10,
            color: "#008F6D",
          },
          strikeThrough: true,
          underline: true,
        },
      },
      {
        text: "hello world \n hello",
        position: {
          position: Position.center,
        },
        style: {
          color: "#FFFF00",
          fontSize: 30,
          fontName: "Arial",
          textBackgroundStyle: {
            padding: "10% 10%",
            color: "#0FFF00",
          },
          strikeThrough: true,
          underline: true,
        },
      },
    ],
  };

  const image_options: ImageMarkOptions = {
    backgroundImage: {
      src: "https://developer.huawei.com/allianceCmsResource/resource/HUAWEI_Developer_VUE/images/yuekan/xintexing00.jpg",
    },
    watermarkImages: [
      {
        src: "https://developer.huawei.com/allianceCmsResource/resource/HUAWEI_Developer_VUE/images/yingyongicon.png",
        rotate: 20,
        position: {
          position: Position.topLeft,
        },
      },
      {
        src: "https://developer.huawei.com/allianceCmsResource/resource/HUAWEI_Developer_VUE/images/yingyongicon.png",
        rotate: 50,
        position: {
          position: Position.bottomCenter,
        },
      },
    ],
  };

  const markText = () => {
    Marker.markText(text_options)
      .then((result) => {
        setTextMarkUrl(result);
      })
      .catch((error) => {
        console.log("error", error);
      });
  };

  const markImage = () => {
    Marker.markImage(image_options)
      .then((result) => {
        setImageMarkUrl(result);
      })
      .catch((error) => {
        console.log("error", error);
      });
  };
  return (
    <ScrollView style={{ flex: 1 }}>
      <View style={styles.body}>
        <View style={styles.sectionContainer}>
          <Text style={styles.sectionTitle}>{"image marker"}</Text>
          <Button title="Mark image " color="#9a73ef" onPress={markImage} />
          <Text style={styles.sectionTitle}>{imageurl}</Text>
          <Image
            resizeMode="contain"
            source={{ uri: imageurl, width: 300, height: 300 }}
          />
        </View>
      </View>
      <View style={styles.body}>
        <View style={styles.sectionContainer}>
          <Text style={styles.sectionTitle}>{"image marker"}</Text>
          <Button title="mark text " color="#9a73ef" onPress={markText} />
          <Text style={styles.sectionTitle}>{texturl}</Text>
          <Image
            resizeMode="contain"
            source={{ uri: texturl, width: 300, height: 300 }}
          />
        </View>
      </View>
    </ScrollView>
  );
};
const styles = StyleSheet.create({
  body: {
    backgroundColor: Colors.dark,
  },
  sectionContainer: {
    marginTop: 32,
    paddingHorizontal: 24,
  },
  sectionTitle: {
    marginBottom: 30,
    fontSize: 12,
    fontWeight: "600",
    color: Colors.white,
  },
});
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

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
    "@react-native-oh-tpl/react-native-image-marker": "file:../../node_modules/@react-native-oh-tpl/react-native-image-marker/harmony/image_marker.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] or details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing RNImageMarkerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNImageMarkerPackage} from '@react-native-oh-tpl/react-native-image-marker/ts';


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+    new RNImageMarkerPackage(ctx)
  ];
}
```

### 4. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-image-marker Releases](https://github.com/react-native-oh-library/react-native-image-marker/releases)

### Permission Requirements

If network images are used, network information permissions need to be added in module.json 5 in the entry directory

Open the `entry/src/main/module.json5` file and add the following code:

```js
...
"requestPermissions": [
    {
    "name": "ohos.permission.INTERNET"
    }
]
```

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name      | Description                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ------------------------------ | ------ | -------- | ----------- | ----------------- |
| markImage | mark icons on background image | string | no       | Android/iOS | yes               |
| markText  | mark texts on background image | string | no       | Android/iOS | yes               |

#### markImage

```js
markImage(options: ImageMarkOptions): Promise<string>;
```

##### ImageMarkOptions

| Name            | Description                                                    | Type                          | Required | Platform    | HarmonyOS Support |
| --------------- | -------------------------------------------------------------- | ----------------------------- | -------- | ----------- | ----------------- |
| backgroundImage | background image options                                       | ImageOptions                  | yes      | iOS/Android | yes               |
| quality         | image quality `0-100`, `100` is best quality. defaultValue 100 | number                        | no       | iOS/Android | yes               |
| filename        | save image name                                                | string                        | no       | iOS/Android | yes               |
| saveFormat      | save image format 'png','jpg','base64',default 'png'           | ImageFormat                   | no       | iOS/Android | yes               |
| watermarkImages | watermark images                                               | Array\<WatermarkImageOptions> | yes      | iOS/Android | yes               |

##### ImageOptions

| Name   | Description                                 | Type   | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| src    | image src, local image                      | string | yes      | iOS/Android | yes               |
| scale  | image scale `>0`.defaultValue 1             | number | no       | iOS/Android | yes               |
| rotate | rotate image rotate `0-360`.defaultValue 0  | number | no       | iOS/Android | yes               |
| alpha  | transparent of image `0 - 1`.defaultValue 1 | number | no       | iOS/Android | yes               |

##### ImageFormat

| Name   | Description       | Type   | Required | Platform    | HarmonyOS Support |
| ------ | ----------------- | ------ | -------- | ----------- | ----------------- |
| png    | iamge type png    | string | no       | iOS/Android | yes               |
| jpg    | iamge type jpg    | string | no       | iOS/Android | yes               |
| base64 | iamge type base64 | string | no       | iOS/Android | yes               |

##### WatermarkImageOptions

| Name     | Description                                 | Type            | Required | Platform    | HarmonyOS Support |
| -------- | ------------------------------------------- | --------------- | -------- | ----------- | ----------------- |
| src      | image src, local image                      | string          | yes      | iOS/Android | yes               |
| scale    | image scale `>0`.defaultValue 1             | number          | no       | iOS/Android | yes               |
| rotate   | rotate image rotate `0-360`.defaultValue 0  | number          | no       | iOS/Android | yes               |
| alpha    | transparent of image `0 - 1`.defaultValue 1 | number          | no       | iOS/Android | yes               |
| position | the position of icon on background image    | PositionOptions | no       | iOS/Android | yes               |

##### PositionOptions

| Name     | Description                               | Type            | Required | Platform    | HarmonyOS Support |
| -------- | ----------------------------------------- | --------------- | -------- | ----------- | ----------------- |
| X        | horizontal coordinate on background image | number / string | no       | iOS/Android | yes               |
| Y        | vertical coordinate on background image   | number / string | no       | iOS/Android | yes               |
| position | position enum                             | Position        | no       | iOS/Android | yes               |

##### Position

| Name         | Description                       | Type   | Required | Platform    | HarmonyOS Support |
| ------------ | --------------------------------- | ------ | -------- | ----------- | ----------------- |
| topLeft      | top left on background image      | string | no       | iOS/Android | yes               |
| topCenter    | top center on background image    | string | no       | iOS/Android | yes               |
| topRight     | top right on background image     | string | no       | iOS/Android | yes               |
| bottomLeft   | bottom left on background image   | string | no       | iOS/Android | yes               |
| bottomCenter | bottom center on background image | string | no       | iOS/Android | yes               |
| bottomRight  | bottom right on background image  | string | no       | iOS/Android | yes               |
| center       | center on background image        | string | no       | iOS/Android | yes               |

#### markText

```json
markText(options: TextMarkOptions): Promise<string>;
```

##### TextMarkOptions

| Name            | Description                                                | Type                | Required | Platform    | HarmonyOS Support |
| --------------- | ---------------------------------------------------------- | ------------------- | -------- | ----------- | ----------------- |
| backgroundImage | background image options                                   | ImageOptions        | yes      | iOS/Android | yes               |
| watermarkTexts  | text options                                               | Array\<TextOptions> | yes      | iOS/Android | yes               |
| quality         | image quality 0-100, 100 is best quality. defaultValue 100 | number              | no       | iOS/Android | yes               |
| filename        | save image name                                            | string              | no       | iOS/Android | yes               |
| saveFormat      | save image format 'png','jpg','base64',default 'png'       | ImageFormat         | no       | iOS/Android | yes               |

##### TextOptions

| Name     | Description           | Type            | Required | Platform    | HarmonyOS Support |
| -------- | --------------------- | --------------- | -------- | ----------- | ----------------- |
| text     | text content          | string          | yes      | iOS/Android | yes               |
| position | text position options | PositionOptions | no       | iOS/Android | yes               |
| style    | text style            | TextStyle       | no       | iOS/Android | yes               |

##### TextStyle

| Name                | Description                                        | Type                | Required | Platform    | HarmonyOS Support |
| ------------------- | -------------------------------------------------- | ------------------- | -------- | ----------- | ----------------- |
| color               | font color                                         | string              | yes      | iOS/Android | yes               |
| fontName            | font name                                          | string              | no       | iOS/Android | yes               |
| fontSize            | font size                                          | number              | no       | iOS/Android | yes               |
| shadowStyle         | text shadow style                                  | ShadowLayerStyle    | no       | iOS/Android | yes               |
| textBackgroundStyle | text background style                              | TextBackgroundStyle | no       | iOS/Android | yes               |
| underline           | text underline style                               | boolean             | no       | iOS/Android | yes               |
| skewX               | css italic with degree, you can use italic instead | number              | no       | iOS/Android | yes               |
| strikeThrough       | text stroke                                        | boolean             | no       | iOS/Android | yes               |
| textAlign           | text align . 'left' / 'center' / 'right'           | string              | no       | iOS/Android | yes               |
| italic              | text italic                                        | boolean             | no       | iOS/Android | yes               |
| bold                | text bold                                          | boolean             | no       | iOS/Android | yes               |
| rotate              | rotate text                                        | number              | no       | iOS/Android | yes               |

##### ShadowLayerStyle

| Name   | Description     | Type   | Required | Platform    | HarmonyOS Support |
| ------ | --------------- | ------ | -------- | ----------- | ----------------- |
| dx     | shadow offset x | number | yes      | iOS/Android | yes               |
| dy     | shadow offset y | number | yes      | iOS/Android | yes               |
| radius | shadow radius   | number | yes      | iOS/Android | yes               |
| color  | shadow color    | string | yes      | iOS/Android | yes               |

##### TextBackgroundStyle

extends Padding
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| type | background type .TextBackgroundType enum | TextBackgroundType | no | iOS/Android | yes |
| color | background color | string | yes | iOS/Android | yes |
| cornerRadius |background corner radius | CornerRadius | no | iOS/Android | yes |
| padding | padding for text background，Up to four values, separated by spaces | number / string | no | iOS/Android | yes |
| paddingLeft | padding left for text background | number / string | no | iOS/Android | yes |
| paddingRight | padding right for text background | number / string | no | iOS/Android | yes |
| paddingTop | padding top for text background | number / string | no | iOS/Android | yes |
| paddingBottom | padding bottom for text background | number / string | no | iOS/Android | yes |
| paddingHorizontal | padding left and right (horizontal) for text background | number / string | no | iOS/Android | yes |
| paddingVertical | padding top and bottom (vertical) for text background | number / string | no | iOS/Android | yes |
| paddingX |padding x, alias of paddingHorizontal | number / string | no | iOS/Android | yes |
| paddingY | padding y, alias of paddingVertical | number / string | no | iOS/Android | yes |

##### TextBackgroundType

| Name     | Description              | Type   | Required | Platform    | HarmonyOS Support |
| -------- | ------------------------ | ------ | -------- | ----------- | ----------------- |
| stretchX | background type stretchX | string | no       | iOS/Android | yes               |
| stretchY | background type stretchY | string | no       | iOS/Android | yes               |
| none     | background type fit      | string | no       | iOS/Android | yes               |

##### CornerRadius

| Name        | Description        | Type        | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------ | ----------- | -------- | ----------- | ----------------- |
| topLeft     | topLeft Radius     | RadiusValue | no       | iOS/Android | yes               |
| topRight    | topRight Radius    | RadiusValue | no       | iOS/Android | yes               |
| bottomLeft  | bottomLeft Radius  | RadiusValue | no       | iOS/Android | yes               |
| bottomRight | bottomRight Radius | RadiusValue | no       | iOS/Android | yes               |
| all         | all Radius         | RadiusValue | no       | iOS/Android | yes               |

##### RadiusValue

| Name | Description        | Type            | Required | Platform    | HarmonyOS Support |
| ---- | ------------------ | --------------- | -------- | ----------- | ----------------- |
| x    | radius value for x | number / string | no       | iOS/Android | yes               |
| y    | radius value for y | number / string | no       | iOS/Android | yes               |

## Known Issues

- [x] Harmony OS is not support font name feature now: [issue#7](https://github.com/react-native-oh-library/react-native-image-marker/issues/7)
- [x] Harmony OS is not support font skewX feature now: [issue#8](https://github.com/react-native-oh-library/react-native-image-marker/issues/8)
- [x] Harmony OS is not support font italic feature now:[issue#9](https://github.com/react-native-oh-library/react-native-image-marker/issues/9)

## Others

## License

This project is licensed under[The MIT License(MIT)](https://github.com/JimmyDaddy/react-native-image-marker/blob/master/LICENSE).
