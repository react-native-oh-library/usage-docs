> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-viewing</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jobtoday/react-native-image-viewing/blob/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jobtoday/react-native-image-viewing/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-image-viewing)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-image-viewing Releases](https://github.com/react-native-oh-library/react-native-image-viewing/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

Go to the project directory and execute the following instruction:

#### npm

```bash
npm install @react-native-oh-tpl/react-native-image-viewing@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-image-viewing@file:#
```

quick use:

```js
import React, { useState } from "react";
import {
  Alert,
  Platform,
  SafeAreaView,
  StatusBar,
  StyleSheet,
  Text,
  View,
  Image, ScrollView, TouchableOpacity
} from "react-native";
import memoize from "lodash/memoize";
import get from "lodash/get";
import ImageViewing from "react-native-image-viewing";
import {ImageSource} from "react-native-image-viewing/dist/@types"

type Props = {
  images: string[];
  onPress: (index: number) => void;
  shift?: number;
};

const IMAGE_WIDTH = 120;
const IMAGE_HEIGH = 120;

const architecture = [
  {
    thumbnail: "https://img.zcool.cn/community/01d191576ccecb0000018c1b64e382.jpg@1280w_1l_2o_100sh.jpg",
    original: "https://img.zcool.cn/community/01d191576ccecb0000018c1b64e382.jpg@1280w_1l_2o_100sh.jpg",
  },
  {
    thumbnail: "https://p0.ssl.qhimgs1.com/sdr/400__/t0461b1cfd7e4ef2b66.jpg",
    original: "https://p0.ssl.qhimgs1.com/sdr/400__/t0461b1cfd7e4ef2b66.jpg",
  },
  {
    thumbnail: "https://p0.ssl.qhimgs1.com/sdr/400__/t017c44dc545b663cce.jpg",
    original: "https://p0.ssl.qhimgs1.com/sdr/400__/t017c44dc545b663cce.jpg",
  }
];


const ImageList = ({ images, shift = 0, onPress }: Props) => (
  <ScrollView
    horizontal
    style={styles1.root}
    contentOffset={{ x: shift * IMAGE_WIDTH, y: 0 }}
    contentContainerStyle={styles1.container}
  >
    {images.map((imageUrl, index) => (
      <TouchableOpacity
        style={styles1.button}
        key={`${imageUrl}_${index}`}
        activeOpacity={0.8}
        onPress={() => onPress(index)}
      >
        {
          typeof imageUrl === 'string' ? <Image source={{ uri: imageUrl }} key={`${index}`} style={styles1.image} /> : <Image source={ imageUrl } key={`${index}`} doubleTapToZoomEnabled={true} style={styles1.image} />
        }
      </TouchableOpacity>
    ))}
  </ScrollView>
);

const styles1 = StyleSheet.create({
  root: { flexGrow: 0 },
  container: {
    flex: 0,
    paddingLeft: 10,
    marginBottom: 10
  },
  button: {
    marginRight: 10
  },
  image: {
    width: IMAGE_WIDTH,
    height: IMAGE_HEIGH,
    borderRadius: 10
  }
});

function App() {
  const [currentImageIndex, setImageIndex] = useState(0);
  const [images, setImages] = useState(architecture);
  const [isVisible, setIsVisible] = useState(false);

  const onSelect = (images, index) => {
    setImageIndex(index);
    setImages(images);
    setIsVisible(true);
  };

  const onRequestClose = () => setIsVisible(false);


  const getImageSource = memoize((images): ImageSource[] =>
    images.map((image) =>
      typeof image.original === "number"
        ? image.original
        : { uri: image.original as string }
    )
  );

  return (
    <SafeAreaView style={styles.root}>
      <ImageList
        images={architecture.map((image) => image.thumbnail)}
        onPress={(index) => onSelect(architecture, index)}
        shift={0.75}
      />
      <ImageViewing
        images={getImageSource(images)}
        imageIndex={currentImageIndex}
        visible={isVisible}
        onRequestClose={onRequestClose}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  root: {
    flex: 1,
    backgroundColor: "#000",
    ...Platform.select({
      android: { paddingTop: StatusBar.currentHeight },
      default: null,
    }),
  },
  about: {
    flex: 1,
    marginTop: -12,
    alignItems: "center",
    justifyContent: "center",
  },
  name: {
    textAlign: "center",
    fontSize: 24,
    fontWeight: "200",
    color: "#FFFFFFEE",
  },
});

```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-image-viewing Releases](https://github.com/react-native-oh-library/react-native-image-viewing/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                   | Description                                                                                 | Type                                                        | Platform | Required | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------- | -------- | -------- | ----------------- |
| images                 | Array of images to display                                                                  | ImageSource[]                                               | All      | Yes      | Yes               |
| keyExtractor           | Uniqely identifying each image                                                              | (imageSrc: ImageSource, index: number) => string            | All      | No       | Yes               |
| imageIndex             | Current index of image to display                                                           | number                                                      | All      | Yes      | Yes               |
| visible                | Is modal shown or not                                                                       | boolean                                                     | All      | No       | Yes               |
| onRequestClose         | Function called to close the modal                                                          | function                                                    | All      | Yes      | Yes               |
| onImageIndexChange     | Function called when image index has been changed                                           | function                                                    | All      | No       | Yes               |
| onLongPress            | Function called when image long pressed                                                     | function (event: GestureResponderEvent, image: ImageSource) | All      | No       | Yes               |
| delayLongPress         | Delay in ms, before onLongPress is called: default                                          | number                                                      | All      | No       | Yes               |
| animationType          | Animation modal presented with: default                                                     | none, fade, slide                                           | All      | No       | Yes               |
| presentationStyle      | Modal presentation style: default: fullScreen Android: Use overFullScreen to hide StatusBar | fullScreen, pageSheet, formSheet, overFullScreen            | All      | No       | Yes               |
| backgroundColor        | Background color of the modal in HEX                                                        | string                                                      | All      | No       | Yes               |
| swipeToCloseEnabled    | Close modal with swipe up or down: default                                                  | boolean                                                     | All      | No       | No                |
| doubleTapToZoomEnabled | Zoom image by double tap on it: default                                                     | boolean                                                     | All      | No       | No                |
| HeaderComponent        | Header component, gets current imageIndex as a prop                                         | component, function                                         | All      | No       | Yes               |
| FooterComponent        | Footer component, gets current imageIndex as a prop                                         | component, function                                         | All      | No       | Yes               |

## Known Issues

- [x] 组件上下滑动关闭暂未实现，由于 scrollView 的 naticeEvent.velocityPropertiesHarmonyOS 暂不支持 [issue#6](https://github.com/react-native-oh-library/react-native-image-viewing/issues/6)
- [x] 组件双击放大方法暂未实现，由于 doubleTapToZoomEnabledPropertiesHarmonyOS 暂不支持 [issue#7](https://github.com/react-native-oh-library/react-native-image-viewing/issues/7)
- [x] 组件 animationType 淡入淡出效果暂未实现，由于 modal 组件未适配 [issue#8](https://github.com/react-native-oh-library/react-native-image-viewing/issues/8)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/jobtoday/react-native-image-viewing/blob/master/LICENSE).
