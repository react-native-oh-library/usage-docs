> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-camera-kit</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/teslamotors/react-native-camera-kit">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/teslamotors/react-native-camera-kit/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-camera-kit)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-camera-kit Releases](https://github.com/react-native-oh-library/react-native-camera-kit/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-camera-kit@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-camera-kit@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。
### camera example
``` js
import React, {useRef, useState} from 'react';
import {Text, StyleSheet, View, Button} from 'react-native';
import {CameraApi, CameraType,Camera} from 'react-native-camera-kit';

export const CameraDemo: React.FC = (): JSX.Element => {
  const nativeRef = useRef<CameraApi>(null);
  const [zoom, setZoom] = useState<number>(0);
  const [errorStr, setErrorStr] = useState<string>('');
  const [photo, setPhoto] = useState<string>('');

  const onError = (e: any) => {
    setErrorStr(e.nativeEvent.errorMessage);
  };

  const onZoom = (e: any) => {
    setZoom(e.nativeEvent.zoom);
  };

  const onPhoto = async () => {
    const result = await nativeRef.current?.capture();
    result && setPhoto(JSON.stringify(result));
  };

  return (
    <>
      <View>
        <Camera
          style={{width: '100%', height: 500}}
          ref={nativeRef}
          maxZoom={10}
          cameraType={CameraType.Back}
          flashMode={0}
          onError={onError}
          onZoom={onZoom}
        />
      </View>
      <View>
        <Button title="拍照" onPress={onPhoto} />
        <Text style={styles.text}>zoom:{zoom}</Text>
        <Text style={styles.text}>error:{errorStr}</Text>
        <Text style={styles.text}>photo:{photo}</Text>
      </View>
    </>
  );
};

const styles = StyleSheet.create({
  text: {
    fontSize: 20,
    textAlign: 'center',
    color: '#000',
    marginTop: 10,
  },
});

```
### scanCode example
``` js
import React, {useRef, useState} from 'react';
import {Text, StyleSheet, View} from 'react-native';
import {CameraApi, CameraType,Camera} from 'react-native-camera-kit';

export const ScanCodeDemo: React.FC = (): JSX.Element => {
  const nativeRef = useRef<CameraApi>(null);
  const [zoomStr, setZoomStr] = useState<number>(0);
  const [errorStr, setErrorStr] = useState<string>('');
  const [codeResult, setCodeResult] = useState<string>('');

  const onError = (e: any) => {
    setErrorStr(e.nativeEvent.errorMessage);
  };

  const onZoom = (e: any) => {
    setZoomStr(e.nativeEvent.zoom);
  };

  const onReadCode = (e: any) => {
    setCodeResult(JSON.stringify(e));
  };

  return (
    <>
      <View>
        <Camera
          style={{width: '100%', height: 400}}
          ref={nativeRef}
          maxZoom={50}
          cameraType={CameraType.Back}
          onError={onError}
          onZoom={onZoom}
          scanBarcode
          onReadCode={onReadCode}
          ratioOverlay="4:3"
        />
      </View>
      <View>
        <Text style={styles.text}>zoom:{zoomStr}</Text>
        <Text style={styles.text}>code:{codeResult}</Text>
        <Text style={styles.text}>error:{errorStr}</Text>
      </View>
    </>
  );
};

const styles = StyleSheet.create({
  text: {
    fontSize: 20,
    textAlign: 'center',
    color: '#000',
    marginTop: 10,
  },
});


```


## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json` 添加 overrides字段

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
    "@react-native-oh-tpl/react-native-camera-kit": "file:../../node_modules/@react-native-oh-tpl/react-native-camera-kit/harmony/camera_kit.har"
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

### 3.在 ArkTs 侧引入 RTNCameraKitView 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RTNCameraKitView } from "@react-native-oh-tpl/react-native-camera-kit";

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === RTNCameraKitView.NAME) {
+   RTNCameraKitView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
+   })
+ }
...
}
...
```
在`entry/src/main/ets/pages/index.ets`中，如果当前文件中存在`arkTsComponentNames`数组(后续版本新增内容)，则需要在其中追加：`RTNCameraKitView.NAME`;

```ts
  ...
 const arkTsComponentNames: Array<string> = [..., RTNCameraKitView.NAME]; 
  ...
