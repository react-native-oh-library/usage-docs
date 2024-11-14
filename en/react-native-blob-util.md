> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-blob-util</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/RonRadtke/react-native-blob-util">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/RonRadtke/react-native-blob-util/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-blob-util)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-blob-util Releases](https://github.com/react-native-oh-library/react-native-blob-util/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-blob-util
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-blob-util
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import {
  ScrollView,
  StyleSheet,
  Button,
  View,
  Text,
  NativeEventEmitter,
} from "react-native";
import ReactNativeBlobUtil from "react-native-blob-util";

export default function BlobUtilDemo() {
  const [result, setResult] = useState < string | null > (null);
  const [mkdirParam, setMkdirParam] = useState("");

  const createFile = async () => {
    await ReactNativeBlobUtil.fs.createFile(
      result + "/text.txt",
      "123456",
      "utf8"
    );
  };

  const ls = async () => {
    await ReactNativeBlobUtil.fs.ls(ReactNativeBlobUtil.fs.dirs.CacheDir);
  };

  const createFileASCII = async () => {
    await ReactNativeBlobUtil.fs.createFile(
      result + "/text.txt",
      [102, 111, 111],
      "ascii"
    );
  };

  const unlink = () => {
    ReactNativeBlobUtil.fs.unlink(result + "/text.txt");
  };

  const getConstants = () => {
    let obj = ReactNativeBlobUtil.fs.dirs.CacheDir;
    setResult(obj);
  };

  const writeFile = () => {
    ReactNativeBlobUtil.fs.writeFile(
      result + "/text.txt",
      "Try to write str",
      "utf8"
    );
  };

  const writeStream = () => {
    ReactNativeBlobUtil.fs.writeStream(result + "/text.txt", "utf8", false);
  };

  const writeArrayChunk = () => {
    ReactNativeBlobUtil.fs
      .writeStream(result + "/text.txt", "ascii", false)
      .then((reactNativeBlobUtilWriteStream) => {
        reactNativeBlobUtilWriteStream.encoding = "ascii";
        reactNativeBlobUtilWriteStream.write(["101", "32", "97"]);
      });
  };

  const writeChunk = () => {
    ReactNativeBlobUtil.fs
      .writeStream(result + "/text.txt", "utf8", false)
      .then((reactNativeBlobUtilWriteStream) => {
        reactNativeBlobUtilWriteStream.write("Zm9vIChXcml0ZSBCYXNlNjQpMQ==");
      });
  };

  const closeStream = () => {
    ReactNativeBlobUtil.fs
      .writeStream(result + "/text.txt", "utf8", false)
      .then((reactNativeBlobUtilWriteStream) => {
        setTimeout(() => {
          reactNativeBlobUtilWriteStream.close();
        }, 1000);
      });
  };
  const readStream = () => {
    ReactNativeBlobUtil.fs.readStream(result + "/text.txt", "utf8", 4000, 200);
  };

  const mkdir = () => {
    ReactNativeBlobUtil.fs.mkdir(
      ReactNativeBlobUtil.fs.dirs.DocumentDir + "/" + mkdirParam
    );
  };

  const stat = () => {
    ReactNativeBlobUtil.fs.stat(result + "/text.txt");
  };

  const copyFileToCache = () => {
    ReactNativeBlobUtil.fs.cp(result + "/text.txt", result + "/text1.txt");
  };

  const writeFileArray = () => {
    ReactNativeBlobUtil.fs.writeFile(
      result + "/text.txt",
      [102, 111, 111],
      "ascii"
    );
  };

  const exists = () => {
    ReactNativeBlobUtil.fs.exists(result + "/text.txt");
  };

  const lstat = () => {
    ReactNativeBlobUtil.fs.lstat(result + "/text.txt");
  };

  const mv = () => {
    ReactNativeBlobUtil.fs.mv(result + "/text.txt", result + "/text1.txt");
  };

  const hash = () => {
    ReactNativeBlobUtil.fs.hash(result + "/text.txt", "md5");
  };

  const readFile = () => {
    ReactNativeBlobUtil.fs.readFile(result + "/text.txt", "utf8", 4000);
  };

  const slice = () => {
    ReactNativeBlobUtil.fs.slice(
      result + "/text.txt",
      result + "/text1.txt",
      2,
      5
    );
  };

  const df = () => {
    ReactNativeBlobUtil.fs.df();
  };

  const addListener = () => {
    let obj = "addListener是空实现";
    setResult(obj);
  };

  const removeListeners = () => {
    let obj = "removeListeners是空实现";
    setResult(obj);
  };

  const emitExpiredEvent = () => {
    let obj = "emitExpiredEvent是空实现,三方库没有调用";
    setResult(obj);
  };

  return (
    <View style={styles.container}>
      <View style={styles.titleArea}>
        <Text style={styles.title}>BlobUtil</Text>
      </View>
      <View style={styles.inputArea}>
        <Text style={styles.baseText}>{result}</Text>
      </View>
      <ScrollView style={styles.scrollView}>
        <View style={{ flexDirection: "column" }}>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.getConstants()</Text>
            <Button
              title="运行"
              color="#841584"
              onPress={getConstants}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.createFile()</Text>
            <Button title="运行" color="#841584" onPress={createFile}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.unlink()</Text>
            <Button title="运行" color="#841584" onPress={unlink}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>
              BlobUtilTurboModule.copyFileToCache()
            </Text>
            <Button
              title="运行"
              color="#841584"
              onPress={copyFileToCache}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.writeFile()</Text>
            <Button title="运行" color="#841584" onPress={writeFile}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.stat()</Text>
            <Button title="运行" color="#841584" onPress={stat}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.mkdir()</Text>
            <Button title="运行" color="#841584" onPress={mkdir}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.writeStream()</Text>
            <Button title="运行" color="#841584" onPress={writeStream}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.ls()</Text>
            <Button title="运行" color="#841584" onPress={ls}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>
              BlobUtilTurboModule.createFileASCII()
            </Text>
            <Button
              title="运行"
              color="#841584"
              onPress={createFileASCII}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>
              BlobUtilTurboModule.writeFileArray()
            </Text>
            <Button
              title="运行"
              color="#841584"
              onPress={writeFileArray}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.exists()</Text>
            <Button title="运行" color="#841584" onPress={exists}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.lstat()</Text>
            <Button title="运行" color="#841584" onPress={lstat}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.hash()</Text>
            <Button title="运行" color="#841584" onPress={hash}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.readFile()</Text>
            <Button title="运行" color="#841584" onPress={readFile}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.slice()</Text>
            <Button title="运行" color="#841584" onPress={slice}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.df()</Text>
            <Button title="运行" color="#841584" onPress={df}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.closeStream()</Text>
            <Button title="运行" color="#841584" onPress={closeStream}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>
              BlobUtilTurboModule.writeArrayChunk()
            </Text>
            <Button
              title="运行"
              color="#841584"
              onPress={writeArrayChunk}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.writeChunk()</Text>
            <Button title="运行" color="#841584" onPress={writeChunk}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.readStream()</Text>
            <Button title="运行" color="#841584" onPress={readStream}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>BlobUtilTurboModule.mv()</Text>
            <Button title="运行" color="#841584" onPress={mv}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>addListener()</Text>
            <Button title="运行" color="#841584" onPress={addListener}></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>removeListeners()</Text>
            <Button
              title="运行"
              color="#841584"
              onPress={removeListeners}
            ></Button>
          </View>
          <View style={styles.baseArea}>
            <Text style={{ flex: 1 }}>emitExpiredEvent()</Text>
            <Button
              title="运行"
              color="#841584"
              onPress={emitExpiredEvent}
            ></Button>
          </View>
        </View>
      </ScrollView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: "100%",
    height: "100%",
    flexDirection: "column",
    alignItems: "center",
    backgroundColor: "#F1F3F5",
  },
  baseText: {
    width: "100%",
    height: "100%",
    fontWeight: "bold",
    textAlign: "center",
    fontSize: 16,
    ellipsizeMode: "tail",
    numberOfLines: 2,
  },
  titleArea: {
    width: "90%",
    height: "8%",
    alignItems: "center",
    flexDirection: "row",
  },
  title: {
    width: "90%",
    color: "#000000",
    textAlign: "left",
    fontSize: 30,
  },
  scrollView: {
    width: "90%",
    marginHorizontal: 10,
  },

  inputArea: {
    width: "90%",
    height: "10%",
    borderWidth: 2,
    borderColor: "#000000",
    marginTop: 8,
    justifyContent: "center",
    alignItems: "center",
  },
  baseArea: {
    width: "100%",
    height: 60,
    borderRadius: 4,
    borderColor: "#000000",
    marginTop: 6,
    backgroundColor: "#FFFFFF",
    flexDirection: "row",
    alignItems: "center",
    paddingLeft: 8,
    paddingRight: 8,
  },
});
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
     "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
     "@react-native-oh-tpl/react-native-blob-util": "file:../../node_modules/@react-native-oh-tpl/react-native-blob-util/harmony/blobUtil.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3.Introducing BlobUtilPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import {BlobUtilPackage} from '@react-native-oh-tpl/react-native-blob-util/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new BlobUtilPackage(ctx)
  ];
}
```

### 4.Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-blob-util Releases](https://github.com/react-native-oh-library/react-native-blob-util/releases)

## APIs

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### Fetch API

##### ReactNativeBlobUtil.fetch

| Name    | Description|Type | Required | Platform    | HarmonyOS Support |
| ------- | --------|--- | -------- | ----------- | ----------------- |
| progress | 进度   | Function    | No       | iOS/Android | yes                |
| uploadProgress | 上传进度  | Function        | No       | iOS/Android | yes                |
| cancel | 取消   | Function       | No       | iOS/Android | yes                |

#### Android API

##### ReactNativeBlobUtil.android

|        Name         | Description| Type   | Required | Platform | HarmonyOS Support |
| :-----------------: | :------|----: | :------: | :------: | :---------------: |
|  actionViewIntent   | 动作视图意图| Function  |    No    | Android  |        No         |
|  getContentIntent   | 获取内容意图| Function  |    No    | Android  |        No         |
| addCompleteDownload | 添加完整下载| Function  |    No    | Android  |        No         |

#### File System Access API

##### ReactNativeBlobUtil.fs

|    Name     |            Description  | Type             | Required |  Platform   | HarmonyOS Support |
| :---------: | :---------------------| -----------: | :------: | :---------: | :---------------: |
|    dirs     |                目录 | Function               |    NO    | iOS/Android |        yes        |
| createFile  |              创建文件 | Function             |    NO    | iOS/Android |        yes        |
|  writeFile  |               写文件   | Function            |    NO    | iOS/Android |        yes        |
| writeStream |                写流    | Function            |    NO    | iOS/Android |        yes        |
| appendFile  |              追加文件   | Function           |    NO    | iOS/Android |        yes        |
|  readFile   |              读取文件  | Function            |    NO    | iOS/Android |        yes        |
|    hash     |                哈希   | Function             |    NO    | iOS/Android |        yes        |
| readStream  |                读流    | Function            |    NO    | iOS/Android |        yes        |
|    mkdir    |              创建目录   | Function           |    NO    | iOS/Android |        yes        |
|     ls      |        查看当下的文件和目录| Function        |    NO    | iOS/Android |        yes        |
|     mv      |            移动文件位置  | Function          |    NO    | iOS/Android |        yes        |
|     cp      |              复制文件   | Function           |    NO    | iOS/Android |        yes        |
|   exists    |          检查文件是否存在 | Function         |    NO    | iOS/Android |        yes        |
|    isDir    |             是否是目录  | Function           |    NO    | iOS/Android |        yes        |
|   unlink    |              删除文件   | Function           |    NO    | iOS/Android |        yes        |
|    lstat    |      获取目录下文件的统计数据 | Function     |    NO    | iOS/Android |        yes        |
|    stat     |   类似地获取数据或目录的统计信息| Function   |    NO    | iOS/Android |        yes        |
|  scanFile   |              扫描文件    | Function          |    NO    |   Android   |        no         |
|    asset    |                资产      | Function          |    NO    | iOS/Android |        yes        |
|     df      | 获取设备的可用磁盘空间和总磁盘空间| Function |    NO    | iOS/Android |        yes        |

#### iOS API

#### ReactNativeBlobUtil.ios

| Name            | Description      | Type                      | Required | Platform | HarmonyOS Support |
| --------------- | ----------------------| ---------------- | -------- | -------- | ----------------- |
| previewDocument | 文档查看器--需要系统权限  | Function             | No       | iOS      | yes                |
| openDocument    | 显示与文件交互的选项菜单--需要系统权限| Function | No       | iOS      | yes                |

#### Network Utils

##### ReactNativeBlobUtil.net

| Name          | Description| Type | Required | Platform    | HarmonyOS Support |
| ------------- | ----------- | ---| ----- | ----------- | ----------------- |
| getCookies    | 获取 cookie| Function | No       | iOS/Android | no                |
| removeCookies | 删除 cookie| Function | No       | iOS/Android | no               |

#### Session API

##### ReactNativeBlobUtil.session

| Name    | Description| Type | Required | Platform    | HarmonyOS Support |
| ------- | ----------- | --| ------ | ----------- | ----------------- |
| add | 向此会话添加文件路径   | Function     | No       | iOS/Android | yes                |
| remove | 从此会话中删除会话条目而不删除文件  | Function      | No       | iOS/Android | yes                |
| list | 返回包含此会话中的文件路径的数组   | Function     | No       | iOS/Android | yes                |
| dispose | 删除会话中的所有文件  | Function      | No       | iOS/Android | yes                |

#### MediaStore(Android Media Storage)

##### ReactNativeBlobUtil.MediaCollection

| Name             | Description | Type   | Required | Platform | HarmonyOS Support |
| ---------------- | --------| ------ | -------- | -------- | ----------------- |
| CopyToMediaStore | 复制到媒体存储| Function | No       | Android  | no                |
| createMediaFile  | 创建媒体文件| Function   | No       | Android  | no                |
| writeMediaFile   | 写媒体文件 | Function    | No       | Android  | no                |
| copyToInternal   | 复制到内部 | Function    | No       | Android  | no                |

#### Utils API

| Name   | Description| Type | Required | Platform    | HarmonyOS Support |
| ------ | ----------- | ---| ----- | ----------- | ----------------- |
| wrap   |  使文件路径可以被识别| Function           | No       | iOS/Android | yes                |
| base64 |   使用base64编码解码| Function          | No       | iOS/Android | yes                |
| session |  用于管理缓存文件 | Function          | No       | iOS/Android | yes                |

## Known Issues

 - [ ] blob-util在使用getCookies、removeCookies	在Android、iOS、Harmony OS 上使用都会报错: [issue#381](https://github.com/RonRadtke/react-native-blob-util/issues/381)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/RonRadtke/react-native-blob-util/blob/master/LICENSE).
