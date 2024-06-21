<!-- {% raw %} -->
> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-dotenv</code> </h1>
</p>
<p align="center">
 	<a href="https://github.com/goatandsheep/react-native-dotenv">
          <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/goatandsheep/react-native-dotenv/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/goatandsheep/react-native-dotenv)

## 安装与使用

### 安装

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
 npm install -D react-native-dotenv@^3.4.9
```

#### **yarn**

```bash
yarn add -D react-native-dotenv@^3.4.9
```

<!-- tabs:end -->

### 使用

基础配置：

**.babelrc**

```json
{
  "plugins": [["module:react-native-dotenv"]]
}
```

**.env**

```
API_URL=https://api.example.org
API_TOKEN=abc123
```

In **users.js**

```js
import { API_URL, API_TOKEN } from "@env";

fetch(`${API_URL}/users`, {
  headers: {
    Authorization: `Bearer ${API_TOKEN}`,
  },
});
```

### 安全模式

若启用安全模式，则只允许使用在 `.env` 文件中定义的环境变量。这将完全忽略环境中已经定义的所有内容。

`.env` 文件必须存在

```json
{
  "plugins": [
    [
      "module:react-native-dotenv",
      {
        "safe": true
      }
    ]
  ]
}
```

### 允许 undefined

允许导入未定义的变量，导入的值为 undefined。

```json
{
  "plugins": [
    [
      "module:react-native-dotenv",
      {
        "allowUndefined": true
      }
    ]
  ]
}
```

In **users.js**

```js
import { UNDEFINED_VAR } from "@env";

console.log(UNDEFINED_VAR === undefined); // true
```

当设置为 false 时，将抛出错误。

### 覆写 envName

请查看 [官方说明](https://github.com/goatandsheep/react-native-dotenv?tab=readme-ov-file#override-envname)

### 多环境 (Multi-env)

该三方库现在支持读取特定环境的变量。这意味着可以从多个文件中导入环境变量，例如 `.env`, `.env.development`, `.env.Production` 和 `.env.test`。这是基于 [dotenv-flow](https://www.npmjs.com/package/dotenv-flow) 实现的。

若要进行选择，需要为每个环境使用 NODE_ENV 设置脚本

**package.json**

<!-- tabs:start -->

#### **windows**

```json
{
  "scripts": {
    "start:development": "set NODE_ENV=development&& npx react-native start",
    "start:production": "set NODE_ENV=production&& npx react-native start"
  }
}
```

#### **iOS & Linux**

```json
{
  "scripts": {
    "start:development": "NODE_ENV=development npx react-native start",
    "start:production": "NODE_ENV=production npx react-native start"
  }
}
```

<!-- tabs:end -->

### TypeScript

对于使用 TypeScript 的库，需要手动指定类型：

- 在你的工程创建 `types` 文件夹
- 进入文件夹，创建 `*.d.tsx` 文件，比如 `env.d.ts`
- 在此文件中，以下面的形式声明一个 module

```ts
declare module "@env" {
  export const API_BASE: string;
}
```

把所有你的 `.env` 的变量加入这个 module 内。

最后，在 `tsconfig.json` 文件中添加 `typeRoots` 字段

```json
{
...
  "compilerOptions": {
    ...
      "typeRoots": ["./src/types"],
    ...
  }
...
}
```

### 缓存

> [!WARNING] 请务必查看这一小节

已知问题：在 Android 和 HarmonyOS 里，均会出现因为缓存导致的环境变量无法更新的问题，所以需要添加一些配置，让每次打包的时候清空缓存，以达到能读取新的环境变量的效果。

首先确保以下依赖已经配置到你的 `package.json` 内

```json
"resolutions": {
  "@babel/core": "^7.20.2",
  "babel-loader": "^8.3.0"
}
```

在 babel config 中添加 `api.cache(false)`，例如

```js
// .babel.config.js
module.exports = function (api) {
  api.cache(false);
  return {
    presets: ["module:metro-react-native-babel-preset"],
    plugins: [["module:react-native-dotenv"]],
  };
};
```

在 `metro.config.js` 中添加 `resetCache: true`，例如

```js
// metro.config.js
module.exports = {
  resetCache:true,
  ...
}
```

更多清除缓存的方法请参考 [react-naitve-dotenv 官方指引](https://github.com/goatandsheep/react-native-dotenv)

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/goatandsheep/react-native-dotenv/blob/main/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->