> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>@react-native-community/image-editor</code> </h1>
</p>

This project is based on [@react-native-community/image-editor@3.2.0](https://github.com/callstack/react-native-image-editor).

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/image-editor`, The version correspondence details are as follows:

| Version                   | Package Name                                      | Repository         | Release                    |
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |
| <= 3.2.1@deprecated | @react-native-oh-tpl/image-editor | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-image-editor) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-image-editor/releases) |
| > 3.2.1                   | @react-native-ohos/image-editor   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-image-editor) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-image-editor/releases) |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/image-editor
```

#### **yarn**

```bash
yarn add @react-native-ohos/image-editor
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.


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

## 2. Manual Link

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2 Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/image-editor": "file:../../node_modules/@react-native-ohos/image-editor/harmony/image_editor.har"
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

### 2.3 Configuring CMakeLists and Introducing ImageEditorPackage

> [!TIP] Version v3.2.1-rc.1 and above requires.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/image-editor/src/main/cpp" ./image-editor)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_image_editor)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "ReactNativeOhosReactNativeImageEditorPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<ImageEditorPackage>(ctx),
    };
}
```

### 2.4 Introducing xxx Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {ImageEditorPackage} from '@react-native-ohos/image-editor/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new ImageEditorPackage(ctx)
  ];
}
```

### 2.5 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

Check the release version information in the release address of the third-party library: [@react-native-ohos/image-editor Releases](https://gitee.com/openharmony-sig/rntpc_react-native-image-editor/releases)

## 4. Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| `offset`      | The top-left corner of the cropped image, specified in the original image's coordinate space                 | object | yes      | All      | yes               |
| `size`        | Size (dimensions) of the cropped image  | object | yes      | All      | yes               |
| `displaySize` | Size to which you want to scale the cropped image     | object | no       | All      | yes               |
| `resizeMode`  | Resizing mode to use when scaling the image**Default value**: `'cover'` | string     | no       | All      | yes              |
| `quality`     | A value in range `0.0` - `1.0` specifying compression level of the result image. `1` means no compression (highest quality) and `0` the highest compression (lowest quality)<br/>**Default value**: `0.9` | number | no       | All      | yes               |
| `format`      | The format of the resulting image.<br/>**Default value**: based on the provided image;<br/>if value determination is not possible, `'jpeg'` will be used as a fallback.         | string | no       | All      | yes               |

## 5. APIs

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| cropImage | Crop the image specified by the URI param. If URI points to a remote image, it will be downloaded automatically. If the image cannot be loaded/downloaded, the promise will be rejected.<br/><br/>If the cropping process is successful, the resultant cropped image will be stored in the cache path, and the CropResult returned in the promise will point to the image in the cache path. ⚠️ Remember to delete the cropped image from the cache path when you are done with it. | function | yes | ios/Android | yes               |

## 6. Known Issues

## 7. Others

## 8. License

This project is licensed under [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-image-editor/blob/master/LICENSE).

