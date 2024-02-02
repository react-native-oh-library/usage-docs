> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-transtiongroup</code> </h1>
</p>
<p align="center">
     <a href="https://github.com/madsleejensen/react-native-transitiongroup/blob/master/README.md">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
</p>


> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-transitiongroup)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-tpl/库名> Releases](https://github.com/react-native-oh-library/react-native-transitiongroup/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-transitiongroup@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-transitiongroup@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react';
import {
  StyleSheet,
  Text,
  View,
  TouchableOpacity,
  Easing
} from 'react-native';
import TransitionGroup, { FadeInOutTransition } from 'react-native-transitiongroup';


export function TransitiongroupExample() {
  const [showText, setShowText] = useState(false);

  const handleToggle = () => {
    setShowText(!showText);
  };

  return (
    <View style={styles.container}>
      <View style={styles.relativeContainer}>
        <TouchableOpacity onPress={handleToggle} style={styles.button}>
          <Text style={styles.buttonText}>{showText ? 'Hide' : 'Show'}</Text>
        </TouchableOpacity>

        <TransitionGroup style={styles.absoluteContainer}>
          {showText && (
            <FadeInOutTransition>
              <Text style={styles.text}>Hello, Transition Group!!</Text>
            </FadeInOutTransition>
          )}
        </TransitionGroup>

        <TransitionGroup style={styles.absoluteContainerTwo}>
          {showText && (
            <FadeInOutTransition inDuration={3000}>
              <Text style={styles.text}>I'm Later</Text>
            </FadeInOutTransition>
          )}
        </TransitionGroup>

        <TransitionGroup style={styles.absoluteContainerThree}>
          {showText && (
            <FadeInOutTransition
              inDuration={1000}
              outDuration={500}
              easing={Easing.ease} // 使用 ease 缓动函数
              inDelay={200}
              outDelay={0}
              pointerEvents="box-only"
              style={{ backgroundColor: "pink" }}>
              <Text style={styles.text}>I'm Pink</Text>
            </FadeInOutTransition>
          )}
        </TransitionGroup>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  relativeContainer: {
    position: 'relative',
  },
  button: {
    backgroundColor: '#3f51b5',
    padding: 10,
    borderRadius: 5,
    marginBottom: 20,
  },
  buttonText: {
    color: '#fff',
    fontWeight: 'bold',
    fontSize: 16,
  },
  absoluteContainer: {
    position: 'absolute',
    bottom: -50,
    left: -100,
  },
  absoluteContainerTwo: {
    position: 'absolute',
    bottom: -150,
    left: -100,
  },
  absoluteContainerThree: {
    position: 'absolute',
    bottom: -250,
    left: -100,
  },
  text: {
    fontSize: 24,
    fontWeight: 'bold',
  },
});

```

## 约束与限制

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
> 详情见 [react-native-transtiongroup 源库地址](https://github.com/imchintan/react-native-transtiongroup/blob/master/README.md)

| 名称          | 描述                                | 参数类型 | 是否必填 | Platform | HarmonyOS Support |
| ------------- | ---------------------------------- | -------- | -------- | -------- | ----------------- |
| easing        | 缓动函数                            | func     | yes      | All      | yes               |
| inDelay       | 组件加载时开始动画前的延迟时间（毫秒） | number   | yes      | All      | yes               |
| inDuration    | 组件加载时动画的持续时间（毫秒）      | number   | yes      | All      | yes               |
| outDelay      | 组件销毁时开始动画前的延迟时间（毫秒） | number   | yes      | All      | yes              |
| outDuration   | 组件销毁时动画的持续时间（毫秒）      | number   | yes      | All      | yes              |
| pointerEvents | 控制View是否可以成为触摸事件的目标    | string   | yes      | All      | yes              |
| style         | 组件样式                            | style   | yes      | All      | yes              |

## 遗留问题

原库使用refs方法，现在改为使用react.createRef方法代替。
原库中使用的ViewPropTypes，现在改为使用PropTypes方法代替。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/imchintan/react-native-transtiongroup/blob/master/package.json) ，请自由地享受和参与开源。