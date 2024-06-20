> 模板版本：v0.2.0

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


> [!TIP] 
>
> [Github 地址](https://github.com/ZhangTaoK/react-native-marquee-ab)

## 安装与使用

进入到工程目录并输入以下命令：

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

<!-- {% raw %} -->
```tsx
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
<!-- {% endraw %} -->

## Props

**MarqueeHorizontal props**

| Name             | Description | Type    | Required | Platform                                         | notes                                  |
| ---------------- | ----------- | ------- | -------- | :----------------------------------------------- | -------------------------------------- |
| duration         | number      | 10000ms | yes      | 执行完成整个动画所需要的时间(ms)不常用           |                                        |
| speed            | number      | 0       | no       | 平均的滚动速度，跑马灯使用这个属性（建议传入60） |                                        |
| textList         | array       | []      | yes      | 滚动的文字数组，具体数据格式请参照textList.item  |                                        |
| width            | number      | 375     | yes      | 宽度，不能使用flex                               |                                        |
| height           | number      | 50      | yes      | 高度，不能使用flex                               |                                        |
| direction        | string      | left    | yes      | 动画方向(向左向右滚动)`left` or `right`          |                                        |
| reverse          | boolean     | false   | yes      | 是否将整个文本数据倒叙显示                       | 设置为true时，只有第一次进入时才会生效 |
| separator        | number      | 20      | yes      | 两个item之间的间隙                               |                                        |
| bgContainerStyle | object      |         | no       | 背景样式                                         |                                        |
| textStyle        | object      |         | no       | 文本样式                                         |                                        |
| onTextClick      | function    |         | yes      | 点击事件回调：(item) => void                     |                                        |

#### **MarqueeVertical props**

| Name             | Description | Type  | Required | Platform                                                     |
| ---------------- | ----------- | ----- | -------- | :----------------------------------------------------------- |
| duration         | number      | 600   | yes      | 执行整个动画的完成时间(ms)                                   |
| textList         | array       | []    | yes      | 滚动的文字数组，具体数据格式请参照textList.item              |
| width            | number      | 375   | no       | 宽度，不能使用flex                                           |
| height           | number      | 50    | no       | 高度，不能使用flex                                           |
| delay            | number      | 12000 | yes      | 文本停顿时间(ms)                                             |
| direction        | string      | up    | yes      | 动画方向(向上向下滚动)`up` or `down`                         |
| numberOfLines    | number      | 1     | yes      | 同一个数据的文本行数                                         |
| headViews        | array       | []    | no       | 在文本最前面加上一个自定义view，效果如图例所示，用法请参照事例用法，length长度与textList必须一致 |
| viewStyle        | object      |       | yes      | 每一行文本的样式                                             |
| bgContainerStyle | object      |       | no       | 背景样式                                                     |
| textStyle        | object      |       | no       | 文本样式                                                     |
| onTextClick      | function    |       | yes      | 点击事件回调：(item) => void                                 |

#### textList.item props

| prop     | type     | default | required | description                      |
| -------- | -------- | ------- | -------- | -------------------------------- |
| label    | string   |         | yes      | 用作点击事件的回调               |
| value    | string   |         | yes      | 文本显示                         |
| [object] | [object] |         | no       | 可随意添加数据供自己特殊需求使用 |

## 遗留问题

- [ ] MarqueeHorizontal的reverse属性在HarmonyOS上只有第一次修改会触发生效，而原库在iOS上该属性已经失效。issue:https://github.com/ZhangTaoK/react-native-marquee-ab/issues/58

## 开源协议

本项目基于 [The MIT License (MIT)](https://choosealicense.com/licenses/mit/) ，请自由地享受和参与开源。
