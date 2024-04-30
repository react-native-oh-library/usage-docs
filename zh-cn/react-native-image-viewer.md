> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-image-viewer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-image-viewer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-image-viewer/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-image-viewer)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-tpl/react-native-image-viewer> Releases](https://github.com/react-native-oh-library/react-native-image-viewer/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-image-viewer@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-image-viewer@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

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
  // 向下滑动的阈值
  const [flipThreshold, setFlipThreshold] = useState(0);
  // 页脚位置
  const [footerContainerStyle, setFlexooterContainerStyle] = useState(100);
  // 翻页动画时间
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
          <Button title="清空" onPress={clearBtn} />
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

## 兼容性

在以下版本验证通过

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## 属性

| Name                   | Description                                                                                                                                                                                                                          | Type                                                                                                                             | Required                                                   | Platform    | HarmonyOS Support | Remark                                   |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------- | ----------- | ----------------- | ---------------------------------------- |
| imageUrls              | Image Source                                                                                                                                                                                                                         | array                                                                                                                            | yes                                                        | Android IOS | YES               |                                          |
| enableImageZoom        | Enable image zoom                                                                                                                                                                                                                    | boolean                                                                                                                          | no                                                         | Android IOS | NO                |                                          |
| onShowModal            | The callback for show modal                                                                                                                                                                                                          | function <br />(content?: JSX.Element) => void                                                                                   | no                                                         | NO          | NO                | 此属性在HarmonyOS，Android ，IOS均不生效 |
| onCancel               | The callback for cancel modal                                                                                                                                                                                                        | function <br />() => void                                                                                                        | no                                                         | Android IOS | YES               |                                          |
| flipThreshold          | Swipe threshold of the next page                                                                                                                                                                                                     | number                                                                                                                           | no                                                         | Android IOS | YES               |                                          |
| maxOverflow            | The X position maximum, that current page can slide to the next page                                                                                                                                                                 | number                                                                                                                           | no                                                         | Android IOS | YES               |                                          |
| index                  | Init index of images                                                                                                                                                                                                                 | number                                                                                                                           | no                                                         | Android IOS | YES               |                                          |
| failImageSource        | placeholder for fail                                                                                                                                                                                                                 | string, object<br />{url: string}                                                                                                | no                                                         | Android IOS | YES               |                                          |
| loadingRender          | placeholder for loading                                                                                                                                                                                                              | function<br />() => React.ReactElement<any>                                                                                      | no                                                         | Android IOS | YES               |                                          |
| onSaveToCamera         | The callback for save to camera                                                                                                                                                                                                      | function<br />(index?: number => void                                                                                            | no                                                         | Android IOS | YES               |                                          |
| onChange               | When the image changed                                                                                                                                                                                                               | function<br />(index?: number => void                                                                                            | no                                                         | Android IOS | YES               |                                          |
| onMove                 | ()=> {}                                                                                                                                                                                                                              | ( position: [IOnMove](https://github.com/ascoders/react-native-image-zoom/blob/master/src/image-zoom/image-zoom.type.ts) )=>void | reports movement position data (helpful to build overlays) | Android IOS | YES               |                                          |
| saveToLocalByLongPress | Enable save to camera when long press                                                                                                                                                                                                | boolean                                                                                                                          | no                                                         | Android IOS | YES               |                                          |
| onClick                | Onclick                                                                                                                                                                                                                              | function<br />(onCancel?: function) => void                                                                                      | no                                                         | Android IOS | YES               |                                          |
| onDoubleClick          | OnDoubleClick                                                                                                                                                                                                                        | function<br />(onCancel?: function) => void                                                                                      | no                                                         | Android IOS | YES               |                                          |
| onSave                 | The picture is saved to the local method, if you write this method will not call the system default method for Android does not support saveToCameraRoll remote picture, you can call this callback in Android call native interface | function<br />(url: string) => void                                                                                              | no                                                         | Android IOS | YES               |                                          |
| renderHeader           | Custom header                                                                                                                                                                                                                        | function<br />(currentIndex?: number) => React.ReactElement<any>                                                                 | no                                                         | Android IOS | YES               |                                          |
| renderFooter           | Custom footer                                                                                                                                                                                                                        | function<br />(currentIndex?: number) => React.ReactElement<any>                                                                 | no                                                         | Android IOS | YES               |                                          |
| renderIndicator        | Custom indicator                                                                                                                                                                                                                     | function<br />`(currentIndex?: number, allSize?) => React.ReactElement<any>`: number                                             | no                                                         | Android IOS | YES               |                                          |
| renderImage            | Custom image component                                                                                                                                                                                                               | function<br />(props: any) => React.ReactElement<any>                                                                            | no                                                         | Android IOS | YES               |                                          |
| renderArrowLeft        | Custom left arrow                                                                                                                                                                                                                    | function<br />() => React.ReactElement<any>                                                                                      | no                                                         | Android IOS | YES               |                                          |
| renderArrowRight       | Custom right arrow                                                                                                                                                                                                                   | function<br />() => React.ReactElement<any>                                                                                      | no                                                         | Android IOS | YES               |                                          |
| onSwipeDown            | Callback for swipe down                                                                                                                                                                                                              | function<br />() => void                                                                                                         | no                                                         | Android IOS | YES               |                                          |
| footerContainerStyle   | custom style props for container that will be holding your footer that you pass                                                                                                                                                      | object<br />{someStyle: someValue}                                                                                               | no                                                         | Android IOS | YES               |                                          |
| backgroundColor        | Component background color                                                                                                                                                                                                           | string<br />white                                                                                                                | no                                                         | Android IOS | YES               |                                          |
| enableSwipeDown        | Enable swipe down to close image viewer. When swipe down, will trigger onCancel.                                                                                                                                                     | boolean                                                                                                                          | no                                                         | Android IOS | YES               |                                          |
| swipeDownThreshold     | Threshold for firing swipe down function                                                                                                                                                                                             | number                                                                                                                           | no                                                         | Android IOS | YES               |                                          |
| doubleClickInterval    | Double click interval.                                                                                                                                                                                                               | number                                                                                                                           | no                                                         | Android IOS | YES               |                                          |
| pageAnimateTime        | Set the animation time for page flipping.                                                                                                                                                                                            | number                                                                                                                           | no                                                         | Android IOS | YES               |                                          |
| enablePreload          | Preload the next image                                                                                                                                                                                                               | boolean                                                                                                                          | no                                                         | Android IOS | YES               |                                          |
| useNativeDriver        | Whether to animate using [`useNativeDriver`](https://reactnative.dev/docs/animations#using-the-native-driver)                                                                                                                        | boolean                                                                                                                          | no                                                         | Android IOS | YES               |                                          |
| menus                  | Custom menus, with 2 methods:`cancel` to hide menus and `saveToLocal` to save image to camera                                                                                                                                        | function<br />({cancel,saveToLocal}) => React.ReactElement<any>                                                                  | no                                                         | Android IOS | YES               |                                          |
| menuContext            | Custom menu context.                                                                                                                                                                                                                 | object<br />{someKey: someValue}                                                                                                 | no                                                         | Android IOS | YES               |                                          |

## 遗留问题

- [ ] 本库 CameraRoll.saveToCameraRoll 还未完全鸿蒙化，暂不支持调起相册 （未解决）[#I99NUM](https://gitee.com/chenchen2019710/usage-docs/issues/I99NUM)
- [ ] 本库依赖 react-native-image-zoom ,enableImageZoom属性还未完全鸿蒙化（未解决）[#I99NP7](https://gitee.com/wuyasmile/usage-docs/issues/I99NP7)
- [ ] 本库依赖 react-native-image-zoom ,长按触发框架图片拖拽，应用崩溃（未解决）[#I99NQ7](https://gitee.com/wuyasmile/usage-docs/issues/I99NQ7)

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/react-native-oh-library/react-native-image-viewer/blob/sig/LICENSE) ，请自由地享受和参与开源。
