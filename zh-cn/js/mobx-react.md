> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>mobx-react</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mobxjs/mobx/blob/mobx-react%407.6.0/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/mobxjs/mobx/tree/mobx-react%407.6.0)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install mobx-react@7.6.0
```

#### **yarn**

```bash
yarn add mobx-react@7.6.0
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
import { observer, inject, Provider } from 'mobx-react';
import { observable, action, makeObservable } from 'mobx';

class CounterStore {
  count = 0;

  constructor() {
    makeObservable(this, {
      count: observable,
      increment: action,
      decrement: action,
    });
  }

  increment = () => {
    this.count += 1;
  };

  decrement = () => {
    this.count -= 1;
  };
}

const counterStore = new CounterStore();

// Counter 组件，使用 @inject 和 @observer 进行连接
@inject('counterStore')
@observer
class Counter extends React.Component {
  render() {
    const { counterStore } = this.props;
    return (
      <View style={styles.container}>
        <Text style={styles.text}>Count: {counterStore.count}</Text>
        <Button title="Increment" onPress={counterStore.increment} />
        <Button title="Decrement" onPress={counterStore.decrement} />
      </View>
    );
  }
}

const App = () => {
  return (
    <Provider counterStore={counterStore}>
      <View style={styles.container}>
        <Counter />
      </View>
    </Provider>
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

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

详情查看[mobx-react官方文档](https://github.com/mobxjs/mobx-react)

如下是已验证接口展示:

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name     | Description                                                                                                                                                | Type     | Required | HarmonyOS Support |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| Observer | Observer is a React component, which applies observer to an anonymous region in your component                                                             | function | no       | yes               |
| Provider | is a component that can pass stores (or other stuff) using React's context mechanism to child components                                                   | function | no       | yes               |
| inject   | can be used to pick up those stores. It is a higher order component that takes a list of strings and makes those stores available to the wrapped component | function | no       | yes               |

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mobxjs/mobx/blob/mobx-react%407.6.0/LICENSE) ，请自由地享受和参与开源。
