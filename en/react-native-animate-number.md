> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-animate-number</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/wkh237/react-native-animate-number">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github address](https://github.com/wkh237/react-native-animate-number)

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

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
    setProgress ("Animation is being updated...");
  };
  const onFinish = () => {
    setFinish ("Animation update completed");
  };
  return (
    <View style={styles.container}>
      <View style={styles.button}>
        <Button title={"Click to start animation"} onPress={onPress} />;
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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71 (API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## Properties

| Name         | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| `value`      | The value of AnimateNumber component.                        | number   | yes      | Android IOS | YES               |
| `countBy`    | Set this property to force the component's value increase/decrease by this number. | number   | No       | Android IOS | YES               |
| `interval`   | Base interval of each animation frame, in `ms`.              | number   | No       | Android IOS | YES               |
| `steps`      | Set total frame number of animation, say, if interval is 14 and steps is 30, the animation will take 14x30ms to finish when it uses linear timing function. | number   | No       | Android IOS | YES               |
| `timing`     | A style object that allow you to customize the WebView style. | number   | No       | Android IOS | YES               |
| `formatter`  | The custom css content will be added to the page's <head>.   | string   | No       | Android IOS | YES               |
| `onProgress` | Either updated height or width will trigger onSizeUpdated.   | function | No       | Android IOS | YES               |
| `onFinish`   | Boolean value that determines whether a horizontal scroll indicator is shown in the WebView. | function | No       | Android IOS | YES               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://www.mit-license.org/).