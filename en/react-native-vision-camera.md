> Template version: v0.2.2

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



> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-vision-camera)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-vision-camera Releases](https://github.com/react-native-oh-library/react-native-vision-camera/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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
                <Button title="photograph" onPress={onTakePhoto}></Button>
            </View>
        </View>
    );
}

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
    "@react-native-oh-tpl/react-native-vision-camera": "file:../../node_modules/@react-native-oh-tpl/react-native-vision-camera/harmony/vision_camera.har",
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

### 3. Configuring CMakeLists and Introducing VisionCameraPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4. Introducing VisionCameraView Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

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
In `entry/src/main/ets/pages/index. ets`, if there is an `arkTsWidgetNames` array in the current file (which will be added in later versions), it is necessary to append `VisionCameraView` to it NAME`;

```ts
  ...
 const arkTsComponentNames: Array<string> = [..., VisionCameraView.NAME]; 
  ...
```

### 5. Introducing VisionCameraModulePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 6. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-vision-camera Releases](https://github.com/react-native-oh-library/react-native-vision-camera/releases)

### Permission Requirements

Among the following permissions, there is the system_basic permission, while the default application permission is normal. Only normal level permissions can be used, so you may encounter an error 9568289 when installing the hap package. Please refer to the [document](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/bm-tool-V5#ZH-CN_TOPIC_0000001884757326__%E5%AE%89%E8%A3%85hap%E6%97%B6%E6%8F%90%E7%A4%BAcode9568289-error-install-failed-due-to-grant-request-permissions-failed) to modify the application level to system_basic.

####  Include applicable permissions in the module.json5 file within the entry directory.

Open `entry/src/main/module.json5` and add the following code:

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

#### Apply the reasons for applicable permission in the entry directory.

Open `entry/src/main/resources/base/element/string.json` and add the following code:

```diff
...
{
  "string": [
+    {
+      "name": "camera_reason",
+      "value": "use camera"
+    },
+    {
+      "name": "location_reason",
+      "value": "Get current location"
+    },
+    {
+      "name": "microphone_reason",
+      "value": "Use microphone"
+    },
  ]
}
```

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

- [ ] HDR photography not supported [issue#1](https://github.com/react-native-oh-library/react-native-vision-camera/issues/1) 
- [ ] Lossy buffer compression not supported [issue#2](https://github.com/react-native-oh-library/react-native-vision-camera/issues/2) 
- [ ] Night mode not available [issue#3](https://github.com/react-native-oh-library/react-native-vision-camera/issues/3) 
- [ ] Depth data capabilities not implemented [issue#4](https://github.com/react-native-oh-library/react-native-vision-camera/issues/4) 
- [ ] Third-party library skia is not HarmonyOS-compatible [issue#5](https://github.com/react-native-oh-library/react-native-vision-camera/issues/5) 
- [ ] Content distortion correction not supported [issue#6](https://github.com/react-native-oh-library/react-native-vision-camera/issues/6) 
- [ ] Red-eye removal not supported [issue#7](https://github.com/react-native-oh-library/react-native-vision-camera/issues/7) 
- [ ] Shutter sound cannot be independently controlled [issue#8](https://github.com/react-native-oh-library/react-native-vision-camera/issues/8) 
- [ ] Querying sensor rotation angle not supported [issue#9](https://github.com/react-native-oh-library/react-native-vision-camera/issues/9) 
- [ ] Querying hardware level not supported [issue#10](https://github.com/react-native-oh-library/react-native-vision-camera/issues/10) 
- [ ] Querying the minimum distance for proper device focusing not supported [issue#11](https://github.com/react-native-oh-library/react-native-vision-camera/issues/11) 
- [ ] Querying device name not supported [issue#12](https://github.com/react-native-oh-library/react-native-vision-camera/issues/12) 
- [ ] Queried CameraType always shows as unspecified camera type [issue#13](https://github.com/react-native-oh-library/react-native-vision-camera/issues/13) 
- [ ] Querying sensor rotation angle not supported (Duplicate) [issue#14](https://github.com/react-native-oh-library/react-native-vision-camera/issues/14) 
- [ ] Querying support for low-light enhancement not supported [issue#15](https://github.com/react-native-oh-library/react-native-vision-camera/issues/15) 
- [ ] Camera on HarmonyOS side cannot obtain video field of view [issue#16](https://github.com/react-native-oh-library/react-native-vision-camera/issues/16) 
- [ ] Querying maxISO and minISO not supported [issue#17](https://github.com/react-native-oh-library/react-native-vision-camera/issues/17) 
- [ ] Saving snapshots not supported [issue#18](https://github.com/react-native-oh-library/react-native-vision-camera/issues/18) 
- [ ] Temporary files cannot be deleted when video recording is canceled [issue#19](https://github.com/react-native-oh-library/react-native-vision-camera/issues/19) 
- [ ] Camera device changes cannot be monitored [issue#20](https://github.com/react-native-oh-library/react-native-vision-camera/issues/20) 

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mrousavy/react-native-vision-camera/blob/main/LICENSE).

