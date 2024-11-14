> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-content-loader</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/danilowoz/react-content-loader">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/danilowoz/react-content-loader/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-content-loader)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-content-loader Releases](https://github.com/react-native-oh-library/react-content-loader/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-content-loader
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-content-loader
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import ContentLoader, { Facebook, Code, List, BulletList, Instagram, Rect, Circle } from 'react-content-loader/native'
import { View, ScrollView } from "react-native"

export function AppExample() {
    return <View style={{ flex: 1, backgroundColor: 'white' }}>
        <ScrollView >
            <ContentLoader
                width={'100%'}
                height={80}
                animate={false}
                viewBox="0 0 380 70"
            >
                <Circle cx="30" cy="30" r="30" />
                <Rect x="80" y="17" rx="4" ry="4" width="300" height="13" />
                <Rect x="80" y="40" rx="3" ry="3" width="250" height="10" />
            </ContentLoader>
            <Facebook></Facebook>
            <Code></Code>
            <List></List>
            <BulletList></BulletList>
            <Instagram></Instagram>
        </ScrollView>
    </View>
}

```
## Link

本库依赖@react-native-oh-tpl/react-native-svg，如已在鸿蒙工程中引入过该库，则无需再次引入。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档](/zh-cn/react-native-svg-capi.md)进行引入


## 约束与限制

### 兼容性


要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-content-loader Releases](https://github.com/react-native-oh-library/react-content-loader/releases)


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Options

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| animate  | Opt-out of animations with false         | boolean  | no | all      | yes |
| speed  | Animation speed in seconds         | number  | no | all      | yes |
| rtl  | Content right-to-left         | boolean  | no | all      | yes |
| backgroundColor  | Used as background of animation         | string  | no | all      | yes |
| viewBox  | Use viewBox props to set a custom viewBox value,for more information about how to use it,read the article [How to Scale SVG](https://css-tricks.com/scale-svg/)         | string  | no | all      | yes |
| foregroundColor  | Used as the foreground of animation         | string  | no | all      | yes |
| interval  |  Animation interval in seconds         | number  | no | all      | yes |
| beforeMask  | Define custom shapes before content         | JSX.Element  | no | all      | partially |
| uniqueKey  | Use the same value of prop key, that will solve inconsistency on the SSR         | string  | no | React DOM only      | no |
| title  |  It's used to describe what element it is. Use '' (empty string) to remove.    | string  | no | React DOM only      | no |
| baseUrl  | Required if you're using `<base url="/" />` document `<head/>`. This prop is common used as: `<ContentLoader baseUrl={window.location.pathname} />` which will fill the SVG attribute with the relative path. Related [#93](https://github.com/danilowoz/react-content-loader/issues/93). | string  | no | React DOM only      | no |
| backgroundOpacity  |  Background opacity (0 = transparent, 1 = opaque)used to solve an issue in [Safari](#safari--ios)     | number  | no | React DOM only      | no |
| foregroundOpacity  |  Animation opacity (0 = transparent, 1 = opaque)used to solve an issue in [Safari](#safari--ios)     | number  | no | React DOM only      | no |
| style  |  css style     | React.CSSProperties  | no | React DOM only      | no |


## 遗留问题
- [ ]  beforeMask属性设置非svg暴露出来的组件时无效: [issue#256](https://github.com/react-native-oh-library/react-native-harmony-svg/issues/256) 
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/danilowoz/react-content-loader/blob/master/LICENSE) ，请自由地享受和参与开源。