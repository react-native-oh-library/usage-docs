> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-header-scroll-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/meliorence/react-native-render-html">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bamlab/react-native-image-header-scroll-view/blob/master/LICENCE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>





> [!TIP] [Github 地址](https://github.com/bamlab/react-native-image-header-scroll-view)
> 因 v1.0.0 中存在无法触发 TriggeringView 组件回调的问题，以下基于 v0.10.3 版本验证

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-image-header-scroll-view@0.10.3
```

#### **yarn**

```bash
yarn add react-native-image-header-scroll-view@0.10.3
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useEffect, useState } from 'react';
import { StyleSheet, Text, View, Image,Animated,StatusBar, Dimensions ,Easing} from 'react-native';
import ImageHeaderScrollView ,{TriggeringView}  from 'react-native-image-header-scroll-view';
const MIN_HEIGHT = 80;
const MAX_HEIGHT = 250;
const tvShowContent = {
  title: 'Doctor Who',
  overview: `
    The Doctor looks and seems human. He's handsome, witty, and could be mistaken for just another man in the street.

    But he is a Time Lord: a 900 year old alien with 2 hearts, part of a gifted civilization who mastered time travel.

    The Doctor saves planets for a living – more of a hobby actually, and he's very, very good at it.

    He's saved us from alien menaces and evil from before time began – but just who is he?`,
  year: 2005,
  genres: ['Action & Adventure', 'Drama', 'Sci-Fi & Fantasy'],
  keywords: [
    'time travel',
    'time machine',
    'phone booth',
    'alien',
    'time traveler',
    'police box',
    'space and aliens',
  ],
};

const styles = StyleSheet.create({
  image: {
    height: MAX_HEIGHT,
    width: Dimensions.get('window').width,
    alignSelf: 'stretch',
    resizeMode: 'cover',
  },
  title: {
    fontSize: 20,
  },
  name: {
    fontWeight: 'bold',
  },
  section: {
    padding: 20,
    borderBottomWidth: 1,
    borderBottomColor: '#cccccc',
    backgroundColor: 'white',
  },
  sectionTitle: {
    fontSize: 18,
    fontWeight: 'bold',
  },
  sectionContent: {
    fontSize: 16,
    textAlign: 'justify',
  },
  keywords: {
    flexDirection: 'row',
    justifyContent: 'flex-start',
    alignItems: 'flex-start',
    flexWrap: 'wrap',
  },
  keywordContainer: {
    backgroundColor: '#999999',
    borderRadius: 10,
    margin: 10,
    padding: 10,
  },
  keyword: {
    fontSize: 16,
    color: 'white',
  },
  titleContainer: {
    flex: 1,
    alignSelf: 'stretch',
    justifyContent: 'center',
    alignItems: 'center',
  },
  imageTitle: {
    color: 'white',
    backgroundColor: 'transparent',
    fontSize: 24,
  },
  navTitleView: {
    height: MIN_HEIGHT,
    justifyContent: 'center',
    alignItems: 'center',
    paddingTop: 16,
    opacity: 0,
  },
  navTitle: {
    color: 'white',
    fontSize: 18,
    backgroundColor: 'transparent',
  },
  sectionLarge: {
    height: 600,
  },
});

function HeaderImageExample () {
    const [visible, setVisible] = useState(false);
    const fadeAnim = new Animated.Value(0);
    useEffect(() => {
        if (visible) {
          Animated.timing(fadeAnim, {
            toValue: 1,
            duration: 100,
            easing: Easing.bounce,
            useNativeDriver: true,
          }).start();
        } else {
          // 如果当前是不可见的，则执行淡出动画
          Animated.timing(fadeAnim, {
            toValue: 0,
            duration: 100,
            easing: Easing.bounce,
            useNativeDriver: true,
          }).start();
        }
      }, [visible, fadeAnim]);  
 
    return (
      <View style={{ flex: 1 }}>
        <StatusBar barStyle="light-content" />
        <ImageHeaderScrollView
          maxHeight={MAX_HEIGHT} 
          minHeight={MIN_HEIGHT}  
          maxOverlayOpacity={0.8} 
          minOverlayOpacity={0.2}   
          fadeOutForeground={true} 
          foregroundParallaxRatio={1}
          overlayColor={'blue'} 
          renderHeader={() => <Image source={'请输入本地图片路径'} style={styles.image} />} 
          renderFixedForeground={() => (
            <Animated.View
                    style={[styles.navTitleView,{ opacity: fadeAnim}]}  >
                    <Text style={styles.navTitle}>
                        {tvShowContent.title}, ({tvShowContent.year})
                    </Text>
            </Animated.View>
          )} 
          renderForeground={() => (
            <View style={styles.titleContainer}>
              <Text style={styles.imageTitle}>{tvShowContent.title}</Text>
            </View> as any
          )}  
          useNativeDriver={true}
          disableHeaderGrow={false}>
         <>
          <TriggeringView
            onHide={() => setVisible(true)}
            onDisplay={() => setVisible(false)}
          >
            <Text style={styles.title}>
              <Text style={styles.name}>{tvShowContent.title}</Text>, ({tvShowContent.year})
            </Text>
          </TriggeringView>
          <View style={styles.section}>
            <Text style={styles.sectionTitle}>Overview</Text>
            <Text style={styles.sectionContent}>{tvShowContent.overview}</Text>
          </View>
          <View style={[styles.section, styles.sectionLarge]}>
            <Text style={styles.sectionTitle}>Keywords</Text>
            <View style={styles.keywords}>
              {tvShowContent.keywords.map(keyword => (
                <View style={styles.keywordContainer} key={keyword}>
                  <Text style={styles.keyword}>{keyword}</Text>
                </View>
              ))}
            </View>
          </View>
          </>
        </ImageHeaderScrollView>
      </View>
    );
  
}

