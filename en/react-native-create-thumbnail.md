> Template version: v0.2.0

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


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-create-thumbnail)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-create-thumbnail Releases](https://github.com/react-native-oh-library/react-native-create-thumbnail/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-create-thumbnail
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-create-thumbnail
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```js
import React, {useState } from 'react';
import {  StyleSheet, Text, Button ,ScrollView,View} from 'react-native';
import { createThumbnail } from 'react-native-create-thumbnail';

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
             <Button title='Running' color='#841584' onPress={CreateThumbnail}></Button>
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
    "@react-native-oh-tpl/react-native-create-thumbnail": "file:../../node_modules/@react-native-oh-tpl/react-native-create-thumbnail/harmony/createThumbnail.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] The source code is located in the harmony folder within the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-create-thumbnail": "file:../../node_modules/@react-native-oh-tpl/react-native-create-thumbnail/harmony/createThumbnail"
  }
```

run the following instruction on the terminal:

```bash
cd entry
ohpm install --no-link
```

### 3. Introducing BlobUtilPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-create-thumbnail Releases](https://github.com/react-native-oh-library/react-native-create-thumbnail/releases)

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### **createThumbnail**
| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
|  createThumbnail    | thumbnail generator with storage/cache management and support for both local and remote videos  | function | NO | yes |

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|        Name         | Description  |   type   | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------: | :------: | :------: | :---------------: | :---------------: |
|  url | Path to video file (local or remote)   |    String    | yes  |   Android/ios    |    yes    |
|  timeStamp | Thumbnail timestamp (in milliseconds)   |    Number     | NO  |   Android/ios    |    yes    |
|  format | Thumbnail format, can be one of: jpeg, or png   |    String      | NO  |   Android/ios    |    yes    |
|  dirSize | Maximum size of the cache directory (in megabytes). When this directory is full, the previously generated thumbnails will be deleted to clear about half of it's size.   |    Number       | NO  |   Android/ios    |    yes    |
|  headers | Headers to load the video with. e.g. { Authorization: 'someAuthToken' }   |    Object      | NO  |   Android/ios    |    yes    |
|  cacheName | Cache name for this thumbnail to avoid duplicate generation. If specified, and a thumbnail already exists with the same cache name, it will be returned instead of generating a new one.   |    String     | NO  |   Android/ios    |    yes    |
## Return Value

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|        Name         | Description  |   type   | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------: | :------: | :------: | :---------------: | :---------------: |
|  path | Path to generated thumbnail   |    String    | NO  |   Android/ios    |    yes    |
|  size | Size (in bytes) of thumbnail   |    Number     | NO  |   Android/ios    |    yes    |
|  mime | Mimetype of thumbnail   |    String    | NO  |   Android/ios    |    yes    |
|  width | Thumbnail width   |    Number     | NO  |   Android/ios    |    yes    |
|  height | Thumbnail height   |    Number     | NO  |   Android/ios    |    yes    |



## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/souvik-ghosh/react-native-create-thumbnail/blob/master/LICENSE).
