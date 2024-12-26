> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-rotate</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/dgladkov/react-native-image-rotate">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/dgladkov/react-native-image-rotate/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-image-rotate)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-image-rotate Releases](https://github.com/react-native-oh-library/react-native-image-rotate/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

Go to the project directory and execute the following instruction:

#### npm

```bash
npm install @react-native-oh-tpl/react-native-image-rotate@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-image-rotate@file:#
```

The following code shows the basic use scenario of the repository:

```js
import React, { Component } from 'react';
import {
  Image,
  StyleSheet,
  Text,
  TouchableHighlight,
  View
} from 'react-native';

import ImageRotate from 'react-native-image-rotate';

const SOURCE_IMAGE = 'https://upload.wikimedia.org/wikipedia/en/5/56/Warcraft_Teaser_Poster.jpg';

export default class App extends Component {

  constructor() {
    super();
    this.state = {
      image: SOURCE_IMAGE,
      currentAngle: 0,
      width: 150,
      height: 240,
    };

    this.rotate = this.rotate.bind(this);
  }

  rotate(angle) {
    const nextAngle = this.state.currentAngle + angle;
    ImageRotate.rotateImage(
      SOURCE_IMAGE,
      nextAngle,
      (uri) => {
        this.setState({
          image: uri,
          currentAngle: nextAngle,
          width: this.state.height,
          height: this.state.width,
        });
      },
      (error) => {
        console.error(error);
      }
    );
  }

  render() {
    return (
      <View style={styles.container}>
        <View style={styles.imageContainer}>
          <Image style={{width: this.state.width, height: this.state.height}} source={{uri: this.state.image}} />
        </View>
        <TouchableHighlight
          onPress={() => this.rotate(90)}
          style={styles.button}
        >
          <Text style={styles.text}>ROTATE CW</Text>
        </TouchableHighlight>

        <TouchableHighlight
          onPress={() => this.rotate(-90)}
          style={styles.button}
        >
          <Text style={styles.text}>ROTATE CCW</Text>
        </TouchableHighlight>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  button: {
    backgroundColor: 'red',
    padding: 5,
    margin: 5,
  },
  imageContainer: {
    height: 240,
    justifyContent: 'center',
  },
  text: {
    color: 'white',
  },
});

```

## Use Codegen

If this repository has been adapted to Codegen, generate the bridge code of the third-party library by using the Codegen. For details, see[ Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the harmony directory of the HarmonyOS project in DevEco Studio.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

1. Use the HAR file.
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-image-rotate": "file:../../node_modules/@react-native-oh-tpl/react-native-image-rotate/harmony/imageRotate.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see[Directly Linking Source Code](/en/link-source-code.md)

### 3.Introducing RNImageRotatePackage Package to ArkTS

Open the entry/src/main/ets/RNPackagesFactory.ts file and add the following code:

```diff
  ...
  
+  import { RNImageRotatePackage } from '@react-native-oh-tpl/react-native-image-rotate/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNImageRotatePackage(ctx)
  ];
}
```

### 4.Running

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-image-rotate Releases](https://github.com/react-native-oh-library/react-native-image-rotate/releases)

## Static Method

> [!TIP]The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!TIP]If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name        | Description    | Type     | Required | Platform    | HarmonyOS   Support |
| ----------- | -------------- | -------- | -------- | ----------- | ------------------- |
| rotateImage | rotate picture | Function | no       | iOS/Android | yes                 |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/dgladkov/react-native-image-rotate/blob/master/LICENSE).
