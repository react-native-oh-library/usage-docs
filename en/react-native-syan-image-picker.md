> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-syan-image-picker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/syanbo/react-native-syan-image-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/syanbo/react-native-syan-image-picker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-syan-image-picker) 

## Installation and Usage

Find the matching version information in the release address of a third-party library:[@react-native-oh-tpl/react-native-syan-image-picker Releases](https://github.com/react-native-oh-library/react-native-syan-image-picker/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-syan-image-picker
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-syan-image-picker
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import {
  StyleSheet,
  Text,
  View,
  Image,
  ScrollView,
  TouchableOpacity,
  Dimensions
} from 'react-native';
import SYImagePicker from "react-native-syan-image-picker";

export default class App extends Component<{}> {
 constructor(props) {
    super(props);
    this.state = {
      photos: [],
    };
  }
 /**
 * 开启压缩，选择一张照片先裁剪然后再压缩，并支持base64编码
 **/
SYImagePicker.showImagePicker(
        {
          /**
          * imageCount为1才支持裁剪
          **/
          imageCount: 1, 
          isCrop: true,
          quality: 90,
          compress: true, // 开启压缩
          enableBase64: false,
        },
        (err, photos) => {
          if (!err) {
            this.setState({
              photos,
            });
          } else {
            console.log(err);
          }
        },
    );
/**
 * 关闭压缩，多选照片并支持base64编码
 **/
 handleAsyncSelectPhoto = async () => {
    SYImagePicker.removeAllPhoto()
    try {
      const photos = await SYImagePicker.asyncShowImagePicker({
        imageCount: 8, //指定选择的照片数量
        enableBase64: true, // 支持base64编码
      });
      // 选择成功
      this.setState({
        photos: [...this.state.photos, ...photos],
      });
    } catch (err) {
      console.log(err);
      // 取消选择，err.message为"取消"
    }
  };
/**
* 缓存清除
**/
handleDeleteCache = () => {
    SYImagePicker.deleteCache();
  };

/**
* 移除选中的图片
**/
handleDeletePhoto = index => {
  const { selectedPhotos: oldPhotos } = this.state;
  const selectedPhotos = oldPhotos.filter((photo, photoIndex) => photoIndex !== index);
  // 更新原生图片数组
  SYImagePicker.removePhotoAtIndex(index);
  }

/**
* 移除选中的全部图片
**/
STImagePicke.removeAllPhoto()

/**
* 调用相机
**/
SyanImagePicker.openCamera(options, (err, photos) => {
  if (err) {
    // 取消选择
    return;
  }
  // 选择成功，渲染图片
  // ...
})

/**
* 选择视频
**/
SyanImagePicker.openVideoPicker(options, (err, videos) => {
  if (err) {
    // 取消选择
    return;
  }
  // 选择成功，处理视频
  // ...
})

}
```

## Use Codegen

This repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

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

### 2.Configure Entry

**(1)Create ImageCropAbility.ets under entry/src/main/ets/entryability**

```
import UIAbility from '@ohos.app.ability.UIAbility'
import window from '@ohos.window'

const TAG = 'ImageEditAbility';

export default class ImageCropAbility extends UIAbility {

  onWindowStageCreate(windowStage: window.WindowStage) {
    this.setWindowOrientation(windowStage, window.Orientation.PORTRAIT)
    windowStage.loadContent('pages/ImageEdit', (err, data) => {
      if (err.code) {
        console.info(TAG,'Failed to load the content. Cause: %{public}s',
          JSON.stringify(err) ?? '')
        return;
      }
      console.info(TAG,'Succeeded in loading the content')
    });
    try {
      windowStage.getMainWindowSync().setWindowLayoutFullScreen(true, (err)=>{
        if (err.code) {
          console.error('Failed to enable the full-screen mode. Cause: ' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in enabling the full-screen mode.');
      })
    } catch (exception) {
      console.error('Failed to set the system bar to be invisible. Cause: ' + JSON.stringify(exception));
    }
  }

  setWindowOrientation(stage: window.WindowStage, orientation: window.Orientation): void {
    console.info(TAG,"into setWindowOrientation :")
    if (!stage || !orientation) {
      return;
    }
    stage.getMainWindow().then(windowInstance => {
      windowInstance.setPreferredOrientation(orientation);
    })
  }

  onBackground() {
    this.context.terminateSelf();
  }
}
```

**(2)Register ImageCropAbility.ets in entry/src/main/module.json5.**

```
"abilities":[{
        "name": "ImageCropAbility",
        "srcEntry": "./ets/entryability/ImageCropAbility.ets",
        "description": "$string:EntryAbility_desc",
        "icon": "$media:icon",
        "startWindowIcon": "$media:startIcon",
        "startWindowBackground": "$color:start_window_background",
        "removeMissionAfterTerminate": true,

}
...
]

```

**(3)Create ImageEdit.ets under entry/src/main/ets/pages.**

```
import { ImageCrop } from '@react-native-oh-tpl/react-native-syan-image-picker';

@Entry
@Component
struct ImageEdit {

 build() {
  Row(){
   Column(){
    ImageCrop();
   }
   .width('100%')
  }
  .height('100%')
 }
}
```

**(4)Add configuration in entry/src/main/resources/base/profile/main_pages.json.**

```
{
 "src": [
  "pages/Index",
  "pages/ImageEdit"
 ]
}
```

### 3. Introducing Native Code

Currently, two methods are available:


Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-syan-image-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-syan-image-picker/harmony/syan_image_picker.har"
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

### 4. Introducing SyanImagePickerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+   import {SyanImagePickerPackage} from '@react-native-oh-tpl/react-native-syan-image-picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SyanImagePickerPackage(ctx)
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

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-syan-image-picker Releases](https://github.com/react-native-oh-library/react-native-syan-image-picker/releases)

This document is verified based on the following versions:

1.  RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1 B.0.22、IDE：DevEco Studio 5.0.3.300SP2; ROM：3.0.0.24;



## ImagePickerOption(选择图片或数据的配置项)
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                            | Description                                                  | Type    | Required |  Platform   | HarmonyOS Support |
| ------------------------------- | ------------------------------------------------------------ | ------- | :------: | :---------: | :---------------: |
| imageCount                      | 最大选择图片数目，默认6                                      | number  |   yes    | iOS/Android |        yes        |
| isCamera                        | 是否允许用户在内部拍照，默认true                             | boolean |   yes    | iOS/Android |        yes        |
| isCrop                          | 是否允许裁剪，默认false, imageCount 为1才生效                | boolean |   yes    | iOS/Android |        yes        |
| compress                        | 是否压缩照片                                                 | boolean |   yes    | iOS/Android |        yes        |
| quality                         | 压缩质量                                                     | number  |   yes    | iOS/Android |        yes        |
| enableBase64                    | 是否返回base64编码，默认不返回                               | boolean |   yes    | iOS/Android |        yes        |
| videoCount                      | 选择的视频个数                                               | number  |   yes    | iOS/Android |        yes        |
| allowPickingMultipleVideo       | 允许选择多个视频                                             | boolean |   yes    | iOS/Android |        yes        |
| isRecordSelected                | 是否已选图片                                                 | bool    |   yes    | iOS/Android |        yes         |
| CropW                           | 裁剪宽度，默认屏幕宽度60%                                    | number  |   yes    | iOS/Android |        yes         |
| CropH                           | 裁剪高度，默认屏幕宽度60%                                    | number  |   yes    | iOS/Android |        yes         |
| isGif                           | 是否允许选择GIF，默认false，暂无回调GIF数据                  | boolean |   yes    | iOS/Android |        no         |
| showCropCircle                  | 是否显示圆形裁剪区域，默认false                              | boolean |   yes    | iOS/Android |        yes         |
| circleCropRadius                | 圆形裁剪半径，默认屏幕宽度一半                               | number  |   yes    | iOS/Android |        yes         |
| showCropFrame                   | 是否显示裁剪区域，默认true                                   | boolean |   yes    | Android |        no         |
| showCropGrid                    | 是否隐藏裁剪区域网格，默认false                              | boolean |   yes    | Android |        no         |
| freeStyleCropEnabled            | 裁剪框是否可拖拽                                             | boolean |   yes    | Android |        no         |
| rotateEnabled                   | 裁剪是否可旋转图片                                           | boolean |   yes    | Android |        no         |
| scaleEnabled                    | 裁剪是否可放大缩小图片                                       | boolean |   yes    | Android |        no         |
| compressFocusAlpha              | 压缩时保留图片透明度（开启后png压缩后尺寸会变大但是透明度会保留) | boolean |   yes    | iOS/Android |        no         |
| minimumCompressSize             | 小于100kb的图片不压缩（Android）                             | number  |   yes    | Android |        no         |
| allowPickingOriginalPhoto       | 选择原生图片                                                 | boolean |   yes    | iOS/Android |        yes         |
| MaxSecond                       | 选择视频最大时长，默认是180秒                                | number  |   yes    | Android |        no         |
| videoMaximumDuration            | 视频最大拍摄时间，默认是10分钟，单位是秒                     | number  |   yes    | iOS/Android |        yes         |
| isWeChatStyle                   | 是否是微信风格选择界面 Android Only                          | boolean |   yes    | Android |        no         |
| sortAscendingByModificationDate | 对照片排序，按修改时间升序，默认是YES。如果设置为NO,最新的照片会显示在最前面，内部的拍照按钮会排在第一个 | boolean |   yes    | iOS/Android |        no         |
| MinSecond                       | 选择视频最小时长，默认是1秒                                  | number  |   yes    | Android |        no         |
| showSelectedIndex               | 是否显示序号， 默认不显示                                    | boolean |   yes    | iOS/Android |        no         |

## SelectedPhoto（选择的图片或视频的返回结果）
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name         | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| width        | 图片宽度                                                     | number | yes      | iOS/Android | yes               |
| height       | 图片高度                                                     | number | yes      | iOS/Android | yes               |
| original_uri | 图片原始路径                                                 | string | yes      | iOS/Android | yes               |
| uri          | 图片路径                                                     | string | yes      | iOS/Android | yes               |
| type         | 文件类型                                                     | string | yes      | iOS/Android | yes               |
| size         | 图片大小，单位为字节 b                                       | number | yes      | iOS/Android | yes               |
| base64       | 图片的 base64 编码，如果 enableBase64 设置 false，则不返回该属性 | string | yes      | iOS/Android | yes               |

## API
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                        | Type                                                     | Required | Platform    | HarmonyOS Support |
| -------------------- | ---------------------------------- | -------------------------------------------------------- | -------- | ----------- | ----------------- |
| showImagePicker      | 打开图片选择器，选择图片           | callback: (err: null \| string, photos: SelectedPhoto[]) | yes      | iOS/Android | yes               |
| asyncShowImagePicker | 打开图片选择器，选择图片           | Promise<SelectedPhoto[]>                                 | yes      | iOS/Android | yes               |
| openCamera           | 打开相机拍照，并可以选择所拍的照片 | callback: (err: null \| string, photos: SelectedPhoto[]) | yes      | iOS/Android | yes               |
| asyncOpenCamera      | 打开相机拍照，并可以选择所拍的照片 | Promise<SelectedPhoto[]>                                 | yes      | iOS/Android | yes               |
| deleteCache          | 清除缓存                           | void                                                     | yes      | iOS/Android | yes               |
| removePhotoAtIndex   | 删除已选择照片的索引               | void                                                     | yes      | iOS/Android | yes               |
| removeAllPhoto       | 删除所有已选择的照片               | void                                                     | yes      | iOS/Android | yes               |
| openVideoPicker      | 打开视频选择器,选择视频            | callback: (err: null \| string, photos: SelectedPhoto[]) | yes      | iOS/Android | yes               |

## Known Issues

- [ ]  isRecordSelected: 是否已选图片[issues#2](https://github.com/react-native-oh-library/react-native-syan-image-picker/issues/2)
- [ ]  isGif: 是否允许选择GIF[issues#5](https://github.com/react-native-oh-library/react-native-syan-image-picker/issues/5)
- [ ]  compressFocusAlpha: 压缩时保留图片透明度[issues#13](https://github.com/react-native-oh-library/react-native-syan-image-picker/issues/13)
- [ ]  sortAscendingByModificationDate: 对照片排序，按修改时间升序[issues#19](https://github.com/react-native-oh-library/react-native-syan-image-picker/issues/19)
- [ ]  showSelectedIndex: 是否显示序号[issues#21](https://github.com/react-native-oh-library/react-native-syan-image-picker/issues/21)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/syanbo/react-native-syan-image-picker/blob/master/LICENSE).
