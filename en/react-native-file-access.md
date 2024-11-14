> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-file-access</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/alpha0010/react-native-file-access">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/alpha0010/react-native-file-access/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-file-access)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-file-access Releases](https://github.com/react-native-oh-library/react-native-file-access/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-file-access
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-file-access
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

> [!TIP] 以下 demo 中使用的是本地文件。

```js
import React, { useEffect, useState } from 'react';
import { Button, SafeAreaView, ScrollView, StyleSheet, Text, View } from 'react-native';
import { Dirs, FileSystem } from 'react-native-file-access';

export function FileAccessDemo() {
  const [info, setInfo] = useState<{ key: string; value: string }[]>([]);
  const [result, setResult] = useState<string | null>('') || null;
  const [fileContent, setFileContent] = useState('');
  const [mkdirParam, setMkdirParam] = useState('');
  const [statInfo, setStatInfo] = useState<any>([]);
  const [isExists, setExists] = useState<boolean | string>('');
  const [lsList, setLsList] = useState<any>([]);
  const [totalSize, setTotalSize] = useState<number>();
  const [freeSize, setFreeSize] = useState<number>();
  const [hashValue, setHashValue] = useState<string>();
  const [statDirInfo, setStatDirInfo] = useState<object[]>([]);
  const [readFileChunkInfo, setReadFileChunkInfo] = useState<string>();
  const [concatBeyts, setConcatBeyts] = useState<number>();
  const [dirOrNot, setDirOrNot] = useState<any>('');

  const wirteFile = () => {
    FileSystem.writeFile(Dirs.DocumentDir + '/0801' + '/text1.txt', "DDDD", "utf8")
  };

  const readFile = () => {
    FileSystem.readFile(Dirs.DocumentDir + "/0801.txt").then((res) => {
      setFileContent(res);
    })
  };

  const unlink = () => {
    FileSystem.unlink(Dirs.DocumentDir + '/0812.txt');
  };

  const mkdir = () => {
    FileSystem.mkdir(Dirs.DocumentDir + "/wxwx").then((res) => {
      setMkdirParam(res);
    }).catch((error) => {
      console.log(error, 'error')
    });
  };

  const mv = () => {
    FileSystem.mv(Dirs.DocumentDir + "/text.txt", Dirs.DocumentDir + "/text1.txt");
  };

  const unzip = () => {
    FileSystem.unzip(Dirs.DocumentDir + "/wxwx.zip", Dirs.DocumentDir);
  };

  const stat = () => {
    FileSystem.stat(Dirs.DocumentDir + "/text1.txt").then((res) => {
      setStatInfo(JSON.stringify(res));
    }).catch(err => {
      console.log(err);
    })
  };

  const exists = () => {
    FileSystem.exists(Dirs.DocumentDir + "/text1.txt").then((res) => {
      setExists(res);
    }).catch((error) => {
      console.log(error, 'error');
    });
  };

  const cp = async () => {
    await FileSystem.cp(Dirs.DocumentDir + "/text1.txt", Dirs.DocumentDir + "/text4.txt")
  };

  const hash = () => {
    FileSystem.hash(Dirs.DocumentDir + "/text1.txt", 'SHA-256').then((res) => {
      setHashValue(res);
    }).catch((error) => {
      console.log(error, 'error')
    });
  };

  const isDir = async () => {
    let res = await FileSystem.isDir(Dirs.DocumentDir + '/text1.txt');
    setDirOrNot(res);
  };

  const ls = async () => {
    await FileSystem.ls(Dirs.DocumentDir).then((res) => {
      setLsList(res.join('、'));
    }).catch((error) => {
      console.log(error, 'error')
    });
  };

  const df = async () => {
    await FileSystem.df().then(res => {
      setFreeSize(res?.internal_free);
      setTotalSize(res?.internal_total);
    })
  };

  const statDir = () => {
    FileSystem.statDir(Dirs.DocumentDir).then(res => {
      setStatDirInfo(res);
    }).catch(err => {
      console.log(err);
    });
  };

  const readFileChunk = () => {
    FileSystem.readFileChunk(Dirs.DocumentDir + "/text2.txt", 1, 1, 'utf8').then((res) => {
      setReadFileChunkInfo(res);
    }).catch((error) => {
      console.log(error, 'error')
    });
  };

  const appendFile = async () => {
    await FileSystem.appendFile(Dirs.DocumentDir + "/text3.txt", "AAAAAA", 'utf8');
  }

  const concatFiles = async () => {
    await FileSystem.concatFiles(Dirs.DocumentDir + "/text3.txt", Dirs.DocumentDir + "/text4.txt").then((res) => {
      setConcatBeyts(res)
    }).catch((error) => {
      console.log(error, 'error')
    });
  };

  return (
    <ScrollView>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.wirteFile()</Text>
        <Button title=" Running" color="#841584" onPress={wirteFile}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.readFile()</Text>
          <Button title=" Running" color="#841584" onPress={readFile}></Button>
        </View>
        <Text>read the file contents: {fileContent}</Text>
      </View>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.unlink()</Text>
        <Button title=" Running" color="#841584" onPress={unlink}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.mkdir()</Text>
          <Button title=" Running" color="#841584" onPress={mkdir}></Button>
        </View>
        <Text>new directory path: {mkdirParam}</Text>
      </View>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.mv()</Text>
        <Button title=" Running" color="#841584" onPress={mv}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.stat()</Text>
          <Button title=" Running" color="#841584" onPress={stat}></Button>
        </View>
        <Text>file information: {statInfo}</Text>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.exists()</Text>
          <Button title=" Running" color="#841584" onPress={exists}></Button>
        </View>
        <Text>does the file exist: {isExists === '' ? '' : isExists ? 'exist' : 'does not exist'}</Text>
      </View>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.cp()</Text>
        <Button title=" Running" color="#841584" onPress={cp}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.isDir()</Text>
          <Button title=" Running" color="#841584" onPress={isDir}></Button>
        </View>
        <Text>is it a directory: {dirOrNot === '' ? '' : dirOrNot ? 'yes' : 'no'}</Text>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.ls()</Text>
          <Button title=" Running" color="#841584" onPress={ls}></Button>
        </View>
        <Text>files in the directory: {lsList}</Text>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.df()</Text>
          <Button title=" Running" color="#841584" onPress={df}></Button>
        </View>
        <Text>available space: {freeSize ? (freeSize / (1024 * 1024 * 1024)).toFixed(2) : ''}GB</Text>
        <Text>total space: {totalSize ? (totalSize / (1024 * 1024 * 1024)).toFixed(2) : ''}GB</Text>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.hash()</Text>
          <Button title=" Running" color="#841584" onPress={hash}></Button>
        </View>
        <Text>hash value: {hashValue}</Text>
      </View>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.unzip()</Text>
        <Button title=" Running" color="#841584" onPress={unzip}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.statDir()</Text>
          <Button title=" Running" color="#841584" onPress={statDir}></Button>
        </View>
        <Text>the following is the file information in the directory</Text>
        {statDirInfo.map((item, index) => (<Text key={index}>{JSON.stringify(item)}</Text>))}
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.readFileChunk()</Text>
          <Button title=" Running" color="#841584" onPress={readFileChunk}></Button>
        </View>
        <Text>read part of the file content: {readFileChunkInfo}</Text>
      </View>
      <View style={styles.baseArea}>
        <Text style={{ flex: 1 }}>FileAccess.appendFile()</Text>
        <Button title=" Running" color="#841584" onPress={appendFile}></Button>
      </View>
      <View style={{ height: 'auto', backgroundColor: "#FFF", marginTop: 6 }}>
        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>FileAccess.concatFiles()</Text>
          <Button title=" Running" color="#841584" onPress={concatFiles}></Button>
        </View>
        <Text>number of bytes written: {concatBeyts}</Text>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1 },
  key: { flex: 1.5, padding: 2 },
  row: { flexDirection: 'row', paddingVertical: 2 },
  value: { flex: 4, padding: 2 },
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
     "@react-native-oh-tpl/react-native-file-access": "file:../../node_modules/@react-native-oh-tpl/react-native-file-access/harmony/file_access.har"
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

### 3. Introducing RNFileAccessPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNFileAccessPackage } from '@react-native-oh-tpl/react-native-file-access/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNFileAccessPackage(ctx)
  ];
}
```

