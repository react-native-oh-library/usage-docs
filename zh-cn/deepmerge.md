> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>deepmerge</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/TehShrike/deepmerge/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/TehShrike/deepmerge)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install deepmerge@4.3.1
```

#### **yarn**

```bash
yarn add deepmerge@4.3.1
```

<!-- tabs:end -->

快速使用：

```js
import React from 'react';
import { View, Text, StyleSheet, ScrollView } from 'react-native';
import deepmerge from 'deepmerge';

const App = () => {
  // 定义两个需要合并的对象
  const object1 = {
    name: 'John',
    age: 30,
    address: {
      street: '123 Main St',
      city: 'Springfield',
    },
  };

  const object2 = {
    age: 31,
    address: {
      country: 'USA',
    },
    hobbies: ['Reading', 'Hiking'],
  };

  // 使用 deepmerge 合并两个对象
  const mergedObject = deepmerge(object1, object2);

  return (
    <ScrollView contentContainerStyle={styles.container}>
      <Text style={styles.title}>Object 1:</Text>
      <Text style={styles.text}>{JSON.stringify(object1, null, 2)}</Text>

      <Text style={styles.title}>Object 2:</Text>
      <Text style={styles.text}>{JSON.stringify(object2, null, 2)}</Text>

      <Text style={styles.title}>Merged Object:</Text>
      <Text style={styles.text}>{JSON.stringify(mergedObject, null, 2)}</Text>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flexGrow: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f5fcff',
    padding: 20,
  },
  title: {
    fontSize: 20,
    fontWeight: 'bold',
    marginVertical: 10,
  },
  text: {
    fontSize: 16,
    marginBottom: 20,
    textAlign: 'left',
    width: '100%',
  },
});

export default App;
```

## 约束与限制

### 兼容性

在下述版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [deepmerge源库地址](https://github.com/TehShrike/deepmerge)

| Name                                     | Description                                                                                          | Type     | Required | HarmonyOS Support |
| ---------------------------------------- | ---------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| deepmerge(x, y, [options])               | Merge two objects x and y deeply, returning a new merged object with the elements from both x and y. | function | no       | yes               |
| deepmerge.all(arrayOfObjects, [options]) | Merges any number of objects into a single result object.                                            | function | no       | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/TehShrike/deepmerge/blob/master/license.txt) ，请自由地享受和参与开源。
