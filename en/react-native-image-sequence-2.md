> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-sequence</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bwindsor/react-native-image-sequence">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bwindsor/react-native-image-sequence/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-image-sequence)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-image-sequence Releases](https://github.com/react-native-oh-library/react-native-image-sequence/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-sequence-2
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-sequence-2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

TestDemo.tsx

```js
import React, { useState } from "react";
import { SafeAreaView, StyleSheet } from "react-native-harmony";
import { View, Text, Switch, TextInput, Button } from "react-native";
import TestDemo2 from "./TestDemo2";

const images = [
  { uri: "https://octodex.github.com/images/stormtroopocat.jpg" },
  { uri: 'https://octodex.github.com/images/saint_nictocat.jpg' },
  require("./assets/2.jpg"),
  require("./assets/3.jpg"),
  require("./assets/4.jpg"),
  require("./assets/5.jpg"),
  require("./assets/6.jpg"),
];

export interface sequenceType {
  images: NodeRequire[];
  loop: boolean;
  startFrameIndex: number;
  framesPerSecond: number;
  downsampleWidth: number;
  downsampleHeight: number;
}

const ImageSequenceDemo = (props: any) => {
  const [loopData, setLoopData] = useState(false);
  const [isShow, setIsShow] = useState(false);
  const [winWidth, setWinWidth] = useState(300);
  const [winHeight, setWinHeight] = useState(200);
  const [downsampleWidth, setDownSampleWidth] = useState(-1);
  const [downsampleHeight, setDownSampleHeight] = useState(-1);

  // Set Sampling Width
  const inputSampleWidth = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setDownSampleWidth(Number(value));
  };

  // Set Sampling Height
  const inputSampleHeight = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setDownSampleHeight(Number(value));
  };

  // Set Starting Position
  const [startFrameIndex, setFrameIndex] = useState(0);
  const inputStartFrameIndex = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    let _value = Number(value);
    if (Number(value) > images.length) {
      _value = 0;
    }
    setFrameIndex(_value);
  };

  // Set Rate
  const [framesPerSecond, setFramesPerSecond] = useState(24);
  const inputFramesPerSecond = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    let _value = Number(value);
    if (Number(value) <= 0) {
      _value = 24;
    }
    setFramesPerSecond(_value);
  };

  const buttonIsShow = () => {
    setIsShow(!isShow);
  };

  const inputSetWinWidth = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setWinWidth(Number(value));
  };

  const inputSetWinHeight = (value: string) => {
    if (isNaN(Number(value))) {
      return;
    }
    setWinHeight(Number(value));
  };

  return (
    <SafeAreaView>
      <View>
        <View>
          <Text>
            Current view size:width: {winWidth}, height:{winHeight}
          </Text>
          <Text>
            Activate Loop:<Switch onValueChange={(value) => setLoopData(value)}></Switch>
          </Text>
          <View>
            <Text>Image Width/Height:</Text>
            <View style={styles.box}>
              <TextInput
                style={[styles.input, styles.input1]}
                onChangeText={(value) => inputSetWinWidth(value)}
                defaultValue="300"
                keyboardType="numeric"
              />
              <TextInput
                style={[styles.input, styles.input1]}
                onChangeText={(value) => inputSetWinHeight(value)}
                defaultValue="200"
                keyboardType="numeric"
              />
            </View>
          </View>
          <Text>Initial Position:</Text>
          <TextInput
            style={styles.input}
            onChangeText={(value) => inputStartFrameIndex(value)}
            defaultValue="0"
            keyboardType="numeric"
          />
          <Text>Playback Speed:</Text>
          <TextInput
            style={styles.input}
            onChangeText={(value) => inputFramesPerSecond(value)}
            defaultValue="24"
            keyboardType="numeric"
          />
          <View>
             <Text>Sampling Width/Height:</Text>
             <View style={styles.box}>
                <TextInput style={[styles.input, styles.input1]} onChangeText={value => inputSampleWidth(value)} defaultValue='-1' keyboardType='default' />
                 <TextInput style={[styles.input, styles.input1]} onChangeText={value => inputSampleHeight(value)} defaultValue='-1' keyboardType='default' />
              </View>
           </View>
        </View>
        {!isShow ? (
          <Button title="display" onPress={() => buttonIsShow()} />
        ) : (
          <Button title="return" onPress={() => buttonIsShow()} />
        )}
        {isShow ? (
          <TestDemo2
            loop={loopData}
            images={images}
            width={winWidth}
            height={winHeight}
            startFrameIndex={startFrameIndex}
            framesPerSecond={framesPerSecond}
            downsampleWidth={downsampleWidth}
            downsampleHeight={downsampleHeight}
          />
        ) : null}
      </View>
    </SafeAreaView>
  );
};
const styles = StyleSheet.create({
  continer: {
    flex: 1,
    justifyContent: "center",
    width: "100%",
    height: "100%",
  },
  title: {
    textAlign: "center",
    marginVertical: 8,
  },
  fixToText: {
    flexDirection: "row",
    justifyContent: "space-between",
  },
  separator: {
    marginVertical: 8,
    borderBottomColor: "#737373",
    borderBottomWidth: StyleSheet.hairlineWidth,
  },
  input: {
    height: 40,
    margin: 12,
    borderWidth: 1,
    borderColor: "red",
    padding: 10,
    width: 200,
  },
  box: {
    flexDirection: "row",
    justifyContent: "flex-start",
  },
  input1: {
    width: 100,
  },
});

export default ImageSequenceDemo;
```

