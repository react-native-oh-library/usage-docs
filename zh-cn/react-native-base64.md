> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-base64</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/eranbo/react-native-base64">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/eranbo/react-native-base64/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/eranbo/react-native-base64)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm i react-native-base64@0.2.1
```

#### **yarn**

```bash
yarn add react-native-base64@0.2.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react';
import base64 from 'react-native-base64';
import {
   ScrollView,
   StyleSheet,
   Text,
   TextInput,
   useColorScheme,
   View,
} from 'react-native';

import {
   Colors,
} from 'react-native/Libraries/NewAppScreen';

export function Base64Page(): JSX.Element {
   const isDarkMode = useColorScheme() === 'dark';
   const [word, setWord] = useState('react native');
   const encodeWord = base64.encode(word);
   const decodeWord = base64.decode(encodeWord);
   const wordEqualDecodeWord = `word equal decode word: ${word === decodeWord}`；
   const byteArrayWord = Uint8Array.from(word.split(''), w => w.charCodeAt(0));
   const encodeWordFromByteArray = base64.encodeFromByteArray(byteArrayWord);
   const decodeFromByteArray = base64.decode(encodeWordFromByteArray);
   const backgroundStyle = {
      backgroundColor: isDarkMode ? Colors.darker : Colors.lighter,
   };

  return (
      <ScrollView
        contentInsetAdjustmentBehavior="automatic"
        style={backgroundStyle}>
        <View
          style={{ backgroundColor: isDarkMode ? Colors.black : Colors.white, }}>
          <View style={styles.cardView}>
            <Text>Test Word: </Text>
            <TextInput
              style={styles.TextInput}
              onChangeText={setWord}
              value={word}
            ></TextInput>
            <Text style={{marginTop: 12}}>encode Result: <Text style={{color: 'orange'}}>{encodeWord}</Text></Text>
            <Text style={{marginTop: 12}}>decode Result: <Text style={{color: 'orange'}}>{decodeWord}</Text></Text>
            <Text style={{marginTop: 12}}>encodeFromByteArray Result: <Text style={{color: 'orange'}}>{encodeWordFromByteArray}</Text></Text>
            <Text style={{marginTop: 12}}>decode the value above Result: <Text style={{color: 'orange'}}>{decodeFromByteArray}</Text></Text>
          </View>
        </View>
      </ScrollView>
  );

}

const styles = StyleSheet.create({
   cardView: { margin: 10, backgroundColor: '#f0f0f0', display: 'flex', padding: 10, borderRadius: 8 },
   TextInput: {height: 40, borderColor: '#ccc', borderWidth: 1, borderRadius: 4, width: '90%'},
   highlight: {
      fontWeight: '700',
   },
});

```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.29; SDK：HarmonyOS-Next-DB1 5.0.0.61; IDE：DevEco Studio 5.0.3.706; ROM：5.0.0.61;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 静态方法:

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| encode  | encode from string  | string  | no | Android、iOS | yes |
| decode  | decode base64 strings   | string  | no | Android、iOS | yes |
| encodeFromByteArray  | encode from Unit8Array  | Unit8Array  | no | Android、iOS | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/eranbo/react-native-base64/blob/master/LICENSE) ，请自由地享受和参与开源。