<!-- {% raw %} -->
> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>redux</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/reduxjs/redux/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [GitHub address](https://github.com/reduxjs/redux)

## Installation and Usage

#### **yarn**

```bash
yarn add redux@^5.0.1
```

#### **npm**

```bash
npm install redux@^5.0.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

1.编写子reducer，负责state具体变化的过程

```ts
const defaultState = {
  number: 100,
};
type State = {
  counterState: {
    number: number;
  };
};

const counterReducer = (state = defaultState, action: { type: any }) => {
  switch (action.type) {
    case "ADD_NUMBER":
      return {
        ...state,
        number: state.number + 1,
      };
    default:
      return state;
  }
};

const rootReducer = combineReducers({
  counterState: counterReducer,
});
```

2.定义 Slice State 和 Action Types。每个 slice 文件都应该为其初始 state 值定义一个类型，以便 createSlice 能够推断每个案例 reducer 中的 state 类型。

```ts
const rootReducer = combineReducers({ counterState: counterReducerfun });
const store = createStore(rootReducer);
const addNumberAction = { type: "ADD_NUMBER" };
```

3.在<code>&lt;App&gt;</code>的外层放置一个<code>&lt;Provider&gt;</code>，并将 store 作为 prop 传递

```ts
export default function TestPage() {
  return (
    <Provider store={store}> 
      <View style={styles.container}>
        <Counter></Counter>
      </View>
    </Provider>
  );
}
```

4.在 React 组件中使用 Redux State 和 Actions

```ts
import React, { useState } from "react";

import { useSelector, useDispatch } from "react-redux";

import { decrement, increment } from "./counterSlice";

export function Counter() {
  const number = useAppSelector((state: State) => state.counter.number);
  const dispatch = useAppDispatch();

}
```

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.11;
   SDK：OpenHarmony(api11) 4.1.0.53;
   IDE：DevEco Studio 4.1.3.412;
   ROM：2.0.0.52;
2. RNOH：0.72.13;
   SDK：HarmonyOS NEXT Developer Preview1;
   IDE：DevEco Studio 4.1.3.500;
   ROM：2.0.0.59;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Static Methods

For details, see [Redux Official Documents](https://www.redux.org.cn/api/compose.html)

#### **createStore**

| Name          | Description                                                                                                        | Type     | Required | HarmonyOS Support |
| ------------- | ------------------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| createStore() | Create a Redux store that contains the complete state tree of your program. The application should have a storage. | function | NO       | yes               |

#### **Store**

| Name                        | Description                                                                                                        | Type     | Required | HarmonyOS Support |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| getState()                  | Returns the current state tree of the application. It is the same value returned by the last reducer of the store. | function | NO       | yes               |
| dispatch(action)            | This is the only way to trigger state changes                                                                      | function | NO       | yes               |
| subscribe(listener)         | Add a change listener                                                                                              | function | NO       | yes               |
| replaceReducer(nextReducer) | Replace the reducer currently used by the store to calculate state                                                 | function | NO       | yes               |

#### **combineReducers**

| Name              | Description                                                                                                                                                                                            | Type     | Required | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| combineReducers() | The combineReducers auxiliary function is to combine an object with multiple different reducer functions as value into a final reducer function, and then call the createStore method on this reducer. | function | NO       | yes               |

#### **bindActionCreators**

| Name              | Description                                                                                   | Type     | Required | HarmonyOS Support |
| ----------------- | --------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| combineReducers() | Convert an object whose value is a different action creator into an object with the same key. | function | NO       | yes               |

#### **compose**

| Name      | Description                                    | Type     | Required | HarmonyOS Support |
| --------- | ---------------------------------------------- | -------- | -------- | ----------------- |
| compose() | Combine multiple functions from right to left. | function | NO       | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/reduxjs/redux/blob/master/LICENSE.md).

<!-- {% endraw %} -->