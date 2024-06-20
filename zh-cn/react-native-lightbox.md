> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-lightbox</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/cbbfcd/react-native-lightbox">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/cbbfcd/react-native-lightbox/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/cbbfcd/react-native-lightbox)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-lightbox-v2@0.9.0
```

#### **yarn**

```bash
yarn add react-native-lightbox-v2@0.9.0
```

<!-- tabs:end -->

> [!WARNING] 使用时 import 的库名不变。

```ts
import React, { useState } from 'react';
import {
    Image,
    ScrollView,
    StyleSheet,
    Text,
    TouchableOpacity,
    View,
    SafeAreaView,
    Alert,
} from 'react-native';

import Lightbox from 'react-native-lightbox-v2';


const BASE_PADDING = 10;


export const ReactNativeLightBoxExample = () => {
    let [info, setInfo] = useState('')

    const callBack = (type: any) => {
        setInfo(type)
        Alert.alert(type)
    }

    let eventObject = {
        willClose: () => callBack('willClose'),
        onClose: () => callBack('onClose'),
        onOpen: () => callBack('onOpen'),
        didOpen: () => callBack('didOpen'),
        onLongPress: () => callBack('onLongPress'),
        onLayout: () => callBack('onLayout'),
        doubleTapCallback: () => callBack('doubleTapCallback'),
        longPressCallback: () => callBack('longPressCallback'),
    }

    return (
        <View style={styles.container}>
            <View>
                <Text>eventCallBack {info}</Text>
            </View>
            <View style={styles.text}>
                <Text>eventCallBack </Text>
            </View>
            <Lightbox {...eventObject}>
                <View style={styles.customHeaderBox}>
                    <Text>I have eventCallBack</Text>
                </View>
            </Lightbox>

            <View style={styles.text}><Text>renderHeader </Text></View>
            <Lightbox
                renderHeader={close => (
                    <TouchableOpacity onPress={close}>
                        <Text style={styles.closeButton}>Close</Text>
                    </TouchableOpacity>
                )}>
                <View style={styles.customHeaderBox}>
                    <Text>I have a custom header</Text>
                </View>
            </Lightbox>
            <View style={styles.text}><Text>renderContent </Text></View>
            <Lightbox
                renderContent={() =>
                    <View style={styles.customHeaderBox}>
                        <Text style={{ color: 'red' }}>renderContent</Text>
                    </View>}>
                <View style={styles.customHeaderBox}>
                    <Text>I have a custom renderContent</Text>
                </View>
            </Lightbox>
        </View>
    )

}
const styles = StyleSheet.create({
    container: {
        paddingHorizontal: BASE_PADDING,
        backgroundColor: 'white'
    },
    closeButton: {
        color: 'white',
        borderWidth: 1,
        borderColor: 'white',
        padding: 8,
        borderRadius: 3,
        textAlign: 'center',
        margin: 10,
        alignSelf: 'flex-end',
    },
    customHeaderBox: {
        height: 150,
        backgroundColor: '#6C7A89',
        justifyContent: 'center',
        alignItems: 'center',
    },

    row: {
        flexDirection: 'row',
        marginLeft: -BASE_PADDING,
        marginRight: -BASE_PADDING,
    },
    col: {
        flex: 1,
    },

    contain: {
        flex: 1,
        height: 150,
    },
    text: {
        marginVertical: BASE_PADDING * 2,
    }
});

```


## 约束与限制

### 兼容性
本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 属性
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


该库为UI组件库，通过配置属性标签，实现对应的功能。

| Name                        | Description        | Type                     |Required           |Platform           | HarmonyOS Support |
|-----------------------------|------------|---------------------------------|-------------------|-------------------|-------------------|
| **`activeProps`**           | 可选属性，在lightbox模式下应用于内容组件， 可用于应用自定义样式或更高分辨率的图源。  | `object`                                              |no                 |all               | yes               |
| **`renderHeader(close)`**   | 自定义header，用于替换默认的 X 按钮| `function`                                                            |  no              |all             | yes               |
| **`renderContent`**         | 自定义lightbox内容，用于替换默认的子内容| `function`                                                                       |no|all                    | yes               |
| **`willClose`**             | lightbox关闭前触发 | `function`                                                                 |no|all                                           | yes               |
| **`onClose`**               | lightbox关闭时触发| `function`                            |no|all                                               | yes               |
| **`onOpen`**                |lightbox打开时触发| `function`                           |no|all                                                | yes               |
| **`didOpen`**               | lightbox打开后触发| `function`                                           |no|all                                         | yes               |
| **`onLongPress`**           | lightbox长按时触发 | `function`                           |no|all                                        | yes               |
| **`onLayout`**              | lightbox布局完成后触发| `function`                                   |no|all                                   | yes               |
| **`doubleTapCallback`**     | lightbox双击时触发| `function`                               |no|all                                                 | yes               |
| **`doubleTapZoomEnabled`**  | 开启双击缩放功能 , 默认为 `true`| `boolean`                         |no|all                       | yes               |
| **`doubleTapGapTimer`**     | 确定双击的时间间隔，默认为 `500ms` | `number`                                            |no|all     | yes               |
| **`longPressGapTimer`**     | 确定长按的的时间间隔，默认为 `2000ms`| `number`                                                                                  |no|all          | yes               |
| **`longPressCallback`**     | 内容长按后触发| `function`                                 |no|all                                    | yes               |
| **`doubleTapZoomToCenter`** | 双击时缩放到中间| `boolean`                                                                        |no|all                                       | yes               |
| **`doubleTapMaxZoom`**      | 最大放大系数，默认为 `2`| `number`                                               |no|all                                  | yes               |
| **`doubleTapZoomStep`**     | 每次双击的缩放比例，默认为 `0.5`| `number`                           |no|all                                          | yes               |
| **`underlayColor`**         | 可触摸背景的颜色，默认为 `black`| `string`                                                                   |no|all                                 | yes               |
| **`backgroundColor`**       | lightbox 背景颜色，默认为  `black`| `string`                                                              |no|all                                       | yes               |
| **`swipeToDismiss`**        | 启用手势以通过向上或向下轻扫来取消全屏模式，默认为 `true`| `bool`                                                 |no|all             | yes               |
| **`disabled`**              | 禁用lightbox。默认为 `false`| `bool`                                                   |no|all                                                           | yes               |
| **`style`**                 | lightbox视图包装器的样式| `object`                                 |no|all                                                                     | yes               |
| **`dragDismissThreshold`**  | 滑动退出的阈值距离，默认为 `150`| `number`                                             |no|all                                                | yes               |
| **`modalProps`**            | 任何其他你需要的modal属性，默认为 `{}`| `object`                                          |no|all                                                           | yes               |
| **`useNativeDriver`**       | 是否使用本机驱动程序，默认为 `false`| `bool`                                        |no|all                                                                  | yes               |
| **`springConfig`**          | [`Animated.spring`](https://facebook.github.io/react-native/docs/animations.html) 配置， 默认为 `{ tension: 30, friction: 7 }`。| `object`       |no|all  | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/cbbfcd/react-native-lightbox/blob/master/LICENSE) ，请自由地享受和参与开源。