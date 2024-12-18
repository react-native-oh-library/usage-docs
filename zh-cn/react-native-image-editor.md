> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>@react-native-community/image-editor</code> </h1>
</p>

本项目基于 [@react-native-community/image-editor@3.2.0](https://github.com/callstack/react-native-image-editor) 开发。

该第三方库的仓库已迁移至 Gitee，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/image-editor`，具体版本所属关系如下：

| Version                   | Package Name                                      | Repository         | Release                    |
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |
| <= 3.2.1@deprecated | @react-native-oh-tpl/image-editor | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-image-editor) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-image-editor/releases) |
| > 3.2.1                   | @react-native-ohos/image-editor   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-image-editor) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-image-editor/releases) |

## 1. 安装与使用

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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
            <Text>未生成图片</Text>
          )}
          <View style={styles.button}>
            <Text>{croppedImageURI}</Text>
            <Button title="确定" onPress={() => this._crop()} />
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

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 2.2. 引入原生端代码

目前有两种方法：

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@react-native-ohos/image-editor": "file:../../node_modules/@react-native-ohos/image-editor/harmony/image_editor.har"
  }
```

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 2.3. 配置 CMakeLists 和引入 ImageEditorPackage

> [!TIP] 版本 v3.2.1-rc.1 及以上需要

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/image-editor/src/main/cpp" ./image-editor)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_image_editor)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 2.4. 在 ArkTs 侧引入 xxx Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {ImageEditorPackage} from '@react-native-ohos/image-editor/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new ImageEditorPackage(ctx)
  ];
}
```

### 2.5. 运行

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1. 兼容性

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/image-editor Releases](https://gitee.com/openharmony-sig/rntpc_react-native-image-editor/releases)

## 4. 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| `offset`      | The top-left corner of the cropped image, specified in the original image's coordinate space                 | object | yes      | All      | yes               |
| `size`        | Size (dimensions) of the cropped image  | object | yes      | All      | yes               |
| `displaySize` | Size to which you want to scale the cropped image     | object | no       | All      | yes               |
| `resizeMode`  | Resizing mode to use when scaling the image**Default value**: `'cover'` | string     | no       | All      | yes              |
| `quality`     | A value in range `0.0` - `1.0` specifying compression level of the result image. `1` means no compression (highest quality) and `0` the highest compression (lowest quality)<br/>**Default value**: `0.9` | number | no       | All      | yes               |
| `format`      | The format of the resulting image.<br/>**Default value**: based on the provided image;<br/>if value determination is not possible, `'jpeg'` will be used as a fallback.         | string | no       | All      | yes               |

## 5. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| cropImage | Crop the image specified by the URI param. If URI points to a remote image, it will be downloaded automatically. If the image cannot be loaded/downloaded, the promise will be rejected.<br/><br/>If the cropping process is successful, the resultant cropped image will be stored in the cache path, and the CropResult returned in the promise will point to the image in the cache path. ⚠️ Remember to delete the cropped image from the cache path when you are done with it. | function | yes | ios/Android | yes               |

## 6. 遗留问题

## 7. 其他

## 8. 开源协议

本项目基于 [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-image-editor/blob/master/LICENSE) ，请自由地享受和参与开源。
