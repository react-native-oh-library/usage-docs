> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-animatable</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/oblador/react-native-animatable">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/oblador/react-native-animatable/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/oblador/react-native-animatable)


## 安装与使用


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-animatable@1.4.0
```

#### **yarn**

```bash
yarn add react-native-animatable@1.4.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import { useState } from 'react';
import { TouchableOpacity } from 'react-native';
import * as Animatable from 'react-native-animatable';

export default function ExampleView() {
    const [textFontSize, setTextFontSize] = useState(10);
    return (
        <Animatable.View style={{ padding: 50, backgroundColor: '#333333' }}>
            <Animatable.Text
                animation="slideInDown"
                iterationCount={5}
                direction="reverse"
                style={{ color: 'white', textAlign: 'center' }}
                duration={2000}
                onAnimationBegin={() => { console.log('test onAnimationBegin') }}
                onAnimationEnd={() => { console.log('test onAnimationEnd') }}
            >Up and down you go</Animatable.Text>
            <Animatable.Text animation="bounce" easing="ease-out" iterationCount="infinite" iterationDelay={1500} style={{ textAlign: 'center' }} useNativeDriver={true} isInteraction={true}>❤️</Animatable.Text>
            <Animatable.Text animation="fadeIn" delay={2000} style={{ textAlign: 'center', marginTop: 50, color: 'white' }}>(*^▽^*)</Animatable.Text>
            <TouchableOpacity onPress={() => setTextFontSize(textFontSize + 5)}>
                <Animatable.Text
                    transition="fontSize"
                    style={{ textAlign: 'center', marginTop: 50, color: 'white', fontSize: textFontSize || 10 }}
                    onTransitionBegin={() => { console.log('test onTransitionBegin') }}
                    onTransitionEnd={() => { console.log('test onTransitionEnd') }}
                >test</Animatable.Text>
            </TouchableOpacity>
        </Animatable.View>
    )
}   
```



## 约束与限制

### 兼容性
要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 电脑ROM。

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1 B.0.18； IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

Name | Description | Type | Required | Platform | HarmonyOS   Support
-- | -- | -- | -- | -- | --
animation | 动画的名称，请参见下面的可用动画 | string/undefined | / | all | yes
duration | 动画将运行的时间（毫秒） | number/undefined | / | all | yes
delay | （可选）延迟动画（毫秒） | number/undefined | / | all | yes
direction | 动画的方向，特别适用于重复动画。有效值：正常、反向、交替、交替反向 | string/undefined | / | all | yes
easing | 动画的计时功能。有效值：自定义函数或线性、易进、易出、易入 | string/undefined | / | all | yes
iterationCount | 运行动画的次数，对于循环动画使用无穷大。 | number/undefined | / | all | yes
iterationDelay | 关于动画迭代之间的暂停时间（毫秒） | number/undefined | / | all | yes
transition | 要转换的样式属性，例如不透明度、旋转或字体大小。对多个属性使用数组。 | string/array/undefined | / | all | yes
onAnimationBegin | 启动动画时调用的函数。 | Function/undefined | / | all | yes
onAnimationEnd | 当动画成功完成或取消时调用的函数。函数是用endState参数调用的，请参阅endState.finished以查看动画是否已完成。 | Function/undefined | / | all | yes
onTransitionBegin | 在样式转换开始时调用的函数。使用属性参数调用函数以区分样式。 | Function/undefined | / | all | yes
onTransitionEnd | 当样式转换成功完成或取消时调用的函数。使用属性参数调用函数以区分样式。 | Function/undefined | / | all | yes
useNativeDriver | 是否使用本机或JavaScript动画驱动程序。本机驱动程序可以帮助提高性能，但不能处理所有类型的样式。 | Function/undefined | / | all | yes
isInteraction | 此动画是否在交互管理器上创建“交互控制柄”。 | Boolean | / | all | yes




## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/oblador/react-native-animatable/blob/master/LICENSE) ，请自由地享受和参与开源。
