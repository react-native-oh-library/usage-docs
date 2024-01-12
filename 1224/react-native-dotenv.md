> 模板版本：v0.1.2

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

>[!tip] [Github 地址](https://github.com/goatandsheep/react-native-dotenv)


## 安装与使用

进入到工程目录并输入以下命令：

#### **yarn**

```bash
yarn add -D react-native-dotenv@^3.4.9
```
<!-- tabs:start -->

#### **npm**

```bash
 npm install -D react-native-dotenv@^3.4.9
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
.babel.config.js：
Basic setup:
module.exports=function(api){
	api.cache(false);      //解决缓存导致无法更新变量读取问题
	return{
		presets:['module:metro-react-native-babel-preset'],
		plugins:[
			["module:react-native-dotenv"]
		]
	}
}

If the defaults do not cut it for your project, this outlines the available options for your Babel configuration and their respective default values, but you do not need to add them if you are using the default settings.

{
  "plugins": [
    ["module:react-native-dotenv", {
      "envName": "MY_ENV",
      "moduleName": "@env",
      "path": ".env",
    }]
  ]
}
.env：

API_URL=https://api.example.org
API_TOKEN=abc123

In users.js：

import {API_URL, API_TOKEN} from "@env"

fetch(`${API_URL}/users`, {
  headers: {
    'Authorization': `Bearer ${API_TOKEN}`
  }
})

Multi-env

// package.json
{
  "scripts": {
   	"start_harmony:dev":"set NODE_ENV=dev&& npm run start",
	"start_harmony:test":"set NODE_ENV=test&& npm run start"
  }
}
Or
{
  "scripts": {
   	"start_harmony:dev":"set MY_ENV=dev&& npm run start",
	"start_harmony:test":"set MY_ENV=test&& npm run start"
  }
}

For the library to work with TypeScript, you must manually specify the types for the module.

Create a types folder in your project
Inside that folder, create a *.d.tsxfile, say, env.d.tsx
in that file, declare a module as the following format:

declare module '@env' {
  export const API_URL: string,API_TOKEN:string;
}
Add all of your .env variables inside this module.

Finally, add this folder into the typeRoots field in your tsconfig.json file:
{
...
  "compilerOptions": {
    ...
      "typeRoots": ["./src/types"],
    ...  
  }
...
}


Cacheing

When using with babel-loader with caching enabled you will run into issues where environment changes won’t be picked up. This is due to the fact that babel-loader computes a cacheIdentifier that does not take your .env file(s) into account. The good news is that a recent update has fixed this problem as long as you're using a new version of Babel. Many react native libraries have not updated their Babel version yet so to force the version, add in your package.json:

"resolutions": {
  "@babel/core": "^7.20.2",
  "babel-loader": "^8.3.0"
}
If this does not work, you should set api.cache(false) in your babel config

metro.config.js : resetCache: true  //解决缓存导致无法更新变量读取问题
```

## 约束与限制

### 兼容性

 在下述版本验证通过：

 1. IDE：DevEco Studio 4.1.3.412;SDK：OpenHarmony(api11) 4.1.0.53;测试设备：Mate40 Pro(NOH-AN00);ROM：2.0.0.52(SP22C00E52R1P17log);RNOH：0.72.11

## 使用场景

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [react-native-dotenv源库地址](https://github.com/goatandsheep/react-native-dotenv)

| Name | Description |   Platform | HarmonyOS Support |
| ---- | ---- | ---- |   -------- |
| Single-env | 单环境使用场景  |All |  yes |
| Multi-env | 多环境使用场景 |  All |  yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/goatandsheep/react-native-dotenv/blob/main/LICENSE) ，请自由地享受和参与开源。
