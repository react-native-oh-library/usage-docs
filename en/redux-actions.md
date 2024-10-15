<!-- {% raw %} -->
> Template version: v0.1.3

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

> [!tip] [GitHub address](https://github.com/redux-utilities/redux-actions)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install redux-actions@2.6.5

// The TypeScript project needs to download the type declaration for the corresponding package
npm i @types/redux-actions -D
```

#### **yarn**

```bash
yarn add redux-actions@2.6.5

// The TypeScript project needs to download the type declaration for the corresponding package
yarn add @types/redux-actions -D
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository：

To run the demo, you need to install the following dependencies：

```bash
npm install redux@^5.0.1
npm install react-redux@^9.1.0
```

1.Define the type of state

// LoginType.ts

```ts
export interface IAppUser {
  id: string;
  name: string;
}
```

2.Define actions

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

3.Define reducer

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
  // Default Value cannot be null
  appUser: {},
};

export default createReducers(
  {
    // The payload parameter name is fixed, and the type is derived
    [LOGIN_ACTION.LOGIN]: (state, { payload }: Action<IAppUser>) => {
      console.log("createReducers LOGIN_ACTION.LOGIN", JSON.stringify(payload));
      return {
        ...state,
        appUser: payload,
      };
    },
    // Exception handling
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

4.Define the store

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

5.Mount state and action to components through Connector

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
          title="Modify the Appuser"
          onPress={() => {
            props.onLogin({ id: "1", userName: "123" });
          }}
        />
      </View>
      <View style={styles.viewTextStyle}>
        <Button
          title="Modify the Appuser Name"
          onPress={() => {
            props.onChangeName({ id: "1", userName: "456" });
          }}
        />
      </View>
      <Button title="Clear Appuser" onPress={props.onLogout} />
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

6.use

// index.tsx

```tsx
import { Provider } from "react-redux";
import { StyleSheet, View } from "react-native";
import store from "./loginStore";
import Login from "./loginDemo";

// Export component
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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name                                                               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Type     | Required | Platform    | HarmonyOS Support |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| createAction(type, payloadCreator, metaCreator)                    | Calling createAction with a type will return an action creator for dispatching actions. type must implement toString and is the only required parameter for createAction.payloadCreator must be a function, undefined, or null. If payloadCreator is undefined or null, the identity function is used. metaCreator is an optional function that creates metadata for the payload. It receives the same arguments as the payload creator, but its result becomes the meta field of the resulting action. If metaCreator is undefined or not a function, the meta field is omitted. | Function | no       | android/ios | yes               |
| createActions(actionMap[, options], ...identityActions[, options]) | Returns an object mapping action types to action creators. Returns an object mapping action types to action creators. actionMap is an object which can optionally have a recursive data structure, with action types as keys, and whose values must be either. identityActions is an optional list of positional string arguments that are action type strings; these action types will use the identity payload creator.                                                                                                                                                         | Function | no       | android/ios | yes               |
| handleAction(type, reducer\|reducerMap, defaultState)              | Wraps a reducer so that it only handles Flux Standard Actions of a certain type. If a reducer function is passed, it is used to handle both normal actions and failed actions.You can use this form if you know a certain type of action will never fail, like the increment example above. if the reducer argument (reducer) is undefined, then the identity function is used. The third parameter defaultState is required, and is used when undefined is passed to the reducer.                                                                                                | Function | no       | android/ios | yes               |
| handleActions(reducerMap, defaultState[, options])                 | Creates multiple reducers using handleAction() and combines them into a single reducer that handles multiple actions. Accepts a map where the keys are passed as the first parameter to handleAction() (the action type), and the values are passed as the second parameter (either a reducer or reducer map). The map must not be empty.                                                                                                                                                                                                                                         | Function | no       | android/ios | yes               |
| combineActions(...types)                                           | Combine any number of action types or action creators. types is a list of positional arguments which can be action type strings, symbols, or action creators.                                                                                                                                                                                                                                                                                                                                                                                                                     | Function | no       | android/ios | yes               |

## Known Issues

It is currently recommended to use version 2.6.5. If it is updated to version 3.0.0, the original library will have the following known problems：

- [ ] Compile error：this package itself specifies a `main` module field that could not be resolved[issue#1967](https://github.com/pmndrs/zustand/discussions/1967)
- [ ] Run an error：import.meta' is currently unsupported Buffer size 12286 starts with[issue#394](https://github.com/redux-utilities/redux-actions/issues/394)

## Others

## License


This project is licensed under [The MIT License (MIT)](https://github.com/redux-utilities/redux-actions/blob/master/LICENSE).

<!-- {% endraw %} -->