> Template version: v0.2.2

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



> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-camera-kit)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-library/react-native-camera-kit Releases](https://github.com/react-native-oh-library/react-native-camera-kit/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-camera-kit
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-camera-kit
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.
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
        <Button title="onPhoto" onPress={onPhoto} />
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
    "@react-native-oh-tpl/react-native-camera-kit": "file:../../node_modules/@react-native-oh-tpl/react-native-camera-kit/harmony/camera_kit.har"
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

### 3. Configuring CMakeLists and Introducing xxx Package

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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
> [!TIP] If the repository uses a mixed solution, the component name needs to be added.  

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ RTNCameraKitView.NAME
  ];
```

### 4. Introducing RTNCameraKitPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

Check the release version information in the release address of the third-party library：[@react-native-oh-library/react-native-camera-kit Releases](https://github.com/react-native-oh-library/react-native-camera-kit/releases)

### Permission Requirements

The following permissions include the `system_basic` permission, but the default application permission is `normal`. Only the `normal` permission can be used. Therefore, the error * 9568289 * * * may be reported during the installation of the HAP package. For details, see [Document](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/bm-tool-V5#ZH-CN_TOPIC_0000001884757326__%E5%AE%89%E8%A3%85hap%E6%97%B6%E6%8F%90%E7%A4%BAcode9568289-error-install-failed-due-to-grant-request-permissions-failed) Change the application level to `system_basic`.

#### Add permissions to the module.json5 file in the entry directory.

Open `entry/src/main/module.json5` and add the following information:

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.CAMERA",
+    "reason": "$string:camera_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  },
+  {
+    "name": "ohos.permission.MICROPHONE",
+    "reason": "$string:microphone_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  },
+  {
+    "name": "ohos.permission.APPROXIMATELY_LOCATION",
+    "reason": "$string:location_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"inuse"
+    }
+  }
]
```

#### Add the reason for applying for the preceding permission to the entry directory.

Open `entry/src/main/resources/base/element/string.json` and add the following information:

```diff
...
{
  "string": [
+    {
+      "name": "camera_reason",
+      "value": "camera_reason"
+    },
+    {
+      "name": "location_reason",
+      "value": "location_reason"
+    },
+    {
+      "name": "microphone_reason",
+      "value": "microphone_reason"
+    },
  ]
}
```

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**Camera**：CameraComponent

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

**ScanCode**：ScanCodeComponent

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

## Methods

| Name  | Description         | Type       | Required | Platform | HarmonyOS Support |
| ----- | ------------------- | ---------- | -------- | -------- | ----------------- |
| capture  | Capture image as JPEG.  | Promise<CaptureData> | No       | All      | Yes               |
| requestDeviceCameraAuthorization  | `AVAuthorizationStatusAuthorized` returns `true` otherwise, returns `false` | Promise<boolean> | No       | All      | Yes               |
| checkDeviceCameraAuthorizationStatus  | `AVAuthorizationStatusAuthorized` returns `true` otherwise, returns `false` | Promise<boolean> | All      | Yes               |Yes|


## Known Issues

- [ ] The sensor rotation angle cannot be queried. [issue#1](https://github.com/react-native-oh-library/react-native-camera-kit/issues/1) 
- [ ] The front camera cannot be used for code scanning. [issue#2](https://github.com/react-native-oh-library/react-native-camera-kit/issues/2) 
- [ ] The flashMode and torchMode attributes cannot be set at the same time. [issue#3](https://github.com/react-native-oh-library/react-native-camera-kit/issues/3)
- [ ] The onCaptureButtonPressOut attribute is not supported. [issue#4](https://github.com/react-native-oh-library/react-native-camera-kit/issues/4)
- [ ] The resetFocusWhenMotionDetected attribute is not supported. [issue#5](https://github.com/react-native-oh-library/react-native-camera-kit/issues/5)
- [ ] The resizeMode attribute is not supported currently. [issue#6](https://github.com/react-native-oh-library/react-native-camera-kit/issues/6)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/teslamotors/react-native-camera-kit/blob/master/LICENSE).
