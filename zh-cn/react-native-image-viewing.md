<!-- {% raw %} -->
> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-image-viewing</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-image-viewer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-image-viewer/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-viewing)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-tpl/react-native-image-viewing> Releases](https://github.com/react-native-oh-library/react-native-image-viewing/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

进入到工程目录并输入以下命令：

#### npm

```bash
npm install @react-native-oh-tpl/react-native-image-viewing@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-image-viewing@file:#
```

快速使用：

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
        <Image source={{ uri: imageUrl }} style={styles1.image} />
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

## 兼容性

在下述版本验证通过:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## API列表

| Name                   | Description                                                                                 | Type                                                        | Required | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------------------------------------- | ----------------------------------------------------------- | -------- | ----------------- |
| images                 | Array of images to display                                                                  | ImageSource[]                                               | Yes      | Yes               |
| keyExtractor           | Uniqely identifying each image                                                              | (imageSrc: ImageSource, index: number) => string            | No       | Yes               |
| imageIndex             | Current index of image to display                                                           | number                                                      | Yes      | Yes               |
| visible                | Is modal shown or not                                                                       | boolean                                                     | No       | Yes               |
| onRequestClose         | Function called to close the modal                                                          | function                                                    | Yes      | Yes               |
| onImageIndexChange     | Function called when image index has been changed                                           | function                                                    | No       | Yes               |
| onLongPress            | Function called when image long pressed                                                     | function (event: GestureResponderEvent, image: ImageSource) | No       | Yes               |
| delayLongPress         | Delay in ms, before onLongPress is called: default                                          | number                                                      | No       | Yes               |
| animationType          | Animation modal presented with: default                                                     | none, fade, slide                                           | No       | Yes               |
| presentationStyle      | Modal presentation style: default: fullScreen Android: Use overFullScreen to hide StatusBar | fullScreen, pageSheet, formSheet, overFullScreen            | No       | Yes               |
| backgroundColor        | Background color of the modal in HEX                                                        | string                                                      | No       | Yes               |
| swipeToCloseEnabled    | Close modal with swipe up or down: default                                                  | boolean                                                     | No       | Yes               |
| doubleTapToZoomEnabled | Zoom image by double tap on it: default                                                     | boolean                                                     | No       | Yes               |
| HeaderComponent        | Header component, gets current imageIndex as a prop                                         | component, function                                         | No       | Yes               |
| FooterComponent        | Footer component, gets current imageIndex as a prop                                         | component, function                                         | No       | Yes               |

## 遗留问题

- [ ] 本库 swipeToCloseEnabled，doubleTapToZoomEnabled，animationType 还未完全HarmonyOS化，暂不支持上下滑动关闭、双击放大与动画效果功能 （未解决）[#I9DNQU](https://gitee.com/react-native-oh-library/usage-docs/issues/I9DQPA)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/facebook/prop-types/blob/v15.8.1/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->