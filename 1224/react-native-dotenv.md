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
1.配置babel.config.js文件如下：
	module.exports=function(api){
		api.cache(false);
		return{
			presets:['module:metro-react-native-babel-preset'],
			plugins:[
				["module:react-native-dotenv"]
			]
		}
	}

2.在根目录下新建.env文件，并配置如下代码：
	API_URL=env.url
	API_TOKEN=env.token
  在根目录下新建.env.dev文件，配置如下代码：
	API_URL=dev.url
	API_TOKEN=dev.token
  在根目录下新建.env.test文件，配置如下代码：
	API_URL=test.url
	API_TOKEN=test.token

3.根目录下新建types文件夹，在此目录下新建env.d.tsx文件，并配置如下代码：
	daclare module '@env'{
		export const API_URL:string,API_TOKEN:string
	}

4.将第3步的文件添加到tsconfig.json文件中，配置如下：
	{
		"extends":"@tsconfig/react-native/tsconfig.json",
		"compilerOptions":{
			"typeRoots":["./types"]
		}
	}

5.页面中引入，代码配置如下：
	import React from 'react';
	import {View,Text} from 'react-native';
	import {API_URL,API_TOKEN} from "@env"

	function DotenvTest({}):JSX.Element{
		return (
			<View>
				<Text>DotenvTest</Text>
				<Text>API_URL:{API_URL}</Text>
				<Text>API_TOKEN:{API_TOKEN}</Text>
			</View>
		)
	}
	export default DotenvTest

6.在工程文件的package.json文件的"scrips"中配置如下代码：
	"start_harmony:dev":"set NODE_ENV=dev&& npm run dev"
	"start_harmony:test":"set NODE_ENV=test&& npm run dev"

7.在metro.config.js文件中修改为以下代码：
	const config={
		resetCache:true,
		transformer:{
			getTransformOptions:async()=>({
				transform:{
					experimentalImportSupport:false,
					inlineRequires:true
				}
			})
		}
	}

8.单环境：执行npm run dev指令，生成bundle后运行鸿蒙侧，启动页面，观察页面读取到.env文件中的变量值
  多环境：分别执行npm run start_harmony:dev 或者npm run start_harmony:test命令，生成bundle后运行鸿蒙侧，启动页面，观察页面读取到.env.dev和.env.test文件中的变量值


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
