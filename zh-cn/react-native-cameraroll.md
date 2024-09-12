> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-cameraroll</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-cameraroll/react-native-cameraroll">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/react-native-cameraroll/react-native-cameraroll/blob/master/LICENCE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github 地址](https://github.com/react-native-oh-library/react-native-cameraroll)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-cameraroll Releases](https://github.com/react-native-oh-library/react-native-cameraroll/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/camera-roll@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/camera-roll@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { View, Button } from "react-native";
import {
  CameraRoll
} from "@react-native-camera-roll/camera-roll";

export default function App() {
  return (
    <View>
      Button
        title="savePhotos"
        onPress={() => {
          CameraRoll.saveAsset("https://res.vmallres.com/uomcdn/CN/cms/202409/9d386e73605e4c759c1896e8ac7ce34b.jpg.webp").then((res) => {
            console.log('res-----',res);
          });
        }}
      />
    </View>
  );
}
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/camera-roll": "file:../../node_modules/@react-native-oh-tpl/camera-roll/harmony/camera_roll.har"
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

### 3.在 ArkTs 侧引入 CameraRollPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { CameraRollPackage } from '@react-native-oh-tpl/camera-roll/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CameraRollPackage(ctx),
  ];
}
```

### 4.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/camera-roll Releases](https://github.com/react-native-oh-library/react-native-cameraroll/releases)

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**CameraRoll**
| Name | Description | Type | Required | Platform | HarmonyOS Support | Remarks |
| ---- | ----------- | ---- | -------- | -------- | ------------------ | ---- |
| save | 保存图片/视频 | function | no | android,ios | partially | 由于原库版本升级，该方法已弃用，可用saveAsset接口代替。 |
| saveAsset | 保存图片/视频 | function | no | android,ios | partially |  |
| saveToCameraRoll | 保存图片/视频 | function | no | android,ios | partially | 内部调用saveAsset接口 |
| getPhotos | 查找图片/视频 | function | no | android,ios | no | 由于Harmony OS安全策略调整，涉及到ohos.permission.READ_IMAGEVIDEO和ohos.permission.WRITE_IMAGEVIDEO权限的接口无法上架使用，因此该接口暂无法使用。 |
| getAlbums | 查找相册 | function | no | android,ios | no | 由于Harmony OS安全策略调整，涉及到ohos.permission.READ_IMAGEVIDEO和ohos.permission.WRITE_IMAGEVIDEO权限的接口无法上架使用，因此该接口暂无法使用。 |
| deletePhotos | 删除图片/视频 | function | no | android,ios | no | 由于Harmony OS安全策略调整，涉及到ohos.permission.READ_IMAGEVIDEO和ohos.permission.WRITE_IMAGEVIDEO权限的接口无法上架使用，因此该接口暂无法使用。 |
| iosGetImageDataById | 获取图片数据 | function | no | ios | no | 由于Harmony OS安全策略调整，涉及到ohos.permission.READ_IMAGEVIDEO和ohos.permission.WRITE_IMAGEVIDEO权限的接口无法上架使用，因此该接口暂无法使用。 |
| getPhotoThumbnail | 获取缩略图 | function | no | ios | no | 由于Harmony OS安全策略调整，涉及到ohos.permission.READ_IMAGEVIDEO和ohos.permission.WRITE_IMAGEVIDEO权限的接口无法上架使用，因此该接口暂无法使用。 |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                       | Description                                | Type     | Required | Platform | HarmonyOS Support | Remarks                                                      |
| :----------------------------------------- | :----------------------------------------- | -------- | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| `iosReadGalleryPermission`                 | 权限验证                                   | function | no       | ios      | no                |                                                              |
| `iosRequestReadWriteGalleryPermission`     | 读写权限申请                               | function | no       | ios      | no                |                                                              |
| `iosRequestAddOnlyGalleryPermission`       | 添加权限申请                               | function | no       | ios      | no                |                                                              |
| `iosRefreshGallerySelection`               | 图片列表刷新                               | function | no       | ios      | no                |                                                              |
| `harmonyReadGalleryPermission`             | 对标`iosReadGalleryPermission`             | function | no       | harmony  | no                | 由于Harmony OS安全策略调整，涉及到ohos.permission.READ_IMAGEVIDEO和ohos.permission.WRITE_IMAGEVIDEO权限的接口无法上架使用，因此该接口暂无法使用。 |
| `harmonyRequestReadWriteGalleryPermission` | 对标`iosRequestReadWriteGalleryPermission` | function | no       | harmony  | no                | 由于Harmony OS安全策略调整，涉及到ohos.permission.READ_IMAGEVIDEO和ohos.permission.WRITE_IMAGEVIDEO权限的接口无法上架使用，因此该接口暂无法使用。 |
| `harmonyRequestAddOnlyGalleryPermission`   | 对标`iosRequestAddOnlyGalleryPermission`   | function | no       | harmony  | no                | 由于Harmony OS安全策略调整，涉及到ohos.permission.READ_IMAGEVIDEO和ohos.permission.WRITE_IMAGEVIDEO权限的接口无法上架使用，因此该接口暂无法使用。 |
| `harmonyRefreshGallerySelection`           | 对标`iosRefreshGallerySelection`           | function | no       | harmony  | no                |                                                              |

## 遗留问题

- [ ] deletePhotos删除图片/视频，未实现 HarmonyOS 化: [issue#5](https://github.com/react-native-oh-library/react-native-cameraroll/issues/5)
- [ ] harmonyRefreshGallerySelection，HarmonyOS 暂无对应图片列表刷新的接口：[issue#8](https://github.com/react-native-oh-library/react-native-cameraroll/issues/8)
- [ ] 部分接口由于Harmony OS安全策略调整无法使用: [issue#25](https://github.com/react-native-oh-library/react-native-cameraroll/issues/25)
- [ ] saveAsset接口未完全支持: [issue#26](https://github.com/react-native-oh-library/react-native-cameraroll/issues/26)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-cameraroll/react-native-cameraroll/blob/master/LICENCE) ，请自由地享受和参与开源。