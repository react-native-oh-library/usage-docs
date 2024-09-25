> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-marquee-ab</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/stack">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://choosealicense.com/licenses/mit/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/ZhangTaoK/react-native-marquee-ab)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install --save react-native-marquee-ab@1.2.6
```

#### **yarn**

```bash
yarn add react-native-marquee-ab@1.2.6
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import React, { Component } from 'react';
import {
    View,
    Text,
    Image,
    Dimensions,
} from 'react-native';
import { MarqueeHorizontal,MarqueeVertical } from 'react-native-marquee-ab';
export default class TestPage extends Component {
    render() {
        let mWidth = Dimensions.get('window').width;
        return (
            <View style={{ flex: 1, backgroundColor: '#FFFFFF' }}>
                <View style={{ height: 50, backgroundColor: '#FFFFFF', width: '100%' }} />
                <MarqueeHorizontal
                    textList={[
                        { label: '1', value: 'item1:一闪一闪亮晶晶，满天都是小星星' },
                        { label: '2', value: 'item2:两只老虎跑的快' },
                        { label: '3', value: 'item3:蓝蓝的天上白云飘，白云下面小肥羊儿跑' },
                    ]}
                    speed={60}
                    width={mWidth}
                    height={50}
                    direction={'left'}
                    reverse={false}
                    bgContainerStyle={{ backgroundColor: '#FFFF00' }}
                    textStyle={{ fontSize: 16, color: '#FF0000' }}
                    onTextClick={(item) => {
                        alert('' + JSON.stringify(item));
                    }}
                />
            </View>
        )
    }
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.29; SDK：HarmonyOS NEXT Developer Beta6; IDE：DevEco Studio 5.0.3.706; ROM：NEXT.0.0.65;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**MarqueeHorizontal props**

| Name             | Description                                      | Type           | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------ | -------------- | -------- | ----------- | ----------------- |
| duration         | 执行完成整个动画所需要的时间(ms)不常用           | number         | yes      | iOS/Android | yes               |
| speed            | 平均的滚动速度，跑马灯使用这个属性（建议传入60） | number         | no       | iOS/Android | yes               |
| textList         | 滚动的文字数组，具体数据格式请参照textList.item  | array          | yes      | iOS/Android | yes               |
| width            | 宽度，不能使用flex                               | number         | yes      | iOS/Android | yes               |
| height           | 高度，不能使用flex                               | number         | yes      | iOS/Android | yes               |
| direction        | 动画方向(向左向右滚动)`left` or `right`          | string         | yes      | iOS/Android | yes               |
| reverse          | 是否将整个文本数据倒叙显示                       | boolean        | yes      | iOS/Android | yes               |
| separator        | 两个item之间的间隙                               | number         | yes      | iOS/Android | yes               |
| bgContainerStyle | 背景样式                                         | object         | no       | iOS/Android | yes               |
| textStyle        | 文本样式                                         | object         | no       | iOS/Android | yes               |
| onTextClick      | 点击事件回调                                     | (item) => void | yes      | iOS/Android | yes               |

**MarqueeVertical props**

| Name             | Description                                                  | Type           | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------------- | -------- | ----------- | ----------------- |
| duration         | 执行完成整个动画所需要的时间(ms)                             | number         | yes      | iOS/Android | yes               |
| textList         | 滚动的文字数组，具体数据格式请参照textList.item              | array          | yes      | iOS/Android | yes               |
| width            | 宽度，不能使用flex                                           | number         | no       | iOS/Android | yes               |
| height           | 高度，不能使用flex                                           | number         | no       | iOS/Android | yes               |
| delay            | 文本停顿时间(ms)                                             | number         | yes      | iOS/Android | yes               |
| direction        | 动画方向(向上向下滚动)`up` or `down`                         | string         | yes      | iOS/Android | yes               |
| numberOfLines    | 同一个数据的文本行数                                         | number         | yes      | iOS/Android | yes               |
| headViews        | 在文本最前面加上一个自定义view，效果如图例所示，用法请参照事例用法，length长度与textList必须一致 | array          | no       | iOS/Android | yes               |
| viewStyle        | 每一行文本的样式                                             | object         | yes      | iOS/Android | yes               |
| bgContainerStyle | 背景样式                                                     | object         | no       | iOS/Android | yes               |
| textStyle        | 文本样式                                                     | object         | no       | iOS/Android | yes               |
| onTextClick      | 点击事件回调                                                 | (item) => void | yes      | iOS/Android | yes               |

**textList.item props**

| Name     | Description                      | Type     | Required | Platform    | HarmonyOS Support |
| -------- | -------------------------------- | -------- | -------- | ----------- | ----------------- |
| label    | 用作点击事件的回调               | string   | yes      | iOS/Android | yes               |
| value    | 文本显示                         | string   | yes      | iOS/Android | yes               |
| [object] | 可随意添加数据供自己特殊需求使用 | [object] | no       | iOS/Android | yes               |

## 遗留问题

- [ ] MarqueeHorizontal的reverse属性在HarmonyOS上只有第一次修改会触发生效，而原库在iOS上该属性已经失效。未实现HarmonyOS化 问题[issue#58](https://github.com/ZhangTaoK/react-native-marquee-ab/issues/58)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://choosealicense.com/licenses/mit/) ，请自由地享受和参与开源。
