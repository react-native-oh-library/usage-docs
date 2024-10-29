> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/goatandsheep/react-native-dotenv)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
 npm install -D react-native-dotenv@3.4.9
```

#### **yarn**

```bash
yarn add -D react-native-dotenv@3.4.9
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import {API_URL, API_TOKEN} from '@env';
import {View, Text} from 'react-native';
import {useState, useEffect} from 'react';

export function TestDotenv() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch(`${API_URL}/product/mirrors.html`, {
      headers: {
        Authorization: `Bearer ${API_TOKEN}`,
      },
    })
      .then(res => res.json())
      .then(res => {
        console.log(res);
      });
  }, []);

  return (
    <View>
      <Text style={{color:"red",fontSize:30}}>{API_URL}</Text>
    </View>
  );
}
```

Basic Configuration:

**`.babelrc` or `babel.config.js`**

```json
{
  "plugins": [["module:react-native-dotenv"]]
}
```

**`.babelrc` or `babel.config.js`**

> [!TIP] 如果默认值不适合您项目，这里会列出 Babel 配置的可用选项及其各自的默认值，但如果您使用默认设置，则无需添加它们。

```json
module.exports = function(api) {
  api.cache(false)
  module.exports = {
    plugins: [
      [
        'module:react-native-dotenv',
        {
          envName: 'APP_ENV',
          moduleName: '@env',
          path: '.env',
          blocklist: null, // 黑名单 string[]
          allowlist: null, // 白名单 string[]
          blacklist: null, // DEPRECATED 弃用
          whitelist: null, // DEPRECATED 弃用
          safe: false, // 安全模式
          allowUndefined: true, // 允许变量未定义
          verbose: false, // 
        },
      ],
    ],
  };
}
```

**.env**

```
API_URL=https://api.example.org
API_TOKEN=abc123
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

```json
module.exports = function(api) {
  api.cache(false)
  module.exports = {
    plugins: [
      [
        'module:react-native-dotenv',
        {
          moduleName: '@env',
          // 多环境须修改 path：'.env.development' 或 '.env.Production' 或 '.env.test'
          path: '.env', 
        },
      ],
    ],
  };
}
```

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
- 进入文件夹，创建 `*.d.ts` 文件，比如 `env.d.ts`
- 在此文件中，以下面的形式声明一个 module

```ts
declare module "@env" {
  export const API_BASE: string;
}
```

把所有你的 `.env` 的变量加入这个 module 内。

Finally, add the `typeRoots` field to the `tsconfig.json` file

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

### Cache

> [!WARNING] 请务必查看这一小节

已知问题：在 Android 和 HarmonyOS 里，均会出现因为缓存导致的环境变量无法更新的问题，所以需要添加一些配置，让每次打包的时候清空缓存，以达到能读取新的环境变量的效果。

首先确保以下依赖已经配置到你的 `package.json` 内

```json
"resolutions": {
  "@babel/core": "^7.20.2",
  "babel-loader": "^8.3.0"
}
```

Add `api.cache(false)` to the `babel.config.js` file, for example:

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

Add `resetCache: true` to the `metro.config.js` file, for example:

```js
// metro.config.js
module.exports = {
  resetCache:true,
  ...
}
```

更多清除缓存的方法请参考 [react-naitve-dotenv 官方指引](https://github.com/goatandsheep/react-native-dotenv)

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.1.430; ROM: 3.0.0.26;
2. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71(API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/goatandsheep/react-native-dotenv/blob/main/LICENSE).
