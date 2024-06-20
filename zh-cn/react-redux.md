> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-redux</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/reduxjs/react-redux/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/reduxjs/react-redux?tab=readme-ov-file)

## 安装与使用

#### **yarn**

```bash
yarn add react-redux@^9.1.0
```

#### **npm**

```bash
npm install react-redux@^9.1.0
```

<!-- tabs:end -->

下面展示了这个库的基本使用场景：

1.创建一个命名为store.ts的文件

<!-- {% raw %} -->
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

//从store 本身推断 `RootState` 和 `AppDispatch` 类型
export type RootState = ReturnType<typeof store.getState>;
// 推断类型：{posts: PostsState, comments: CommentsState, users: UsersState}
export type AppDispatch = typeof store.dispatch;
```

2.创建store.ts的文件后，在<code>&lt;App&gt;</code>的外层放置一个<code>&lt;Provider&gt;</code>，并将 store 作为 prop 传递

```ts
// 导出组件
export default function TestPage() {
  return (
    <Provider store={store}> // 将store作为props传递给组件，这样组件就能访问到store和dispatch方法了。
      <View style={styles.container}>
        <UserInfo></UserInfo>
        <FromData></FromData>
      </View>
    </Provider>
  );
}
```

3.创建一个命名为Hooks.ts的文件,虽然可以将 RootState 和 AppDispatch 类型导入每个组件，但最好创建 useDispatch 和 useSelector hooks 类型化版本以供在应用程序中使用。

```ts
import { TypedUseSelectorHook, useDispatch, useSelector } from "react-redux";
import type { RootState, AppDispatch } from "./store";

// 在整个应用程序中使用，而不是简单的 `useDispatch` 和 `useSelector`
export const useAppDispatch: () => AppDispatch = useDispatch;
export const useAppSelector: TypedUseSelectorHook<RootState> = useSelector;
```

4.定义 Slice State 和 Action Types。每个 slice 文件都应该为其初始 state 值定义一个类型，以便 createSlice 能够推断每个案例 reducer 中的 state 类型。

```ts
import { createSlice, PayloadAction } from "@reduxjs/toolkit";
import type { RootState } from "../store";

//定义 slice state 的类型
interface CounterState {
  user: {};
}
//使用该类型定义初始 state
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

// selectors 等其他代码可以使用导入的 `RootState` 类型
export const selectCount = (state: RootState) => state.user.user;

export default counterSlice.reducer;
```

生成的 action creators 将根据你为 reducer 提供的 PayloadAction<T> 类型正确输入以接收 payload 参数。例如，incrementByAmount 需要一个 number 作为其参数。

在某些情况下，TypeScript 可能会不必要地收紧初始 state 的类型。如果发生这种情况，你可以通过使用 as 转换初始 state 来解决它，而不是声明变量的类型：

```ts
//定义 slice state 的类型
interface CounterState {
  user: {};
}
```

5.在 React 组件中使用 Redux State 和 Actions

```ts
import React, { useState } from "react";

import { useAppSelector, useAppDispatch } from "app/hooks";

import { decrement, increment } from "./counterSlice";

export function Counter() {
  // `state` arg 已经正确被键入 `RootState`
  const count = useAppSelector((state) => state.counter.value);
  const dispatch = useAppDispatch();

  // 省略渲染逻辑
}
```
<!-- {% endraw %} -->

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.11;
   SDK：OpenHarmony(api11) 4.1.0.53;
   IDE：DevEco Studio 4.1.3.412;
   ROM：2.0.0.52;
2. RNOH：0.72.13;
   SDK：HarmonyOS NEXT Developer Preview1;
   IDE：DevEco Studio 4.1.3.500;
   ROM：2.0.0.58;

## 静态方法

详情查看[React Redux官方文档](https://cn.react-redux.js.org/introduction/getting-started)

#### **Hooks**

| Name          | Description                                                                                                                | Type     | Required | HarmonyOS Support |
| ------------- | -------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| useSelector() | From there, you may import any of the listed React Redux hooks APIs and use them within your function components.          | function | NO       | yes               |
| useDispatch() | This hook returns a reference to the dispatch function from the Redux store. You may use it to dispatch actions as needed. | function | NO       | yes               |
| useStore()    | This hook returns a reference to the same Redux store that was passed in to the <Provider> component.                      | function | NO       | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/reduxjs/react-redux/blob/master/LICENSE.md) ，请自由地享受和参与开源。
