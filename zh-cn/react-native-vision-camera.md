> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-vision-camera</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mrousavy/react-native-vision-camera">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mrousavy/react-native-vision-camera/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-vision-camera)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-vision-camera Releases](https://github.com/react-native-oh-library/react-native-vision-camera/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-vision-camera
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-vision-camera
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import { Button, Text, View } from 'react-native';
import React, { useRef } from 'react';
import { Camera, useCameraDevice, useCameraFormat, useCameraPermission } from 'react-native-vision-camera';

export default function VisionCameraDemo() {
    const device = useCameraDevice('back');
    const format = useCameraFormat(device, [
        { videoResolution: { width: 3048, height: 2160 } },
        { fps: 60 },
    ]);
    const { hasPermission, requestPermission } = useCameraPermission();
    const camera = useRef<Camera>(null);

    if (!device) {
        return <Text>No Devices</Text>;
    }

    if (!hasPermission) {
        requestPermission();
    }

    const onTakePhoto = async () => {
        const photoFile = await camera.current?.takePhoto();
        console.log("takePhoto photoFile:" + photoFile);
    };

    return (
        <View style={{ flex: 1 }}>
            <Camera
                style={{ flex: 1 }}
                ref={camera}
                device={device}
                format={format}
                isActive={true}
                preview={true}
                photo={true}
            />
            <View style={{ width: '100%', position: 'absolute', bottom: 0, left: 0, zIndex: 999 }}>
                <Button title="拍照" onPress={onTakePhoto}></Button>
            </View>
        </View>
    );
}

```

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
    "@react-native-oh-tpl/react-native-vision-camera": "file:../../node_modules/@react-native-oh-tpl/react-native-vision-camera/harmony/vision_camera.har",
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

### 3.配置 CMakeLists 和引入 xxxPackge

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-vision-camera/src/main/cpp" ./vision-camera)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")
+file(GLOB VISION_CAMERA_CPP_FILES "${OH_MODULES}/@react-native-oh-tpl/react-native-vision-camera/src/main/cpp/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
+    ${VISION_CAMERA_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_vision_camera)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+#include "VisionCameraPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<VisionCameraPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 VisionCameraView 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { VisionCameraView } from "@react-native-oh-tpl/react-native-vision-camera";

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === VisionCameraView.NAME) {
+   VisionCameraView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
+   })
+ }
...
}
...
```
在`entry/src/main/ets/pages/index.ets`中，如果当前文件中存在`arkTsComponentNames`数组(后续版本新增内容)，则需要在其中追加：`VisionCameraView.NAME`;

```ts
  ...
 const arkTsComponentNames: Array<string> = [..., VisionCameraView.NAME]; 
  ...
```



