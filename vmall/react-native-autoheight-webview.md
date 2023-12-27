> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>react-native-autoheight-webview</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-autoheight-webview">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/iou90/react-native-autoheight-webview/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-autoheight-webview)

## 安装与使用

进入到工程目录并输入以下命令：

```bash
yarn add @react-native-oh-tpl/react-native-autoheight-webview
```

或者

```bash
npm install @react-native-oh-tpl/react-native-autoheight-webview
```

下面的代码展示了这个库的基本使用场景：

```js
import AutoHeightWebView from "react-native-autoheight-webview";

<AutoHeightWebView source={{ uri: "https://reactnative.dev/" }} />;
```

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-webview 的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-webview 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/vmall/react-native-webview.md#link)进行引入

## 约束与限制

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[ @react-native-oh-tpl/react-native-autoheight-webview Releases](https://github.com/react-native-oh-library/react-native-autoheight-webview/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                              | Description                                                                                                                                                                                                                                   | Type                                                                                                          | Required | Platform | HarmonyOS Support                                                                                                 |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------------------------------------------------------------------------------------------------------- |
| `source`                          | Loads static HTML or a URI (with optional headers) in the WebView                                                                                                                                                                             | object                                                                                                        | yes      | All      | partially (Only of: <br />**Load uri :**<br />uri <br />headers <br />**Static HTML :**<br />html <br />baseUrl ) |
| `originWhitelist?`                | List of origin strings to allow being navigated to.                                                                                                                                                                                           | string[]                                                                                                      | No       | All      | yes                                                                                                               |
| `scalesPageToFit?`                | Boolean that controls whether the web content is scaled to fit the view and enables the user to change the scale.                                                                                                                             | boolean                                                                                                       | No       | android  | yes                                                                                                               |
| `customScript?`                   | -                                                                                                                                                                                                                                             | string                                                                                                        | No       | All      | yes                                                                                                               |
| `style?`                          | A style object that allow you to customize the WebView style.                                                                                                                                                                                 | Style                                                                                                         | No       | All      | yes                                                                                                               |
| `customStyle?`                    | The custom css content will be added to the page's <head>.                                                                                                                                                                                    | string                                                                                                        | No       | All      | yes                                                                                                               |
| `onSizeUpdated?`                  | Either updated height or width will trigger onSizeUpdated.                                                                                                                                                                                    | function                                                                                                      | No       | All      | yes                                                                                                               |
| `showsHorizontalScrollIndicator?` | Boolean value that determines whether a horizontal scroll indicator is shown in the WebView.                                                                                                                                                  | boolean                                                                                                       | No       | All      | yes                                                                                                               |
| `showsVerticalScrollIndicator`    | Boolean value that determines whether a vertical scroll indicator is shown in the WebView.                                                                                                                                                    | boolean                                                                                                       | No       | All      | yes                                                                                                               |
| `files?`                          | Using local or remote files. To add local files: Add files to android/app/src/main/assets/ (depends on baseUrl) on android; add files to web/ (depends on baseUrl) on iOS; add files to harmony/entry/src/main/resoureces/rawfile on harmony. | PropTypes.arrayOf(PropTypes.shape({ href: PropTypes.string, type: PropTypes.string, rel: PropTypes.string })) | No       | All      | yes                                                                                                               |
| `scrollEnabledWithZoomedin?`      | Making the webview scrollable on iOS when zoomed in even if scrollEnabled is false.                                                                                                                                                           | boolean                                                                                                       | No       | ios      | no                                                                                                                |
| `viewportContent?`                | Please note that 'width=device-width' with scalesPageToFit may cause some layout issues on Android and harmony, for these conditions, using customScript prop to apply custom viewport meta.                                                  | string                                                                                                        | No       | All      | yes                                                                                                               |

## 遗留问题

- [ ] autoheight-webview 部分属性未实现鸿蒙化[issue#1](https://github.com/react-native-oh-library/react-native-autoheight-webview/issues/1)
- [ ] 中文乱码[issue#2](https://github.com/react-native-oh-library/react-native-autoheight-webview/issues/2)

## 其他

## 开源协议

本项目基于 [The ISC License (ISC)](https://github.com/iou90/react-native-autoheight-webview/blob/master/LICENSE) ，请自由地享受和参与开源。
