> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>redux-actions</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/redux-utilities/redux-actions">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/redux-utilities/redux-actions/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!tip] [Github 地址](https://github.com/redux-utilities/redux-actions)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install redux-actions@2.6.5

// typescript 项目需下载对应包的类型声明
npm i @types/redux-actions -D
```

#### **yarn**

```bash
yarn add redux-actions@2.6.5

// typescript 项目需下载对应包的类型声明
yarn add @types/redux-actions -D
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

运行demo还需安装以下依赖：

```bash
npm install redux
npm install react-redux
```

1.定义state的类型

// LoginType.ts

```ts
export interface IAppUser {
  id: string;
  name: string;
}
```

2.定义action

// loginAction.ts

```ts
import { IAppUser } from "./loginType";
import { createActions } from "redux-actions";

export const LOGIN_ACTION = {
  LOGIN: "login",
  LOGOUT: "logout",
  CHANGENAME: "changName",
};

export default createActions({
  [LOGIN_ACTION.LOGIN]: (appUser: IAppUser) => appUser,
  [LOGIN_ACTION.LOGOUT]: () => null,
  [LOGIN_ACTION.CHANGENAME]: (appUser: IAppUser) => appUser,
});
```

3.定义reducer

// loginReducer.ts

```ts
import { LOGIN_ACTION } from "./loginAction";
import {
  Action,
  handleActions as createReducers,
  combineActions,
} from "redux-actions";
import { IAppUser } from "./loginType";

const defaultState = {
  // defautl value 不能为null
  appUser: {},
};

export default createReducers(
  {
    // payload 参数名固定，类型推导
    [LOGIN_ACTION.LOGIN]: (state, { payload }: Action<IAppUser>) => {
      console.log("createReducers LOGIN_ACTION.LOGIN", JSON.stringify(payload));
      return {
        ...state,
        appUser: payload,
      };
    },
    // 异常处理
    [LOGIN_ACTION.LOGOUT]: {
      next(state) {
        console.log("createReducers LOGIN_ACTION.LOGOUT", JSON.stringify({}));
        return {
          ...state,
          appUser: {},
        };
      },
      throw(state) {
        return state;
      },
    },
    [`${combineActions(LOGIN_ACTION.LOGIN, LOGIN_ACTION.CHANGENAME)}`]: (
      state,
      { payload }: Action<IAppUser>,
    ) => {
      console.log(
        "createReducers combineActions",
        JSON.stringify(state.appUser),
        "action" + JSON.stringify(payload),
      );
      return {
        ...state,
        appUser: payload,
      };
    },
  },
  defaultState,
);
```

4.定义store

// loginStore.ts

```ts
import { legacy_createStore as createStore, combineReducers } from "redux";
import loginReducer from "./loginReducer";

export const rootReducer = combineReducers({
  login: loginReducer,
});

const store = createStore(rootReducer);

export type RootState = ReturnType<typeof rootReducer>;
export type AppDispatch = typeof store.dispatch;
export default store;
```

5.通过connector将state和action挂载到组件

// loginDemo.tsx

```tsx
import { connect, ConnectedProps } from "react-redux";
import { Button, View, Text, StyleSheet } from "react-native";
import { RootState } from "./loginStore";
import actions, { LOGIN_ACTION } from "./loginAction";

const mapState = (state: RootState) => ({
  appUser: state.login.appUser,
});

const mapDispatch = {
  onLogin: actions[LOGIN_ACTION.LOGIN],
  onLogout: actions[LOGIN_ACTION.LOGOUT],
  onChangeName: actions[LOGIN_ACTION.CHANGENAME],
};

const connector = connect(mapState, mapDispatch);
type PropsFromRedux = ConnectedProps<typeof connector>;

const Login = (props: PropsFromRedux) => {
  return (
    <View style={styles.viewStyle}>
      <View style={styles.viewTextStyle}>
        <Text style={styles.textStyle}>
          appUser：{JSON.stringify(props.appUser)}
        </Text>
      </View>
      <View style={styles.viewTextStyle}>
        <Button
          title="修改appUser"
          onPress={() => {
            props.onLogin({ id: "1", userName: "123" });
          }}
        />
      </View>
      <View style={styles.viewTextStyle}>
        <Button
          title="修改appUser name"
          onPress={() => {
            props.onChangeName({ id: "1", userName: "456" });
          }}
        />
      </View>
      <Button title="清空appUser" onPress={props.onLogout} />
    </View>
  );
};

const styles = StyleSheet.create({
  viewStyle: {
    display: "flex",
    flexDirection: "column",
    width: 300,
  },
  viewTextStyle: {
    marginBottom: 10,
  },
  textStyle: {
    fontSize: 20,
  },
});

export default connector(Login);
```