```

### 4.在 ArkTs 侧引入 RTNCameraKitPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RTNCameraKitPackage } from "@react-native-oh-tpl/react-native-camera-kit/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RTNCameraKitPackage(ctx),
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-camera-kit Releases](https://github.com/react-native-oh-library/react-native-camera-kit/releases)


## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Camera**：相机组件

| Name            | Description          | Type     | Required | Platform    | HarmonyOS Support |
|-----------------|----------------------|----------|----------|-------------|-------------------|
| ref | Reference on the camera view     | Ref | no       | All | yes               |
| style | Style to apply on the camera view | StyleProp\<ViewStyle> | no       | All | yes               |
| flashMode  | Camera flash mode. Default: `auto` | 'on'`/`'off'`/`'auto' | no       | All | yes               |
| focusMode  | Camera focus mode. Default: on     | 'on'`/`'off' | no       | All | yes               |
| zoomMode  | Enable the pinch to zoom gesture. Default: on     | 'on'`/`'off' | no       | All | yes               |
| zoom  | Control the zoom. Default: 1.0     | Number | no       | All | yes               |
| maxZoom  | Maximum zoom allowed (but not beyond what camera allows). Default: undefined (camera default max)     | Number | no       | All | yes               |
| onZoom  | Callback when user makes a pinch gesture, regardless of what the zoom prop was set to. Returned event contains zoom. Ex: onZoom={(e) => console.log(e.nativeEvent.zoom)}.     | Function | no       | All | yes               |
| torchMode  | Toggle flash light when camera is active. Default: off     | 'on'`/`'off' | no       | All | yes               |
| cameraType  | Choose what camera to use. Default: `CameraType. | 'front'/'back' | no       | All | yes               |
| onOrientationChange  | Callback when physical device orientation changes. Returned event contains orientation. Ex: onOrientationChange={(event) => console.log(event.nativeEvent.orientation)}. Use import { Orientation } from 'react-native-camera-kit'; if (event.nativeEvent.orientation === Orientation.PORTRAIT) { ... } to understand the new value     | Function | no       | iOS | yes               |
| onError  | Android only. Callback when camera fails to initialize. Ex: onError={(e) => console.log(e.nativeEvent.errorMessage)}.     | Function | no       | Android | yes               |
| shutterPhotoSound  |Android only. Enable or disable the shutter sound when capturing a photo. Default: `true`     | Boolean | no       | Android | yes   
| ratioOverlay  | Show a guiding overlay in the camera preview for the selected ratio. Does not crop image as of v9.0. Example: '16:9'     | String | no       | iOS | yes               |
| ratioOverlayColor  | Any color with alpha. Default: '#ffffff77'     | String | no       | All | yes               |
| resetFocusTimeout  | Dismiss tap to focus after this many milliseconds. Default 0 (disabled). Example: 5000 is 5 seconds.     | Number | no       | All | yes               |
| resetFocusWhenMotionDetected	  | Dismiss tap to focus when focus area content changes. Native iOS feature, see documentation: https://developer.apple.com/documentation/avfoundation/avcapturedevice/1624644-subjectareachangemonitoringenabl?language=objc). Default true.     | Boolean | no       | iOS | no             |
| resizeMode  | Determines the scaling and cropping behavior of content within the view. cover (resizeAspectFill on iOS) scales the content to fill the view completely, potentially cropping content if its aspect ratio differs from the view. contain (resizeAspect on iOS) scales the content to fit within the view's bounds without cropping, ensuring all content is visible but may introduce letterboxing. Default behavior depends on the specific use case.     | 'cover' / 'contain' | no       | iOS | no             |
| onCaptureButtonPressIn  | Callback when iPhone capture button is pressed in. Ex: onCaptureButtonPressIn={() => console.log("volume button pressed in")}    | Function | no       | iOS | yes          |
| onCaptureButtonPressOut  | Callback when iPhone capture button is released. Ex: onCaptureButtonPressOut={() => console.log("volume button released")}     | Function | no       | iOS | no             |

**ScanCode**：扫码组件

