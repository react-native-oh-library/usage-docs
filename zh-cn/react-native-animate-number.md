模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-animate-number</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wkh237/react-native-animate-number">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/wkh237/react-native-animate-number)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-animate-number@0.1.2
```

#### **yarn**

```bash
yarn add react-native-animate-number@0.1.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useState } from "react";
import { StyleSheet, Text, View, Button } from "react-native";
import AnimateNumber from "react-native-animate-number";

const App = () => {
  const [value, setValue] = useState(0);
  const onPress = () => {
    setValue(100);
  };
  const [finish, setFinish] = useState("");
  const [progress, setProgress] = useState("");
  const onProgress = () => {
    setProgress("动画正在更新...");
  };
  const onFinish = () => {
    setFinish("动画更新完成");
  };
  return (
    <View style={styles.container}>
      <View style={styles.button}>
        <Button title={"点击开始动画"} onPress={onPress} />
      </View>
      <Text style={styles.row}>
        <Text>linear:</Text>
        <AnimateNumber
          value={value}
          timing="linear"
          countBy={1}
          interval={150}
        />
      </Text>
      <Text style={styles.row}>
        <Text>easeOut:</Text>
        <AnimateNumber
          value={value}
          timing="easeOut"
          countBy={1}
          interval={150}
        />
      </Text>
      <Text style={styles.row}>
        <Text>easeIn:</Text>
        <AnimateNumber
          value={value}
          timing="easeIn"
          countBy={1}
          interval={150}
        />
      </Text>
      <Text style={styles.row}>
        <Text>steps:</Text>
        <AnimateNumber value={value} steps={5} interval={2000} />
      </Text>
      <Text style={styles.row}>
        <Text>Formate Example:</Text>
        <AnimateNumber
          value={value}
          countBy={1}
          interval={150}
          formatter={(val) => {
            return "$ " + parseFloat(val).toFixed(2);
          }}
        />
      </Text>
      <Text style={styles.row}>
        <Text>{progress}</Text>
      </Text>
      <Text style={styles.row}>
        <AnimateNumber
          value={30}
          countBy={5}
          interval={600}
          onProgress={onProgress}
          onFinish={onFinish}
        />
      </Text>
      <Text style={styles.row}>
        <Text>{finish}</Text>
      </Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    justifyContent: "center",
    flex: 1,
    alignItems: "center",
  },
  row: {
    fontSize: 20,
    fontWeight: "bold",
    flexDirection: "row",
    marginBottom: 20,
  },
  button: {
    marginBottom: 20,
  },
});

export default App;
```

## 兼容性

在以下版本验证通过

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;

## 属性

| Name         | Description                                                                                                                                                 | Type     | Required | Platform    | HarmonyOS Support |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| `value`      | The value of AnimateNumber component.                                                                                                                       | number   | yes      | Android IOS | YES               |
| `countBy`    | Set this property to force the component's value increase/decrease by this number.                                                                          | number   | No       | Android IOS | YES               |
| `interval`   | Base interval of each animation frame, in `ms`.                                                                                                             | number   | No       | Android IOS | YES               |
| `steps`      | Set total frame number of animation, say, if interval is 14 and steps is 30, the animation will take 14x30ms to finish when it uses linear timing function. | number   | No       | Android IOS | YES               |
| `timing`     | A style object that allow you to customize the WebView style.                                                                                               | number   | No       | Android IOS | YES               |
| `formatter`  | The custom css content will be added to the page's <head>.                                                                                                  | string   | No       | Android IOS | YES               |
| `onProgress` | Either updated height or width will trigger onSizeUpdated.                                                                                                  | function | No       | Android IOS | YES               |
| `onFinish`   | Boolean value that determines whether a horizontal scroll indicator is shown in the WebView.                                                                | function | No       | Android IOS | YES               |

## 遗留问题

## 其他