6.使用

// index.tsx

```tsx
import { Provider } from "react-redux";
import { StyleSheet, View } from "react-native";
import store from "./loginStore";
import Login from "./loginDemo";

// 导出组件
export default function ReduxDemo() {
  return (
    <Provider store={store}>
      <View style={styles.container}>
        <Login />
      </View>
    </Provider>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
  },

  counterViewStyle: {
    backgroundColor: "pink",
    width: 200,
    height: 60,

    flexDirection: "row",
    alignItems: "center",
    justifyContent: "space-around",
  },
});
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                                               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Type     | Required | Platform    | HarmonyOS Support |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| createAction(type, payloadCreator, metaCreator)                    | Calling createAction with a type will return an action creator for dispatching actions. type must implement toString and is the only required parameter for createAction.payloadCreator must be a function, undefined, or null. If payloadCreator is undefined or null, the identity function is used. metaCreator is an optional function that creates metadata for the payload. It receives the same arguments as the payload creator, but its result becomes the meta field of the resulting action. If metaCreator is undefined or not a function, the meta field is omitted. | Function | no       | android/ios | yes               |
| createActions(actionMap[, options], ...identityActions[, options]) | Returns an object mapping action types to action creators. Returns an object mapping action types to action creators. actionMap is an object which can optionally have a recursive data structure, with action types as keys, and whose values must be either. identityActions is an optional list of positional string arguments that are action type strings; these action types will use the identity payload creator.                                                                                                                                                         | Function | no       | android/ios | yes               |
| handleAction(type, reducer\|reducerMap, defaultState)              | Wraps a reducer so that it only handles Flux Standard Actions of a certain type. If a reducer function is passed, it is used to handle both normal actions and failed actions.You can use this form if you know a certain type of action will never fail, like the increment example above. if the reducer argument (reducer) is undefined, then the identity function is used. The third parameter defaultState is required, and is used when undefined is passed to the reducer.                                                                                                | Function | no       | android/ios | yes               |
| handleActions(reducerMap, defaultState[, options])                 | Creates multiple reducers using handleAction() and combines them into a single reducer that handles multiple actions. Accepts a map where the keys are passed as the first parameter to handleAction() (the action type), and the values are passed as the second parameter (either a reducer or reducer map). The map must not be empty.                                                                                                                                                                                                                                         | Function | no       | android/ios | yes               |
| combineActions(...types)                                           | Combine any number of action types or action creators. types is a list of positional arguments which can be action type strings, symbols, or action creators.                                                                                                                                                                                                                                                                                                                                                                                                                     | Function | no       | android/ios | yes               |

## 遗留问题

当前推荐使用2.6.5版本，若更新到3.0.0版本原库会有如下已知问题：

- [ ] 编译错误：this package itself specifies a `main` module field that could not be resolved[issue#1967](https://github.com/pmndrs/zustand/discussions/1967)
- [ ] 运行错误：import.meta' is currently unsupported Buffer size 12286 starts with[issue#394](https://github.com/redux-utilities/redux-actions/issues/394)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/redux-utilities/redux-actions/blob/master/LICENSE) ，请自由地享受和参与开源。
