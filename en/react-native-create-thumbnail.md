<!-- {% raw %} -->
> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-create-thumbnail</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/souvik-ghosh/react-native-create-thumbnail">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/souvik-ghosh/react-native-create-thumbnail/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-create-thumbnail)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-create-thumbnail Releases](https://github.com/react-native-oh-library/react-native-create-thumbnail/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-create-thumbnail@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-create-thumbnail@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React, {useState } from 'react';
import {  StyleSheet, Text, Button ,ScrollView,View} from 'react-native';
import { createThumbnail } from 'react-native-create-thumbnail';

// 导出组件
export default function CreateThumbnailDemo() {

  const [text, setText] = useState('');

  const CreateThumbnail = async()=> {
    let obj = await createThumbnail({ 
      url:'https://media.w3.org/2010/05/sintel/trailer.mp4',
      timeStamp: 10000
    });
    setText(JSON.stringify(obj))
  }

  return (
    <View style={styles.container}>
      <View style={styles.titleArea}>
        <Text style = {styles.title}>Math</Text>
      </View>
      <View style = {styles.inputArea}>
        <Text style={styles.baseText}>
          {text}
        </Text>
      </View>
      <ScrollView style={styles.scrollView}>
        <View style={ { flexDirection: 'column'}}>
          <View style ={styles.baseArea}>
             <Text style= {{flex:1}}>createThumbnail</Text>
             <Button title='运行' color='#841584' onPress={CreateThumbnail}></Button>
          </View>
    
        </View>
      </ScrollView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: '100%',
    height: '100%',
    flexDirection: 'column',
    alignItems: 'center',
    backgroundColor: '#F1F3F5',
  }, 
  baseText: {
    fontWeight: 'bold',
    textAlign:'center',
    fontSize:16
  },

  titleArea:{
    width:'90%',
    height:'8%',
    alignItems:'center',
    flexDirection:'row',
  },

  title: {
    width:'90%',
    color:'#000000',
    textAlign:'left',
    fontSize: 30,
  },

  scrollView: {
    width:'90%',
    marginHorizontal: 20,
  },

  inputArea: {
    width:'90%',
    height:'30%',
    borderWidth:2,
    borderColor:'#000000',
    marginTop:8,
    justifyContent:'center',
    alignItems:'center',
  },
  baseArea: {
    width:'100%',
    height:60,
    borderRadius:4,
    borderColor:'#000000',
    marginTop:8,
    backgroundColor:'#FFFFFF',
    flexDirection: 'row',
    alignItems:'center',
    paddingLeft:8,
    paddingRight:8
  }
});
```

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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-create-thumbnail": "file:../../node_modules/@react-native-oh-tpl/react-native-create-thumbnail/harmony/createThumbnail.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-create-thumbnail": "file:../../node_modules/@react-native-oh-tpl/react-native-create-thumbnail/harmony/createThumbnail"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 3.在 ArkTs 侧引入 BlobUtilPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { CreateThumbnailPackage } from '@react-native-oh-tpl/react-native-create-thumbnail/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CreateThumbnailPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-create-thumbnail Releases](https://github.com/react-native-oh-library/react-native-create-thumbnail/releases)

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### **createThumbnail**
| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
|  createThumbnail    | thumbnail generator with storage/cache management and support for both local and remote videos  | function | NO | yes |

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|        Name         | Description  |   type   | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------: | :------: | :------: | :---------------: | :---------------: |
|  url | Path to video file (local or remote)   |    String    | yes  |   Android/ios    |    yes    |
|  timeStamp | Thumbnail timestamp (in milliseconds)   |    Number     | NO  |   Android/ios    |    yes    |
|  format | Thumbnail format, can be one of: jpeg, or png   |    String      | NO  |   Android/ios    |    yes    |
|  dirSize | Maximum size of the cache directory (in megabytes). When this directory is full, the previously generated thumbnails will be deleted to clear about half of it's size.   |    Number       | NO  |   Android/ios    |    yes    |
|  headers | Headers to load the video with. e.g. { Authorization: 'someAuthToken' }   |    Object      | NO  |   Android/ios    |    yes    |
|  cacheName | Cache name for this thumbnail to avoid duplicate generation. If specified, and a thumbnail already exists with the same cache name, it will be returned instead of generating a new one.   |    String     | NO  |   Android/ios    |    yes    |
## 返回值

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|        Name         | Description  |   type   | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------: | :------: | :------: | :---------------: | :---------------: |
|  path | Path to generated thumbnail   |    String    | NO  |   Android/ios    |    yes    |
|  size | Size (in bytes) of thumbnail   |    Number     | NO  |   Android/ios    |    yes    |
|  mime | Mimetype of thumbnail   |    String    | NO  |   Android/ios    |    yes    |
|  width | Thumbnail width   |    Number     | NO  |   Android/ios    |    yes    |
|  height | Thumbnail height   |    Number     | NO  |   Android/ios    |    yes    |



## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/souvik-ghosh/react-native-create-thumbnail/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->