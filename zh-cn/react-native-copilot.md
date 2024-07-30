> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-copilot</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mohebifar/react-native-copilot">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mohebifar/react-native-copilot/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/mohebifar/react-native-copilot)

## 安装与使用
<!-- tabs:start -->
进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install --save react-native-copilot@3.3.2
```

#### **yarn**

```bash
yarn add react-native-copilot@3.3.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, { useEffect, useState } from "react";
import {
  Image,
  SafeAreaView,
  StyleSheet,
  Switch,
  Text,
  TouchableOpacity,
  View,
} from "react-native";
import {
  CopilotProvider,
  CopilotStep,
  walkthroughable,
  useCopilot,
} from "react-native-copilot";

const WalkthroughableText = walkthroughable(Text);
const WalkthroughableImage = walkthroughable(Image);

function App() {
  const { start, copilotEvents } = useCopilot();
  const [secondStepActive, setSecondStepActive] = useState(true);
  const [lastEvent, setLastEvent] = useState(null);

  useEffect(() => {
    copilotEvents.on("stepChange", (step) => {
      setLastEvent(`stepChange: ${step.name}`);
    });
    copilotEvents.on("start", () => {
      setLastEvent(`start`);
    });
    copilotEvents.on("stop", () => {
      setLastEvent(`stop`);
    });
  }, [copilotEvents]);

  return (
    <SafeAreaView style={styles.container}>
      <CopilotStep
        text="Hey! This is the first step of the tour!"
        order={1}
        name="openApp"
      >
        <WalkthroughableText style={styles.title}>
          {'Welcome to the demo of\n"React Native Copilot"'}
        </WalkthroughableText>
      </CopilotStep>
      <View style={styles.middleView}>
        <CopilotStep
          active={secondStepActive}
          text="Here goes your profile picture!"
          order={2}
          name="secondText"
        >
          <WalkthroughableImage
            source={require('../assets/react-native-copilot-man.jpeg')}
            style={styles.profilePhoto}
          />
        </CopilotStep>
        <View style={styles.activeSwitchContainer}>
          <Text>Profile photo step activated?</Text>
          <View style={{ flexGrow: 1 }} />
          <Switch
            onValueChange={(secondStepActive) =>
              setSecondStepActive(secondStepActive)
            }
            value={secondStepActive}
          />
        </View>
        <TouchableOpacity style={styles.button} onPress={() => start()}>
          <Text style={styles.buttonText}>START THE TUTORIAL!</Text>
        </TouchableOpacity>
        <View style={styles.eventContainer}>
          <Text>{lastEvent && `Last event: ${lastEvent}`}</Text>
        </View>
      </View>
      <View style={styles.row}>
        <CopilotStep
          text="Here is an item in the corner of the screen."
          order={3}
          name="thirdText"
        >
          <WalkthroughableText >
            <View style={styles.imageView}><Image source={require('../assets/react-native-copilot-nickname.png')} /></View>
          </WalkthroughableText>
        </CopilotStep>
        <View style={styles.imageView}><Image source={require('../assets/react-native-copilot-earphone.png')} /></View>
        <View style={styles.imageView}><Image source={require('../assets/react-native-copilot-glass.png')} /></View>
        <View style={styles.imageView}><Image source={require('../assets/react-native-copilot-scan.png')} /></View>
        <View style={styles.imageView}><Image source={require('../assets/react-native-copilot-todo.png')} /></View>
      </View>
    </SafeAreaView>
  );
}

const AppwithProvider = () => (
  <CopilotProvider stopOnOutsideClick androidStatusBarVisible>
    <App />
  </CopilotProvider>
);

export default AppwithProvider;

const styles = StyleSheet.create({
  imageView: {
    width: 50,
    height: 50,
    justifyContent: 'space-evenly',
    alignItems: 'center'
  },
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    paddingTop: 25,
  },
  title: {
    fontSize: 24,
    textAlign: "center",
  },
  profilePhoto: {
    width: 140,
    height: 140,
    borderRadius: 70,
    marginVertical: 20,
  },
  middleView: {
    flex: 1,
    alignItems: "center",
  },
  button: {
    backgroundColor: "#2980b9",
    paddingVertical: 10,
    paddingHorizontal: 15,
  },
  buttonText: {
    color: "white",
    fontSize: 16,
  },
  row: {
    flexDirection: "row",
    alignItems: 'center',
    justifyContent: "space-between",
  },
  tabItem: {
    flex: 1,
    textAlign: "center",
  },
  activeSwitchContainer: {
    flexDirection: "row",
    justifyContent: "space-between",
    marginBottom: 20,
    alignItems: "center",
    paddingHorizontal: 25,
  },
  eventContainer: {
    marginTop: 20,
  },
});
```
## Link

本库在HarmonyOS NEXT侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在HarmonyOS NEXT工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg-capi.md#link)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;

## 属性
详细请查看 [react-native-copilot](https://github.com/mohebifar/react-native-copilot/blob/master/README.md) 的文档介绍

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                       | Type     | Required | Platform    | HarmonyOS Support |
| --------------- | --------------------------------- | -------- | -------- | ----------- | ----------------- |
| CopilotProps    | Prompt Style Properties           | type     | no       | Android/iOS | yes               |
| TooltipProps    | Prompt Tool Properties            | type     | no       | Android/iOS | yes               |
| CopilotProvider | Custom Tooltip Styles             | function | no       | Android/iOS | yes               |
| CopilotStep     | Customizing Component Step Styles | function | no       | Android/iOS | yes               |
| DefaultUI       | Default UI Attributes             | object   | no       | Android/iOS | yes               |
| useCopilot      | Use Prompt Style                  | function | no       | Android/iOS | yes               |
| walkthroughable | Wrappable Components              | function | no       | Android/iOS | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mohebifar/react-native-copilot/blob/master/LICENSE) ，请自由地享受和参与开源。