<!-- {% raw %} -->
> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-zoom-viewer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ascoders/react-native-image-viewer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ascoders/react-native-image-viewer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-image-viewer)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-image-zoom-viewer Releases](https://github.com/react-native-oh-library/react-native-image-viewer/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-image-zoom-viewer@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-image-zoom-viewer@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```tsx
import React, { useState } from "react";
import {
  Text,
  View,
  Button,
  Image,
  ScrollView,
  StyleSheet,
} from "react-native";
import ImageViewer from "react-native-image-zoom-viewer";

const ReactImageZoon = () => {
  const [flipThreshold, setFlipThreshold] = useState(0);
  const [footerContainerStyle, setFlexooterContainerStyle] = useState(100);
  const [pageAnimateTimeA, setPageAnimateTime] = useState(0);

  const [changeStatus, setChangeStatus] = useState("");
  const renderHeaderFun = () => {
    return (
      <View style={{ backgroundColor: "red" }}>
        <Text style={{ backgroundColor: "red", color: "#fff", fontSize: 20 }}>
          自定义页头或页脚
        </Text>
      </View>
    );
  };

  const renderArrowLeftFun = () => {
    return (
      <View style={{ width: 20, height: 20 }}>
        <Image
          source={{
            uri: "https://bpic.51yuansu.com/pic2/cover/00/52/03/5816a254309d2_610.jpg",
          }}
          style={{ width: "100%", height: "100%" }}
        ></Image>
      </View>
    );
  };
  const renrenderArrowRightFun = () => {
    return (
      <View style={{ width: 20, height: 20 }}>
        <Image
          source={{
            uri: "https://pic.616pic.com/ys_img/00/13/60/slee3clqRZ.jpg",
          }}
          style={{ width: "100%", height: "100%" }}
        ></Image>
      </View>
    );
  };

  const renderIndicatorFn = (currentIndex?: number, allSize?: number) => {
    return (
      <View
        style={{
          position: "absolute",
          left: 0,
          right: 0,
          top: 38,
          zIndex: 99,
          backgroundColor: "red",
        }}
      >
        <Text style={{ color: "#fff" }}> {`${currentIndex}/${allSize}`}</Text>
      </View>
    );
  };

  const images = [
    {
      url: "",
      props: {
        // headers: ...
        source: require("./assets/1.png"),
      },
    },
    {
      url: "https://octodex.github.com/images/godotocat.png",
      props: {
        // headers: ...
      },
    },
    {
      url: "",
      props: {},
    },
  ];

  const clearBtn = () => {
    setChangeStatus("");
    setFlexooterContainerStyle(100);
    setPageAnimateTime(0);
  };
  return (
    <View style={{ width: "100%", height: "100%" }}>
      <ScrollView>
        <View>
          <Text>
            imageUrls enableImageZoom;index;saveToLocalByLongPress;
            backgroundColor,onChange;
            flipThreshold;renderIndicator;renderArrowRight
            renderArrowLeft;pageAnimateTime;renderHeader;renderFooter;
            onClick;footerContainerStyle;failImageSource
          </Text>
          <Text>保存到相机的回调onSaveToCamera</Text>
          <Text>查看更改的状态{changeStatus}</Text>
        </View>
        <View style={{ width: "100%", height: 500 }}>
          <ImageViewer
            image
            Urls={images}
            index={1}
            enableImageZoom={true}
            backgroundColor={"pink"}
            saveToLocalByLongPress={false}
            onSave={null}
            onSaveToCamera={() => {
              setChangeStatus("onSaveToCamera");
            }}
            onChange={() => {
              setChangeStatus("onChange");
            }}
            onClick={() => {
              setChangeStatus("onClick");
            }}
            flipThreshold={flipThreshold}
            renderArrowLeft={renderArrowLeftFun}
            renderArrowRight={renrenderArrowRightFun}
            pageAnimateTime={pageAnimateTimeA}
            renderHeader={renderHeaderFun}
            renderFooter={renderHeaderFun}
            renderIndicator={renderIndicatorFn}
            footerContainerStyle={{
              bottom: footerContainerStyle,
              position: "absolute",
              zIndex: 9999,
            }}
            failImageSource={{
              width: 300,
              height: 300,
              url: "https://octodex.github.com/images/Robotocat.png",
            }}
          />
        </View>
        <View style={styles.container}>
          <Button title="下一页滑动0" onPress={() => setFlipThreshold(0)} />
          <Button
            title="下一页滑动阈值1000"
            onPress={() => setFlipThreshold(1000)}
          />
          <Button
            title="页脚位置"
            onPress={() => setFlexooterContainerStyle(200)}
          />
          <Button title="Clear" onPress={clearBtn} />
        </View>
        <Text></Text>
        <Button
          title="翻页动画"
          onPress={() => setPageAnimateTime(500)}
        ></Button>
      </ScrollView>
    </View>
  );
};
const styles = StyleSheet.create({
  container: {
    flexDirection: "row",
    justifyContent: "space-around",
  },
});

export default ReactImageZoon;
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-image-zoom-viewer Releases](https://github.com/react-native-oh-library/react-native-image-viewer/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                   | Description                                                  | Type                                                         | Platform    | HarmonyOS Support | Remark                                   |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- | ----------------- | ---------------------------------------- |
| imageUrls              | Image Source                                                 | array                                                        | Android iOS | YES               |                                          |
| enableImageZoom        | Enable image zoom                                            | boolean                                                      | Android iOS | NO                |                                          |
| onShowModal            | The callback for show modal                                  | function <br />(content?: JSX.Element) => void               | NO          | NO                | 此属性在HarmonyOS，Android ，iOS均不生效 |
| onCancel               | The callback for cancel modal                                | function <br />() => void                                    | Android iOS | YES               |                                          |
| flipThreshold          | Swipe threshold of the next page                             | number                                                       | Android iOS | YES               |                                          |
| maxOverflow            | The X position maximum, that current page can slide to the next page | number                                                       | Android iOS | YES               |                                          |
| index                  | Init index of images                                         | number                                                       | Android iOS | YES               |                                          |
| failImageSource        | placeholder for fail                                         | string, object<br />{url: string}                            | Android iOS | YES               |                                          |
| loadingRender          | placeholder for loading                                      | function<br />() => React.ReactElement<any>                  | Android iOS | YES               |                                          |
| onSaveToCamera         | The callback for save to camera                              | function<br />(index?: number => void                        | Android iOS | YES               |                                          |
| onChange               | When the image changed                                       | function<br />(index?: number => void                        | Android iOS | YES               |                                          |
| onMove                 | ()=> {}                                                      | ( position: [onMove](https://github.com/ascoders/react-native-image-zoom/blob/master/src/image-zoom/image-zoom.type.ts) )=>void | Android iOS | YES               |                                          |
| saveToLocalByLongPress | Enable save to camera when long press                        | boolean                                                      | Android iOS | YES               |                                          |
| onClick                | Onclick                                                      | function<br />(onCancel?: function) => void                  | Android iOS | YES               |                                          |
| onDoubleClick          | OnDoubleClick                                                | function<br />(onCancel?: function) => void                  | Android iOS | YES               |                                          |
| onSave                 | The picture is saved to the local method, if you write this method will not call the system default method for Android does not support saveToCameraRoll remote picture, you can call this callback in Android call native interface | function<br />(url: string) => void                          | Android iOS | YES               |                                          |
| renderHeader           | Custom header                                                | function<br />(currentIndex?: number) => React.ReactElement<any> | Android iOS | YES               |                                          |
| renderFooter           | Custom footer                                                | function<br />(currentIndex?: number) => React.ReactElement<any> | Android iOS | YES               |                                          |
| renderIndicator        | Custom indicator                                             | function<br />`(currentIndex?: number, allSize?) => React.ReactElement<any>`: number | Android iOS | YES               |                                          |
| renderImage            | Custom image component                                       | function<br />(props: any) => React.ReactElement<any>        | Android iOS | YES               |                                          |
| renderArrowLeft        | Custom left arrow                                            | function<br />() => React.ReactElement<any>                  | Android iOS | YES               |                                          |
| renderArrowRight       | Custom right arrow                                           | function<br />() => React.ReactElement<any>                  | Android iOS | YES               |                                          |
| onSwipeDown            | Callback for swipe down                                      | function<br />() => void                                     | Android iOS | YES               |                                          |
| footerContainerStyle   | custom style props for container that will be holding your footer that you pass | object<br />{someStyle: someValue}                           | Android iOS | YES               |                                          |
| backgroundColor        | Component background color                                   | string<br />white                                            | Android iOS | YES               |                                          |
| enableSwipeDown        | Enable swipe down to close image viewer. When swipe down, will trigger onCancel. | boolean                                                      | Android iOS | YES               |                                          |
| swipeDownThreshold     | Threshold for firing swipe down function                     | number                                                       | Android iOS | YES               |                                          |
| doubleClickInterval    | Double click interval.                                       | number                                                       | Android iOS | YES               |                                          |
| pageAnimateTime        | Set the animation time for page flipping.                    | number                                                       | Android iOS | YES               |                                          |
| enablePreload          | Preload the next image                                       | boolean                                                      | Android iOS | YES               |                                          |
| useNativeDriver        | Whether to animate using [`useNativeDriver`](https://reactnative.dev/docs/animations#using-the-native-driver) | boolean                                                      | Android iOS | YES               |                                          |
| menus                  | Custom menus, with 2 methods:`cancel` to hide menus and `saveToLocal` to save image to camera | function<br />({cancel,saveToLocal}) => React.ReactElement<any> | Android iOS | YES               |                                          |
| menuContext            | Custom menu context.                                         | object<br />{someKey: someValue}                             | Android iOS | YES               |                                          |

## Known Issues

- [ ] 本库 CameraRoll.saveToCameraRoll 还未完全 HarmonyOS 化，暂不支持调起相册 （未解决）[issues#1](https://github.com/react-native-oh-library/react-native-image-viewer/issues/1)
- [ ] 本库依赖 react-native-image-zoom ,enableImageZoom属性还未完全 HarmonyOS 化（未解决）[issues#2](https://github.com/react-native-oh-library/react-native-image-viewer/issues/1)
- [ ] 本库依赖 react-native-image-zoom ,长按触发框架图片拖拽，应用崩溃（未解决）[issues#3](https://github.com/react-native-oh-library/react-native-image-viewer/issues/1)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ascoders/react-native-image-viewer/blob/master/LICENSE).

<!-- {% endraw %} -->