| Name            | Description          | Type     | Required | Platform    | HarmonyOS Support |
|-----------------|----------------------|----------|----------|-------------|-------------------|
| ref | Reference on the camera view     | Ref | no       | All      | yes               |
| style | Style to apply on the camera view | StyleProp\<ViewStyle> | no       | All | yes               |
| flashMode  | Get secret value     | 'on'`/`'off'`/`'auto' | no       | All | yes          |
| zoomMode  | Enable the pinch to zoom gesture. Default: on     | 'on'`/`'off' | no       | All | yes               |
| zoom  | Control the zoom. Default: 1.0     | Number | no       | All | yes               |
| maxZoom  | Maximum zoom allowed (but not beyond what camera allows). Default: undefined (camera default max)     | Number | no       | All | yes               |
| onZoom  | Callback when user makes a pinch gesture, regardless of what the zoom prop was set to. Returned event contains zoom. Ex: onZoom={(e) => console.log(e.nativeEvent.zoom)}.     | Function | no       | All | yes               |
| torchMode  | Toggle flash light when camera is active. Default: off     | 'on'`/`'off' | no       | All | yes               |
| cameraType                   | Choose what camera to use. Default: `CameraType.             | 'front'/'back'        | no       | All | no                |
| onOrientationChange  | Callback when physical device orientation changes. Returned event contains orientation. Ex: onOrientationChange={(event) => console.log(event.nativeEvent.orientation)}. Use import { Orientation } from 'react-native-camera-kit'; if (event.nativeEvent.orientation === Orientation.PORTRAIT) { ... } to understand the new value     | Function | no       | iOS | no             |
| onError  | Android only. Callback when camera fails to initialize. Ex: onError={(e) => console.log(e.nativeEvent.errorMessage)}.     | Function | no       | Android | yes               |
| resetFocusTimeout  | Dismiss tap to focus after this many milliseconds. Default 0 (disabled). Example: 5000 is 5 seconds.     | Number | no       | All | yes               |
| scanThrottleDelay  | Duration between scan detection in milliseconds. Default 2000 (2s)     | Number | no       | All | yes              |
| scanBarcode  | Enable barcode scanner. Default: `false`     | boolean | no       | All | yes               |
| showFrame  | Show frame in barcode scanner. Default: `false`     | boolean | no       | All | yes               |
| laserColor  | Color of barcode scanner laser visualization. Default: `red`     | string | no       | All | yes               |
| frameColor  | Color of barcode scanner frame visualization. Default: `yellow`     | string | no       | All | yes               |
| onReadCode  | Callback when scanner successfully reads barcode. Returned event contains `codeStringValue`. Default: `null`. Ex: `onReadCode={(event) => console.log(event.nativeEvent.codeStringValue)}     | Function | no       | All | yes               |

## 静态方法

| Name  | Description         | Type       | Required | Platform | HarmonyOS Support |
| ----- | ------------------- | ---------- | -------- | -------- | ----------------- |
| capture  | Capture image as JPEG.  | Promise<CaptureData> | No       | All      | Yes               |
| requestDeviceCameraAuthorization  | `AVAuthorizationStatusAuthorized` returns `true` otherwise, returns `false` | Promise<boolean> | No       | All      | Yes               |
| checkDeviceCameraAuthorizationStatus  | `AVAuthorizationStatusAuthorized` returns `true` otherwise, returns `false` | Promise<boolean> | All      | Yes               |Yes|


## 遗留问题

- [ ] 不支持查询传感器旋转角度 [issue#1](https://github.com/react-native-oh-library/react-native-camera-kit/issues/1) 
- [ ] 不支持使用前置相机进行扫码 [issue#2](https://github.com/react-native-oh-library/react-native-camera-kit/issues/2) 
- [ ] 不能同时设置flashMode和torchMode属性 [issue#3](https://github.com/react-native-oh-library/react-native-camera-kit/issues/3)
- [ ] 暂不支持onCaptureButtonPressOut属性 [issue#4](https://github.com/react-native-oh-library/react-native-camera-kit/issues/4)
- [ ] 暂不支持resetFocusWhenMotionDetected属性 [issue#5](https://github.com/react-native-oh-library/react-native-camera-kit/issues/5)
- [ ] 暂不支持resizeMode属性 [issue#6](https://github.com/react-native-oh-library/react-native-camera-kit/issues/6)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/teslamotors/react-native-camera-kit/blob/master/LICENSE) ，请自由地享受和参与开源。
