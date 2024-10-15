<!-- {% raw %} -->
> Template version: v0.1.3

<p align="center">
  <h1 align="center"> <code>redux-logger</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/LogRocket/redux-logger">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/TehShrike/deepmerge/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!tip] [GitHub address](https://github.com/LogRocket/redux-logger)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install redux-logger@^3.0.6
```

#### **yarn**

```bash
yarn add redux-logger@^3.0.6
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository：

Scene one：

```js
import { applyMiddleware, createStore } from "redux";
// Logger with default options
import logger from "redux-logger";
const store = createStore(reducer, applyMiddleware(logger));
```

Scene two：

```js
import { applyMiddleware, createStore } from "redux";
import { createLogger } from "redux-logger";

const logger = createLogger({
  // ...options
});

const store = createStore(reducer, applyMiddleware(logger));
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name         | Description    | Type     | Required | Platform    | HarmonyOS Support |
| ------------ | -------------- | -------- | -------- | ----------- | ----------------- |
| logger       | default logger | Function | no       | ios/android | yes               |
| createLogger | options logger | Function | no       | ios/android | yes               |

## Known Issuess

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/LogRocket/redux-logger/blob/master/LICENSE).

<!-- {% endraw %} -->