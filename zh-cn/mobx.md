> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>mobx</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mobxjs/mobx/blob/mobx%406.10.0/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/mobxjs/mobx/tree/mobx%406.10.0)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install mobx@6.10.0
```

#### **yarn**

```bash
yarn add mobx@6.10.0
```

<!-- tabs:end -->

快速使用：

```js
module.exports = {
  presets: ["module:metro-react-native-babel-preset"],
  plugins: [
    ["@babel/plugin-proposal-decorators", { version: "legacy" }],
    ["@babel/plugin-transform-class-properties", { loose: true }],
  ],
};
```

安装babel相关依赖:

```bash
npm install @babel/core

npm install @babel/plugin-proposal-decorators --save-dev

npm install @babel/plugin-transform-class-properties --save-dev
```

下面的代码展示了这个库的基本使用场景：

```js
import React from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';
import { observer } from 'mobx-react-lite';
import { makeAutoObservable } from 'mobx';

class CounterStore {
  count = 0;

  constructor() {
    makeAutoObservable(this);
  }

  increment() {
    this.count += 1;
  }

  decrement() {
    this.count -= 1;
  }
}

// 创建一个store的实例
const counterStore = new CounterStore();

// 使用observer包裹组件，监听状态变化
const Counter = observer(() => {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Count: {counterStore.count}</Text>
      <Button title="Increment" onPress={() => counterStore.increment()} />
      <Button title="Decrement" onPress={() => counterStore.decrement()} />
    </View>
  );
});

const App = () => {
  return (
    <View style={styles.container}>
      <Counter />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f5fcff',
  },
  text: {
    fontSize: 20,
    marginBottom: 20,
  },
});

export default App;
```

## 约束与限制

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

详情查看[mobx官方文档](https://mobx.js.org/api.html)

如下是已验证接口展示:

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### **Creating observables**

| Name               | Description                                                                               | Type     | Required | HarmonyOS Support |
| ------------------ | ----------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| makeAutoObservable | Automatically make properties, objects, arrays, Maps and Sets observable                  | function | no       | yes               |
| makeObservable     | Properties, entire objects, arrays, Maps and Sets can all be made observable              | function | no       | yes               |
| observable         | Clones an object and makes it observable. Source can be a plain object, array, Map or Set | function | no       | yes               |

#### **Actions**

| Name         | Description                                                                                  | Type     | Required | HarmonyOS Support |
| ------------ | -------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| action       | Use on functions that intend to modify the state                                             | function | no       | yes               |
| action.bound | Like action, but will also bind the action to the instance so that `this` will always be set | function | no       | yes               |
| runInAction  | Create a one-time action that is immediately invoked                                         | function | no       | yes               |
| flow         | MobX friendly replacement for async / await that supports cancellation                       | function | no       | yes               |
| flowResult   | For TypeScript users only. Utility that casts the output of the generator to a promise       | function | no       | yes               |

#### **Computeds**

| Name     | Description                                                                                                                                  | Type     | Required | HarmonyOS Support |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| computed | Creates an observable value that is derived from other observables, but won't be recomputed unless one of the underlying observables changes | function | no       | yes               |

#### **Reactions**

| Name     | Description                                                          | Type     | Required | HarmonyOS Support |
| -------- | -------------------------------------------------------------------- | -------- | -------- | ----------------- |
| autorun  | Reruns a function every time anything it observes changes            | function | no       | yes               |
| reaction | Reruns a side effect when any selected data changes                  | function | no       | yes               |
| when     | Executes a side effect once when a observable condition becomes true | function | no       | yes               |

#### **Introspection utilities**

| Name               | Description                                         | Type     | Required | HarmonyOS Support |
| ------------------ | --------------------------------------------------- | -------- | -------- | ----------------- |
| isObservable       | Is the object / collection made observable by MobX? | function | no       | yes               |
| isObservableArray  | Is the value an observable array?                   | function | no       | yes               |
| isObservableMap    | Is the value an observable Map?                     | function | no       | yes               |
| isObservableObject | Is the value an observable object?                  | function | no       | yes               |
| isObservableProp   | Is the property observable?                         | function | no       | yes               |
| isObservableSet    | Is the value an observable Set?                     | function | no       | yes               |

#### **Configuration**

| Name      | Description                                                      | Type     | Required | HarmonyOS Support |
| --------- | ---------------------------------------------------------------- | -------- | -------- | ----------------- |
| configure | Usage: sets global behavior settings on the active MobX instance | function | no       | yes               |

#### **Utilities**

| Name | Description                                                      | Type     | Required | HarmonyOS Support |
| ---- | ---------------------------------------------------------------- | -------- | -------- | ----------------- |
| toJS | Recursively converts an observable object to a JavaScript object | function | no       | yes               |

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mobxjs/mobx/blob/mobx%406.10.0/LICENSE) ，请自由地享受和参与开源。
