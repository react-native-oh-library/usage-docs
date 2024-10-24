> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/eranbo/react-native-base64)

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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
   const wordEqualDecodeWord = `word equal decode word: ${word === decodeWord}`;
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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.29; SDK：HarmonyOS-Next-DB1 5.0.0.61; IDE：DevEco Studio 5.0.3.706; ROM：5.0.0.61;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform    | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- |-------------| ------------------ |
| encode  | encode from string  | string  | no | Android iOS | yes |
| decode  | decode base64 strings   | string  | no | Android iOS | yes |
| encodeFromByteArray  | encode from Unit8Array  | Unit8Array  | no | Android iOS | yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/eranbo/react-native-base64/blob/master/LICENSE).
