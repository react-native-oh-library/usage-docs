> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-reanimated-carousel</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/dohooo/react-native-reanimated-carousel">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/dohooo/react-native-reanimated-carousel/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/dohooo/react-native-reanimated-carousel)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-reanimated-carousel@3.5.1
```

#### **yarn**

```bash
yarn add react-native-reanimated-carousel@3.5.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!TIP] 本示例依赖 react-native-gesture-handler、react-native-reanimated 库，参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)、[@react-native-oh-tpl/react-native-reanimated 文档](/zh-cn/react-native-reanimated.md)进行引入。

```ts
import React, { useState, useRef } from "react";
import { ScrollView } from "react-native-gesture-handler";
import type { ICarouselInstance } from "react-native-reanimated-carousel";
import Carousel from "react-native-reanimated-carousel";
import { View, Text, Button, Dimensions, SafeAreaView, StyleSheet } from "react-native";
import { useSharedValue } from "react-native-reanimated";

const PAGE_HEIGHT = Dimensions.get("window").height;
const PAGE_WIDTH = Dimensions.get("window").width;

export function ReanimatedCarouselExample() {
	const scrollOffsetValue = useSharedValue<number>(1);
	const [data, setData] = useState([...new Array(4).keys()]);
	const [isVertical, setIsVertical] = useState(false);
	const [isFast, setIsFast] = useState(false);
	const [isAutoPlay, setIsAutoPlay] = useState(true);
	const [isPagingEnabled, setIsPagingEnabled] = useState(true);
	const [value, setValue] = useState(0);
	const ref = useRef<ICarouselInstance>(null);

	return (
		<SafeAreaView edges={["bottom"]} style={{ flex: 1 }}>
			<Carousel
				ref={ref}
				width={PAGE_WIDTH}
				height={PAGE_HEIGHT / 2}
				loop
				enabled // Default is true, just for demo
				defaultScrollOffsetValue={scrollOffsetValue}
				testID={"testBox"}
				vertical={isVertical}
				autoPlay={isAutoPlay}
				autoPlayInterval={isFast ? 200 : 2000}
				data={data}
				pagingEnabled={isPagingEnabled}
				onSnapToItem={(index) => setValue(index)}
				renderItem={({ index }) => {
					return (
						<View
							key={index}
							style={{
								width: PAGE_WIDTH,
								height: PAGE_HEIGHT / 2,
								...styles.swiperView
							}}
						>
							<Text style={{ fontSize: 20, color: "white" }}>{`slide${value + 1}`}</Text>
						</View>
					);
				}}
			/>
			<ScrollView style={{ flex: 1 }}>
				<View style={styles.optView}>
					<Button
						title="Change the data length to 5"
						onPress={() => {
							setData([...new Array(5).keys()]);
						}}
					/>
				</View>
				<View style={styles.optView}>
					<Button
						title="Change the data length to 3"
						onPress={() => {
							setData([...new Array(3).keys()]);
						}}
					/>
				</View>
				<View style={styles.optView}>
					<Button
						title={isVertical ? "Set horizontal" : "Set Vertical"}
						onPress={() => {
							setIsVertical(!isVertical);
						}}
					/>
				</View>
				<View style={styles.optView}>
					<Button
						title={isFast ? "NORMAL" : "FAST"}
						onPress={() => {
							setIsFast(!isFast);
						}}
					/>
				</View>
				<View style={styles.optView}>
					<Button
						title={`PagingEnabled:${isPagingEnabled.toString()}`}
						onPress={() => {
							setIsPagingEnabled(!isPagingEnabled);
						}}
					/>
				</View>
				<View style={styles.optView}>
					<Button
						title={`ElementsText.AUTOPLAY:${isAutoPlay}`}
						onPress={() => {
							setIsAutoPlay(!isAutoPlay);
						}}
					></Button>
				</View>
				<View style={styles.optView}>
					<Button
						title="prev"
						onPress={() => {
							ref.current?.scrollTo({ count: -1, animated: true });
						}}
					/>
				</View>
				<View style={styles.optView}>
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

const styles = StyleSheet.create({
	swiperView: {
		backgroundColor: "skyblue",
		justifyContent: "center",
		alignItems: "center"
	},
	optView: {
		flexDirection: "row",
		gap: 10,
		padding: 5
	}
});
```

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-gesture-handler、@react-native-oh-tpl/react-native-reanimated 的原生端代码，如已在鸿蒙工程中引入过这两个库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)、[@react-native-oh-tpl/react-native-reanimated 文档](/zh-cn/react-native-reanimated.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.29; SDK: HarmonyOS-Next-DB6 5.0.0.61; IDE: DevEco Studio 5.0.3.706; ROM: NEXT.0.0.61;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Basic Props

| Name | Description | Required | Default | Type | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- | --- |
| data | Carousel items data set | yes |  | T[] | All | yes |
| renderItem | Render carousel item | yes |  | (info: { item: T, index: number, animationValue: SharedValue\<number> }) => React.ReactElement | All | yes |
| defaultScrollOffsetValue | The default animated value of the carousel. | no | useSharedValue<number>(0) | boolean | All | yes |
| autoFillData | Auto fill data array to allow loop playback when the loop props is true.([1] => [1, 1, 1]；[1, 2] => [1, 2, 1, 2]) | no | true | boolean | All | yes |
| vertical | Layout items vertically instead of horizontally | no | false | boolean | All | yes |
| width | Specified carousel item width | `vertical` no `horizontal` yes | '100%' | number \| undefined | All | yes |
| height | Specified carousel item height | `vertical` yes `horizontal` no | '100%' | number \| undefined | All | yes |
| mode | Carousel Animated transitions | no | default | 'horizontal-stack'\|'vertical-stack'\|'parallax' | All | yes |
| modeConfig | Stack layout animation style. Different modes correspond to different configurations | no | { snapDirection: 'left',moveSize: window.width,stackInterval: 30,scaleInterval: 0.08,rotateZDeg: 135} |  | All | yes |
| style | Carousel container style | no | {} | ViewStyle | All | yes |
| defaultIndex | Default index | no | 0 | number | All | yes |
| autoPlay | Auto play | no | false | boolean | All | yes |
| autoPlayReverse | Auto play reverse playback | no | false | boolean | All | yes |
| autoPlayInterval | Auto play playback interval | no | 1000 | number | All | yes |
| scrollAnimationDuration | Time a scroll animation takes to finish | no | 500 | number | All | yes |
| loop | Carousel loop playback | no | true | boolean | All | yes |
| testID | Used to locate this view in end-to-end tests | no |  | string | All | yes |
| onSnapToItem | Callback fired when navigating to an item | no |  | (index: number) => void | All | yes |
| onScrollBegin | Callback fired when scroll begin | no |  | () => void | All | yes |
| onScrollEnd | Callback fired when scroll end | no |  | (index: number) => void | All | yes |
| withAnimation | Specifies the scrolling animation effect | no |  | {type: 'spring';config: WithSpringConfig;} \| {type: 'timing';config: WithTimingConfig;} | All | yes |
| panGestureHandlerProps | PanGestureHandler props | no | {} | Omit<Partial\<PanGestureHandlerProps\>,'onHandlerStateChange'> | All | yes |
| windowSize | The maximum number of items that can respond to pan gesture events, `0` means all items will respond to pan gesture events | no | 0 | number | All | yes |
| onProgressChange | On progress change. `offsetProgress`:Total of offset distance (0 390 780 ...); `absoluteProgress`:Convert to index (0 1 2 ...) | no |  | onProgressChange?: (offsetProgress: number,absoluteProgress: number) => void | All | yes |
| pagingEnabled | When true, the scroll view stops on multiples of the scroll view's size when scrolling | no | true | boolean | All | yes |
| overscrollEnabled | If enabled, the item will scroll to the first placement when scrolling past the edge rather than closing to the last. (previous conditions: loop=false) | no | true | boolean | All | yes |
| snapEnabled | If enabled, releasing the touch will scroll to the nearest item, valid when pagingEnabled=false | no | true | boolean | All | yes |
| enabled | when false, Carousel will not respond to any gestures | no | true | boolean | All | yes |
| customConfig | Custom carousel config | no |  | () => {type?: 'negative' \| 'positive';viewCount?: number;} | All | yes |
| customAnimation | Custom animations | no |  | (value: number) => Animated.AnimatedStyleProp<ViewStyle> | All | yes |
| maxScrollDistancePerSwipe | Maximum offset value for one scroll. If `props.vertical = true`, this will be `maxScrollDistancePerSwipeY`. If `props.vertical = false`, this will be `maxScrollDistancePerSwipeX`. | no |  | number | All | yes |

### `modeConfig` Parallax

| Name | Description | Required | Default | Type | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- | --- |
| parallaxScrollingOffset | control prev/next item offset | no | 100 | number | All | yes |
| parallaxScrollingScale | control prev/current/next item scale | no | 0.8 | number | All | yes |
| parallaxAdjacentItemScale | control prev/next item scale | no | parallaxAdjacentItemScale \|\| Math.pow(parallaxScrollingScale, 2) | number | All | yes |

### `modeConfig` Stack

| Name            | Description              | Required | Default       | Type            | Platform | HarmonyOS Support |
| --------------- | ------------------------ | -------- | ------------- | --------------- | -------- | ----------------- |
| showLength      | Display number           | no       | data.length-1 | number          | All      | yes               |
| moveSize        | Item translate size      | no       | screen.width  | number          | All      | yes               |
| stackInterval   | The spacing of each item | no       | 18            | number          | All      | yes               |
| scaleInterval   | The scale of each item   | no       | 0.04          | number          | All      | yes               |
| opacityInterval | The opacity of each item | no       | 0.1           | number          | All      | yes               |
| rotateZDeg      | The item rotation Angle  | no       | 30            | number          | All      | yes               |
| snapDirection   | Slide direction          | no       | 'left'        | 'left'\|'right' | All      | yes               |

### Ref

| Name | description | Required | Default | Type | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- | --- |
| prev | Scroll to previous item, it takes one optional argument (count), which allows you to specify how many items to cross | no |  | ({ count: number, animated: boolean, onFinished?: () => void }) => void | All | yes |
| next | Scroll to next item, it takes one optional argument (count), which allows you to specify how many items to cross | no |  | ({ count: number, animated: boolean, onFinished?: () => void }) => void | All | yes |
| scrollTo | Use count to scroll to a position where relative to the current position, scrollTo({count:-2}) is equivalent to prev(2), scrollTo({count:2}) is equivalent to next(2). And also can jump to specific position, e.g. scrollTo({index:2,animated:false}) | no |  | ({ index: number, count: number, animated: boolean, onFinished?: () => void }) => void | All | yes |
| getCurrentIndex | Get current item index | no |  | ()=>number | All | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/dohooo/react-native-reanimated-carousel/blob/main/LICENSE) ，请自由地享受和参与开源。
