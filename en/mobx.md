> Template version: v0.1.3

<p align="center">
  <h1 align="center"> <code>mobx</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mobxjs/mobx/blob/mobx%406.10.0/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github address](https://github.com/mobxjs/mobx/tree/mobx%406.10.0)

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

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

// Create an instance of a store
const counterStore = new CounterStore();

// Use observer to package components and listen for status changes
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

### Compatibility

Verified in the following version:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## attribute

View details[MOBX official documentation](https://mobx.js.org/api.html)

The following is a display of validated interfaces:

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Others

## License

This project is licensed under  [The MIT License (MIT)](https://github.com/mobxjs/mobx/blob/mobx%406.10.0/LICENSE), Please enjoy and participate freely in open source.