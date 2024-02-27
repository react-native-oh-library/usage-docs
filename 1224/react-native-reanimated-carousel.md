> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>react-native-transtiongroup</code> </h1>
</p>
<p align="center">
     <a href="https://github.com/dohooo/react-native-reanimated-carousel/blob/main/README.md">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
</p>


> [!tip] [Github 地址](https://github.com/dohooo/react-native-reanimated-carousel)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add react-native-reanimated-carousel
```

#### **npm**

```bash
npm install react-native-reanimated-carousel
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import * as React from "react";
import { ScrollView } from "react-native-gesture-handler";
import type { ICarouselInstance } from "react-native-reanimated-carousel";
import Carousel from "react-native-reanimated-carousel";
import { SafeAreaView } from "react-native-safe-area-context";

import SButton from "./components/SButton";
import { ElementsText, window } from "./constants";
import { useWindowDimensions, View, Text, Button } from "react-native";
import { useSharedValue } from "@react-native-oh-tpl/react-native-reanimated";

const PAGE_WIDTH = window.width;

function App() {
  const windowWidth = useWindowDimensions().width;
  const scrollOffsetValue = useSharedValue<number>(1);
  const [data, setData] = React.useState([...new Array(4).keys()]);
  const [isVertical, setIsVertical] = React.useState(false);
  const [isFast, setIsFast] = React.useState(false);
  const [isAutoPlay, setIsAutoPlay] = React.useState(true);
  const [isPagingEnabled, setIsPagingEnabled] = React.useState(true);
  const [value, setValue] = React.useState(0);
  const ref = React.useRef<ICarouselInstance>(null);

  const baseOptions = isVertical
    ? ({
      vertical: true,
      width: windowWidth,
      height: PAGE_WIDTH / 2,
    } as const)
    : ({
      vertical: false,
      width: windowWidth,
      height: PAGE_WIDTH / 2,
    } as const);

  return (
    <SafeAreaView edges={["bottom"]} style={{ flex: 1 }}>
      <Carousel
        {...baseOptions}
        loop
        enabled // Default is true, just for demo
        ref={ref}
        defaultScrollOffsetValue={scrollOffsetValue}
        testID={"xxx"}
        style={{ width: "100%" }}
        autoPlay={isAutoPlay}
        autoPlayInterval={isFast ? 100 : 2000}
        data={data}
        // onScrollStart={()=>{console.log('===1')}}
        onScrollEnd={() => { console.log('===2') }}

        // onConfigurePanGesture={g => g.enabled(false)}
        pagingEnabled={isPagingEnabled}
        onSnapToItem={index => setValue(index)}
        renderItem={({ index }) => {return <View
          key={index}
          style={{
            width: windowWidth,
            height: PAGE_WIDTH / 2,
            backgroundColor: "skyblue",
            justifyContent: "center",
            alignItems: "center",
          }}
        >
          <Text style={{ fontSize: 20, color: "white" }}>
            {`slide${value + 1}`}
          </Text>
        </View>}}
      />
      <ScrollView style={{ flex: 1 }}>
        <View
          style={{
            marginTop: 20,
            backgroundColor: "#26292E",
            borderRadius: 50,
            paddingLeft: 20,
            paddingRight: 20,
            padding: 10,
          }}>
          <Button
            title="Change the data length to 5"
            onPress={() => {
              setData([...new Array(5).keys()]);
            }}
          />
        </View>
        <View
          style={{
            marginTop: 20,
            backgroundColor: "#26292E",
            borderRadius: 50,
            paddingLeft: 20,
            paddingRight: 20,
            padding: 10,
          }}>
          <Button
            title="Change the data length to 3"
            onPress={() => {
              setData([...new Array(3).keys()]);
            }}
          />
        </View>
        <View
          style={{
            marginTop: 20,
            backgroundColor: "#26292E",
            borderRadius: 50,
            paddingLeft: 20,
            paddingRight: 20,
            padding: 10,
          }}>
          <Button
            title={isVertical ? "Set horizontal" : "Set Vertical"}
            onPress={() => {
              setIsVertical(!isVertical);
            }}
          />
        </View>
        <View
          style={{
            marginTop: 20,
            backgroundColor: "#26292E",
            borderRadius: 50,
            paddingLeft: 20,
            paddingRight: 20,
            padding: 10,
          }}>
          <Button
            title={isFast ? "NORMAL" : "FAST"}
            onPress={() => {
              setIsFast(!isFast);
            }}
          />
        </View>
        <View
          style={{
            marginTop: 20,
            backgroundColor: "#26292E",
            borderRadius: 50,
            paddingLeft: 20,
            paddingRight: 20,
            padding: 10,
          }}>
          <Button
            title={`PagingEnabled:${isPagingEnabled.toString()}`}
            onPress={() => {
              setIsPagingEnabled(!isPagingEnabled);
            }}
          />
        </View>
        <View
          style={{
            marginTop: 20,
            backgroundColor: "#26292E",
            borderRadius: 50,
            paddingLeft: 20,
            paddingRight: 20,
            padding: 10,
          }}>
          <Button
            title={`ElementsText.AUTOPLAY:${isAutoPlay}`}
            onPress={() => {
              setIsAutoPlay(!isAutoPlay);
            }}
          ></Button>
        </View>
        <View
          style={{
            marginTop: 20,
            backgroundColor: "#26292E",
            borderRadius: 50,
            paddingLeft: 20,
            paddingRight: 20,
            padding: 10,
          }}>
          <Button
            title="Log current index"
            onPress={() => {
              console.info("9999999999",ref.current?.getCurrentIndex());
            }}
          />
        </View>

        <View
          style={{
            marginTop: 20,
            backgroundColor: "#26292E",
            borderRadius: 50,
            paddingLeft: 20,
            paddingRight: 20,
            padding: 10,
          }}>
          <Button
            title={`Change-data-length-to:${data.length === 6 ? 8 : 6}`}
            onPress={() => {
              setData(
                data.length === 6
                  ? [...new Array(8).keys()]
                  : [...new Array(6).keys()],
              );
            }}
          />
        </View>
        <View
          style={{
            marginTop: 20,
            backgroundColor: "#26292E",
            borderRadius: 50,
            paddingLeft: 20,
            paddingRight: 20,
            padding: 10,
          }}>
          <Button
            title="prev"
            onPress={() => {
              ref.current?.scrollTo({ count: -1, animated: true });
            }}
          />
        </View>
        <View
          style={{
            marginTop: 20,
            backgroundColor: "#26292E",
            borderRadius: 50,
            paddingLeft: 20,
            paddingRight: 20,
            padding: 10,
          }}>
          <Button
            title="next"
            onPress={() => {
              ref.current?.scrollTo({ count: 1, animated: true });
            }}
          />
        </View>

      </ScrollView>
    </SafeAreaView>
  );
}

export default App;

```

## 约束与限制

## 兼容性

在下述版本验证通过:

IDE: Deveco Studio 4.1.3.500;

SDK: HarmonyOS NEXT Developer Preview1;

测试设备: Mate60 (BRA-AL00);

ROM: 204.1.0.59(SP2DEVC00E60R4P1) ;

RNOH: 0.72.12;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
> 详情见 [react-native-reanimated-carousel 源库地址](https://github.com/dohooo/react-native-reanimated-carousel/blob/main/README.md)

| 名称          | 描述                                                                          | 参数类型 | 是否必填 | Platform | HarmonyOS Support |
| ------------- | ---------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| data                             | 要显示的数据数组                                            | array    | yes      | All      | yes               |
| renderItem                       | 渲染每个项目的函数。接收一个参数 index，表示当前项的索引       | func     | yes      | All      | yes               |
| loop                             | 是否循环播放                                                | boolean  | yes      | All      | yes               |
| enabled                          | 是否启用轮播图功能                                          | boolean  | yes      | All      | yes              |
| autoPlay                         | 是否自动播放                                               | boolean   | yes      | All      | yes              |
| autoPlayInterval                 | 自动播放的时间间隔（以毫秒为单位）                           | number   | yes      | All      | yes              |
| defaultScrollOffsetValue         | 初始滚动偏移值                                             | number   | yes      | All      | yes              |
| onScrollStart                    | 滚动开始时的回调函数                                        | func     | yes      | All      | yes              |
| onScrollEnd                      | 滚动结束时的回调函数                                        | func     | yes      | All      | yes              |
| onSnapToItem                     | 切换到新项目时的回调函数。接收一个参数 index，表示新项目的索引 | func     | yes      | All      | yes              |
| pagingEnabled                    | 是否启用分页滚动                                            | boolean  | yes      | All      | yes              |
| scrollTo                         | 滚动到指定项的方法                                          | func     | yes      | All      | yes              |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/dohooo/react-native-reanimated-carousel/blob/main/LICENSE) ，请自由地享受和参与开源。