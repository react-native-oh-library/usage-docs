<!-- {% raw %} -->
> Template version: v0.1.3

<p align="center">
  <h1 align="center"> <code>redux-persist</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/rt2zz/redux-persist/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [GitHub address](https://github.com/rt2zz/redux-persist)

## Installation and Usage

#### **yarn**

```bash
yarn add redux-persist@6.0.0
```

#### **npm**

```bash
npm install redux-persist@6.0.0
```

To achieve persistence, you also need to rely on the 'HarmonyOS-enabled async-storage' library for native database reading and writing, as shown in the installation and use documents below：

> [async-storage Installation and use documentation](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-async-storage-async-storage.md)

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

1.Create a file named store.ts

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

// Persistent configuration
const persistConfig = {
  key: "root",
  storage: AsyncStorage,
  // The following configuration is set to not persist comment data
  blacklist: ["comments", "shoppingCart"],
  // Persistent reducer
  // whitelist: [ 'products', 'uiControl', 'shoppingCart']
  // debug: false,
  throttle: 50,
  // keyPrefix: '',
  // serialize: false
};

// Persistent configuration of shopping cart
const cartPersistConfig = {
  key: "cart",
  storage: AsyncStorage,
  transforms: [cartTransform],
};

const reducers = combineReducers({
  products: productReducer, // goods
  comments: commentsReducer, // Product Review
  uiControl: uiControlReducer, //Page jump configuration
  shoppingCart: persistReducer(cartPersistConfig, shoppingCartReducer), //Shopping cart data
});

const rootStore = configureStore({
  reducer: persistReducer(persistConfig, reducers),
  //Ignoring the action of redux reverse and not configuring it will result in an error.
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

2.Once the store.ts file is created, place a <code>&lt;PersistGate&gt;</code> on the outer layer of the &gt; of the <code>&lt;App</code> and pass the persistRootStore as a prop

```ts
import store, {persistRootStore} from './store'
    ...
    <Provider store={store}>
      <PersistGate loading={null} persistor={persistRootStore}>
        <App />
      </PersistGate>
    </Provider>
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
3. RNOH：0.72.13;
   SDK：HarmonyOS NEXT Developer Preview1;
   IDE：DevEco Studio 4.1.3.500;
   ROM：2.0.0.59;

## Static Methods

Please check for details [redux-persist official documentation](https://github.com/rt2zz/redux-persist/blob/master/README.md#api)

#### **Hooks**

| Name                            | Description                                                                               | Type     | Required | HarmonyOS Support |
| ------------------------------- | ----------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| persistReducer(config, reducer) | returns an enhanced reducer                                                               | function | NO       | yes               |
| persistStore(store)             | returns persistor object with the following methods .purge() .flush() .pause() .persist() | function | NO       | yes               |
| createMigrate(migrations)       | Create a new version of the store                                                         | function | NO       | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/rt2zz/redux-persist/blob/master/LICENSE).

<!-- {% endraw %} -->