### 4. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-file-access Releases](https://github.com/react-native-oh-library/react-native-file-access/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.。

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### File System Access API

| Name           | Description                                                                                    | Type     | Platform | Required    | HarmonyOS Support |
| -------------- | ---------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| appendFile     | Append content to a file.                                                                      | Function | No       | iOS/Android | Yes               |
| concatFiles    | Append a file to another file. Returns number of bytes written.                                | Function | No       | iOS/Android | Yes               |
| cp             | Copy a file.                                                                                   | Function | No       | iOS/Android | Yes               |
| cpAsset        | Copy a bundled asset file.                                                                     | Function | No       | iOS/Android | Yes               |
| cpExternal     | Copy a file to an externally controlled location.                                              | Function | No       | iOS/Android | Yes               |
| df             | Check device available space.                                                                  | Function | No       | iOS/Android | Yes               |
| exists         | Check if a path exists.                                                                        | Function | No       | iOS/Android | Yes               |
| fetch          | Save a network request to a file.                                                              | Function | No       | iOS/Android | Yes               |
| getAppGroupDir | Get the directory for your app group (iOS & MacOS only).                                       | Function | No       | iOS         | No                |
| hash           | Hash the file content.                                                                         | Function | No       | iOS/Android | Yes               |
| isDir          | Check if a path is a directory.                                                                | Function | No       | iOS/Android | Yes               |
| ls             | List files in a directory.                                                                     | Function | No       | iOS/Android | Yes               |
| mkdir          | Make a new directory.                                                                          | Function | No       | iOS/Android | Yes               |
| mv             | Move a file.                                                                                   | Function | No       | iOS/Android | Yes               |
| readFile       | Read the content of a file.                                                                    | Function | No       | iOS/Android | Yes               |
| readFileChunk  | Read a chunk of the content of a file, starting from byte at offset, reading for length bytes. | Function | No       | iOS/Android | Yes               |
| stat           | Read file metadata.                                                                            | Function | No       | iOS/Android | Yes               |
| statDir        | Read metadata of all files in a directory.                                                     | Function | No       | iOS/Android | Yes               |
| unlink         | Delete a file.                                                                                 | Function | No       | iOS/Android | Yes               |
| unzip          | Extract a zip archive.                                                                         | Function | No       | iOS/Android | Yes               |
| writeFile      | Write content to a file.                                                                       | Function | No       | iOS/Android | Yes               |

## Known Issues

- [ ] getAppGroupDir method (Get application directory permissions, iOS, Mac iOS only) This is a dependency problem. Currently, the Harmony side does not provide support. [issue#4](https://github.com/react-native-oh-library/react-native-file-access/issues/4)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/alpha0010/react-native-file-access/blob/master/LICENSE).
