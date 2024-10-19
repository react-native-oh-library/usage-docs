<!-- {% raw %} -->
> Template version: v0.1.3

<p align="center">
  <h1 align="center"> <code>mobx-react</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mobxjs/mobx/blob/mobx-react%407.6.0/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/mobxjs/mobx/tree/mobx-react%407.6.0)

## Installation and Usage

Go to the project directory and execute the following instruction:

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

Quick use:

```js
module.exports = {
  presets: ["module:metro-react-native-babel-preset"],
  plugins: [
    ["@babel/plugin-proposal-decorators", { version: "legacy" }],
    ["@babel/plugin-transform-class-properties", { loose: true }],
  ],
};
```

Install Babel related dependencies:

```bash
npm install @babel/core

npm install @babel/plugin-proposal-decorators --save-dev

npm install @babel/plugin-transform-class-properties --save-dev
```

mobx-react is used as an example.

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

// Counter component, connect using @inject and @observer
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

### Compatibility

The following is a display of validated interfaces:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## attribute

View details[Official documentation of mobx-react](https://github.com/mobxjs/mobx-react)

The following is a display of validated interfaces:

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name     | Description                                                                                                                                                | Type     | Required | HarmonyOS Support |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| Observer | Observer is a React component, which applies observer to an anonymous region in your component                                                             | function | no       | yes               |
| Provider | is a component that can pass stores (or other stuff) using React's context mechanism to child components                                                   | function | no       | yes               |
| inject   | can be used to pick up those stores. It is a higher order component that takes a list of strings and makes those stores available to the wrapped component | function | no       | yes               |

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mobxjs/mobx/blob/mobx-react%407.6.0/LICENSE), Please enjoy and participate freely in open source.


<!-- {% endraw %} -->