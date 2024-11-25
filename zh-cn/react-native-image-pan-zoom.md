模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-zoom)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-image-zoom Releases](https://github.com/react-native-oh-library/react-native-image-zoom/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-zoom
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-zoom
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React from "react"
import { Image, Text, Button } from "react-native"
import ImageZoom from "react-native-image-pan-zoom"
export default function () {
  const [cropWidth, setCropWidth] = React.useState<number>(300)
  const [cropHeight, setCropHeight] = React.useState<number>(300)
  const [imageWidth, setImageWidth] = React.useState<number>(600)
  const [imageHeight, setImageHeight] = React.useState<number>(600)
  const [panToMove, setPanToMove] = React.useState<boolean>(false)

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
  )
}
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-image-zoom Releases](https://github.com/react-native-oh-library/react-native-image-zoom/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-image-zoom](https://github.com/ascoders/react-native-image-zoom)

ImageZoom

| Name   | Description          | Type          | Required | Platform | HarmonyOS Support |   
| ---- | ------------------ | ----------------------- | -------- | -------- | ----------------- | 
| **cropWidth**   | operating area width              | number      | YES      | ALL      | YES    |           
| **cropHeight**           | operating area height                                                                                                                                                 | number                                                                                                                             | YES      | ALL      | YES               |                                                                                            
| **imageWidth**           | picture width                                                                                                                                                         | number                                                                                                                             | YES      | ALL      | YES                                                                                                           
| **imageHeight**          | picture height                                                                                                                                                        | number                                                                                                                             | YES      | ALL      | YES                                                                                                           |
| `onClick`                          | onClick                                                                                                                                                               | (eventParams: [IOnClick](https://github.com/ascoders/react-native-image-zoom/blob/master/src/image-zoom/image-zoom.type.ts))=>void | NO       | ALL      | YES                                                                                                           |
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

## 遗留问题

- [x] 双指缩放在 harmony 框架侧不支持使用 [issues#1](https://github.com/react-native-oh-library/react-native-image-zoom/issues/1)

- [x] 长按图片后，rn 框架图片拖拽属性导致程序崩溃 [issues#2](https://github.com/react-native-oh-library/react-native-image-zoom/issues/2)

- [x] onPanResponderTerminationRequest 方法，harmony 端与 android 端表现不一致 [issues#3](https://github.com/react-native-oh-library/react-native-image-zoom/issues/3)


## 其他

- 下滑图片，然后双击放大，再次下滑表现异常，已在源库基础上修改[上库地址](https://github.com/react-native-oh-library/react-native-image-zoom)，源库已被存档，不能新建 issue，特此记录

- onDragLeft 此回调函数源码未实现，详见:[issues#103](https://github.com/ascoders/react-native-image-zoom/issues/103)

- useHardwareTextureAndroid 此属性仅 Android 生效

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ascoders/react-native-image-zoom/blob/master/LICENSE) ，请自由地享受和参与开源。
