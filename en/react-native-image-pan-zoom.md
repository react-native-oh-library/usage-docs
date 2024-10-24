Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-pan-zoom</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/ascoders/react-native-image-zoom/blob/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ascoders/react-native-image-zoom/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-image-zoom)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-library/react-native-image-zoom Releases](https://github.com/react-native-oh-library/react-native-image-zoom/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-zoom@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-zoom@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```tsx
import React from "react";
import { Image, Text, Button } from "react-native";
import ImageZoom from "react-native-image-pan-zoom";
export default function () {
  const [cropWidth, setCropWidth] = React.useState<number>(300);
  const [cropHeight, setCropHeight] = React.useState<number>(300);
  const [imageWidth, setImageWidth] = React.useState<number>(600);
  const [imageHeight, setImageHeight] = React.useState<number>(600);
  const [panToMove, setPanToMove] = React.useState<boolean>(false);

  return (
    <>
      <Text>{`panToMove value: ${panToMove} `}</Text>
      <ImageZoom
        cropWidth={cropWidth}
        cropHeight={cropHeight}
        imageWidth={imageWidth}
        imageHeight={imageHeight}
        enableDoubleClickZoom={false}
        panToMove={panToMove}
        enableCenterFocus={false}
        pinchToZoom={false}
      >
        <Image
          style={{
            width: imageWidth,
            height: imageHeight,
          }}
          source={{
            uri: "https://img0.baidu.com/it/u=3570889183,2260151218&fm=253&fmt=auto&app=138&f=JPEG?w=800&h=500",
          }}
        />
      </ImageZoom>
      <Button
        title="change panToMove value"
        onPress={() => setPanToMove(!panToMove)}
      />
    </>
  );
}
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-image-zoom Releases](https://github.com/react-native-oh-library/react-native-image-zoom/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-image-zoom](https://github.com/ascoders/react-native-image-zoom)

ImageZoom

| Name                               | Description                                                                                                                                                           | Type                                                                                                                               | Required | Platform | HarmonyOS Support |
| ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| **cropWidth**                      | operating area width                                                                                                                                                  | number                                                                                                                             | YES      | ALL      | YES               |
| **cropHeight**                     | operating area height                                                                                                                                                 | number                                                                                                                             | YES      | ALL      | YES               |
| **imageWidth**                     | picture width                                                                                                                                                         | number                                                                                                                             | YES      | ALL      | YES               |
| **imageHeight**                    | picture height                                                                                                                                                        | number                                                                                                                             | YES      | ALL      | YES               |
| `onClick`                          | onClick                                                                                                                                                               | (eventParams: [IOnClick](https://github.com/ascoders/react-native-image-zoom/blob/master/src/image-zoom/image-zoom.type.ts))=>void | NO       | ALL      | YES               |
| `onDoubleClick`                    | onDoubleClick                                                                                                                                                         | (eventParams: IOnClick)=>void                                                                                                      | NO       | ALL      | YES               |
| `panToMove`                        | allow to move picture with one finger                                                                                                                                 | boolean                                                                                                                            | NO       | ALL      | YES               |
| `pinchToZoom`                      | allow scale with two fingers                                                                                                                                          | boolean                                                                                                                            | NO       | ALL      | YES               |
| `enableDoubleClickZoom`            | allow double-click to enlarge                                                                                                                                         | boolean                                                                                                                            | NO       | ALL      | YES               |
| `clickDistance`                    | how many finger movement can also trigger `onClick`                                                                                                                   | number                                                                                                                             | NO       | ALL      | YES               |
| `horizontalOuterRangeOffset`       | horizontal beyond the distance, the parent to do picture switching, you can listen to this function. When this function is triggered, you can do the switch operation | (offsetX?: number)=>void                                                                                                           | NO       | ALL      | YES               |
| `onDragLeft`                       | trigger to switch to the left of the graph, the left sliding speed exceeds the threshold when triggered                                                               | ()=>void                                                                                                                           | NO       | \        | NO                |
| `responderRelease`                 | let go but do not cancel                                                                                                                                              | (vx: number)=>void                                                                                                                 | NO       | ALL      | YES               |
| `maxOverflow`                      | maximum sliding threshold                                                                                                                                             | number                                                                                                                             | NO       | ALL      | YES               |
| `longPressTime`                    | long press threshold                                                                                                                                                  | number                                                                                                                             | NO       | ALL      | YES               |
| `onLongPress`                      | on longPress                                                                                                                                                          | (eventParams: [IOnClick](https://github.com/ascoders/react-native-image-zoom/blob/master/src/image-zoom/image-zoom.type.ts))=>void | NO       | ALL      | YES               |
| `doubleClickInterval	`              | time allocated for second click to be considered as doublClick event                                                                                                  | number                                                                                                                             | NO       | ALL      | YES               |
| `onMove`                           | reports movement position data (helpful to build overlays)                                                                                                            | ( position: [IOnMove](https://github.com/ascoders/react-native-image-zoom/blob/master/src/image-zoom/image-zoom.type.ts) )=>void   | NO       | ALL      | YES               |
| `centerOn`                         | if given this will cause the map to pan and zoom to the desired location                                                                                              | { x: number, y: number, scale: number, duration: number }                                                                          | NO       | ALL      | YES               |
| `enableSwipeDown`                  | for enabling vertical movement if user doesn't want it                                                                                                                | boolean                                                                                                                            | NO       | ALL      | YES               |
| `enableCenterFocus`                | for disabling focus on image center if user doesn't want it                                                                                                           | boolean                                                                                                                            | NO       | ALL      | YES               |
| `onSwipeDown`                      | function that fires when user swipes down                                                                                                                             | () => void                                                                                                                         | NO       | ALL      | YES               |
| `swipeDownThreshold`               | threshold for firing swipe down function                                                                                                                              | number                                                                                                                             | NO       | ALL      | YES               |
| `minScale`                         | minimum zoom scale                                                                                                                                                    | number                                                                                                                             | NO       | ALL      | YES               |
| `maxScale`                         | maximum zoom scale                                                                                                                                                    | number                                                                                                                             | NO       | ALL      | YES               |
| `useNativeDriver`                  | Whether to animate using [`useNativeDriver`](https://reactnative.dev/docs/animations#using-the-native-driver)                                                         | boolean                                                                                                                            | NO       | ALL      | YES               |
| `onStartShouldSetPanResponder`     | Override onStartShouldSetPanResponder behavior                                                                                                                        | () => boolean                                                                                                                      | NO       | ALL      | YES               |
| `onMoveShouldSetPanResponder`      | Override onMoveShouldSetPanResponder behavior                                                                                                                         | () => boolean                                                                                                                      | NO       | ALL      | YES               |
| `onPanResponderTerminationRequest` | Override onPanResponderTerminationRequest behavior                                                                                                                    | () => boolean                                                                                                                      | NO       | ALL      | YES               |
| `useHardwareTextureAndroid`        | for disabling rendering to hardware texture on Android                                                                                                                | boolean                                                                                                                            | NO       | Android  | NO                |

## Known Issues

- [x] 双指缩放在 harmony 框架侧不支持使用 [issues#1](https://github.com/react-native-oh-library/react-native-image-zoom/issues/1)

- [x] 长按图片后，rn 框架图片拖拽 Properties 导致程序崩溃 [issues#2](https://github.com/react-native-oh-library/react-native-image-zoom/issues/2)

- [x] onPanResponderTerminationRequest 方法，harmony 端与 android 端表现不一致 [issues#3](https://github.com/react-native-oh-library/react-native-image-zoom/issues/3)

## Others

- 下滑图片，然后双击放大，再次下滑表现异常，已在源库基础上修改[上库地址](https://github.com/react-native-oh-library/react-native-image-zoom)，源库已被存档，不能新建 issue，特此记录

- onDragLeft 此回调函数源码未实现，详见:[issues#103](https://github.com/ascoders/react-native-image-zoom/issues/103)

- useHardwareTextureAndroid 此 Properties 仅 Android 生效

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ascoders/react-native-image-zoom/blob/master/LICENSE).
