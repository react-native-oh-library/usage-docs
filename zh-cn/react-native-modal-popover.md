<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-modal-popover</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/doomsower/react-native-modal-popover">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/doomsower/react-native-modal-popover/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-modal-popover)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-modal-popover Releases](https://github.com/react-native-oh-library/react-native-modal-popover/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-modal-popover@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-modal-popover@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js

import React from 'react';
import { TestSuite, Tester, TestCase } from '@rnoh/testerino';
import { Button, StyleSheet, Text, View, Dimensions } from 'react-native';
import { Popover, usePopover } from 'react-native-modal-popover';
const { width, height } = Dimensions.get('window');

const styles = StyleSheet.create({
  app: {
    ...StyleSheet.absoluteFillObject,
    width: '100%',
    height: height - 200,
    display: 'flex',
    flexDirection: 'column',
    alignItems: 'flex-start',
    justifyContent: 'space-between',
    backgroundColor: '#c2ffd2',
  },
  content: {
    padding: 16,
    backgroundColor: 'pink',
    borderRadius: 8,
  },
  arrow: {
    borderTopColor: 'pink',
  },
  background: {
    backgroundColor: 'rgba(0, 0, 255, 0.5)',
  },
});

export function PopoverCenterExample() {
  const {
    openPopover,
    closePopover,
    popoverVisible,
    touchableRef,
    popoverAnchorRect,
  } = usePopover();
  const {
    openPopover: openPopover1,
    closePopover: closePopover1,
    popoverVisible: popoverVisible1,
    touchableRef: touchableRef1,
    popoverAnchorRect: popoverAnchorRect1,
  } = usePopover();
  const {
    openPopover: openPopover2,
    closePopover: closePopover2,
    popoverVisible: popoverVisible2,
    touchableRef: touchableRef2,
    popoverAnchorRect: popoverAnchorRect2,
  } = usePopover();
  const {
    openPopover: openPopover4,
    closePopover: closePopover4,
    popoverVisible: popoverVisible4,
    touchableRef: touchableRef4,
    popoverAnchorRect: popoverAnchorRect4,
  } = usePopover();
  const {
    openPopover: openPopover3,
    closePopover: closePopover3,
    popoverVisible: popoverVisible3,
    touchableRef: touchableRef3,
    popoverAnchorRect: popoverAnchorRect3,
  } = usePopover();
  const {
    openPopover: openPopover5,
    closePopover: closePopover5,
    popoverVisible: popoverVisible5,
    touchableRef: touchableRef5,
    popoverAnchorRect: popoverAnchorRect5,
  } = usePopover();
  const {
    openPopover: openPopover6,
    closePopover: closePopover6,
    popoverVisible: popoverVisible6,
    touchableRef: touchableRef6,
    popoverAnchorRect: popoverAnchorRect6,
  } = usePopover();
  const {
    openPopover: openPopover7,
    closePopover: closePopover7,
    popoverVisible: popoverVisible7,
    touchableRef: touchableRef7,
    popoverAnchorRect: popoverAnchorRect7,
  } = usePopover();
  const {
    openPopover: openPopover8,
    closePopover: closePopover8,
    popoverVisible: popoverVisible8,
    touchableRef: touchableRef8,
    popoverAnchorRect: popoverAnchorRect8,
  } = usePopover();
  const title = <Text ref={touchableRef} >Press me!222</Text>
  return (
    <Tester>
      <TestSuite name='popoverTesteCenterDemo'>
        <TestCase itShould='popover' tags={['C_API']}>
          <View style={styles.app} >
            <View style={{ width: '100%', display: 'flex', flexDirection: 'row', justifyContent: 'space-between' }}>
              <Button title='Press1' ref={touchableRef} onPress={openPopover} />
              <Button title='Press2' ref={touchableRef1} onPress={openPopover1} />
              <Button title='Press3' ref={touchableRef2} onPress={openPopover2} />
            </View>
            <View style={{ width: '100%', display: 'flex', flexDirection: 'row', justifyContent: 'space-between' }}>
              <Button title='Press4' ref={touchableRef3} onPress={openPopover3} />
              <Button title='Press5' ref={touchableRef4} onPress={openPopover4} />
              <Button title='Press6' ref={touchableRef5} onPress={openPopover5} />
            </View>
            <View style={{ width: '100%', display: 'flex', flexDirection: 'row', justifyContent: 'space-between' }}>
              <Button title='Press7' ref={touchableRef6} onPress={openPopover6} />
              <Button title='Press8' ref={touchableRef7} onPress={openPopover7} />
              <Button title='Press9' ref={touchableRef8} onPress={openPopover8} />
            </View>
            <Popover
              // placement={'top'}
              contentStyle={styles.content}
              arrowStyle={styles.arrow}
              backgroundStyle={styles.background}
              visible={popoverVisible6}
              onClose={closePopover6}
              fromRect={popoverAnchorRect6}
              supportedOrientations={['portrait', 'landscape']}>
              <Text>Hello77!</Text>
            </Popover>

            <Popover
              placement={'top'}
              contentStyle={styles.content}
              arrowStyle={styles.arrow}
              backgroundStyle={styles.background}
              visible={popoverVisible7}
              onClose={closePopover7}
              fromRect={popoverAnchorRect7}
              supportedOrientations={['portrait', 'landscape']}>
              <Text>Hello88!</Text>
            </Popover>
            <Popover
              contentStyle={styles.content}
              arrowStyle={styles.arrow}
              backgroundStyle={styles.background}
              visible={popoverVisible8}
              onClose={closePopover8}
              fromRect={popoverAnchorRect8}
              supportedOrientations={['portrait', 'landscape']}>
              <Text>Hello99!</Text>
            </Popover>
            <Popover
              // placement={'top'}
              contentStyle={styles.content}
              arrowStyle={styles.arrow}
              backgroundStyle={styles.background}
              visible={popoverVisible3}
              onClose={closePopover3}
              fromRect={popoverAnchorRect3}
              supportedOrientations={['portrait', 'landscape']}>
              <Text>Hello44!</Text>
            </Popover>

            <Popover
              placement={'top'}
              contentStyle={styles.content}
              arrowStyle={styles.arrow}
              backgroundStyle={styles.background}
              visible={popoverVisible4}
              onClose={closePopover4}
              fromRect={popoverAnchorRect4}
              supportedOrientations={['portrait', 'landscape']}>
              <Text>Hello55!</Text>
            </Popover>
            <Popover
              // placement={'top'}
              contentStyle={styles.content}
              arrowStyle={styles.arrow}
              backgroundStyle={styles.background}
              visible={popoverVisible5}
              onClose={closePopover5}
              fromRect={popoverAnchorRect5}
              supportedOrientations={['portrait', 'landscape']}>
              <Text>Hello66!</Text>
            </Popover>

            <Popover
              // placement={'top'}
              contentStyle={styles.content}
              arrowStyle={styles.arrow}
              backgroundStyle={styles.background}
              visible={popoverVisible}
              onClose={closePopover}
              fromRect={popoverAnchorRect}
              supportedOrientations={['portrait', 'landscape']}>
              <Text>Hello11!</Text>
            </Popover>

            <Popover
              placement={'top'}
              contentStyle={styles.content}
              arrowStyle={styles.arrow}
              backgroundStyle={styles.background}
              visible={popoverVisible1}
              onClose={closePopover1}
              fromRect={popoverAnchorRect1}
              supportedOrientations={['portrait', 'landscape']}>
              <Text>Hello22!</Text>
            </Popover>
            <Popover
              // placement={'top'}
              contentStyle={styles.content}
              arrowStyle={styles.arrow}
              backgroundStyle={styles.background}
              visible={popoverVisible2}
              onClose={closePopover2}
              fromRect={popoverAnchorRect2}
              supportedOrientations={['portrait', 'landscape']}>
              <Text>Hello33!</Text>
            </Popover>
          </View>
        </TestCase>

      </TestSuite>
    </Tester>
  );
};
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-modal-popover Releases](https://github.com/react-native-oh-library/react-native-modal-popover/releases)


## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


### Popover

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ----------- |
| visible  | Show/Hide the popover      | bool  | NO | ALL      | YES |
| fromRect  | 	Rectangle at which to anchor the popover. Optional when used inside PopoverTouchable, required when used standalone. If you set this property, you should also change it when screen orientation changes.      | Rect | YES | ALL      | YES |
| displayArea  | Area where the popover is allowed to be displayed. Important note: if you use non-default value here and you want to handle screen orientation changes, it is your responsibility to change this value when screen orientation changes.      | Rect  | NO | ALL      | YES |
| placement  | How to position the popover top or bottom or start or end or auto. When 'auto' is specified, it will determine the ideal placement so that the popover is fully visible within displayArea.      | string  | NO | ALL      | YES |
| onClose  | Callback to be fired when the user closes the popover      | function  | NO | ALL      | YES |
| onDismiss  | Callback to be fired after the popup closes      | function  | NO | ALL      | YES |
|backgroundStyle  | Custom style to be applied to background overlay      | ViewStyle  | NO | ALL      | YES |
| contentStyle  | Custom style to be applied to popover reactangle. Use it to set round corners, background color, etc.      | ViewStyle  | NO | ALL      | YES |
| arrowStyle  | Custom style to be applied to popover arrow. Use borderTopColor to match content backgroundColor      | ViewStyle  | NO | ALL      | YES |
| duration  | Animation duration     | number  | NO | ALL      | YES |
| easing  | Function that returns easing function for show or hide animation, depending on show argument     | (show: boolean) => (value: number) => number  | NO | ALL      | YES |
| useNativeDriver  | Defines if animations should use native driver     | bool  | NO | ALL      | YES |
| supportedOrientations  | This prop is passed to react-native Modal, see react-native docs. Set this to ['portrait', 'landscape'] if you want your popover to resprect screen orientation.     | array of enum('portrait', 'portrait-upside-down', 'landscape', 'landscape-left', 'landscape-right')  | NO | ALL      | YES |
| calculateStatusBar  | Defines if while use status bar height while calculating "Y" origin of anchor.     | bool  | NO | ALL      | YES |
| PopoverController  | openPopover  | Call this function when you want to open popover, e.g. pass to onPress of a Button     | () => void  | NO | ALL      | YES |


### PopoverController

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| closePopover  | Call this function when you want to close popover. Typically you pass this as onClose prop of Popover, which will make popover close when tapped outside. If you have a button inside popover which should close the popover, pass this function to this button.     | () => void  | NO | ALL      | YES |
| popoverVisible  | CPass this to visible prop of Popover component   | bool  | NO | ALL      | YES |
| setPopoverAnchor (PopoverController) / touchableRef (usePopover)  | Pass this as ref to popover UI handle. This will bind popover display position to the position of this UI handle.   | ref function  | NO | ALL      | YES |
 | popoverAnchorRect  | Pass this as fromRect prop of Popover component   | Rect  | YES | ALL      | YES |

## 遗留问题

## 其他

## 开源协议

本项目基于 [License](https://github.com/doomsower/react-native-modal-popover/blob/master/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->