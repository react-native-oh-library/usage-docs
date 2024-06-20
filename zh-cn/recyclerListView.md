> 模板版本：v0.1.2

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

> [!tip] [Github 地址](https://github.com/Flipkart/recyclerlistview)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install recyclerlistview
```

#### **yarn**

```bash
yarn add recyclerlistview
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, { Component } from "react";
import { View, Text, Dimensions } from "react-native";
import {
  RecyclerListView,
  DataProvider,
  LayoutProvider,
} from "recyclerlistview";

const ViewTypes = {
  FULL: 0,
  HALF_LEFT: 1,
  HALF_RIGHT: 2,
};

let containerCount = 0;

class CellContainer extends React.Component {
  constructor(args) {
    super(args);
    this._containerId = containerCount++;
  }
  render() {
    return (
      <View {...this.props}>
        {this.props.children}
        <Text>Cell Id: {this._containerId}</Text>
      </View>
    );
  }
}

export default class RecycleTestComponent extends React.Component {
  constructor(args) {
    super(args);

    let { width } = Dimensions.get("window");

    let dataProvider = new DataProvider((r1, r2) => {
      return r1 !== r2;
    });

    this._layoutProvider = new LayoutProvider(
      (index) => {
        if (index % 3 === 0) {
          return ViewTypes.FULL;
        } else if (index % 3 === 1) {
          return ViewTypes.HALF_LEFT;
        } else {
          return ViewTypes.HALF_RIGHT;
        }
      },
      (type, dim) => {
        switch (type) {
          case ViewTypes.HALF_LEFT:
            dim.width = width / 2;
            dim.height = 160;
            break;
          case ViewTypes.HALF_RIGHT:
            dim.width = width / 2;
            dim.height = 160;
            break;
          case ViewTypes.FULL:
            dim.width = width;
            dim.height = 140;
            break;
          default:
            dim.width = 0;
            dim.height = 0;
        }
      },
    );

    this._rowRenderer = this._rowRenderer.bind(this);

    this.state = {
      dataProvider: dataProvider.cloneWithRows(this._generateArray(300)),
    };
  }

  _generateArray(n) {
    let arr = new Array(n);
    for (let i = 0; i < n; i++) {
      arr[i] = i;
    }
    return arr;
  }

  _rowRenderer(type, data) {
    switch (type) {
      case ViewTypes.HALF_LEFT:
        return (
          <CellContainer style={styles.containerGridLeft}>
            <Text>Data: {data}</Text>
          </CellContainer>
        );
      case ViewTypes.HALF_RIGHT:
        return (
          <CellContainer style={styles.containerGridRight}>
            <Text>Data: {data}</Text>
          </CellContainer>
        );
      case ViewTypes.FULL:
        return (
          <CellContainer style={styles.container}>
            <Text>Data: {data}</Text>
          </CellContainer>
        );
      default:
        return null;
    }
  }

  render() {
    return (
      <RecyclerListView
        layoutProvider={this._layoutProvider}
        dataProvider={this.state.dataProvider}
        rowRenderer={this._rowRenderer}
      />
    );
  }
}
const styles = {
  container: {
    justifyContent: "space-around",
    alignItems: "center",
    flex: 1,
    backgroundColor: "#00a1f1",
  },
  containerGridLeft: {
    justifyContent: "space-around",
    alignItems: "center",
    flex: 1,
    backgroundColor: "#ffbb00",
  },
  containerGridRight: {
    justifyContent: "space-around",
    alignItems: "center",
    flex: 1,
    backgroundColor: "#7cbb00",
  },
};
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52(SP22C00E52R1P17log);

## 属性

详情见 [RecyclerListView 源库地址](https://github.com/Flipkart/recyclerlistview)

| Name                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Type                                                                                       | Required | Platform | HarmonyOS Support |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| layoutProvider                 | Constructor function that defines the layout (height / width) of each element                                                                                                                                                                                                                                                                                                                                                                                                  | BaseLayoutProvider                                                                         | Yes      | All      | Yes               |
| dataProvider                   | Constructor function the defines the data for each element                                                                                                                                                                                                                                                                                                                                                                                                                     | DataProvider                                                                               | Yes      | All      | Yes               |
| contextProvider                | Used to maintain scroll position in case view gets destroyed, which often happens with back navigation                                                                                                                                                                                                                                                                                                                                                                         | ContextProvider                                                                            | No       | All      | No                |
| rowRenderer                    | Method that returns react component to be rendered. You get the type, data, index and extendedState of the view in the callback                                                                                                                                                                                                                                                                                                                                                | (type: string \| number, data: any, index: number) => JSX.Element \| JSX.Element[] \| null | Yes      | All      | Yes               |
| initialOffset                  | Initial offset you want to start rendering from; This is very useful if you want to maintain scroll context across pages.                                                                                                                                                                                                                                                                                                                                                      | number                                                                                     | No       | All      | Yes               |
| renderAheadOffset              | specify how many pixels in advance you want views to be rendered. Increasing this value can help reduce blanks (if any). However, keeping this as low as possible should be the intent. Higher values also increase re-render compute                                                                                                                                                                                                                                          | number                                                                                     | No       | All      | Yes               |
| isHorizontal                   | If true, the list will operate horizontally rather than vertically                                                                                                                                                                                                                                                                                                                                                                                                             | boolean                                                                                    | No       | All      | Yes               |
| onScroll                       | On scroll callback function that executes as a user scrolls                                                                                                                                                                                                                                                                                                                                                                                                                    | rawEvent: ScrollEvent, offsetX: number, offsetY: number) => void                           | No       | All      | Yes               |
| onRecreate                     | callback function that gets executed when recreating the recycler view from context provider                                                                                                                                                                                                                                                                                                                                                                                   | (params: OnRecreateParams) => void                                                         | No       | All      | No                |
| externalScrollView             | Use this to pass your on implementation of BaseScrollView                                                                                                                                                                                                                                                                                                                                                                                                                      | { new (props: ScrollViewDefaultProps): BaseScrollView }                                    | No       | All      | No                |
| onEndReached                   | Callback function executed when the end of the view is hit (minus onEndThreshold if defined)                                                                                                                                                                                                                                                                                                                                                                                   | () => void                                                                                 | No       | All      | Yes               |
| onEndReachedThreshold          | Specify how many pixels in advance for the onEndReached callback                                                                                                                                                                                                                                                                                                                                                                                                               | number                                                                                     | No       | All      | Yes               |
| onEndReachedThresholdRelative  | Specify how far from the end (in units of visible length of the list) the bottom edge of the list must be from the end of the content to trigger the onEndReached callback                                                                                                                                                                                                                                                                                                     | number                                                                                     | No       | All      | Yes               |
| onVisibleIndicesChanged        | Provides visible index; helpful in sending impression events                                                                                                                                                                                                                                                                                                                                                                                                                   | TOnItemStatusChanged                                                                       | No       | All      | Yes               |
| onVisibleIndexesChanged        | (Deprecated in 2.0 beta) Provides visible index; helpful in sending impression events                                                                                                                                                                                                                                                                                                                                                                                          | TOnItemStatusChanged                                                                       | No       | All      | No                |
| renderFooter                   | Provide this method if you want to render a footer. Helpful in showing a loader while doing incremental loads                                                                                                                                                                                                                                                                                                                                                                  | () => JSX.Element \| JSX.Element[] \| null                                                 | No       | All      | Yes               |
| initialRenderIndex             | Specify the initial item index you want rendering to start from. Preferred over initialOffset if both specified                                                                                                                                                                                                                                                                                                                                                                | number                                                                                     | No       | All      | yes               |
| scrollThrottle                 | iOS only; Scroll throttle duration                                                                                                                                                                                                                                                                                                                                                                                                                                             | number                                                                                     | No       | All      | No                |
| canChangeSize                  | Specify if size can change                                                                                                                                                                                                                                                                                                                                                                                                                                                     | boolean                                                                                    | No       | All      | No                |
| distanceFromWindow             | (Depricated) Use applyWindowCorrection() API with windowShift.                                                                                                                                                                                                                                                                                                                                                                                                                 | number                                                                                     | No       | All      | No                |
| applyWindowCorrection          | (Enhancement/replacement to distanceFromWindow API) Allows updation of the visible windowBounds to based on correctional values passed. User can specify windowShift; in case entire RecyclerListWindow needs to shift down/up, startCorrection; in case when top window bound needs to be shifted for e.x. top window bound to be shifted down is a content overlapping the top edge of RecyclerListView, endCorrection: to alter bottom window bound for a similar use-case. | (offset: number, windowCorrection: WindowCorrection) => void                               | No       | All      | Yes               |
| useWindowScroll                | Web only; Layout Elements in window instead of a scrollable div                                                                                                                                                                                                                                                                                                                                                                                                                | boolean                                                                                    | No       | All      | No                |
| disableRecycling               | Turns off recycling                                                                                                                                                                                                                                                                                                                                                                                                                                                            | boolean                                                                                    | No       | All      | Yes               |
| forceNonDeterministicRendering | Default is false; if enabled dimensions provided in layout provider will not be strictly enforced. Use this if item dimensions cannot be accurately determined                                                                                                                                                                                                                                                                                                                 | boolean                                                                                    | No       | All      | Yes               |
| extendedState                  | In some cases the data passed at row level may not contain all the info that the item depends upon, you can keep all other info outside and pass it down via this prop. Changing this object will cause everything to re-render. Make sure you don't change it often to ensure performance. Re-renders are heavy.                                                                                                                                                              | object                                                                                     | No       | All      | No                |
| itemAnimator                   | Enables animating RecyclerListView item cells (shift, add, remove, etc)                                                                                                                                                                                                                                                                                                                                                                                                        | ItemAnimator                                                                               | No       | All      | No                |
| style                          | To pass down style to inner ScrollView                                                                                                                                                                                                                                                                                                                                                                                                                                         | object                                                                                     | No       | All      | Yes               |
| scrollViewProps                | For all props that need to be proxied to inner/external scrollview. Put them in an object and they'll be spread and passed down.                                                                                                                                                                                                                                                                                                                                               | object                                                                                     | No       | All      | Yes               |
| layoutSize                     | Will prevent the initial empty render required to compute the size of the listview and use these dimensions to render list items in the first render itself. This is useful for cases such as server side rendering. The prop canChangeSize has to be set to true if the size can be changed after rendering. Note that this is not the scroll view size and is used solely for layouting.                                                                                     | Dimension                                                                                  | No       | All      | Yes               |
| onItemLayout                   | A callback function that is executed when an item of the recyclerListView (at an index) has been layout. This can also be used as a proxy to itemsRendered kind of callbacks.                                                                                                                                                                                                                                                                                                  | number                                                                                     | No       | All      | Yes               |
| windowCorrectionConfig         | Used to specify is window correction config and whether it should be applied to some scroll events                                                                                                                                                                                                                                                                                                                                                                             | object                                                                                     | No       | All      | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/Flipkart/recyclerlistview/blob/master/LICENSE.md) ，请自由地享受和参与开源。
