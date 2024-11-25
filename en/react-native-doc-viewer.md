> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-doc-viewer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/philipphecht/react-native-doc-viewer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/philipphecht/react-native-doc-viewer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-doc-viewer)

## 安装与使用

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-doc-viewer Releases](https://github.com/react-native-oh-library/react-native-doc-viewer/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-doc-viewer
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-doc-viewer
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  Platform,
  Button,
  Alert,
  ActivityIndicator,
  NativeAppEventEmitter,
  DeviceEventEmitter,
  NativeModules,
  NativeEventEmitter,
  TouchableHighlight
} from 'react-native';
import OpenFile from 'react-native-doc-viewer';
var RNFS = require('react-native-fs');
var SavePath = Platform.OS === 'ios' ? RNFS.MainBundlePath : RNFS.DocumentDirectoryPath;
export default class DocumentViewerExample extends Component {
 constructor(props) {
    super(props);
    this.state = {
      animating: false,
      progress: "",
      donebuttonclicked: false,
    }
    this.eventEmitter = new NativeEventEmitter(NativeModules.RNReactNativeDocViewer);
    this.eventEmitter.addListener('DoneButtonEvent', (data) => {
      /*
      *Done Button Clicked
      * return true
      */
      console.log(data.close);
      this.setState({donebuttonclicked: data.close});
    })
    this.didPressToObjcButton = this.didPressToObjcButton.bind(this);
  }

  componentDidMount(){
    // download progress
    this.eventEmitter.addListener(
      'RNDownloaderProgress',
      (Event) => {
        console.log("Progress - Download "+Event.progress  + " %")
        this.setState({progress: Event.progress + " %"});
      }

    );
  }

  componentWillUnmount (){
    this.eventEmitter.removeListener();
  }
  /*
  * Handle WWW File Method
  * fileType Default == "" you can use it, to set the File Extension (pdf,doc,xls,ppt etc) when in the Url the File Extension is missing.
  */
  handlePress = () => {
    this.setState({animating: true});
    if(Platform.OS === 'ios'){
      OpenFile.openDoc([{
        url:"https://calibre-ebook.com/downloads/demos/demo.docx",
        fileNameOptional:"test filename"
      }], (error, url) => {
         if (error) {
          this.setState({animating: false});
         } else {
          this.setState({animating: false});
           console.log(url)
         }
       })
    }else{
      this.setState({animating: true});
      OpenFile.openDoc([{
        url:"https://www.huf-haus.com/fileadmin/Bilder/Header/ART_3/Header_HUF_Haus_ART_3___1_.jpg", // Local "file://" + filepath
        fileName:"sample",
        cache:false,
        fileType:"jpg"
      }], (error, url) => {
         if (error) {
          this.setState({animating: false});
           console.error(error);
         } else {
          this.setState({animating: false});
           console.log(url)
         }
       })
    }

  }


  /*
  * Handle Local File Method
  * fileType Default == "" you can use it, to set the File Extension (pdf,doc,xls,ppt etc) when in the Url the File Extension is missing.
  */
  handlePressLocal = () => {
    this.setState({animating: true});
    if(Platform.OS === 'ios'){
        OpenFile.openDoc([{url:SavePath+"/react-native-logo.jpg",
        fileNameOptional:"test filename"
      }], (error, url) => {
         if (error) {
          this.setState({animating: false});
         } else {
          this.setState({animating: false});
           console.log(url)
         }
       })
    }else{
      OpenFile.openDoc([{url:SavePath+"/demo.jpg",
        fileName:"sample",
        cache:false,
        fileType:"jpg"
      }], (error, url) => {
         if (error) {
          this.setState({animating: false});
         } else {
          this.setState({animating: false});
           console.log(url)
         }
       })

    }
  }

    handlePressLocalXLS = () => {
      this.setState({animating: true});
      if(Platform.OS === 'ios'){
          OpenFile.openDoc([{url:SavePath+"/SampleXLSFile_19kb.xls",
          fileNameOptional:"Sample XLS 94-2003"
        }], (error, url) => {
           if (error) {
            this.setState({animating: false});
           } else {
            this.setState({animating: false});
             console.log(url)
           }
         })
      }else{
        OpenFile.openDoc([{url:SavePath+"/demo.jpg",
          fileName:"sample",
          cache:false,
          fileType:"jpg"
        }], (error, url) => {
           if (error) {
            this.setState({animating: false});
           } else {
            this.setState({animating: false});
             console.log(url)
           }
         })

      }
    }


