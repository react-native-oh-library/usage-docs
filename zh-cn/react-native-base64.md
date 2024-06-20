> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-base64</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/eranbo/react-native-base64/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/eranbo/react-native-base64)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm i react-native-base64@0.2.1

// typescript 项目需下载对应包的类型声明
npm i @types/react-native-base64 -D
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

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

   // 输入文字
   const [word, setWord] = useState('react native');
   // 编码输入文字
   const encodeWord = base64.encode(word);
   // 解码输入文字
   const decodeWord = base64.decode(encodeWord);
   // 解码结果 是否 和原文字相同
   const wordEqualDecodeWord = `word equal decode word: ${word === decodeWord}`
   // 将word 转为 unit8 array
   const byteArrayWord = Uint8Array.from(word.split(''), w => w.charCodeAt(0));
   // 对 unit 8 array 进行编码
   const encodeWordFromByteArray = base64.encodeFromByteArray(byteArrayWord);
   // 对 上一步结果进行解码
   const decodeFromByteArray = base64.decode(encodeWordFromByteArray);

   const backgroundStyle = {
      backgroundColor: isDarkMode ? Colors.darker : Colors.lighter,
   };

  return (
    <>
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
    </>
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

## 兼容性

在以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

### base64 提供的方法:

| Name                | Description            | Type       | Required | HarmonyOS Support |
| ------------------- | ---------------------- | ---------- | -------- | ----------------- |
| encode              | encode from string     | string     | No       | Yes               |
| decode              | decode base64 strings  | string     | No       | Yes               |
| encodeFromByteArray | encode from Unit8Array | Unit8Array | No       | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/eranbo/react-native-base64/blob/master/LICENSE) ，请自由地享受和参与开源。
