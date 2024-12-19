> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/LogRocket/redux-logger)

## 安装与使用

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

下面的代码展示了这个库的基本使用场景：

场景一：

```js
import { applyMiddleware, createStore } from "redux";
// Logger with default options
import logger from "redux-logger";
const store = createStore(reducer, applyMiddleware(logger));
```

场景二：

```js
import { applyMiddleware, createStore } from "redux";
import { createLogger } from "redux-logger";

const logger = createLogger({
  // ...options
});

const store = createStore(reducer, applyMiddleware(logger));
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name         | Description    | Type     | Required | Platform    | HarmonyOS Support |
| ------------ | -------------- | -------- | -------- | ----------- | ----------------- |
| logger       | default logger | Function | no       | ios/android | yes               |
| createLogger | options logger | Function | no       | ios/android | yes               |

## 遗留问题s

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/LogRocket/redux-logger/blob/master/LICENSE) ，请自由地享受和参与开源。
