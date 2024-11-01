> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-confirmation-code-field</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/retyui/react-native-confirmation-code-field">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/retyui/react-native-confirmation-code-field/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/retyui/react-native-confirmation-code-field)

## 安装与使用

#### **npm**

```bash
npm install react-native-confirmation-code-field@7.3.2
```

#### **yarn**

```bash
yarn add react-native-confirmation-code-field@7.3.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { SafeAreaView, Text, StyleSheet } from "react-native";

import {
  CodeField,
  Cursor,
  useBlurOnFulfill,
  useClearByFocusCell,
} from "react-native-confirmation-code-field";

const styles = StyleSheet.create({
  root: { flex: 1, padding: 20 },
  title: { textAlign: "center", fontSize: 30 },
  codeFieldRoot: { marginTop: 20 },
  cell: {
    width: 40,
    height: 40,
    lineHeight: 38,
    fontSize: 24,
    borderWidth: 2,
    borderColor: "#00000030",
    textAlign: "center",
  },
  focusCell: {
    borderColor: "#000",
  },
});

const CELL_COUNT = 6;

const App = () => {
  const [value, setValue] = useState("");
  const ref = useBlurOnFulfill({ value, cellCount: CELL_COUNT });
  const [props, getCellOnLayoutHandler] = useClearByFocusCell({
    value,
    setValue,
  });

  return (
    <SafeAreaView style={styles.root}>
      <Text style={styles.title}>Verification</Text>
      <CodeField
        ref={ref}
        {...props}
        // Use `caretHidden={false}` when users can't paste a text value, because context menu doesn't appear
        value={value}
        onChangeText={setValue}
        cellCount={CELL_COUNT}
        rootStyle={styles.codeFieldRoot}
        keyboardType="number-pad"
        textContentType="oneTimeCode"
        renderCell={({ index, symbol, isFocused }) => (
          <Text
            key={index}
            style={[styles.cell, isFocused && styles.focusCell]}
            onLayout={getCellOnLayoutHandler(index)}
          >
            {symbol || (isFocused ? <Cursor /> : null)}
          </Text>
        )}
      />
    </SafeAreaView>
  );
};

export default App;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 组件

> [!tip] "Platform"列表示该组件在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该组件；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name        | Description                                                                                                                                                                                          | Type      | Platform | HarmonyOS Support |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | -------- | ----------------- |
| `CodeField` | This a base component that render RootComponent (default: View) with cells that would be returned by renderCell() and a <TextInput/> that will be invisible and over all cells within root component | component | All      | yes               |
| `Cursor`    | It's a help component for simulation a cursor blinking animation in <Cell/> components                                                                                                               | component | All      | yes               |

## CodeField属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                                                                                                                | Type                     | Required | Platform | HarmonyOS Support |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------- | ------------------------ | -------- | -------- | ----------------- |
| `cellCount`       | Number of characters in input (optional, default: 4)                                                                       | number                   | yes      | All      | yes               |
| `renderCell?`     | Required function for Cell rendering, will be invoke with next options:{index: number, symbol: string, isFocused: boolean} | ReactElement             | No       | All      | yes               |
| `RootComponent?`  | if you want change root component for example using animations RootComponent={Animated.View} (optional, default View)      | ComponentType<any>       | No       | All      | yes               |
| `InputComponent?` | If you want to provide a custom TextInput component that can receive the same props (optional, default TextInput)          | ComponentType<any>       | No       | All      | yes               |
| `rootStyle?`      | Styles for root component (optional)                                                                                       | StyleProp<RootComponent> | No       | All      | yes               |
| `RootProps?`      | Any props that will applied for root component <RootComponent style={rootStyle} {...RootProps} />                          | Object                   | No       | All      | yes               |
| `textInputStyle?` | Styles for invisible <TextInput/>, can be used for testing or debug (optional)                                             | StyleProp<TextStyle>     | No       | All      | yes               |

## Hooks

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Type           | Required | Platform | HarmonyOS Support |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | -------- | -------- | ----------------- |
| `useClearByFocusCell` | Simple hook that add functionality that trim value by pressed cell,After invoke this hook wil return array with two values `[props,getCellOnLayout]`;<br/> -`props`- an object that you should spreed to ` <CodeField/>` <br/> - `getCellOnLayout(index: number): Function` - helper method that returns `onLayout` handler <br/> - If you need to style only one borderX (example `borderBottom`) you need to know about React Native issue with [border styles for `<Text/>` on iOS](https://github.com/facebook/react-native/issues/23537).<br/> - To fix it need `<View/>` wrapper for Cell, but don't forger to move `onLayout={getCellOnLayoutHandler(index)` to `<View/>` | Function       | yes      | All      | yes               |
| `useBlurOnFulfill`    | This hook include a logic to blurring`<TextInput/>`when value fulfilled You should pass two params: <br/> - `value?: string` - a string value that;<br/> - `cellCount: number`;<br/>Returned value will be a TextInput ref that you should pass to`<CodeField/>`component.And when a value length would equal cellCount will be called `.blur()` method.It work perfectly with `useClearByFocusCell` hook                                                                                                                                                                                                                                                                        | Ref<TextInput> | yes      | All      | yes               |

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/Kureev/react-native-blur/blob/master/LICENSE) ，请自由地享受和参与开源。