  /*
  * Binary in URL
  * Binary String in Url
  * fileType Default == "" you can use it, to set the File Extension (pdf,doc,xls,ppt etc) when in the Url you dont have an File Extensions
  */
  handlePressBinaryinUrl = () => {
    this.setState({animating: true});
    if(Platform.OS === 'ios'){
      OpenFile.openDocBinaryinUrl([{
        url:"https://storage.googleapis.com/need-sure/example",
        fileName:"sample",
        fileType:"xml"
      }], (error, url) => {
          if (error) {
            console.error(error);
            this.setState({animating: false});
          } else {
            console.log(url)
            this.setState({animating: false});
          }
        })
    }else{
      OpenFile.openDocBinaryinUrl([{
        url:"https://storage.googleapis.com/need-sure/example",
        fileName:"sample",
        fileType:"xml",
        cache:true
      }], (error, url) => {
          if (error) {
            console.error(error);
            this.setState({animating: false});
          } else {
            console.log(url)
            this.setState({animating: false});
          }
        })
    }
  }

  /*
  * Base64String
  * put only the base64 String without data:application/octet-stream;base64
  * fileType Default == "" you can use it, to set the File Extension (pdf,doc,xls,ppt etc) when in the Url you dont have an File Extensions
  */
  handlePressb64 = () => {
    if(Platform.OS === 'ios'){
      OpenFile.openDocb64([{
        base64:"{BASE64String}"
        fileName:"sample",
        fileType:"png"
      }], (error, url) => {
          if (error) {
            console.error(error);
          } else {
            console.log(url)
          }
        })
    }else{
      OpenFile.openDocb64([{
        base64:"{BASE64String}"
        fileName:"sample",
        fileType:"png",
        cache:true
      }], (error, url) => {
          if (error) {
            console.error(error);
          } else {
            console.log(url)
          }
        })
    }

    /*
  * Video File
  */
  handlePressVideo = () => {
    if(Platform.OS === 'ios'){
      OpenFile.playMovie(video, (error, url) => {
                if (error) {
                    console.error(error);
                } else {
                    console.log(url)
                }
            })
    }else{
      Alert.alert("Android coming soon");
    }
  }


  <Button
          onPress={this.handlePress.bind(this)}
          title="Press Me Open Doc Url"
          accessibilityLabel="See a Document"
        />
        <Button
          onPress={this.handlePressBinaryinUrl.bind(this)}
          title="Press Me Open BinaryinUrl"
          accessibilityLabel="See a Document"
        />
         <Button
          onPress={this.handlePressLocal.bind(this)}
          title="Press Me Open Doc Path"
          accessibilityLabel="See a Document"
        />
        <Button
          onPress={this.handlePressLocalXLS.bind(this)}
          title="Press Me Open XLS DOC Path"
          accessibilityLabel="See a Document"
        />
        <Button
          onPress={this.handlePressb64.bind(this)}
          title="Press Me Open Base64 String"
          accessibilityLabel="See a Document"
        />
        <Button
          onPress={()=>this.handlePressVideo("http://www.sample-videos.com/video/mp4/720/big_buck_bunny_720p_1mb.mp4")}
          title="Press Me Open Video"
          accessibilityLabel="See a Document"
        />
}
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-doc-viewer": "file:../../node_modules/@react-native-oh-tpl/react-native-doc-viewer/harmony/doc_viewer.har"
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

### 3.引入 DocViewPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { DocViewPackage } from "@react-native-oh-tpl/react-native-doc-viewer/ts"

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new DocViewPackage(ctx)
  ];
}
```

### 4.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-doc-viewer Releases](https://github.com/react-native-oh-library/react-native-doc-viewer/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                | Type     | Required | Platform | HarmonyOS Support |
| ------------------ | -------------------------- | -------- | -------- | -------- | ----------------- |
| openDoc            | 打开一个在线文档           | function | no       | All      | yes               |
| openDocBinaryinUrl | 打开一个在线文档           | function | no       | All      | yes               |
| openDocb64         | 将 base64 字符串打开为文档 | function | no       | All      | yes               |

## 遗留问题

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/philipphecht/react-native-doc-viewer/blob/master/LICENSE) ，请自由地享受和参与开源。
