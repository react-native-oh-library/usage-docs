> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>axios</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/axios/axios/blob/v1.x/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/axios/axios)

## Installation and Usage

#### **npm**

```bash
npm install axios@1.6.7
```

#### **bower**

```bash
bower install axios@1.6.7
```

#### **yarn**

```bash
yarn add axios@1.6.7
```

Once the package is installed, you can import the library using `import` or `require` approach:

```js
import axios, { isCancel, AxiosError } from "axios";
```

You can also use the default export, since the named export is just a re-export from the Axios factory:

```js
import axios from "axios";

console.log(axios.isCancel("something"));
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import axios from "axios";
//const axios = require('axios'); // legacy way

// Make a request for a user with a given ID
axios
  .get("/user?ID=12345")
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
  .finally(function () {
    // always executed
  });

// Optionally the request above could also be done as
axios
  .get("/user", {
    params: {
      ID: 12345,
    },
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  })
  .finally(function () {
    // always executed
  });

// Want to use async/await? Add the `async` keyword to your outer function/method.
async function getUser() {
  try {
    const response = await axios.get("/user?ID=12345");
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}
```

## Constraints

## Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                               | Description                |   Type   | Required | HarmonyOS Support |
| :--------------------------------- | -------------------------- | :------: | :------: | :---------------: |
| axios.request(config)              | 别名发送request请求        | function |    /     |        yes        |
| axios.get(url[, config])           | 别名发送get请求            | function |    /     |        yes        |
| axios.delete(url[, config])        | 别名发送delete请求         | function |    /     |        yes        |
| axios.head(url[, config])          | 别名发送head请求           | function |    /     |        yes        |
| axios.options(url[, config])       | 别名发送options请求        | function |    /     |        yes        |
| axios.post(url[, data[, config]])  | 别名发送post请求           | function |    /     |        yes        |
| axios.put(url[, data[, config]])   | 别名发送put请求            | function |    /     |        yes        |
| axios.patch(url[, data[, config]]) | 别名发送patch请求          | function |    /     |        yes        |
| axios#request(config)              | 实例发送request请求        | function |    /     |        yes        |
| axios#get(url[, config])           | 实例发送get请求            | function |    /     |        yes        |
| axios#delete(url[, config])        | 实例发送delete请求         | function |    /     |        yes        |
| axios#head(url[, config])          | 实例发送head请求           | function |    /     |        yes        |
| axios#options(url[, config])       | 实例发送options请求        | function |    /     |        yes        |
| axios#post(url[, data[, config]])  | 实例发送post请求           | function |    /     |        yes        |
| axios#put(url[, data[, config]])   | 实例发送put请求            | function |    /     |        yes        |
| axios#patch(url[, data[, config]]) | 实例发送patch请求          | function |    /     |        yes        |
| url                                | 配置中请求的地址           | function |    /     |        yes        |
| method                             | 配置中请求时使用的方法     | function |    /     |        yes        |
| baseURL                            | 配置中自动加在url地址前    | function |    /     |        yes        |
| headers                            | 配置中自定义请求头         | function |    /     |        yes        |
| params                             | 配置中请求一起发送时的参数 | function |    /     |        yes        |
| data                               | 配置中请求体发送的数据     | function |    /     |        yes        |
| timeout                            | 配置中请求超时的毫秒数     | function |    /     |        yes        |
| proxy                              | 配置中设置代理             | function |    /     |        yes        |
| Response Schema                    | 响应类型                   | function |    /     |        yes        |
| Config Defaults                    | 默认配置                   | function |    /     |        yes        |
| requestInterceptors                | 请求拦截器                 | function |    /     |        yes        |
| responseInterceptors               | 响应拦截器                 | function |    /     |        yes        |
| Handling Errors                    | 错误处理                   | function |    /     |        yes        |
| AbortController                    | 中止控制器                 | function |    /     |        yes        |
| CancelToken                        | 取消令牌                   | function |    /     |        yes        |

## Others

## License

This project is licensed under  [The MIT License (MIT)](https://github.com/Kureev/react-native-blur/blob/master/LICENSE), Please enjoy and participate freely in open source.