### 5.在 ArkTs 侧引入 VisionCameraModulePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { VisionCameraModulePackage } from "@react-native-oh-tpl/react-native-vision-camera/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new VisionCameraModulePackage(ctx),
  ];
}
```

### 6.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-vision-camera Releases](https://github.com/react-native-oh-library/react-native-vision-camera/releases)

### 权限要求

以下权限中有`system_basic` 权限，而默认的应用权限是 `normal` ，只能使用 `normal` 等级的权限，所以可能会在安装hap包时报错**9568289**，请参考 [文档](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/bm-tool-V5#ZH-CN_TOPIC_0000001884757326__%E5%AE%89%E8%A3%85hap%E6%97%B6%E6%8F%90%E7%A4%BAcode9568289-error-install-failed-due-to-grant-request-permissions-failed) 修改应用等级为 `system_basic`

####  在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

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

#### 在 entry 目录下添加申请以上权限的原因

打开 `entry/src/main/resources/base/element/string.json`，添加：

```diff
...
{
  "string": [
+    {
+      "name": "camera_reason",
+      "value": "使用相机"
+    },
+    {
+      "name": "location_reason",
+      "value": "获取当前位置"
+    },
+    {
+      "name": "microphone_reason",
+      "value": "使用麦克风"
+    },
  ]
}
```

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                               | Description                                                  | Type     | Required | Platform          | HarmonyOS  Support |
| ---------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- | ------------------ |
| isActive                           | Whether the Camera should actively stream video frames, or not | boolean  | yes      | All               | yes                |
| device                             | The Camera Device to use                                     | object   | yes      | All               | yes                |
| preview                            | Enables **preview** streaming                                | boolean  | no       | All               | yes                |
| photo                              | Enables **photo capture** with the `takePhoto` function      | boolean  | no       | All               | yes                |
| video                              | Enables **video capture** with the `startRecording` function | boolean  | no       | All               | yes                |
| audio                              | Enables **audio capture** for video recordings               | boolean  | no       | All               | yes                |
| enableLocation                     | Enables location streaming to add GPS EXIF tags to captured photos and  videos | boolean  | no       | All               | yes                |
| torch                              | Set the current torch mode                                   | string   | no       | All               | yes                |
| zoom                               | Specifies the zoom factor of the current camera, in  "factor"/scale | number   | no       | All               | yes                |
| enableZoomGesture                  | Enables or disables the native pinch to zoom gesture         | boolean  | no       | All               | yes                |
| exposure                           | Specifies the Exposure bias of the current camera. A lower value means  darker images, a higher value means brighter images | number   | no       | All               | yes                |
| format                             | Selects a given format. By default, the best matching format is chosen | object   | no       | All               | yes                |
| resizeMode                         | Specifies the Preview's resize mode                          | string   | no       | All               | yes                |
| androidPreviewViewType             | Specifies the implementation mode for the Preview View on Android | string   | no       | Android | no                |
| fps                                | Specify the frames per second this camera should stream frames at. | number   | no       | All               | yes                |
| videoHdr                           | Enables or disables HDR Video Streaming for Preview, Video and Frame  Processor via a 10-bit wide-color pixel format | boolean  | no       | All               | yes                |
| photoHdr                           | Enables or disables HDR Photo Capture via a double capture routine that  combines low- and high exposure photos | boolean  | no       | Android/iOS       | no                 |
| photoQualityBalance                | Configures the photo pipeline for a specific quality balance  prioritization. | string   | no       | All               | yes                |
| enableBufferCompression            | Enables or disables lossy buffer compression for the video stream | boolean  | no       | Android/iOS       | no                 |
| lowLightBoost                      | Enables or disables low-light boost on this camera device.   | boolean  | no       | Android/iOS       | no                 |
| videoStabilizationMode             | Specifies the video stabilization mode to use.               | string   | no       | All               | yes                |
| enableDepthData                    | Enables or disables depth data delivery for photo capture.   | boolean  | no       | Android/iOS       | no                 |
| enablePortraitEffectsMatteDelivery | A boolean specifying whether the photo render pipeline is prepared for  portrait effects matte delivery. | boolean  | no       | Android/iOS       | no                 |
| enableFpsGraph                     | If `true`, show a debug view to display the FPS of the Video Pipeline | boolean  | no       | Android/iOS       | no                 |
| onError                            | Called when any kind of runtime error occured.               | function | no       | All               | yes                |
| onInitialized                      | Called when the camera session was successfully initialized. This will  get called everytime a new device is set. | function | no       | All               | yes                |
| onStarted                          | Called when the camera started the session (`isActive={true}`) | function | no       | All               | yes                |
| onStopped                          | Called when the camera stopped the session (`isActive={false}`) | function | no       | All               | yes                |
| onShutter                          | Called just before a photo or snapshot is captured.          | function | no       | All               | yes                |
| codeScanner                        | A CodeScanner that can detect QR-Codes or Barcodes using platform-native  APIs | object   | no       | All               | yes                |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                            | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| takePhoto                       | Take a single photo and write it's content to a temporary file. | function | no       | All         | yes               |
| focus                           | Focus the camera to a specific point in the coordinate system. | function | no       | All         | yes               |
| startRecording                  | Start a new video recording.                                 | function | no       | All         | yes               |
| stopRecording                   | Stop the current video recording.                            | function | no       | All         | yes               |
| pauseRecording                  | Pauses the current video recording.                          | function | no       | All         | yes               |
| resumeRecording                 | Resumes a currently paused video recording.                  | function | no       | All         | yes               |
| getAvailableCameraDevices       | Get a list of all available camera devices on the current phone. | function | no       | All         | yes               |
| getCameraPermissionStatus       | Gets the current Camera Permission Status.                   | function | no       | All         | yes               |
| requestCameraPermission         | Shows a "request permission" alert to the user, and resolves  with the new camera permission status. | function | no       | All         | yes               |
| getMicrophonePermissionStatus   | Gets the current Microphone-Recording Permission Status.     | function | no       | All         | yes               |
| requestMicrophonePermission     | Shows a "request permission" alert to the user, and resolves  with the new microphone permission status. | function | no       | All         | yes               |
| getLocationPermissionStatus     | Gets the current Location Permission Status.                 | function | no       | All         | yes               |
| requestLocationPermission       | Shows a "request permission" alert to the user, and resolves  with the new location permission status. | function | no       | All         | yes               |
| takeSnapshot                    | Captures a snapshot of the Camera view and write it's content to a  temporary file. | function | no       | Android/iOS | no                |
| cancelRecording                 | Cancel the current video recording. The temporary video file will be  deleted, | function | no       | Android/iOS | no                |
| addCameraDevicesChangedListener | Adds a listener that gets called everytime the Camera Devices change | function | no       | Android/iOS | no                |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                    | Description                                                  | Type | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | ---- | -------- | -------- | ----------------- |
| useCameraDevice         | Get the best matching Camera device that best satisfies your  requirements using a sorting filter. | hook | no       | All      | yes               |
| useCameraDevices        | Get all available Camera Devices this phone has.             | hook | no       | All      | yes               |
| useCameraFormat         | Get the best matching Camera format for the given device that  satisfies your requirements using a sorting filter. By default, formats are  sorted by highest to lowest resolution. | hook | no       | All      | yes               |
| useCameraPermission     | Returns whether the user has granted permission to use the  Camera, or not. | hook | no       | All      | yes               |
| useMicrophonePermission | Returns whether the user has granted permission to use the  Microphone, or not. | hook | no       | All      | yes               |
| useLocationPermission   | Returns whether the user has granted permission to use the  Location, or not. | hook | no       | All      | yes               |
| useCodeScanner          | create a `CodeScanner` instance and pass it to the  `<Camera>` | hook | no       | All      | yes               |
| useFrameProcessor       | Returns a memoized Frame Processor function wich you can pass  to the `<Camera>`. | hook | no       | All      | no                |

## 遗留问题

- [ ] 不支持拍照HDR [issue#1](https://github.com/react-native-oh-library/react-native-vision-camera/issues/1) 
- [ ] 不支持有损缓冲压缩 [issue#2](https://github.com/react-native-oh-library/react-native-vision-camera/issues/2) 
- [ ] 没有夜景模式 [issue#3](https://github.com/react-native-oh-library/react-native-vision-camera/issues/3) 
- [ ] 没有实现深度数据能力 [issue#4](https://github.com/react-native-oh-library/react-native-vision-camera/issues/4) 
- [ ] 依赖三方库skia未 HarmonyOS 化 [issue#5](https://github.com/react-native-oh-library/react-native-vision-camera/issues/5) 
- [ ] 不支持内容失真校正 [issue#6](https://github.com/react-native-oh-library/react-native-vision-camera/issues/6) 
- [ ] 不支持消除红眼 [issue#7](https://github.com/react-native-oh-library/react-native-vision-camera/issues/7) 
- [ ] 快门声音无法独立控制 [issue#8](https://github.com/react-native-oh-library/react-native-vision-camera/issues/8) 
- [ ] 不支持查询传感器旋转角度 [issue#9](https://github.com/react-native-oh-library/react-native-vision-camera/issues/9) 
- [ ] 不支持查询硬件级别 [issue#10](https://github.com/react-native-oh-library/react-native-vision-camera/issues/10) 
- [ ] 不支持查询设备正确对焦的最小距离 [issue#11](https://github.com/react-native-oh-library/react-native-vision-camera/issues/11) 
- [ ] 不支持查询设备名称 [issue#12](https://github.com/react-native-oh-library/react-native-vision-camera/issues/12) 
- [ ] 查询的CameraType一直是相机类型未指定 [issue#13](https://github.com/react-native-oh-library/react-native-vision-camera/issues/13) 
- [ ] 不支持查询传感器旋转角度 [issue#14](https://github.com/react-native-oh-library/react-native-vision-camera/issues/14) 
- [ ] 不支持查询是否支持弱光增强 [issue#15](https://github.com/react-native-oh-library/react-native-vision-camera/issues/15) 
- [ ]  HarmonyOS 侧相机无法获取视频视野 [issue#16](https://github.com/react-native-oh-library/react-native-vision-camera/issues/16) 
- [ ] 不支持查询maxISO和minISO [issue#17](https://github.com/react-native-oh-library/react-native-vision-camera/issues/17) 
- [ ] 不支持保存快照 [issue#18](https://github.com/react-native-oh-library/react-native-vision-camera/issues/18) 
- [ ] 视频录制取消时无法删除临时文件 [issue#19](https://github.com/react-native-oh-library/react-native-vision-camera/issues/19) 
- [ ] 无法监听相机设备变更 [issue#20](https://github.com/react-native-oh-library/react-native-vision-camera/issues/20) 

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mrousavy/react-native-vision-camera/blob/main/LICENSE) ，请自由地享受和参与开源。

