> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>nativewind</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/nativewind/nativewind">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/nativewind/nativewind/blob/main/packages/nativewind/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/nativewind)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/nativewind Releases](https://github.com/react-native-oh-library/nativewind/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/nativewind
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/nativewind
```

#### **tailwind.config.js**

```bash
npx tailwindcss init
```

#### **在你的 tailwind.config.js 文件中添加所有组件文件的路径。**

```diff
module.exports = {
- content: [],
+ content: ["./App.{js,jsx,ts,tsx}", "./screens/**/*.{js,jsx,ts,tsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

#### **修改你的 babel.config.js。**

```diff
module.exports = {
- plugins: [],
+ plugins: ["@react-native-oh-tpl/nativewind/babel"],
};
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import React from 'react';
import { Text, View, ScrollView } from 'react-native';
import { styled } from 'nativewind';

const StyledView = styled(View)
const StyledText = styled(Text)
const NativewindDemo = () => {
    return (
        <StyledView className="flex-1 items-center justify-center">
            <StyledText className="font-bold">
                Hello,World.
            </StyledText>
        </StyledView>
    )
}

export default NativewindDemo
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/nativewind Releases](https://github.com/react-native-oh-library/nativewind/releases)

## API
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                 | Description                                                  | Type                                                         | Required | Platform | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| styled()             | can be used similar to Styled Components,and provide base styling. | (ComponentName:JSX.Element,StyleName?:String) => JSX.Element | no       | All      | yes               |
| StyledComponent      | StyledComponent is the component version of styled accepts your component as prop. | component                                                    | no       | All      | yes               |
| useColorScheme()     | provides access to the devices color scheme.                 | () =>{colorScheme,setColorScheme}                            | no       | All      | yes               |
| NativeWindStyleSheet | A StyleSheet is an abstraction similar to CSS StyleSheets and React Native's StyleSheet | component                                                    | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/nativewind/nativewind/blob/main/packages/nativewind/LICENSE) ，请自由地享受和参与开源。