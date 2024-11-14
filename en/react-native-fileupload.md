> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-fileupload</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/PhilippKrone/react-native-fileupload">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/PhilippKrone/react-native-fileupload/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-fileupload)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-fileupload Releases](https://github.com/react-native-oh-library/react-native-fileupload/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-fileupload
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-fileupload
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

This library requires the following permissions to be added in `entry/src/main/module.json5`.

```json
"requestPermissions": [ 
  { 
    "name": "ohos.permission.INTERNET", 
  }
]
```

```tsx
import React, {Component} from 'react';
import { StyleSheet, Text, View } from 'react-native';
import FileUpload from 'react-native-fileupload';
import Toast from '@remobile/react-native-toast';

export default class FileUploadDemo extends Component {

  componentDidMount () {
    var obj = {
        uploadUrl: 'http://1.2.27.230:9990/upload',// The real server Url
        method: 'POST', // default 'POST',support 'POST' and 'PUT'
        headers: {
          
          'Content-Type': 'multipart/form-data',
        },
        fields: {
            name: 'hello',value: 'world',
        },
        files: [
          {
            name: 'file',// optional
            filename: 'assets_placeholder2000x2000.jpg',
            filepath: '/xxx/assets_placeholder2000x2000.jpg',// The real server filepath
            filetype: 'jpg',// optional
          },
          {
            filename: 'one.w4a',
            filepath: '/xxx/one.w4a', // The real server filepath
            filetype: 'audio/x-m4a',// optional
          },
        ]
    };
    FileUpload.upload(obj, function(err,result) {
      console.log("upload",err,result);
      if(err || result) {
        Toast.showShortCenter(err + result)
      }
    })
  }
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.welcome}>
          Welcome to React Native!
        </Text>
      </View>
    );
  }
}

let styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
});
```

## Use Codegen

this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
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
    "@react-native-oh-tpl/react-native-fileupload": "file:../../node_modules/@react-native-oh-tpl/react-native-fileupload/harmony/fileupload.har"
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

### 3. Configuring CMakeLists and Introducing FileUpLoadPackage

Open `entry/src/main/ets/RNPackagesFactory.ts` and add the following code:

```diff
  ...
+ import {FileUpLoadPackage} from '@react-native-oh-tpl/react-native-fileupload/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new FileUpLoadPackage(ctx)
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

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-fileupload Releases](https://github.com/react-native-oh-library/react-native-fileupload/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| upload | File upload  | void  | yes | iOS/Android  | yes     |

## Known Issues

## Others

## License

This project is licensed under  [The MIT License (MIT)](https://github.com/PhilippKrone/react-native-fileupload/blob/master/LICENSE).
