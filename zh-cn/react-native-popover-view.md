> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>@react-native-oh-tpl/react-native-popover-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-popover-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-popover-view/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-popover-view)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-tpl/react-native-popover-view> Releases](https://github.com/react-native-oh-library/react-native-popover-view/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-popover-view@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-popover-view@file:#
```

<!-- tabs:end -->

快速使用：

```typescript
import React, { useState } from 'react';
import {View, TouchableOpacity, Text, Button, Easing } from 'react-native';
import Popover, {PopoverMode, PopoverPlacement, Rect } from 'react-native-popover-view';

const PopoverDemo = () => {
    const [showPopoverA, setShowPopoverA] = useState(false);
    const [showPopoverB, setShowPopoverB] = useState(false);
    const [showPopoverC, setShowPopoverC] = useState(false);
    const [onOpenStart, setOnOpenStart] = useState(111);
    const [onOpenComplete, setOnOpenComplete] = useState(111);
    const [onCloseStart, setOnCloseStart] = useState(111);
    const [onCloseComplete, setOnCloseComplete] = useState(111);
    const [offsetValue, setOffsetValue] = useState(10);
    return (
        <View>
            <TouchableOpacity>
                <Text>test:from、isVisible</Text>
                <Button
                title= 'testA'
                onPress= {() => setShowPopoverA(true)}
                color= '#841584'
                />
            </TouchableOpacity>
            <Popover
              from= {new Rect(5,100,20,40)}
              isVisible= {showPopoverA}
              onRequestClose={() => {setShowPopoverA(false)}}
              >
              <Text>This is the contents of the popoverA</Text>
            </Popover>
            <TouchableOpacity>
                <Text>test:mode、offset、placement、popoverShift、popoverStyle、backgroundStyle、arrowSize、arrowShift、animationConfig</Text>
                <Button
                onPress = {() => setShowPopoverB(true)}
                title = 'testB'
                color = '#cc15cc'
                />
            </TouchableOpacity>
            <Popover
              from = {new Rect(5,100,20,40)}
              isVisible = {showPopoverB}
              mode = {PopoverMode.RN_MODAL}
              offset = {10}
              placement= {PopoverPlacement.Top}
              popoverShift= {{x:1}}
              popoverStyle= {{backgroundColor: '#f00'}}
              backgroundStyle= {{backgroundColor: '#00f'}}
              arrowSize= {{width:30,height:8}}
              arrowShift= {2}
              animationConfig= {{duration: 600,easing:Easing.inOut(Easing.quad)}}
              onRequestClose= {() => {setShowPopoverB(false)}}
              >
              <Text>This is the contents of the popoverB</Text>
            </Popover>

            <TouchableOpacity>
                <Text>test:displayArea、displayAreaInsets、onOpenStart、onOpenComplete、onRequestClose、onCloseStart、onCloseComplete、onPositionChange、debug</Text>
                <Button
                onPress = {() => setShowPopoverC(true)}
                title = 'testC'
                color = '#87cc94'
                />
            </TouchableOpacity>
            <Popover
              from = {new Rect(5,100,20,40)}
              isVisible = {showPopoverC}
              offset = {offsetValue}
              debug = {true}
              displayArea = {new Rect(50,50,50,50)}
              displayAreaInsets = {{top:20}}
              onOpenStart = {() => {setOnOpenStart(222)}}
              onOpenComplete= {() => {setOnOpenComplete(222)}}
              onRequestClose= {() => {setShowPopoverC(false)}}
              onCloseStart= {() => {setOnCloseStart(222)}}
              onCloseComplete= {() => {setOnCloseComplete(222)}}
              onPositionChange= {() => {setOnCloseStart(222)}}
            >
              <Text>This is the contents of the popoverC</Text>
            </Popover>
            <Text>onOpenStart {onOpenStart}</Text>
            <Text>onOpenComplete {onOpenComplete}</Text>
            <Text>onCloseStart {onCloseStart}</Text>
            <Text>onCloseComplete {onCloseComplete}</Text>
            <Text>onPositionChange {offsetValue}</Text>
            <Button
            onPress = {() => setOffsetValue(offsetValue === 10 ? 20 : 10)}
            title = 'change position'
            color = '#876664'
            />
        </View>
      );
}

export default PopoverDemo;
```

## 约束与限制

#### 兼容性

在下述版本验证通过：

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

**属性&方法**

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                 | Description                                                                                                                                                                                                                                                                                                                                                                    | Type                  | Required | Platform | HarmonyOS Support | remark         |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------- | -------- | -------- | ----------------- | -------------- |
| from                 | Popover source. See From section below.                                                                                                                                                                                                                                                                                                                                        | multiple              | no       | All      | yes               |
| isVisible            | Show/Hide the popover. Required if from is not a Touchable or function that uses showPopover call (see examples). If supplied, takes precedence regardless of from.                                                                                                                                                                                                            | bool                  | no       | All      | yes               |
| mode                 | How to position the popover, one of 'top', 'bottom', 'left', 'right', 'floating', or 'auto'. When 'auto' is specified, it will try to determine the best placement so that the popover is fully visible within displayArea. If an array of options is passed in, it will pick the first option that can accommodate the content.                                               | string OR string list | no       | All      | yes               |
| placement            | One of: 'rn-modal', 'js-modal', 'tooltip'. See Mode section below for details.                                                                                                                                                                                                                                                                                                 | string                | no       | All      | yes               |
| offset               | The amount to shift the popover away from the source. Does not apply if the popover is centered.                                                                                                                                                                                                                                                                               | number                | no       | All      | yes               |
| popoverStyle         | The style of the popover itself. You can override the borderRadius, backgroundColor, or any other style prop for a View.                                                                                                                                                                                                                                                       | object                | no       | All      | yes               |
| popoverShift         | How much to shift the popover in each direction, as a multiplier. Object of shape { x: -1 to 1, y: -1 to 1 }, where both x and y are optional. -1 shifts the popover all the way to the left/top and 1 shifts it to the right/bottom. Currently only applies when placement is floating, but this will apply to all placements in a future version.                            | object                | no       | All      | yes               |
| backgroundStyle      | The style of the background view. Default is a black background with 0.5 opacity.                                                                                                                                                                                                                                                                                              | object                | no       | All      | yes               |
| arrowSize            | The size of the arrow, as an object with width & height properties. The width of the arrow is the size of the arrow on the edge that touches the popover (base of isosceles triangle), while the height covers the distance from the popover to the source view, regardless of the placement of the popover. You can use { width: 0, height: 0 } to hide the arrow completely. | object                | no       | All      | yes               |
| arrowShift           | How much to shift the arrow to either side, as a multiplier. -1 will shift it all the way to the left (or top) corner of the source view, while 1 will shift all the way to the right (or bottom) corner. A value of 0.5 or -0.8 will shift it partly to one side.                                                                                                             | object                | no       | All      | yes               |
| onOpenStart          | Callback to be fired when the open animation starts (before animation)                                                                                                                                                                                                                                                                                                         | function              | no       | All      | yes               |
| onOpenComplete       | Callback to be fired when the open animation ends (after animation)                                                                                                                                                                                                                                                                                                            | function              | no       | All      | yes               |
| onRequestClose       | Callback to be fired when the user taps outside the popover (on the background) or taps the system back button on Android                                                                                                                                                                                                                                                      | function              | no       | All      | yes               |
| onCloseStart         | Callback to be fired when the popover starts closing (before animation)                                                                                                                                                                                                                                                                                                        | function              | no       | All      | yes               |
| onCloseComplete      | Callback to be fired when the popover is finished closing (after animation)                                                                                                                                                                                                                                                                                                    | function              | no       | All      | yes               |
| onPositionChange     | Callback to be fired when the popover position finishes moving position (after animation)                                                                                                                                                                                                                                                                                      | function              | no       | All      | yes               |
| animationConfig      | An object containing any configuration options that can be passed to Animated.timing (e.g. { duration: 600, easing: Easing.inOut(Easing.quad) }). The configuration options you pass will override the defaults for all animations.                                                                                                                                            | object                | no       | All      | yes               |
| displayArea          | Area where the popover is allowed to be displayed. By default, this will be automatically calculated to be the size of the display, or the size of the parent component if mode is not 'rn-modal'.                                                                                                                                                                             | rect                  | no       | All      | yes               |
| displayAreaInsets    | Insets to apply to the display area. The Popover will not be allowed to go beyond the display area minus the insets.                                                                                                                                                                                                                                                           | object                | no       | All      | yes               |
| statusBarTranslucent | For 'rn-modal' mode on Android only. Determines whether the background should go under the status bar. Passed through to RN Modal component, see their docs as well.                                                                                                                                                                                                           | bool                  | no       | Android  | no                | 原库仅支持安卓 |
| verticalOffset       | The amount to vertically shift the popover on the screen, for use in correcting an occasional issue on Android. In certain Android configurations, you may need to apply a verticalOffset of -StatusBar.currentHeight for the popover to originate from the correct place. For shifting the popover in other situations, the offset prop should be used.                       | number                | no       | Android  | no                | 原库仅支持安卓 |
| debug                | Set this to true to turn on debug logging to the console. This is useful for figuring out why a Popover isn't showing.                                                                                                                                                                                                                                                         | bool                  | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/react-native-oh-library/react-native-popover-view/blob/sig/LICENSE) ，请自由地享受和参与开源。
