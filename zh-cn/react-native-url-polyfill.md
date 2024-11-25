> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-url-polyfill</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/charpeni/react-native-url-polyfill">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/charpeni/react-native-url-polyfill/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/charpeni/react-native-url-polyfill)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install --save react-native-url-polyfill@2.0.0
```

#### **yarn**

```bash
yarn add react-native-url-polyfill@2.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { ScrollView, Text, Button, View, StyleSheet } from 'react-native';
import { URL, URLSearchParams } from 'react-native-url-polyfill';

const URLPolyfillDemo = () => {
  const url = new URL('https://github.com');
  const searchParams = new URLSearchParams('abc=456&rn=ReactNative&abc=javascript');

  const [appendResult, setAppendResult] = useState('');
  const [setResult, setSetResult] = useState('');
  const [deleteResult, setDeleteResult] = useState('');
    
  // searchParams.append()
  const appendExample = () => {
    searchParams.append('q', 'CodeHub');
    let result = searchParams.toString();
    setAppendResult(result);
  }

  // searchParams.set()
  const setExample = () => {
    searchParams.set('abc', 'Gitee');
    let result = searchParams.toString();
    setSetResult(result);
  }

  // searchParams.delete()
  const deleteExample = () => {
    searchParams.delete('abc', 'javascript');
    let result = searchParams.toString();
    setDeleteResult(result);
  }

  return (
    <ScrollView>
      <View>
      	<View>
          <Text style={styles.text}>property: href</Text>
          <Text style={styles.result} allowFontScaling>{url.href}</Text>
        </View>

        <View>
          <Text style={styles.text}>Method：append（q,CodeHub）</Text>
          <Button
            title="append"
            color="#9a73ef"
            onPress={appendExample}
          />
          <Text style={styles.result} allowFontScaling>{appendResult}</Text>
        </View>

        <View>
          <Text style={styles.text}>Method：set（abc,Gitee））</Text>
          <Button
            title="set"
            color="#9a73ef"
            onPress={setExample}
          />
          <Text style={styles.result} allowFontScaling>{setResult}</Text>
        </View>

        <View>
          <Text style={styles.text}>Method：delete（abc,javascript）</Text>
          <Button
            title="delete"
            color="#9a73ef"
            onPress={deleteExample}
          />
          <Text style={styles.result} allowFontScaling>{deleteResult}</Text>
        </View>
      </View>
    </ScrollView>
 )
};

const styles = StyleSheet.create({
  text: {
    fontSize: 18,
    marginBottom: 10,
    color: 'red',
  },
  result: {
    marginTop: 10,
    fontSize: 18,
    marginBottom: 10,
    color: 'black',
  }
});

export default URLPolyfillDemo;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name         | Description                                                  | Type            | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------ | --------------- | -------- | ----------- | :---------------- |
| hash         | Gets and sets the fragment portion of the URL.               | string          | no       | Android/iOS | yes               |
| host         | Gets and sets the host portion of the URL.                   | string          | no       | Android/iOS | yes               |
| hostname     | Gets and sets the host name portion of the URL.              | string          | no       | Android/iOS | yes               |
| href         | Gets and sets the serialized URL.                            | string          | no       | Android/iOS | yes               |
| origin       | Gets the read-only serialization of the URL's origin.        | string          | no       | Android/iOS | yes               |
| password     | Gets and sets the password portion of the URL.               | string          | no       | Android/iOS | yes               |
| pathname     | Gets and sets the path portion of the URL.                   | string          | no       | Android/iOS | yes               |
| port         | Gets and sets the port portion of the URL.                   | string          | no       | Android/iOS | yes               |
| protocol     | Gets and sets the protocol portion of the URL.               | string          | no       | Android/iOS | yes               |
| search       | Gets and sets the serialized query portion of the URL.       | string          | no       | Android/iOS | yes               |
| searchParams | Gets the `URLSearchParams` object representing the query parameters of the URL. | URLSearchParams | no       | Android/iOS | yes               |
| username     | Gets and sets the username portion of the URL.               | string          | no       | Android/iOS | yes               |
| size         | The total number of parameter entries on the `URLSearchParams` object. | number          | no       | Android/iOS | yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name     | Description                                                  | Type                               | Required | Platform    | HarmonyOS Support |
| -------- | ------------------------------------------------------------ | ---------------------------------- | -------- | ----------- | ----------------- |
| toString | The `toString()` method on the `URL` object returns the serialized URL. | string                             | no       | Android/iOS | yes               |
| toJSON   | The `toJSON()` method on the `URL` object returns the serialized URL. | string                             | no       | Android/iOS | yes               |
| append   | Append a new name-value pair to the query string.            | void                               | no       | Android/iOS | yes               |
| delete   | where name is `name` and value is `value`,removes all name-value pairs. | void                               | no       | Android/iOS | yes               |
| entries  | Returns an ES6 `Iterator` over each of the name-value pairs in the query. | IterableIterator<[string, string]> | no       | Android/iOS | yes               |
| forEach  | Iterates over each name-value pair in the query and invokes the given function. | void                               | no       | Android/iOS | yes               |
| get      | Returns the value of the first name-value pair whose name is `name`. If there are no such pairs, `null` is returned. | string \| null                     | no       | Android/iOS | yes               |
| getAll   | Returns the values of all name-value pairs whose name is `name`. If there are no such pairs, an empty array is returned. | string[]                           | no       | Android/iOS | yes               |
| has      | Checks if the `URLSearchParams` object contains key-value pair(s) based on `name` and an optional `value` argument. | boolean                            | no       | Android/iOS | yes               |
| keys     | Returns an ES6 `Iterator` over the names of each name-value pair. | IterableIterator<string>           | no       | Android/iOS | yes               |
| set      | Sets the value in the `URLSearchParams` object associated with `name` to `value`. | void                               | no       | Android/iOS | yes               |
| sort     | Sort all existing name-value pairs in-place by their names.  | void                               | no       | Android/iOS | yes               |
| toString | Returns the search parameters serialized as a string on the `URLSearchParams` object, with characters percent-encoded where necessary . | string                             | no       | Android/iOS | yes               |
| values   | Returns an ES6 `Iterator` over the values of each name-value pair. | IterableIterator<string>           | no       | Android/iOS | yes               |

## 遗留问题

## 其他

- [ ] 本库在Harmony、iOS、Android都存在的问题，URLSearchParams对象上size属性无法获取对应参数条目的总数，问题: [issue#472](https://github.com/charpeni/react-native-url-polyfill/issues/472)
- [ ] 本库在Harmony、iOS、Android都存在的问题，URLSearchParams对象上sort方法按名称对现有的key-value进行排序，排序无效果， 问题: [issue#471](https://github.com/charpeni/react-native-url-polyfill/issues/471)

## 开源协议

本项目基于[The MIT License](https://github.com/charpeni/react-native-url-polyfill/blob/main/LICENSE) ，请自由地享受和参与开源。
