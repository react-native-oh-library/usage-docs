> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>redux-persist</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/rt2zz/redux-persist/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/rt2zz/redux-persist)

## 安装与使用

#### **yarn**

```bash
yarn add redux-persist@6.0.0
```

#### **npm**

```bash
npm install redux-persist@6.0.0
```

实现持久化效果还需依赖` HarmonyOS 化的async-storage` 库用于原生数据库读写，安装使用文档如下：

> [async-storage 安装使用文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-async-storage-async-storage.md)

<!-- tabs:end -->

下面展示了这个库的基本使用场景：

1.创建一个命名为store.ts的文件

<!-- {% raw %} -->
```ts
import { configureStore, combineReducers } from "@reduxjs/toolkit";

import {
  persistStore,
  persistReducer,
  FLUSH,
  REHYDRATE,
  PAUSE,
  PERSIST,
  PURGE,
  REGISTER,
  createTransform,
} from "redux-persist";

import AsyncStorage from "@react-native-async-storage/async-storage";
import { cartTransform } from "./cartTransform";

import productReducer from "./product";
import commentsReducer from "./comments";
import uiControlReducer from "./uiControl";
import shoppingCartReducer from "./shoppingCart";

// 持久化配置
const persistConfig = {
  key: "root",
  storage: AsyncStorage,
  // 如下配置为不持久化 评论数据
  blacklist: ["comments", "shoppingCart"],
  // 持久化的 reducer
  // whitelist: [ 'products', 'uiControl', 'shoppingCart']
  // debug: false,
  // throttle: 50,
  // keyPrefix: '',
  // serialize: false
};

// 购物车持久化配置
const cartPersistConfig = {
  key: "cart",
  storage: AsyncStorage,
  transforms: [cartTransform],
};

const reducers = combineReducers({
  products: productReducer, // 商品
  comments: commentsReducer, // 商品评论
  uiControl: uiControlReducer, // 页面跳转配置
  shoppingCart: persistReducer(cartPersistConfig, shoppingCartReducer), // 购物车数据
});

const rootStore = configureStore({
  reducer: persistReducer(persistConfig, reducers),
  // 忽略 redux-persist 的action，不配置会报错。
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware({
      serializableCheck: {
        ignoredActions: [FLUSH, REHYDRATE, REGISTER, PAUSE, PERSIST, PURGE],
      },
    }),
});

export type AppStore = typeof rootStore;

export type RootState = ReturnType<typeof rootStore.getState>;
export type AppDispatch = typeof rootStore.dispatch;

export const persistRootStore = persistStore(rootStore);

export default rootStore;
```

2.创建store.ts的文件后，在<code>&lt;App&gt;</code>的外层放置一个<code>&lt;PersistGate&gt;</code>，并将 persistRootStore 作为 prop 传递

```ts
import store, {persistRootStore} from './store'
    ...
    <Provider store={store}>
      <PersistGate loading={null} persistor={persistRootStore}>
        <App />
      </PersistGate>
    </Provider>
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
3. RNOH：0.72.13;
   SDK：HarmonyOS NEXT Developer Preview1;
   IDE：DevEco Studio 4.1.3.500;
   ROM：2.0.0.59;

## 静态方法

详情查看[redux-persist 官方文档](https://github.com/rt2zz/redux-persist/blob/master/README.md#api)

#### **Hooks**

| Name                            | Description                                                                               | Type     | Required | HarmonyOS Support |
| ------------------------------- | ----------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| persistReducer(config, reducer) | returns an enhanced reducer                                                               | function | NO       | yes               |
| persistStore(store)             | returns persistor object with the following methods .purge() .flush() .pause() .persist() | function | NO       | yes               |
| createMigrate(migrations)       | Create a new version of the store                                                         | function | NO       | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/rt2zz/redux-persist/blob/master/LICENSE) ，请自由地享受和参与开源。
