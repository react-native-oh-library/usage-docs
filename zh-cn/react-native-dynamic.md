<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-dynamic</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/codemotionapps/react-native-dynamic">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/codemotionapps/react-native-dynamic/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/codemotionapps/react-native-dynamic)


## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-dynamic@1.0.0
```

#### **yarn**

```bash
yarn add react-native-dynamic@1.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react';
import {
    View,
    Text, 
    Image, 
    Button
} from 'react-native';
import {
    useDarkMode,
	useDarkModeContext,
	DynamicValue,
	DynamicStyleSheet,
	DarkModeProvider,
	useDynamicValue,
	ColorSchemeProvider,
	useColorSchemeContext,
	useDynamicStyleSheet
} from 'react-native-dynamic'
import { Tester, TestSuite, TestCase } from '@rnoh/testerino';

export default function Extra() {
	const mode = useDarkModeContext()
	const styles = useDynamicStyleSheet(dynamicStyleSheet)
	return (
		<View style={styles.container}>
			<Text style={styles.text}>Forced mode: {mode}</Text>
		</View>
	)
}

const dynamicStyleSheet = new DynamicStyleSheet({
	container: {
		borderColor: 'red',
		borderWidth: 1,
		backgroundColor: new DynamicValue('white', 'black'),
		width: 150,
		height: 50,
		justifyContent: 'center',
		alignItems: 'center',
	},
	text: {
		textAlign: 'center',
		color: new DynamicValue('black', 'white'),
	},
})

function Counter() {
	const [counter, setCounter] = useState(0)
	return <Button title={counter.toString()} onPress={() => setCounter((i) => i + 1)} />
}

const backgroundColors = {
	light: 'white',
	dark: 'black',
}

function Components() {
	const styles = useDynamicValue(dynamicStyles)

	return (
		<View style={styles.container}>
			<Text style={styles.text}>My text</Text>
		</View>
	)
}

export function ReactNativeDynamic() {
	const mode = useDarkModeContext()
	const mode2 = useColorSchemeContext()
	const backgroundColor = backgroundColors[mode2]
    const isDarkMode = useDarkMode()
	const styles = useDynamicValue(dynamicStyles)
	return (
		<View style={styles.container}>
			<Tester>
        		<TestSuite name="ShowActionDynamic">
					<TestCase itShould='render mode of dark or light' tags={['C_API']} >
						<DarkModeProvider mode="dark">
							<Extra />
						</DarkModeProvider>
						<DarkModeProvider mode="light">
							<Extra />
						</DarkModeProvider>
					</TestCase>	
        		</TestSuite>
      		</Tester>
			<Image source={{ uri: 'https://github.com/codemotionapps/react-native-dynamic/blob/master/example/meme.png' }} style={styles.meme} />
			<Text style={styles.initialStyle}>Current mode: {mode}</Text>
			<Text style={styles.initialStyle}>Is dark mode: {isDarkMode ? 'black' : 'white'}</Text>

			<ColorSchemeProvider mode="dark">
				<Components />
			</ColorSchemeProvider>

			<ColorSchemeProvider mode="light">
				<Components />
			</ColorSchemeProvider>

			<Components />
		</View>
	)
}

const dynamicStyles = new DynamicStyleSheet({
	container: {
		flex: 1,
		justifyContent: 'center',
		alignItems: 'center',
		backgroundColor: new DynamicValue('#FFFFFF', '#000000'),
	},
	initialStyle: {
		fontSize: 20,
		textAlign: 'center',
		margin: 10,
		color: new DynamicValue('#000000', '#FFFFFF'),
	},
	image: {
		borderWidth: 1,
		borderColor: new DynamicValue('#000000', '#FFFFFF'),
		width: 80,
		height: 80,
	},
	meme: {
		width: '100%',
		height: 200,
		marginBottom: 20,
	},
	text: {
		color: new DynamicValue('black', 'white'),
		textAlign: 'center',
	},
})

```
## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1；IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.24;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `useDarkMode`  | Returns a boolean. true when dark mode is on. |  function | no     | All  | yes      |
| `DynamicValue`  | A helper class meant to be used with DynamicStyleSheet and useDynamicValue. The first argument is the value to be used with a light color scheme, the second argument is the value to be used with a dark color scheme. | function  |  no     | All   | yes      |
| `DynamicStyleSheet`  | Just like StyleSheet but with support for dynamic values.| function  |  no     | All   | yes      |
| `ColorSchemeProvider`  | Allows you to set a specific mode for children.| function  |  no     | All   | yes      |
| `useDynamicValue`  | Returns the appropriate value depending on the theme. You can either pass a DynamicValue, an object containing dark and light properties, or just two arguments.| function  |  no     | All   | yes      |
| `useColorSchemeContext`  | Returns dark or light but reads value from context.| function  |  no     | All   | yes      |


## 遗留问题

## 其他

## 开源协议
本项目基于 [The MIT License (MIT)](https://github.com/codemotionapps/react-native-dynamic/blob/master/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->