<!-- {% raw %} -->
模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-spinkit</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/maxs15/react-native-spinkit">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/maxs15/react-native-spinkit/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-spinkit)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-spinkit Releases](https://github.com/react-native-oh-library/react-native-spinkit/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-spinkit@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-spinkit@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import Spinkit from 'react-native-spinkit';

const SpinKitDemo: React.FC = (): JSX.Element => {
    return (
    	<Spinkit 
        	type='9CubeGrid' 
        	color='#e74032' 
        	size={60} 
			style={{ backgroundColor: '#fcc424' }} 
            isVisible={true} 
		/>
    )
};

export default SpinKit;
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

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
    "@react-native-oh-tpl/react-native-spinkit": "file:../../node_modules/@react-native-oh-tpl/react-native-spinkit/harmony/spinKit.har"
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

### 在 ArkTs 侧引入 SpinKitView 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import { SpinKitView } from "@react-native-oh-tpl/react-native-spinkit"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
...
+ if (ctx.componentName === SpinKitView.NAME) {
+   SpinKitView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+   })
+ }
 ...
}
```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ SpinKitView.NAME
  ];
```
### 在 ArkTs 侧引入 xxx Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { SpinKitPackage } from '@react-native-oh-tpl/react-native-spinkit/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SpinKitPackage(ctx)
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

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。


请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-spinkit Releases](https://github.com/react-native-oh-library/react-native-spinkit/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**SpinKit**：加载动画渲染组件，接收所有 [View](https://reactnative.dev/docs/view#props) 的props。

| props  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| type                  | Types of Load Animations                                    | string  | No       | All      | Yes               |
| type: Plane           | One Direction Flip Loading Animation                        | string  | No       | All      | Yes               |
| type: CircleFlip      | A circle flips to load animation                            | string  | No       | All      | Yes               |
| type: Bounce          | A circular nested loading animation | string | No | All | Yes |
| type: Wave | Five-bar group loading animation | string | No | All | Yes |
| type: WanderingCubes | Two squares skip loading animation | string | No | All | Yes |
| type: Pulse | A circular diffusion loading animation | string | No | All | Yes |
| type: ChansingDots | Two Circles Bounce Loading Animation | string | No | All | Yes |
| type: ThreeBounce | Three circles display the loading animation in sequence. | string | No | All | Yes |
| type: Circle | Multiple circular circular motion loading animation | string | No | All | Yes |
| type: 9CubeGrid | The nine squares display the loading animation in sequence | string | No | All | Yes |
| type: WordPress | Round wheel inline hollow circle rotating Loading animation | string | No | IOS | Yes |
| type: FadingCircle | Multiple square circular motion loading animation | string | No | All | Yes |
| type: FadingCircleAlt | Multiple circular circular motion loading animation | string | No | All | Yes |
| type: Arc | Rotating ring with notch loading animation | string | No | IOS | Yes |
| type: ArcAlt | Circular progress bar style loading animation | string | No | IOS | Yes |
| isVisible | Visibility of the spinner | boolean | No | All | Yes |
| color | Color of the spinner | string | No | All | Yes |
| size | Visibility of the spinner | number | No | All | Yes |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/maxs15/react-native-spinkit/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->