TestDemo2.tsx

```js
import { StyleSheet, View } from "react-native";
import ImageSequence from 'react-native-image-sequence-2'

const Separator = () => <View style={styles.separator}/>
const TestDemo2 = (props: any) => {
    return (
        <ImageSequence
        images={props.images}
        loop={props.loop}
        startFrameIndex={props.startFrameIndex}
        framesPerSecond={props.framesPerSecond}
        downsampleWidth={props.downsampleWidth}
        downsampleHeight={props.downsampleHeight}
        style={{width: props.width, height: props.height}}
        />
    )
}
const styles = StyleSheet.create({
    separator: {
        marginVertical: 8,
        borderBottomColor: '#737373',
        borderBottomWidth: StyleSheet.hairlineWidth
    }
})

export default TestDemo2
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

1. Method 1 (recommended): Use the HAR file.


> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-image-sequence-2":"file:../../node_modules/@react-native-oh-tpl/react-native-image-sequence-2/harmony/image_sequence.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP]For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

### 3. Introducing RNImageSequence Component to ArkTS


(If the code of the repository is written through CAPI, delete this section.)<br>Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { RNImageSequence } from "@react-native-oh-tpl/react-native-image-sequence-2"

const arkTsComponentNames: Array<string> = ["SampleView", 
"Generated",
"PropsDisplayer",
+ RNImageSequence.NAME
]

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+  if (ctx.componentName === RNImageSequence.NAME) {
+     RNImageSequence({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag
+     })
+   }
...
}
...
```

### 4. Introducing ImageSequencePackage Package to ArkTS


Open the `entry/src/main/ets/RNPackagesFactory.ts`，file and add the following code:

```diff
  ...
+ import { ImageSequencePackage } from "@react-native-oh-tpl/react-native-image-sequence-2/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImageSequencePackage(ctx) 
  ];
}
```

### 5. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-image-sequence Releases](https://github.com/react-native-oh-library/react-native-image-sequence/releases)


This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name             | Description                                                  | Type    | Required | Platform | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| images           | An array of source images. Each element of the array should be the result of a call to require(imagePath) | any[]   | Yes      | All      | Yes               |
| startFrameIndex  | Which index of the images array should the sequence start at. Default: 0 | number  | No       | All      | Yes               |
| framesPerSecond  | Playback speed of the image sequence. Default: 24            | number  | No       | All      | Yes               |
| loop             | Should the sequence loop. Default: true                      | boolean | No       | All      | Yes               |
| downsampleWidth  | The width to use for optional downsampling. Both `downsampleWidth` and `downsampleHeight` must be set to a positive number to enable downsampling. Default: -1 | number  | No       | All      | Yes               |
| downsampleHeight | The height to use for optional downsampling. Both `downsampleWidth` and `downsampleHeight` must be set to a positive number to enable downsampling. Default: -1 | number  | No       | All      | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/bwindsor/react-native-image-sequence/blob/master/LICENSE), Please enjoy and participate freely in open source.
