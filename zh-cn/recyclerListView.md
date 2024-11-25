> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>RecyclerListView</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Flipkart/recyclerlistview">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Flipkart/recyclerlistview/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/Flipkart/recyclerlistview)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install recyclerlistview@4.2.0
```

#### **yarn**

```bash
yarn add recyclerlistview@4.2.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, {useState} from 'react';
import {View, Dimensions, Alert, Text} from 'react-native';
import {RecyclerListView, DataProvider} from 'recyclerlistview';
import {LayoutProvider} from 'recyclerlistview';

const ViewTypes = {
  FIRST: 0,
  SECOND: 1,
  THIRD: 2,
};

class LayoutUtil {
  static getWindowWidth() {
    // To deal with precision issues on android
    return Math.round(Dimensions.get('window').width * 1000) / 1000 - 6; //Adjustment for margin given to RLV;
  }
  static getLayoutProvider(type) {
    return new LayoutProvider(
      index => {
        if (index % 3 === 0) {
          return ViewTypes.FIRST;
        } else if (index % 2 === 0) {
          return ViewTypes.SECOND;
        } else {
          return ViewTypes.THIRD;
        }
      },
      (type, dim, index) => {
        const columnWidth = LayoutUtil.getWindowWidth() / 3;
        if (index % 3 === 0) {
          dim.width = 3 * columnWidth;
          dim.height = 150;
        } else if (index % 2 === 0) {
          dim.width = 2 * columnWidth;
          dim.height = 100;
        } else {
          dim.width = columnWidth;
          dim.height = 100;
        }
      },
    );
  }
}

const generateArray = n => {
  let arr = new Array(n);
  for (let i = 0; i < n; i++) {
    arr[i] = i;
  }
  return arr;
};

export const RecyclerListViewBaseDemo = () => {
  let {width} = Dimensions.get('window');

  let dataProviderInit = new DataProvider((r1, r2) => {
    return r1 !== r2;
  });

  const [dataProvider, setDataProvider] = useState(
    dataProviderInit.cloneWithRows(generateArray(300)),
  );

  const rowRenderer = (type, data) => {
    switch (type) {
      case ViewTypes.FIRST:
        return (
          <View style={styles.containerFirst}>
            <Text style={styles.centerText}>{data}</Text>
          </View>
        );
      case ViewTypes.SECOND:
        return (
          <View style={styles.containerSecond}>
            <Text style={styles.centerText}>{data}</Text>
          </View>
        );
      case ViewTypes.THIRD:
        return (
          <View style={styles.containerThree}>
            <Text style={styles.centerText}>{data}</Text>
          </View>
        );
      default:
        return null;
    }
  };

  return (
    <RecyclerListView
      layoutProvider={LayoutUtil.getLayoutProvider(0)}
      dataProvider={dataProvider}
      rowRenderer={rowRenderer}
    />
  );
};

export default RecyclerListViewBaseDemo;

