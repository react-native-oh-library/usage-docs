> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>redux-thunk</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/reduxjs/redux-thunk?tab=readme-ov-file">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/reduxjs/redux-thunk?tab=MIT-1-ov-file">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [GitHub address](https://github.com/reduxjs/redux-thunk)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install redux-thunk@3.1.0
```

#### **yarn**

```bash
yarn add redux-thunk@3.1.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository：

1.在Redux store中引入redux-thunk中间件

```js
import React from "react";
import { Provider } from "react-redux";
import reducers from "./reducers";
import { thunk } from "redux-thunk";
import { legacy_createStore as createStore, applyMiddleware } from "redux";
import App from "./components/App";

const store = createStore(reducers, applyMiddleware(thunk));

export const TodosExample = () => {
  return (
    <Provider store={store}>
      <App />
    </Provider>
  );
};
```

2.编写一个异步操作的action creator

```
//使用定时器
export const addTodoasync=(text) =>{
    return dispatch => {
      setTimeout(() => {
        dispatch(addTodo(text))
      }, 3000)
    }
  }

  //发起网路请求
export const fetchUser = () => {
  return (dispatch) => {
    dispatch({ type: 'FETCH_USER_REQUEST' });
    fetch('https://jsonplaceholder.typicode.com/users/1')
      .then((response) => response.json())
      .then((user) => {
        dispatch({ type: 'FETCH_USER_SUCCESS', payload: user });
      }).catch((error) => {
        dispatch({ type: 'FETCH_USER_FAILURE', payload: error.message });
      });
  };
  ...
```

3.在组件中dispatch这个action

```
...
let AddTodo = ({ dispatch }) => {
    let input;
    return (
        <View style={styles.container}>
 ...
			<View style={styles.inputContainer}>
                <TextInput style={styles.input}
                    onChangeText={text => {
                        input = text
                    }}
                />
            </View>
            <TouchableOpacity style={styles.btn}
                onPress={() => {
                    dispatch(addTodoasync(input))
                }}
            >
                <Text style={styles.search}>异步添加</Text>
            </TouchableOpacity>
        </View>
    )
}
...
AddTodo = connect()(AddTodo);
export default AddTodo
```

## Constraints

## Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

>
> 详情见 [redux-thunk 源库地址](https://github.com/reduxjs/redux-thunk)

| Name                | Description                              | Type            | Required | Platform | HarmonyOS Support |
| ------------------- | ---------------------------------------- | --------------- | -------- | -------- | ----------------- |
| thunk               | Thunk中间件实例                          | ThunkMiddleware | yes      | All      | yes               |

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name                                             | Description         | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------------------------ | ------------------- | -------- | -------- | -------- | ----------------- |
| withExtraArgument(extraArgument?: ExtraThunkArg) | 创建Thunk中间件方法 | function | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/reduxjs/redux-thunk?tab=MIT-1-ov-file).
