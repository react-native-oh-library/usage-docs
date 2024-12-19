> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-redux</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/reduxjs/react-redux/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/reduxjs/react-redux?tab=readme-ov-file)

## Installation and Usage

#### **yarn**

```bash
yarn add react-redux@^9.1.0
```

#### **npm**

```bash
npm install react-redux@^9.1.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

1. Create a file named store.ts

```ts
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./action/counterSlice";
import inputReducer from "./action/inputInfoReducer";
import userReducer from "./action/UserReducer";

export const store = configureStore({
  reducer: {
    user: userReducer,
  },
});

export type RootState = ReturnType<typeof store.getState>;
export type AppDispatch = typeof store.dispatch;
```

2. Once the store.ts file is created, place a <code>&lt;Provider&gt;</code> on the outer layer of the <code>&lt;App&gt;</code>and pass the store as a prop

```ts
export default function TestPage() {
  return (
    <Provider store={store}>
      <View style={styles.container}>
        <UserInfo></UserInfo>
        <FromData></FromData>
      </View>
    </Provider>
  );
}
```

3. Create a file named Hooks.ts, and while you can import the RootState and AppDispatch types into each component, it's a good idea to create typed versions of useDispatch and useSelector hooks for use in your application.

```ts
import { TypedUseSelectorHook, useDispatch, useSelector } from "react-redux";
import type { RootState, AppDispatch } from "./store";

export const useAppDispatch: () => AppDispatch = useDispatch;
export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector;
```

4. Define Slice States and Action Types. Each slice file should define a type for its initial state value so that createSlice can infer the state type in each case reducer.

```ts
import { createSlice, PayloadAction } from "@reduxjs/toolkit";
import type { RootState } from "../store";

interface CounterState {
  user: {};
}
const initialState: CounterState = {
  user: {
    name: "zhangsna",
    date: "2000-9-30",
    email: "130xxxxxxx@qq.com",
    height: "180",
    hobby: "study",
  },
};
const counterSlice = createSlice({
  name: "initInfo",
  initialState,
  reducers: {
    addUser: (state, action: PayloadAction<object>) => {
      state.user = action.payload;
    },
  },
});

export const { addUser } = counterSlice.actions;

export const selectCount = (state: RootState) => state.user.user;

export default counterSlice.reducer;
```

The resulting action creators will be correctly entered to receive the payload parameter based on the PayloadAction<T> type you provided for the reducer. For example, incrementByAmount requires a number as its argument.

In some cases, TypeScript may unnecessarily tighten the type of the initial state. If this happens, you can work around it by transforming the initial state with as instead of declaring the type of variable:

```ts
interface CounterState {
  user: {};
}
```

5. Use Redux States and Actions in your React components

```ts
import React, { useState } from "react";

import { useAppSelector, useAppDispatch } from "app/hooks";

import { decrement, increment } from "./counterSlice";

export function Counter() {
  const count = useAppSelector((state) => state.counter.value);
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
   ROM：2.0.0.58;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Static Methods

For details, see [React Redux Official Documents](https://cn.react-redux.js.org/introduction/getting-started)

#### **Hooks**

| Name          | Description                                                                                                                | Type     | Required | HarmonyOS Support |
| ------------- | -------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| useSelector() | From there, you may import any of the listed React Redux hooks APIs and use them within your function components.          | function | NO       | yes               |
| useDispatch() | This hook returns a reference to the dispatch function from the Redux store. You may use it to dispatch actions as needed. | function | NO       | yes               |
| useStore()    | This hook returns a reference to the same Redux store that was passed in to the <Provider> component.                      | function | NO       | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/reduxjs/react-redux/blob/master/LICENSE.md).
