> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-transitiongroup</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/madsleejensen/react-native-transitiongroup">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
     <a href="https://www.mit-license.org">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="Supported platforms" />
    </a>
</p>


> [!Tip] [Github 地址](https://github.com/react-native-oh-library/react-native-transitiongroup)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-transitiongroup Releases](https://github.com/react-native-oh-library/react-native-transitiongroup/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

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

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { StyleSheet, Text, View, TouchableOpacity, Easing } from "react-native";
import TransitionGroup, {
  FadeInOutTransition,
} from "react-native-transitiongroup";

export function TransitiongroupExample() {
  const [showText, setShowText] = useState(false);

  const handleToggle = () => {
    setShowText(!showText);
  };

  return (
    <View style={styles.container}>
      <View style={styles.relativeContainer}>
        <TouchableOpacity onPress={handleToggle} style={styles.button}>
          <Text style={styles.buttonText}>{showText ? "Hide" : "Show"}</Text>
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
              easing={Easing.ease} 
              inDelay={200}
              outDelay={0}
              pointerEvents="box-only"
              style={{ backgroundColor: "pink" }}
            >
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
    justifyContent: "center",
    alignItems: "center",
  },
  relativeContainer: {
    position: "relative",
  },
  button: {
    backgroundColor: "#3f51b5",
    padding: 10,
    borderRadius: 5,
    marginBottom: 20,
  },
  buttonText: {
    color: "#fff",
    fontWeight: "bold",
    fontSize: 16,
  },
  absoluteContainer: {
    position: "absolute",
    bottom: -50,
    left: -100,
  },
  absoluteContainerTwo: {
    position: "absolute",
    bottom: -150,
    left: -100,
  },
  absoluteContainerThree: {
    position: "absolute",
    bottom: -250,
    left: -100,
  },
  text: {
    fontSize: 24,
    fontWeight: "bold",
  },
});
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-transitiongroup Releases](https://github.com/react-native-oh-library/react-native-transitiongroup/releases)

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name          | Description                            | type     | Required | Platform | HarmonyOS Support |
| ------------- | -------------------------------------- | -------- | -------- | -------- | ----------------- |
| easing        | 缓动函数                               | function | no       | All      | yes               |
| inDelay       | 组件加载时开始动画前的延迟时间（毫秒） | number   | no       | All      | yes               |
| inDuration    | 组件加载时动画的持续时间（毫秒）       | number   | no       | All      | yes               |
| outDelay      | 组件销毁时开始动画前的延迟时间（毫秒） | number   | no       | All      | yes               |
| outDuration   | 组件销毁时动画的持续时间（毫秒）       | number   | no       | All      | yes               |
| pointerEvents | 控制View是否可以成为触摸事件的目标     | string   | no       | All      | yes               |
| style         | 组件样式                               | style    | no       | All      | yes               |

## 遗留问题

## 其他

- [ ] 原库使用refs方法，现在改为使用react.createRef方法代替。问题: [issue#1](https://github.com/react-native-oh-library/react-native-transitiongroup/issues/1)
- [ ] 原库中使用的ViewPropTypes，现在改为使用PropTypes方法代替。问题: [issue#2](https://github.com/react-native-oh-library/react-native-transitiongroup/issues/2)

## 开源协议

本项目基于 [The MIT License (MIT)](https://www.mit-license.org) ，请自由地享受和参与开源。