const styles = {
  containerFirst: {
    justifyContent: 'space-around',
    alignItems: 'center',
    flex: 1,
    backgroundColor: '#00a1f1',
  },
  containerSecond: {
    justifyContent: 'space-around',
    alignItems: 'center',
    flex: 1,
    backgroundColor: '#ffbb00',
  },
  containerThree: {
    justifyContent: 'space-around',
    alignItems: 'center',
    flex: 1,
    backgroundColor: '#7cbb00',
  },
  centerText: {
    fontSize: 30,
    fontWeight: 'bold',
    color: '#000000',
  },
};
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.25;
2. RNOH：0.72.29; SDK：HarmonyOS NEXT Developer Beta6; IDE：DevEco Studio 5.0.3.706; ROM：3.0.0.61;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                                                                                                                                         | Type                                                                                                                       | Required | Platform | HarmonyOS Support |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| layoutProvider | Constructor function that <br>defines the layout (height /<br> width) of each element | BaseLayoutProvider | Yes      | iOS Android | Yes |
| dataProvider | Constructor function the <br>defines the data for each element | DataProvider | Yes | iOS Android | Yes |
| contextProvider | Used to maintain scroll position <br>in case view gets destroyed,  which <br>often happens with back navigation | ContextProvider | No | iOS Android | Yes |
| rowRenderer | Method that returns react <br>component to be rendered.<br> You get the type, data, index <br>and extendedState of the view <br>in the callback | function | Yes | iOS Android | Yes               |
| initialOffset | Initial offset you want to start<br> rendering from; This is very useful<br> if you want to maintain scroll context<br> across pages. | number | No | iOS Android | Yes              |
| renderAheadOffset | specify how many pixels in <br>advance you want views to <br>be rendered. Increasing this<br> value can help reduce blanks <br>(if any).However, keeping this<br> as low as possible .should be <br>the intent Higher values also .<br>increase re-render compute | number | No | iOS Android | Yes |
| isHorizontal | If true, the list will operate<br> horizontally .rather than vertically | boolean | No | iOS Android | Yes               |
| onScroll | On scroll callback function that <br>executes. as a user scrolls | function | No | iOS Android | Yes             |
| onRecreate | callback function that gets <br>executed. when recreating the <br>recycler view from context provider | function | No | iOS Android | Yes                |
| externalScrollView | Use this to pass your on<br> implementation of BaseScrollView | { new (props: ScrollViewDefaultProps): BaseScrollView } | No | iOS Android | Yes               |
| onEndReached | Callback function executed <br>when the end of the view is hit <br>(minus onEndThreshold if defined) | function | No | iOS Android | Yes               |
| onEndReachedThreshold | Specify how many pixels in advance <br>for the onEndReached callback | number | No | iOS Android | Yes |
| onEndReachedThresholdRelative | Specify how far from the end <br>(in units of visible length of the list)<br> the bottom edge of the list must be  <br>from theend of the content to trigger  <br>the onEndReached callback | number | No | iOS Android | Yes               |
| onVisibleIndicesChanged | Provides visible index; <br> helpful in sending impression events | TOnItemStatusChanged | No | iOS Android | Yes              |
| renderFooter | Provide this method if you want to <br>render a footer. Helpful in showing <br>a loader while doing incremental loads | function | No | iOS Android | Yes               |
| initialRenderIndex | Specify the initial item index you<br> want rendering to start from. Preferred <br>over initialOffset if both specified | number | No | iOS Android | Yes          |
| scrollThrottle | iOS only; Scroll throttle duration | number | No | iOS | No |
| canChangeSize | Specify if size can change | boolean | No | iOS Android | Yes               |
| applyWindowCorrection | (Enhancement/replacement to <br>distanceFromWindow API) Allows  <br>updation of the visible windowBounds <br> to based on correctional values passed. <br>User can specify windowShift; in case <br>entire RecyclerListWindow needs to <br>shift down/up, startCorrection; in case <br>when top window bound needs to be <br>shifted for e.x. top window bound to be <br> shifted down is a content overlapping <br>the top edge of RecyclerListView,<br> endCorrection: to alter bottom window<br>  bound for a similar use-case. | function | No | iOS Android | Yes |
| disableRecycling | Turns off recycling | boolean| No | iOS Android | Yes               |
| forceNonDeterministicRendering | Default is false; <br> if enabled dimensions<br> provided in layout  provider <br>will not be strictly enforced.<br> Use  this if item dimensions <br>cannot be accurately determined | boolean | No | iOS Android | Yes |
| extendedState | In some cases the data passed at row <br>level may not contain all the info that <br>the item depends upon,you can keep <br>all other info outside and pass it down <br>via this prop. Changing this object <br> willcause everything to re-render. Make sureyou don't change it often to ensure<br> performance. Re-renders are heavy. | object | No | iOS Android | Yes |
| itemAnimator | Enables animating RecyclerListView<br> item cells (shift, add, remove, etc) | ItemAnimator | No | iOS Android | Yes                |
| style | To pass down style to inner ScrollView | object | No | iOS Android  | Yes  |
| scrollViewProps | For all props that need to be proxied <br>to inner/external scrollview. Put them <br>in an object and they'll be spread and passed down. | object | No | iOS Android | Yes    |
| layoutSize | Will prevent the initial empty render <br>required to compute the size of the<br> listview and use these dimensions to <br>render list items in the first render <br>itself. This is useful for cases such<br> as server side rendering. The prop canChangeSize has to be set to true<br> if the size can be changed after <br>rendering. Note that this is not the scroll view size and is used solely for layouting. | Dimension | No | iOS Android | Yes              |
| onItemLayout | A callback function that is executed<br> when an item of the recyclerListView<br> (at an index) has been layout. This can also be used as a proxy to itemsRendered kind of callbacks. | number | No | iOS Android | Yes          |
| windowCorrectionConfig | Used to specify is window<br> correction config and whether<br> it should be applied to some <br>scroll events | object | No | iOS Android | Yes               |

## 遗留问题

- [ ] 接口scrollThrottle不支持: [issue#785](https://github.com/Flipkart/recyclerlistview/issues/785)

## 其他

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/Flipkart/recyclerlistview/blob/master/LICENSE.md) ，请自由地享受和参与开源。