export default HeaderImageExample;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.29; SDK：HarmonyOS NEXT Developer Beta6; IDE：DevEco Studio 5.0.3.706; ROM：Next0.0.66;

## API

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### **Header**

| Name                          | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `renderHeader` | Function which return the component to use as header. It can return background image for example.           | function | No       | All      | Yes               |
| `headerImage`               | Function which return the component to use as fixed foreground. The component is displayed with the header but not affected by the overlay.}                            | Image source Props (object or number) | No       | All      | Yes               |
| `maxHeight`                | Min height for the header (in navbar mode)     | number | No       | All      | Yes               |
| `minHeight`                | Sends a ping frame to the server.                            | number | No       | All      | Yes               |
| `minOverlayOpacity`           | Opacity of a black overlay on the header before any scroll | number | No       | All      | Yes               |
| `maxOverlayOpacity`           | Opacity of a black overlay on the header when in navbar mode | number | No       | All      | Yes               |
| `overlayColor`           | Color of the overlay on the header | string | No       | All      | Yes               |
| `useNativeDriver`           | Use native driver for the animation for performance improvement. A few props are unsupported at the moment if useNativeDriver=true (onScroll, ScrollComponent, renderTouchableFixedForeground) | boolean | No       | All      | Yes               |
| `headerContainerStyle`           | Optional styles to be passed to the container of the header component | Object | No       | All      | Yes               |
| `disableHeaderGrow`           | Disable to grow effect on the header | boolean | No       | All      | Yes               |


#### **Foreground**

| Name                          | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `renderForeground` | Function which return the component to use at foreground. The component is render in front of the header and scroll with the ScrollView. It can return a title for example.           | function | No       | All      | Yes               |
| `renderFixedForeground`               | Function which return the component to use as fixed foreground. The component is displayed with the header but not affected by the overlay.}                            | Image source Props (object or number) | No       | All      | Yes               |
| `foregroundExtrapolate`                | Optional prop that allows override extrapolate mode for foreground. Use null to allow extrapolation, which is usefull for using foreground as bottom title   | string | No       | All      | Yes               |
| `foregroundParallaxRatio`                | Ration for parallax effect of foreground when scrolling. If 2, the header goes up two times faster than the scroll                          | number | No       | All      | Yes               |
| `fadeOutForeground`           | If set, add a fade out effect on the foreground when scroll up | boolean | No       | All      | Yes               |
| `renderTouchableFixedForeground`           | Same as renderFixedForeground but allow to use touchable in it. [Can cause performances issues on Android](https://github.com/bamlab/react-native-image-header-scroll-view/issues/6)   | function | No       | All      | Yes               |
| `fixedForegroundContainerStyles`           | 	Optional styles to be passed to the container of the fixed foreground component | Object | No       | All      | Yes               |


#### **Mixed**

| Name                          | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `ScrollViewComponent` | The component to be used for scrolling. Can be any component with an onScroll props (ie. ListView, FlatList, SectionList or ScrollView)         | Component | No       | All      | Yes               |
| `scrollViewBackgroundColor`               | Background color of the scrollView content                        | string | No       | All      | Yes               |



#### **TriggeringView**

| Name                          | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `onBeginHidden` | Called when the component start to be hidden at the top of the scroll view.          | function | No       | All      | Yes               |
| `onHide`               | Called when the component is not displayed any more after scroll up             | function | No       | All      | Yes               |
| `onBeginDisplayed`                | Called when the component begin to be displayed again after scroll down | function | No       | All      | Yes               |
| `onDisplay`                | Called when the component finished to be displayed again.            | function | No       | All      | Yes               |
| `onTouchTop`           | 	Called when the Top of the component touch the Top of the ScrollView. (onDisplay + onBeginHidden) | function | No       | All      | Yes               |
| `onTouchBottom`           | Called when the Bottom of the component touch the Top of the ScrollView. (onHide + onBeginDisplayed)  | function | No       | All      | Yes               |

## 遗留问题
## 其他

- 如何去除图片阴影蒙层？  
  可通过设置 maxOverlayOpacity、minOverlayOpacity 属性为 0，去除图片阴影蒙层。
- 如何禁止滑动回弹效果？
  - 方法 1：设置 disableHeaderGrow 属性为 true
  - 方法 2：设置 bounces 属性为 false

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/bamlab/react-native-image-header-scroll-view/blob/master/LICENCE) ，请自由地享受和参与开源。