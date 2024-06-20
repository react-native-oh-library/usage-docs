> 模板版本：v0.1.3

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

> [!tip] [Github 地址](https://github.com/reduxjs/redux-thunk)

## 安装与使用

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

下面的代码展示了这个库的基本使用场景：

1.在Redux store中引入redux-thunk中间件

<!-- {% raw %} -->
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
<!-- {% endraw %} -->

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

## 约束与限制

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
> 详情见 [redux-thunk 源库地址](https://github.com/reduxjs/redux-thunk)

| Name                | Description                              | Type            | Required | Platform | HarmonyOS Support |
| ------------------- | ---------------------------------------- | --------------- | -------- | -------- | ----------------- |
| thunk               | Thunk中间件实例                          | ThunkMiddleware | yes      | All      | yes               |
| ThunkAction         | ThunkAction类型继承自Redux Action        | Action          | no       | All      | yes               |
| ThunkActionDispatch | 接受一个thunk action创建器并返回一个函数 | Any             | no       | All      | yes               |
| ThunkDispatch       | Thunk重载的dispatch接口                  | Interface       | no       | All      | yes               |
| ThunkMiddleware     | TThunk中间件类型                         | Middleware      | no       | All      | yes               |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                             | Description         | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------------------------ | ------------------- | -------- | -------- | -------- | ----------------- |
| withExtraArgument(extraArgument?: ExtraThunkArg) | 创建Thunk中间件方法 | function | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/reduxjs/redux-thunk?tab=MIT-1-ov-file)，请自由地享受和参与开源。
