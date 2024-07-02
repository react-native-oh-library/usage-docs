<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-file-viewer
</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vinzscam/react-native-file-viewer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vinzscam/react-native-file-viewer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-file-viewer)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-file-viewer Releases](https://github.com/react-native-oh-library/react-native-file-viewer/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-file-viewer@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-file-viewer@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { StyleSheet, ScrollView, Text, TouchableOpacity } from "react-native";
import DocumentPicker from "react-native-document-picker";
import FileViewer from "react-native-file-viewer";

export function FlieViewerExample() {
	const FileViewerTest = async (option?: any) => {
		try {
			// 使用react-native-document-picker来选择本地文件进行打开
			const res: any = await DocumentPicker.pick({
				type: [DocumentPicker.types.allFiles]
			});
			// uri 为本地文件绝对路径
			await FileViewer?.open(res[0].uri, option);
		} catch (e) {
			// error
		}
	};

	const onDismissCb = () => {
		// do sth ...
	};

	return (
		<ScrollView style={{ backgroundColor: "skyblue" }}>
			<TouchableOpacity onPress={() => FileViewerTest()} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar</Text>
			</TouchableOpacity>
			<TouchableOpacity onPress={() => FileViewerTest("show_displayName string")} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar (displayName str)</Text>
			</TouchableOpacity>
			<TouchableOpacity onPress={() => FileViewerTest({ displayName: "show_displayName option" })} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar (displayName opt)</Text>
			</TouchableOpacity>
			<TouchableOpacity onPress={() => FileViewerTest({ showOpenWithDialog: true, onDismiss: onDismissCb })} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar (onDismiss)</Text>
			</TouchableOpacity>
			<TouchableOpacity onPress={() => FileViewerTest({ showOpenWithDialog: true })} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar (showOpenWithDialog)</Text>
			</TouchableOpacity>
			<TouchableOpacity onPress={() => FileViewerTest({ showAppsSuggestions: true })} style={styles.btn}>
				<Text style={styles.btnText}>Toogle Status Bar (showAppsSuggestions)</Text>
			</TouchableOpacity>
		</ScrollView>
	);
}

const styles = StyleSheet.create({
	TextInput: {
		height: 40,
		borderColor: "#ccc",
		borderWidth: 1,
		borderRadius: 4,
		width: "90%"
	},
	btn: {
		borderRadius: 10,
		display: "flex",
		justifyContent: "center",
		alignItems: "center",
		padding: 10,
		margin: 10,
		backgroundColor: "blue"
	},
	btnText: {
		fontWeight: "bold",
		color: "#fff",
		fontSize: 20
	},
	selectBtn: {
		padding: 8,
		margin: 3,
		fontSize: 18,
		borderWidth: 1,
		borderRadius: 8,
		borderColor: "#753c13"
	},
	selectBtnActive: {
		padding: 8,
		margin: 3,
		backgroundColor: "#e2803b",
		fontSize: 18,
		borderRadius: 8,
		borderWidth: 1
	}
});
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-file-viewer": "file:../../node_modules/@react-native-oh-tpl/react-native-file-viewer/harmony/file_viewer.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 在 ArkTs 侧引入 RNFileViewerTurboModule Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { RNFileViewerPackage } from '@react-native-oh-tpl/react-native-file-viewer/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNFileViewerPackage(ctx)
  ];
}
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-file-viewer Releases](https://github.com/react-native-oh-library/react-native-file-viewer/releases)

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### `open(filepath: string, options?: Object): Promise<void>`

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- |
| **filepath** | The absolute path where the file is stored. The file needs to have a valid extension to be successfully detected. Use [react-native-fs constants](https://github.com/itinance/react-native-fs#constants) to determine the absolute path correctly. | string | yes | All | yes |
| **options** (optional) | Some options to customize the behaviour. See below. | Object | no | All | yes |

#### Options

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- |
| **displayName** (optional) | Customize the QuickLook title. | string | no | iOS | yes |
| **onDismiss** (optional) | Callback invoked when the viewer is being dismissed. | function | no | All | partially |
| **showOpenWithDialog** (optional) | If there is more than one app that can open the file, show an _Open With_ dialogue box. | boolean | no | Android | yes |
| **showAppsSuggestions** (optional) | If there is not an installed app that can open the file, open the Play Store with suggested apps. | boolean | no | Android | partially |

## 遗留问题

- [ ] HarmonyOS端暂不支持关闭预览窗口的回调函数调用: [issue#1](https://github.com/react-native-oh-library/react-native-file-viewer/issues/1)
- [ ] HarmonyOS端无法直接跳转到应用市场的推荐应用页，目前只能跳转到应用市场首页: [issue#1](https://github.com/react-native-oh-library/react-native-file-viewer/issues/2)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/vinzscam/react-native-file-viewer/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->
