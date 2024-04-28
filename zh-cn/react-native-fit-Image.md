模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-fit-image</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/huiseoul/react-native-fit-image">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/huiseoul/react-native-fit-image)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-fit-image@1.5.5
```

#### **yarn**

```bash
yarn add react-native-fit-image@1.5.5
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useState, useEffect } from "react";
import {
  View,
  StyleSheet,
  Text,
  ScrollView,
  SafeAreaView,
  Image,
  Button,
} from "react-native";
import FitImage from "react-native-fit-image";
var styles = StyleSheet.create({
  fitImage: {
    borderRadius: 20,
    borderColor: "red",
    borderWidth: 1,
  },
  fitImageWithSize: {
    height: 200,
    width: "100%",
  },
});
const FitImageDemo = () => {
  // 测试onLoad
  const [onLoadDatea, setOnLoad] = useState("初始onLoad未执行");
  // 测试onError
  const [onErrorDatea, setOnError] = useState("初始onError未执行");
  // 测试onLoadStart
  const [onLoadStartDatea, setOnLoadStart] =
    useState("未执行前onLoadStart未执行");
  // 测试onLayOut
  const [onLayOutData, setOnLayout] = useState("未执行前onLayout未执行");
  // 刷新按钮
  const [refLoadData, setRefLoadBtn] = useState(true);
  // 获取本地图片尺寸
  const [imgSizeNum, getImageSizeNum] = useState({ width: 0, height: 0 });
  const img1 = require("./assets/expo.png");
  const getImageSize = () => {
    let res = Image.resolveAssetSource(img1);
    getImageSizeNum({ width: res.width, height: res.height });
  };
  // 获取网络图片尺寸
  const imgHttp = {
    uri: "https://octodex.github.com/images/stormtroopocat.jpg",
  };
  const [imgHttpSize, getHttpSizeNum] = useState({ width: 0, height: 0 });
  // 刷新
  const [reshUiData, setReshUi] = useState(0);
  useEffect(() => {
    getReloadFres();
  }, []);
  const getReloadFres = () => {
    // http远程文件
    Image.getSize(
      imgHttp.uri,
      (width, height) => {
        getHttpSizeNum({ width, height });
      },
      (failure) => {
        console.log("failure", failure);
      },
    );
  };
  //  刷新
  const reLoadFun = () => {
    setRefLoadBtn(false);
    setReshUi(reshUiData + 1);
    getImageSizeNum({ width: 0, height: 0 });
    getHttpSizeNum({ width: 0, height: 0 });
    setRefLoadBtn(true);
    getReloadFres();
  };
  return (
    <SafeAreaView>
      <ScrollView>
        {/* button刷新按钮方便压力测试 */}
        <Button
          onPress={() => {
            reLoadFun();
          }}
          title="刷新"
        ></Button>
        {refLoadData && (
          <View style={{ width: "100%", height: "100%" }}>
            <Text>刷新了{reshUiData}次</Text>
            <View>
              <Text>测试onLoad</Text>
              <Text>{onLoadDatea}</Text>
              <FitImage
                onLoad={() => {
                  console.log("执行了onLoad");
                  setOnLoad("执行了onLoad");
                }}
                style={styles.fitImageWithSize}
                source={require("./assets/expo.png")}
              />
            </View>
            <View>
              <Text>测试base64图片</Text>
              <FitImage
                source={{
                  uri: "data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADMAAAAzCAYAAAA6oTAqAAAAEXRFWHRTb2Z0d2FyZQBwbmdjcnVzaEB1SfMAAABQSURBVGje7dSxCQBACARB+2/ab8BEeQNhFi6WSYzYLYudDQYGBgYGBgYGBgYGBgYGBgZmcvDqYGBgmhivGQYGBgYGBgYGBgYGBgYGBgbmQw+P/eMrC5UTVAAAAABJRU5ErkJggg==",
                }}
                style={{ ...styles.fitImageWithSize }}
              />
            </View>
            <View>
              <Text>
                测试属性originalWidth，originalHeight（在不加宽度高度的情况下）
              </Text>
              <FitImage
                source={require("./assets/expo.png")}
                originalWidth={400}
                originalHeight={400}
              />
            </View>
            <View>
              <Text>
                不加originalWidth，originalHeight和不加宽度高度的情况下
              </Text>
              <FitImage source={require("./assets/expo.png")} />
            </View>
            <View>
              <Text>
                不加originalWidth，originalHeight但是加宽度高度的情况下
              </Text>
              <FitImage
                source={require("./assets/expo.png")}
                style={{ ...styles.fitImageWithSize }}
              />
            </View>
            <View>
              <Text>
                不加originalWidth，originalHeight但是加宽度高度的情况下的网络图片
              </Text>
              <FitImage
                source={{
                  uri: "https://octodex.github.com/images/stormtroopocat.jpg",
                }}
                style={{ ...styles.fitImageWithSize }}
              />
            </View>
            <View>
              <Text>
                加originalWidth，originalHeight但是不加宽度高度的情况下的网络图片
              </Text>
              <FitImage
                source={{
                  uri: "https://octodex.github.com/images/stormtroopocat.jpg",
                }}
                originalWidth={400}
                originalHeight={400}
              />
            </View>
            <View>
              <Text>同时加originalWidth，originalHeight和宽度高度的情况下</Text>
              <FitImage
                source={require("./assets/expo.png")}
                originalWidth={400}
                originalHeight={400}
                style={{ ...styles.fitImageWithSize }}
              />
            </View>
            <View>
              <View>
                <Text>
                  indicator(加载器 为true) indicatorColor(加载器颜色)
                  indicatorSize(值：large small number)
                </Text>
                <Text>值为：large</Text>
                <FitImage
                  indicator={true}
                  indicatorColor="red"
                  indicatorSize="large"
                  style={{ ...styles.fitImageWithSize }}
                  source={require("./assets/expo.png")}
                />
              </View>
              <View>
                <Text>
                  indicator(加载器 为true) indicatorColor(加载器颜色)
                  indicatorSize(值：large small number)
                </Text>
                <Text>small</Text>
                <FitImage
                  indicator={true}
                  indicatorColor="red"
                  indicatorSize="small"
                  style={{ ...styles.fitImageWithSize }}
                  source={require("./assets/expo.png")}
                />
              </View>
              <View>
                <Text>
                  indicator(加载器 为true) indicatorColor(加载器颜色)
                  indicatorSize(值：large small number)
                </Text>
                <Text>number:值越大指示器越大</Text>
                <FitImage
                  indicator={true}
                  indicatorColor="red"
                  indicatorSize={100}
                  style={{ ...styles.fitImageWithSize }}
                  source={require("./assets/expo.png")}
                />
              </View>
              <View>
                <Text>indicator(加载器 为false) </Text>
                <Text>number:值越大指示器越大</Text>
                <FitImage
                  indicator={false}
                  style={{ ...styles.fitImageWithSize }}
                  source={require("./assets/expo.png")}
                />
              </View>
            </View>
            <View>
              <Text>验证网络图片</Text>
              <FitImage
                style={styles.fitImageWithSize}
                source={{
                  uri: "https://octodex.github.com/images/stormtroopocat.jpg",
                }}
              />
            </View>
            <View>
              <Text>获取本地图片宽高</Text>
              <FitImage
                style={styles.fitImageWithSize}
                source={require("./assets/expo.png")}
              />
              <Text>
                宽度：{imgSizeNum.width},高度：{imgSizeNum.height}
              </Text>
              <Button
                onPress={() => {
                  getImageSize();
                }}
                title="调用image图片宽高"
              ></Button>
            </View>
            <View>
              <Text>验证网络图片宽高</Text>
              <Text>
                宽度：{imgHttpSize.width},高度：{imgHttpSize.height}
              </Text>
              <FitImage
                style={{ ...styles.fitImageWithSize, ...styles.fitImage }}
                source={{
                  uri: "https://octodex.github.com/images/stormtroopocat.jpg",
                }}
              />
            </View>
            <View>
              <Text>验证图片圆角</Text>
              <FitImage
                style={{ ...styles.fitImageWithSize, ...styles.fitImage }}
                source={require("./assets/expo.png")}
              />
            </View>
            <View>
              <Text>
                测试resizeMode(cover contain stretch repeat center)，值为cover
              </Text>
              <FitImage
                resizeMode="cover"
                style={{ ...styles.fitImageWithSize }}
                source={require("./assets/expo.png")}
              />
            </View>
            <View>
              <Text>
                测试resizeMode(cover contain stretch repeat center)，值为contain
              </Text>
              <FitImage
                resizeMode="contain"
                style={{ ...styles.fitImageWithSize }}
                source={require("./assets/expo.png")}
              />
            </View>
            <View>
              <Text>
                测试resizeMode(cover contain stretch repeat center)，值为stretch
              </Text>
              <FitImage
                resizeMode="stretch"
                style={{ ...styles.fitImageWithSize }}
                source={require("./assets/expo.png")}
              />
            </View>
            <View>
              <Text>
                测试resizeMode(cover contain stretch repeat center)，值为repeat
              </Text>
              <FitImage
                resizeMode="repeat"
                style={{ ...styles.fitImageWithSize }}
                source={require("./assets/expo.png")}
              />
            </View>
            <View>
              <Text>
                测试resizeMode(cover contain stretch repeat center)，值为center
              </Text>
              <FitImage
                resizeMode="center"
                style={{ ...styles.fitImageWithSize }}
                source={require("./assets/expo.png")}
              />
            </View>

            <View>
              <Text>测试onError</Text>
              <Text>{onErrorDatea}</Text>
              <FitImage
                onError={() => {
                  console.log("执行了onError");
                  setOnError("执行了onError");
                }}
                style={styles.fitImageWithSize}
                source={{ uri: "https://ok.gitHub.io123.png" }}
              />
            </View>
            <View>
              <Text>测试onLoadStart</Text>
              <Text>{onLoadStartDatea}</Text>
              <FitImage
                onLoadStart={() => {
                  console.log("执行了onLoadStart");
                  setOnLoadStart("执行了onLoadStart");
                }}
                style={{ ...styles.fitImageWithSize, borderRadius: 20 }}
                source={require("./assets/expo.png")}
              />
            </View>
            <View>
              <Text>测试onLayOut</Text>
              <Text>{onLayOutData}</Text>
              <FitImage
                onLoadStart={() => {
                  console.log("执行了onLayout");
                  setOnLayout("执行了onLayout");
                }}
                style={{ ...styles.fitImageWithSize, borderRadius: 20 }}
                source={require("./assets/expo.png")}
              />
            </View>
            <View>
              <Text>测试blurRadius(模糊滤镜，值越大越模糊)</Text>
              <FitImage
                source={require("./assets/expo.png")}
                blurRadius={20}
                style={{ ...styles.fitImage, ...styles.fitImageWithSize }}
              />
            </View>
          </View>
        )}
        {!refLoadData && (
          <View style={{ width: "100%", height: "100%" }}>
            <Text>加载中。。。。。。</Text>
          </View>
        )}
      </ScrollView>
    </SafeAreaView>
  );
};
export default FitImageDemo;
```

## 兼容性

在以下版本验证通过

1. RNOH：0.72.13; SDK：HarmonyOS NEXT DP2; IDE：DevEco Studio 4.1.3.700; ROM：2.1.0.72;

## 属性

| Name               | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Type          | Required | Platform                      | HarmonyOS Support | 备注                                                                                                                   |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------- | -------- | ----------------------------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `style`            | 图片宽(width)高(height)，边框等样式                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              | object        | yes      | Android IOS                   | YES               | 在不加orginalWidth与orginalHeight属性时，style里面必须设置宽width，高height才能把图片加载出来                          |
| `source`           | 图片文件源： 本地图片 source={require('./assets/expo.png')}；<br />网略图片 source={{uri:"https://octodex.github.com/images/stormtroopocat.jpg"}}                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | string        | yes      | Android IOS                   | YES               |                                                                                                                        |
| `width`            | 图片style中属性                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | number        | yes      | Android IOS                   | YES               |                                                                                                                        |
| `height`           | 图片style中属性                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | number        | yes      | Android IOS                   | YES               |                                                                                                                        |
| `borderRadius`     | 图片样式（圆角）                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | number        | No       | Android IOS HarmonyOS都不支持 | NO                | 此属性在HarmonyOS，Android ，IOS均不生效;[issues](https://github.com/huiseoul/react-native-fit-image/issues/111)       |
| `indicator`        | 加载器值为true/false (默认true)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | boolean       | No       | Android IOS                   | YES               |                                                                                                                        |
| `indicatorColor`   | 加载器颜色                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | string        | No       | Android IOS                   | YES               |                                                                                                                        |
| `indicatorSize`    | 加载器大小 值：`large` `small` number(例: indicatorSize={20} )                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | string/number | No       | Android IOS                   | YES               |                                                                                                                        |
| resizeMode         | 图片布局 值(cover contain stretch repeat center) `cover`: 在保持图片宽高比的前提下缩放图片，直到宽度和高度都大于等于容器视图的尺寸（如果容器有 padding 内衬的话，则相应减去）。**译注**：这样图片完全覆盖甚至超出容器，容器中不留任何空白。 `contain`: 在保持图片宽高比的前提下缩放图片，直到宽度和高度都小于等于容器视图的尺寸（如果容器有 padding 内衬的话，则相应减去）。**译注**：这样图片完全被包裹在容器中，容器中可能留有空白。 `stretch`: 拉伸图片且不维持宽高比，直到宽高都刚好填满容器。 `repeat`: 重复平铺图片直到填满容器。图片会维持原始尺寸，但是当尺寸超过容器时会在保持宽高比的前提下缩放到能被容器包裹。 `center`: 居中不拉伸。 | string        | No       | Android IOS                   | YES               |                                                                                                                        |
| blurRadius         | 图片模糊滤镜（值越大越模糊）                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | number        | No       | Android IOS                   | YES               |                                                                                                                        |
| onLoad             | 图片加载成功回调                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Function      | No       | Android IOS                   | YES               |                                                                                                                        |
| resolveAssetSource | 获取本地图片宽高 用法：const img1 = require('./assets/expo.png') let res = Image.resolveAssetSource(img1)                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Function      | No       | Android IOS                   | YES               |                                                                                                                        |
| getSize            | 获取网略图片尺寸：Image.getSize(uri,(width,height)=>{},(fail)=>{})                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Function      | No       | Android IOS                   | YES               |                                                                                                                        |
| onError            | 获取图片资源出错                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 | Function      | No       | Android IOS HarmonyOS都不支持 | NO                | [issues](https://github.com/huiseoul/react-native-fit-image/issues/76)；在原库中作者已经说明Some props are not working |
| onLoadStart        | 资源刚加载时候                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Function      | NO       | Android IOS HarmonyOS都不支持 | NO                | [issues](https://github.com/huiseoul/react-native-fit-image/issues/76)；在原库中作者已经说明Some props are not working |
| onLayout           | 资源改变尺寸或者加载时                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           | Function      | NO       | Android IOS HarmonyOS都不支持 | NO                | [issues](https://github.com/huiseoul/react-native-fit-image/issues/76)；在原库中作者已经说明Some props are not working |
| orginalWidth       | 图片原始宽度                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | number        | NO       | Android IOS                   | YES               |                                                                                                                        |
| orginalHeight      | 图片原始高度                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | number        | NO       | Android IOS                   | YES               |                                                                                                                        |

## 原库已知问题

1. 在react-native-fit-image三方库中`onError`.`onLoadStart`.`onLayout`回调方法，在原库文档（react-native-fit-image）作者已说明并没有适配（Some props are not working），有待开发[issues](https://github.com/huiseoul/react-native-fit-image/issues/76)
2. `borderRadius`图片圆角属性，在鸿蒙，ios，安卓均不支持，官方文档互动有提到borderRadius不生效;[issues](https://github.com/huiseoul/react-native-fit-image/issues/111)

## 其他
