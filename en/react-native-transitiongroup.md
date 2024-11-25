> Template version: v0.2.2

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


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-transitiongroup)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-transitiongroup Releases](https://github.com/react-native-oh-library/react-native-transitiongroup/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-transitiongroup
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-transitiongroup
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-transitiongroup Releases](https://github.com/react-native-oh-library/react-native-transitiongroup/releases)

## APIs

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name          | Description                            | type     | Required | Platform | HarmonyOS Support |
| ------------- | -------------------------------------- | -------- | -------- | -------- | ----------------- |
| easing        | 缓动函数                               | function | no       | All      | yes               |
| inDelay       | 组件加载时开始动画前的延迟时间（毫秒） | number   | no       | All      | yes               |
| inDuration    | 组件加载时动画的持续时间（毫秒）       | number   | no       | All      | yes               |
| outDelay      | 组件销毁时开始动画前的延迟时间（毫秒） | number   | no       | All      | yes               |
| outDuration   | 组件销毁时动画的持续时间（毫秒）       | number   | no       | All      | yes               |
| pointerEvents | 控制View是否可以成为触摸事件的目标     | string   | no       | All      | yes               |
| style         | 组件样式                               | style    | no       | All      | yes               |

## Known Issues

## Others

- [ ] 原库使用refs方法，现在改为使用react.createRef方法代替。问题: [issue#1](https://github.com/react-native-oh-library/react-native-transitiongroup/issues/1)
- [ ] 原库中使用的ViewPropTypes，现在改为使用PropTypes方法代替。问题: [issue#2](https://github.com/react-native-oh-library/react-native-transitiongroup/issues/2)

## License

This project is licensed under [The MIT License (MIT)](https://www.mit-license.org).
