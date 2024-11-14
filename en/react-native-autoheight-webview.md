> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-autoheight-webview)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-autoheight-webview Releases](https://github.com/react-native-oh-library/react-native-autoheight-webview/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-autoheight-webview
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-autoheight-webview
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-webview. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 
If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-webview](/en/react-native-webview.md) to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [ @react-native-oh-tpl/react-native-autoheight-webview Releases](https://github.com/react-native-oh-library/react-native-autoheight-webview/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

- [ ] AutoHeightWebview 的originWhitelist属性依赖webview的originWhitelist属性暂未实现HarmonyOS 化[issue#200](https://github.com/react-native-oh-library/react-native-webview/issues/200)
- [ ] AutoHeightWebview 的source属性依赖webview的source属性只是部分实现HarmonyOS 化[issue#200](https://github.com/react-native-oh-library/react-native-webview/issues/200)
- [ ] AutoHeightWebview依赖的webview 部分属性未实现 HarmonyOS 化[issue#17](https://github.com/react-native-oh-library/react-native-webview/issues/17)
- [x] AutoHeightWebview 的scrollEnabledWithZoomedin属性未实现 HarmonyOS 化[issue#1](https://github.com/react-native-oh-library/react-native-autoheight-webview/issues/1)
- [x] 中文乱码[issue#2](https://github.com/react-native-oh-library/react-native-autoheight-webview/issues/2)

## Others

## License

This project is licensed under [The ISC License (ISC)](https://github.com/iou90/react-native-autoheight-webview/blob/master/LICENSE).
