> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@bam.tech/react-native-image-resizer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bamlab/react-native-image-resizer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bamlab/react-native-image-resizer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-image-resizer)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-image-resizer Releases](https://github.com/react-native-oh-library/react-native-image-resizer/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-resizer@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-resizer@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useRef, useState } from 'react';
import {
  Alert,
  Image,
  Platform,
  ScrollView,
  StyleSheet,
  Text,
  TextInput,
  TouchableOpacity,
  View,
} from 'react-native';
import ImageResizer from '@bam.tech/react-native-image-resizer';
import type {
  ResizeMode,
  Response,
} from '@bam.tech/react-native-image-resizer';
import { launchImageLibrary } from 'react-native-image-picker';

const modeOptions: { label: string; value: ResizeMode }[] = [
  {
    label: 'contain',
    value: 'contain',
  },
  {
    label: 'cover',
    value: 'cover',
  },
  {
    label: 'stretch',
    value: 'stretch',
  },
];

const onlyScaleDownOptions: { label: string; value: boolean }[] = [
  {
    label: 'true',
    value: true,
  },
  {
    label: 'false',
    value: false,
  },
];

function ImageResizerDemo() {
  const [selectedMode, setMode] = useState<ResizeMode>('contain');
  const [onlyScaleDown, setOnlyScaleDown] = useState(false);
  const [imageUri, setImageUri] = useState<null | string>();
  const [sizeTarget, setSizeTarget] = useState(80);
  const [resizedImage, setResizedImage] = useState<null | Response>();

  const resize = async () => {
    if (!imageUri) return;

    setResizedImage(null);

    try {
      let result = await ImageResizer.createResizedImage(
        imageUri,
        sizeTarget,
        sizeTarget,
        'JPEG',
        100,
        0,
        undefined,
        false,
        {
          mode: selectedMode,
          onlyScaleDown,
        }
      );

      setResizedImage(result);
    } catch (error) {
      Alert.alert('Unable to resize the photo');
    }
  };
  
  const selectImageFromPicker = async () => {
    launchImageLibrary({ mediaType: 'photo' }, (response) => {
      if (!response || !response.assets) return;
      const asset = response.assets[0];
      if (asset) {
        setImageUri(asset.uri);
      }
    });
  };

  return (
    <ScrollView
      style={styles.scrollView}
      contentContainerStyle={styles.container}
    >
      <Text style={styles.welcome}>Image Resizer example</Text>
      <View style={styles.imageSourceButtonContainer}>
        <TouchableOpacity style={styles.button} onPress={selectImageFromPicker}>
          <Text>{'Select an image (react-native-image-picker)'}</Text>
        </TouchableOpacity>
      </View>
     
      <Text style={styles.instructions}>This is the original image:</Text>
      {imageUri ? (
        <Image
          style={styles.image}
          source={{ uri: imageUri }}
          resizeMode="contain"
        />
      ) : null}

      <Text style={styles.instructions}>Resized image:</Text>
      <Text>Mode: </Text>
      <View style={styles.optionContainer}>
        {modeOptions.map((mode) => (
          <TouchableOpacity
            style={styles.buttonOption}
            onPress={() => setMode(mode.value)}
            key={mode.label}
          >
            <Text>{`${mode.label} ${
              selectedMode === mode.value ? '✅' : ''
            }`}</Text>
          </TouchableOpacity>
        ))}
      </View>

      <Text>Only scale down? </Text>
      <View style={styles.optionContainer}>
        {onlyScaleDownOptions.map((scaleDownOption) => (
          <TouchableOpacity
            style={styles.buttonOption}
            onPress={() => setOnlyScaleDown(scaleDownOption.value)}
            key={scaleDownOption.label}
          >
            <Text>{`${scaleDownOption.label} ${
              onlyScaleDown === scaleDownOption.value ? '✅' : ''
            }`}</Text>
          </TouchableOpacity>
        ))}
      </View>

      <Text>Target size: </Text>
      <TextInput
        style={styles.textInput}
        placeholder={sizeTarget.toString()}
        keyboardType="decimal-pad"
        onChangeText={(text) => {
          setSizeTarget(Number(text));
        }}
      />

      <TouchableOpacity style={styles.button} onPress={resize}>
        <Text>Click me to resize the image</Text>
      </TouchableOpacity>
      {resizedImage ? (
        <>
          <Image
            style={styles.image}
            source={{ uri: resizedImage.uri }}
            resizeMode="contain"
          />
          <Text>Width: {resizedImage.width}</Text>
          <Text>Height: {resizedImage.height}</Text>
        </>
      ) : null}
    </ScrollView>
  );
};  
  
const styles = StyleSheet.create({
  scrollView: {
    backgroundColor: '#F5FCFF',
  },
  container: {
    paddingVertical: 100,
    paddingHorizontal: 10,
  },
  imageSourceButtonContainer: {
    marginBottom: 10,
  },
  welcome: {
    fontSize: 20,
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
  image: {
    height: 250,
    marginBottom: 10,
  },
  button: {
    backgroundColor: '#2596be',
    paddingHorizontal: 30,
    paddingVertical: 20,
    borderRadius: 10,
    alignItems: 'center',
  },
  optionContainer: {
    alignSelf: 'stretch',
    flexDirection: 'row',
    justifyContent: 'space-around',
    marginBottom: 10,
  },
  buttonOption: {
    backgroundColor: '#2596be',
    paddingHorizontal: 10,
    paddingVertical: 10,
    borderRadius: 10,
  },
  textInput: {
    height: 40,
    borderColor: 'black',
    borderWidth: 2,
    margin: 10,
    alignSelf: 'stretch',
    textAlign: 'center',
    overflow: 'hidden',
  },
});

export default ImageResizerDemo;    
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
    "@react-native-oh-tpl/react-native-image-resizer": "file:../../node_modules/@react-native-oh-tpl/react-native-image-resizer/harmony/image_resizer.har"
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

### 3. Configuring CMakeLists and Introducing ImageResizerPackage

Open `entry/src/main/ets/RNPackagesFactory.ts` and add the following code:

```diff
  ...
+ import {ImageResizerPackage} from '@react-native-oh-tpl/react-native-image-resizer/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImageResizerPackage(ctx)
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

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-image-resizer Releases](https://github.com/react-native-oh-library/react-native-image-resizer/releases)


## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description         | Type     | Required | Platform    | HarmonyOS Support |
|--------------------|---------------------|----------|----------|-------------|-------------------|
| createResizedImage | Resize local images | function | No       | Android/iOS | Yes               |

### createResizedImage parameters

| Name                 | Description         | Type    | Platform    | HarmonyOS Support |
|----------------------|---------------------|---------|-------------|-------------------|
| path                 | Path of image file, or a base64 encoded image string prefixed with 'data:image/imagetype' where imagetype is jpeg or png. | string  | Android/iOS | Yes               |
| width                | Width to resize to (see mode for more details) | number  | Android/iOS | Yes               |
| height               | Height to resize to (see mode for more details) | number  | Android/iOS | Yes               |
| compressFormat       | Can be either JPEG, PNG or WEBP. | string  | Android/iOS | Yes               |
| quality              | A number between 0 and 100. Used for the JPEG compression. | number  | Android/iOS | Yes               |
| rotation             | Rotation to apply to the image, in degrees. | number  | Android/iOS | Yes               |
| outputPath           | The resized image path. If null, resized image will be stored in cache folder. To set outputPath make sure to add option for rotation too (if no rotation is needed, just set it to 0). | string  | Android/iOS | Yes               |
| keepMeta             | If true, will attempt to preserve all file metadata/exif info, except the orientation value since the resizing also does rotation correction to the original image. Defaults to false, which means all metadata is lost. Note: This can only be true for JPEG images which are loaded from the file system (not Web). | boolean | Android/iOS | Yes               |
| options.mode         | Similar to react-native Image's resizeMode: either contain (the default), cover, or stretch. contain will fit the image within width and height, preserving its ratio. cover preserves the aspect ratio, and makes sure the image is at least width wide or height tall. stretch will resize the image to exactly width and height. | string  | Android/iOS | Yes               |
| options.onlyScaleDown | 	If true, will never enlarge the image, and will only make it smaller. | boolean | Android/iOS | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/bamlab/react-native-image-resizer/blob/master/LICENSE).