> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>axios</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/axios/axios/blob/v1.x/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/axios/axios)

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

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                               | Description                                          |   Type   | Required | HarmonyOS Support |
| :--------------------------------- | ---------------------------------------------------- | :------: | :------: | :---------------: |
| axios.request(config)              | Alias method for sending a **request**.              | function |    /     |        yes        |
| axios.get(url[, config])           | Alias method for sending a **get** request.          | function |    /     |        yes        |
| axios.delete(url[, config])        | Alias method for sending a **delete** request.       | function |    /     |        yes        |
| axios.head(url[, config])          | Alias method for sending a **head** request.         | function |    /     |        yes        |
| axios.options(url[, config])       | Alias method for sending an **options** request.     | function |    /     |        yes        |
| axios.post(url[, data[, config]])  | Alias method for sending a **post** request.         | function |    /     |        yes        |
| axios.put(url[, data[, config]])   | Alias method for sending a **put** request.          | function |    /     |        yes        |
| axios.patch(url[, data[, config]]) | Alias method for sending a **patch** request.        | function |    /     |        yes        |
| axios#request(config)              | Instance method for sending a **request**.           | function |    /     |        yes        |
| axios#get(url[, config])           | Instance method for sending a **get** request.       | function |    /     |        yes        |
| axios#delete(url[, config])        | Instance method for sending a **delete** request.    | function |    /     |        yes        |
| axios#head(url[, config])          | Instance method for sending a **head** request.      | function |    /     |        yes        |
| axios#options(url[, config])       | Instance method for sending an **options** request.  | function |    /     |        yes        |
| axios#post(url[, data[, config]])  | Instance method for sending a **post** request.      | function |    /     |        yes        |
| axios#put(url[, data[, config]])   | Instance method for sending a **put** request.       | function |    /     |        yes        |
| axios#patch(url[, data[, config]]) | Instance method for sending a **patch** request.     | function |    /     |        yes        |
| url                                | URL requested.                                       | function |    /     |        yes        |
| method                             | Method used to request.                              | function |    /     |        yes        |
| baseURL                            | Base URL added automatically before the URL.         | function |    /     |        yes        |
| headers                            | Custom header requested.                             | function |    /     |        yes        |
| params                             | Parameters to be sent with the request.              | function |    /     |        yes        |
| data                               | Data sent by the request body.                       | function |    /     |        yes        |
| timeout                            | Number of milliseconds in which a request times out. | function |    /     |        yes        |
| proxy                              | Proxy set in the configuration.                      | function |    /     |        yes        |
| Response Schema                    | Response type.                                       | function |    /     |        yes        |
| Config Defaults                    | Default configuration.                               | function |    /     |        yes        |
| requestInterceptors                | Request interceptor.                                 | function |    /     |        yes        |
| responseInterceptors               | Response interceptor.                                | function |    /     |        yes        |
| Handling Errors                    | Error handling.                                      | function |    /     |        yes        |
| AbortController                    | Abort controller.                                    | function |    /     |        yes        |
| CancelToken                        | Cancel token.                                        | function |    /     |        yes        |

## Others

## License

This project is licensed under [MIT License](https://github.com/Kureev/react-native-blur/blob/master/LICENSE).