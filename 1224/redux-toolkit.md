> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>redux-toolkit</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/reduxjs/redux-toolkit?tab=readme-ov-file">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/reduxjs/redux-toolkit?tab=MIT-1-ov-file">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!tip] [Github 地址](https://github.com/reduxjs/redux-toolkit)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[redux-toolkit Releases](https://github.com/reduxjs/redux-toolkit/releases)，并下载适用版本的 tgz 包。
进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @reduxjs/toolkit@2.2.1
```

#### **yarn**

```bash
yarn add @reduxjs/toolkit@2.2.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

1.在index.js入口文件引入provider组件，并添加sotre属性

```js
// index.js
import React from 'react'
import ReactDOM from 'react-dom'
import './index.css'
import App from './App'
import { store } from './app/store'
import { Provider } from 'react-redux'

ReactDOM.render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById('root')
)
```

2.创建一个createSlice切片，并将reducer属性导出：
```js
// features/counter/counterSlice.js
import { createSlice } from '@reduxjs/toolkit'
import type { PayloadAction } from '@reduxjs/toolkit'

export interface CounterState {
  value: number
}

const initialState: CounterState = {
  value: 0,
}

export const counterSlice = createSlice({
  name: 'counter',
  initialState,
  reducers: {
    increment: (state) => {
      state.value += 1
    },
    decrement: (state) => {
      state.value -= 1
    },
    incrementByAmount: (state, action: PayloadAction<number>) => {
      state.value += action.payload
    },
  },
})

export const { increment, decrement, incrementByAmount } = counterSlice.actions

export default counterSlice.reducer
```
3.创建store.js使用configureStore引入上面导出的reducer

```js
// app/store.js
import { configureStore } from '@reduxjs/toolkit'
import counterReducer from '../features/counter/counterSlice'

export const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
})

export type RootState = ReturnType<typeof store.getState>

export type AppDispatch = typeof store.dispatch
```
4.编写conter组件实现简单的增加减少计数

```js
// features/counter/Counter.js
import React from 'react'
import type { RootState } from '../../app/store'
import { useSelector, useDispatch } from 'react-redux'
import { decrement, increment } from './counterSlice'

export function Counter() {
  const count = useSelector((state: RootState) => state.counter.value)
  const dispatch = useDispatch()

  return (
    <div>
      <div>
        <button
          aria-label="Increment value"
          onClick={() => dispatch(increment())}
        >
          Increment
        </button>
        <span>{count}</span>
        <button
          aria-label="Decrement value"
          onClick={() => dispatch(decrement())}
        >
          Decrement
        </button>
      </div>
    </div>
  )
}
```

## 约束与限制

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

## 方法和属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
> 详情见 [redux-toolkit 源库地址](https://github.com/reduxjs/redux-toolkit)

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| -------------------- | --------------- | -------- | -------- | -------- | ----------------- |
| configureStore | 创建store的方法     | Function   | yes      | All      | yes               |
| reducer | configureStore参数，reducer对象     | Object   | yes      | All      | yes               |
| middleware | configureStore参数，存放中间件的数组     | Array   | yes      | All      | yes               |
| devTools | configureStore参数，浏览器调试用具     | Boolean   | yes      | Web      | no              |
| preloadedState | configureStore参数，默认的state值     | Object   | yes      | All      | yes |
| enhancers | configureStore参数，存放增强功能数组     | Array   | yes      | All      | yes |
| getDefaultMiddleware | 获取默认中间件列表     | Function   | yes      | All      | yes |
| immutableCheck | getDefaultMiddleware对象参数属性     | Boolean   | yes      | All      | yes |
| serializableCheck | getDefaultMiddleware对象参数属性     | Boolean   | yes      | All      | yes |
| actionCreatorCheck | getDefaultMiddleware对象参数属性     | Boolean   | yes      | All      | yes |
| createListenerMiddleware | 创建中间件监听函数     | Function   | yes      | All      | yes |
| middleware | createListenerMiddleware属性，中间件列表     | Array   | yes      | All      | yes |
| startListening | createListenerMiddleware属性，添加一个监听     | Function   | yes      | All      | yes |
| stopListening | createListenerMiddleware属性，暂停一个监听     | Function   | yes      | All      | yes |
| clearListeners | createListenerMiddleware属性，清除所有监听     | Function   | yes      | All      | yes |
| addListener | createListenerMiddleware属性，添加一个监听     | Function   | yes      | All      | yes |
| removeListener | createListenerMiddleware属性，暂停一个监听     | Function   | yes      | All      | yes |
| clearAllListeners | createListenerMiddleware属性，清除所有监听     | Function   | yes      | All      | yes |
| createDynamicMiddleware | 创建一个中间件     | Function   | yes      | All      | yes |
| getDefaultEnhancers | 获取默认增强功能组件     | Function   | yes      | All      | yes |
| createReducer | 创建reducer     | Function   | yes      | All      | yes |
| addCase | createReducer函数返回对象参数方法，添加action     | Function   | yes      | All      | yes |
| addMatcher | createReducer函数返回对象参数方法，添加过滤条件     | Function   | yes      | All      | yes |
| addDefaultCase | createReducer函数返回对象参数方法，添加默认action     | Function   | yes      | All      | yes |
| createAction | 创建action     | Function   | yes      | All      | yes |
| createSlice | 创建slice切片    | Function   | yes      | All      | yes |
| name | createSlice属性，store名字    | String   | yes      | All      | yes |
| initialState | createSlice属性，store默认值    | object   | yes      | All      | yes |
| reducers | createSlice属性，reducer对象    | Object   | yes      | All      | yes |
| extraReducers | createSlice属性，额外的reducer对象    | Object   | yes      | All      | yes |
| createAsyncThunk | 创建异步action    | Function   | yes      | All      | yes |
| createEntityAdapter | 创建适配器    | Function   | yes      | All      | yes |
| selectId | createEntityAdapter属性，表示唯一ID    | String   | yes      | All      | yes |
| sortComparer | createEntityAdapter属性，排序方法    | Function   | yes      | All      | yes |
| getInitialState | createEntityAdapter属性，默认状态    | Object   | yes      | All      | yes |
| combineSlices | 结合两个Slice切片    | Function   | yes      | All      | yes |
| createSelector | 创建select选择器    | Function   | yes      | All      | yes |
| combineSlices | 结合两个Slice切片    | Function   | yes      | All      | yes |

## 工具方法
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| -------------------- | --------------- | -------- | -------- | -------- | ----------------- |
| isAllOf | 判断action是否全部通过     | Function   | yes      | All      | yes |
| isAnyOf | 判断action是否有一个通过     | Function   | yes      | All      | yes |
| isAsyncThunkAction | 判断action是否是异步     | Function   | yes      | All      | yes |
| isPending | 判断action是否在执行中    | Function   | yes      | All      | yes |
| isRejected | 判断action是否执行完成     | Function   | yes      | All      | yes |
| isFulfilled | 判断action是否执行失败     | Function   | yes      | All      | yes |
| isRejectedWithValue | 判断action是否执行失败并返回值     | Function   | yes      | All      | yes |
| nanoid | 生成随机字符串     | Function   | yes      | All      | yes |
| miniSerializeError | 打印错误信息     | Function   | yes      | All      | yes |
## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/reduxjs/redux-toolkit?tab=readme-ov-file)，请自由地享受和参与开源。

