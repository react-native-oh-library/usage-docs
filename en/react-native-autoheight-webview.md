<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-autoheight-webview</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/iou90/react-native-autoheight-webview">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/iou90/react-native-autoheight-webview/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-autoheight-webview)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-autoheight-webview Releases](https://github.com/react-native-oh-library/react-native-autoheight-webview/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-autoheight-webview@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-autoheight-webview@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import AutoHeightWebView from "react-native-autoheight-webview";
import { Dimensions } from 'react-native'


export function WebviewExample() {
  return (
    <AutoHeightWebView
    style={{ width: Dimensions.get('window').width - 15, marginTop: 35,}}
    customScript={`document.body.style.background = 'lightyellow';`}
    customStyle={`
      * {
        font-family: 'Times New Roman';
      }
      p {
        font-size: 16px;
      }
    `}
    source={{ html: `
    <p style="font-weight: 400;font-style: normal;font-size: 21px;line-height: 1.58;letter-spacing: -.003em;">Tags are great for describing the essence of your story in a single word or phrase, but stories are rarely about a single thing. <span style="background-color: transparent !important;background-image: linear-gradient(to bottom, rgba(146, 249, 190, 1), rgba(146, 249, 190, 1));">If I pen a story about moving across the country to start a new job in a car with my husband, two cats, a dog, and a tarantula, I wouldn’t only tag the piece with “moving”. I’d also use the tags “pets”, “marriage”, “career change”, and “travel tips”.</span></p>
     ` }}
    
  />
  
  );
}




```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-webview 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-webview 文档](/zh-cn/react-native-webview.md)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[ @react-native-oh-tpl/react-native-autoheight-webview Releases](https://github.com/react-native-oh-library/react-native-autoheight-webview/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                              | Description                                                                                                                                                                                                                                                                                                  | Type                                                               | Required | Platform | HarmonyOS Support                                                                                                 |
|-----------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------|
| `source`                          | Loads static HTML or a URI<br/> (with optional headers) <br />in the WebView                                                                                                                                                                                                                                 | object                                                             | Yes      | iOS,Android      | partially (Only of: <br />**Load uri :**<br />uri <br />headers <br />**Static HTML :**<br />html <br />baseUrl ) |
| `originWhitelist?`                | List of origin strings<br/> to allow being navigated to.                                                                                                                                                                                                                                                     | string[]                                                           | No       | iOS,Android      | no                                                                                                               |
| `scalesPageToFit?`                | Boolean that controls<br/> whether the web content<br/> is scaled to fit the view<br/> and enables the user<br/> to change the scale.                                                                                                                                                                        | boolean                                                            | No       | Android  | yes                                                                                                               |
| `customScript?`                   | -                                                                                                                                                                                                                                                                                                            | string                                                             | No       | iOS,Android      | yes                                                                                                               |
| `style?`                          | A style object that allow you<br/> to customize the WebView style.                                                                                                                                                                                                                                           | Style                                                              | No       | iOS,Android      | yes                                                                                                               |
| `customStyle?`                    | The custom css content<br/> will be added to the page's <head>.                                                                                                                                                                                                                                              | string                                                             | No       | iOS,Android      | yes                                                                                                               |
| `onSizeUpdated?`                  | Either updated height or width<br/> will trigger onSizeUpdated.                                                                                                                                                                                                                                              | function                                                           | No       | iOS,Android      | yes                                                                                                               |
| `showsHorizontalScrollIndicator?` | Boolean value that <br/>determines whether a <br/>horizontal scroll indicator <br/>is shown in the WebView.                                                                                                                                                                                                  | boolean                                                            | No       | iOS,Android      | yes                                                                                                               |
| `showsVerticalScrollIndicator`    | Boolean value that <br/> determines whether a <br/> vertical scroll indicator<br/>  is shown in the WebView.                                                                                                                                                                                                 | boolean                                                            | No       | iOS,Android      | yes                                                                                                               |
| `files?`                          | Using local or remote files. <br />To add local files:<br/>  Add files to <br/> android/app/src/main/assets/ <br/> (depends on baseUrl) <br/>on android;<br/>  add files to <br/> web/ (depends on baseUrl) on iOS;<br/>  add files to <br/>harmony/entry/src/<br/> main/resoureces/rawfile<br/> on harmony. | arrayOf(<br/>{ href: string, <br/>type: string,<br/> rel:string }) | No       | iOS,Android      | yes                                                                                                               |
| `scrollEnabledWithZoomedin?`      | Making the webview scrollable<br /> on iOS when zoomed in even <br />if scrollEnabled is false.                                                                                                                                                                                                              | boolean                                                            | No       | iOS      | yes                                                                                                                |
| `viewportContent?`                | Please note that<br /> 'width=device-width'<br/> with scalesPageToFit<br/>  may cause some layout issues <br/> on Android and harmony, <br/>for these conditions, <br/>using customScript prop<br /> to apply custom viewport meta.                                                                          | string                                                             | No       | iOS,Android      | yes                                                                                                               |

## 遗留问题


- [ ] AutoHeightWebview 的originWhitelist属性依赖webview的originWhitelist属性暂未实现HarmonyOS 化[issue#200](https://github.com/react-native-oh-library/react-native-webview/issues/200)
- [ ] AutoHeightWebview 的source属性依赖webview的source属性只是部分实现HarmonyOS 化[issue#200](https://github.com/react-native-oh-library/react-native-webview/issues/200)
- [ ] AutoHeightWebview依赖的webview 部分属性未实现 HarmonyOS 化[issue#17](https://github.com/react-native-oh-library/react-native-webview/issues/17)
- [x] AutoHeightWebview 的scrollEnabledWithZoomedin属性未实现 HarmonyOS 化[issue#1](https://github.com/react-native-oh-library/react-native-autoheight-webview/issues/1)
- [x] 中文乱码[issue#2](https://github.com/react-native-oh-library/react-native-autoheight-webview/issues/2)

## 其他

## 开源协议

本项目基于 [The ISC License (ISC)](https://github.com/iou90/react-native-autoheight-webview/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->