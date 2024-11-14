> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-drag-sort</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mochixuan/react-native-drag-sort">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mochixuan/react-native-drag-sort/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!tip] [Github 地址](https://github.com/mochixuan/react-native-drag-sort)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-drag-sort Releases](https://github.com/react-native-oh-library/react-native-drag-sort/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-drag-sort
```

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-drag-sort
```

### Tip

> Use priority: DragSortableView > AutoDragSortableView > AnySizeDragSortableView

- 1、If the width and height are fixed and there is no need to slide, use DragSortableView.
- 2、If the width and height are fixed and you need to slide, use AutoDragSortableView.
- 3、If the width and height are arbitrary and need to slide, please use AnySizeDragSortableView.

下面的代码展示了这个库的基本使用场景：

##### DragSortableView组件使用

```js
import React, { useState } from "react";
import { View, Text, StyleSheet, SafeAreaView } from "react-native";
import { DragSortableView } from "react-native-drag-sort";
//此案例id1、id2不支持拖拽
const Dragsort = () => {
  const [data, setData] = useState([
    {
      id: 1,
      title: "固定任务 1",
    },
    {
      id: 2,
      title: "固定任务 2",
    },
    {
      id: 3,
      title: "任务 3",
    },
    {
      id: 4,
      title: "任务 4",
    },
    {
      id: 5,
      title: "任务 5",
    },
    {
      id: 6,
      title: "任务 6",
    },
    {
      id: 7,
      title: "任务 7",
    },
    {
      id: 8,
      title: "任务 8",
    },
  ]);

  return (
    <SafeAreaView style={{ flex: 1 }}>
      <View style={styles.header}>
        <Text style={styles.header_title}>DragSortableView</Text>
      </View>
      <DragSortableView
        dataSource={data}
        parentWidth={400}
        childrenWidth={100}
        childrenHeight={50}
        marginChildrenTop={5}
        marginChildrenBottom={5}
        marginChildrenLeft={5}
        marginChildrenRight={5}
        // onDataChange={setData}
        keyExtractor={(item, index) => item.id}
        onClickItem={(data, item, index) => {
          console.log("点击了第", index, "个元素");
        }}
        onDragStart={() => console.log("Drag started")}
        onDragEnd={() => console.log("Drag end")}
        onDataChange={() => {
          console.log("数据发生变化");
        }}
        fixedItems={[0, 1]}
        delayLongPress={100}
        isDragFreely={true}
        maxScale={1.2}
        minOpacity={0.7}
        renderItem={(item, index) => {
          return (
            <View key={item.id} style={styles.box}>
              <Text style={styles.text}>{item.title}</Text>
            </View>
          );
        }}
        sortable={true}
      />
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  box: {
    // position:'relative',
    // flexDirection: "column",
    justifyContent: "center",
    alignContent: "center",
    borderRadius: 5,
    margin: 20,
    backgroundColor: "#4e71f2",
    height: 50,
    width: 100,
  },
  text: {
    fontSize: 18,
    color: "#fff",
    textAlign: "center",
  },
  header: {
    height: 48,
    justifyContent: "center",
    alignItems: "center",
    borderBottomColor: "#2ecc71",
    borderBottomWidth: 2,
  },
  header_title: {
    color: "#333",
    fontSize: 24,
    fontWeight: "bold",
  },
});
export default Dragsort;
```

##### AutoDragSortableView组件使用

```js
//此案例Item1、Item2不支持拖拽
import React, { useState } from "react";
import { View, Text } from "react-native";
import { AutoDragSortableView } from "react-native-drag-sort";

const AutoDragSortDemo = () => {
  const [data, setData] = useState([
    { id: "1", text: "Item 1" },
    { id: "2", text: "Item 2" },
    { id: "3", text: "Item 3" },
    { id: "4", text: "Item 4" },
    { id: "5", text: "Item 5" },
    { id: "6", text: "Item 6" },
    { id: "7", text: "Item 7" },
    { id: "8", text: "Item 8" },
    { id: "9", text: "Item 9" },
    { id: "10", text: "Item 10" },
    { id: "11", text: "Item 11" },
    { id: "12", text: "Item 12" },
    { id: "13", text: "Item 13" },
    { id: "14", text: "Item 14" },
    { id: "15", text: "Item 15" },
    { id: "16", text: "Item 16" },
    { id: "17", text: "Item 17" },
    { id: "18", text: "Item 18" },
    { id: "19", text: "Item 19" },
    { id: "20", text: "Item 20" },
    { id: "21", text: "Item 21" },
    { id: "22", text: "Item 22" },
    { id: "23", text: "Item 23" },
    { id: "24", text: "Item 24" },
    { id: "25", text: "Item 25" },
    { id: "26", text: "Item 26" },
    { id: "27", text: "Item 27" },
    { id: "28", text: "Item 28" },
  ]);
  const renderHeaderView = (
    <View style={{ height: 50, backgroundColor: "#ff4d4d" }}>
      <Text style={{ fontSize: 18, color: "#fff", textAlign: "center" }}>
        标题
      </Text>
    </View>
  );
  const renderBottomView = (
    <View style={{ height: 50, backgroundColor: "#ff4d4d" }}>
      <Text style={{ fontSize: 18, color: "#fff", textAlign: "center" }}>
        底部
      </Text>
    </View>
  );

  return (
    <AutoDragSortableView
      dataSource={data}
      parentWidth={500}
      childrenWidth={100}
      childrenHeight={100}
      marginChildrenTop={20}
      marginChildrenBottom={20}
      marginChildrenLeft={20}
      marginChildrenRight={20}
      onDataChange={(data) => {
        console.log("数据发生变化");
      }}
      keyExtractor={(item, index) => item.id}
      onClickItem={(data, item, index) => {
        console.log("点击了第", index, "个元素");
      }}
      renderItem={(item, index) => {
        return (
          <View
            key={item.id}
            style={{
              width: 100,
              height: 50,
              borderRadius: 5,
              margin: 5,
              backgroundColor: "#4e71f2",
            }}
          >
            <Text style={{ fontSize: 18, color: "#fff" }}>{item.text}</Text>
          </View>
        );
      }}
      scaleDuration={500} //拖拽项缩放效果的持续时间
      slideDuration={200} //拖拽项滑动效果的持续时间
      autoThrottle={100} //自动滑动到目的地的间隔时间
      autoThrottleDuration={500} //自动滑动到目的地的持续时间
      sortable={true}
      isDragFreely={false}
      fixedItems={[0, 1]}
      delayLongPress={100}
      onDragStart={() => console.log("Drag started")}
      onDragEnd={() => console.log("Drag end")}
      renderHeaderView={renderHeaderView}
      headerViewHeight={50}
      scrollIndicatorInsets={{ top: 0, left: 0, bottom: 0, right: 0 }}
      renderBottomView={renderBottomView}
      bottomViewHeight={50}
      onScrollListener={(event) => {
        console.log("滚动事件", event);
      }}
      onScrollRef={(ref) => {
        console.log("滚动容器", ref);
      }}
    />
  );
};

export default AutoDragSortDemo;
```

##### AnySizeDragSortableView组件使用

```js
import React, { createRef } from "react";
import {
  Text,
  TouchableOpacity,
  StyleSheet,
  View,
  Image,
  Dimensions,
  SafeAreaView,
} from "react-native";
import { AnySizeDragSortableView } from "react-native-drag-sort";

const { width } = Dimensions.get("window");
const headerViewHeight = 160;
const bottomViewHeight = 40;

const getW = (index, isWidth) =>
  isWidth ? (index % 3 === 0 ? width - 40 : (width - 60) / 2) : 80;

export default class AnySizeDragSortDemo extends React.Component {
  constructor(props) {
    super(props);
    const items = [];
    for (let i = 0; i < 26; i++) {
      items.push({
        text: String.fromCharCode(65 + i),
        width: getW(i, true),
        height: getW(i, false),
      });
    }
    this.state = {
      items,
      movedKey: null,
    };

    this.sortableViewRef = createRef();
  }

  onDeleteItem = (item, index) => {
    const items = [...this.state.items];
    items.splice(index, 1);
    this.setState({ items });
  };

  _renderItem = (item, index, isMoved) => {
    const { movedKey } = this.state;
    return (
      <TouchableOpacity
        onLongPress={() => {
          this.setState({ movedKey: item.text });
          this.sortableViewRef.current.startTouch(item, index);
        }}
        onPressOut={() => this.sortableViewRef.current.onPressOut()}
      >
        <View
          style={[
            styles.item_wrap,
            { opacity: movedKey === item.text && !isMoved ? 1 : 1 },
          ]}
        >
          {
            <View style={styles.item_clear_wrap}>
              <TouchableOpacity onPress={() => this.onDeleteItem(item, index)}>
                <Image
                  source={require("../SourceLibraryDemo/data/img/clear.png")}
                  style={styles.item_clear}
                />
              </TouchableOpacity>
            </View>
          }
          <View
            style={[
              styles.item,
              {
                width: item.width,
                height: item.height,
                backgroundColor: isMoved ? "red" : "#f39c12",
              },
            ]}
          >
            {isMoved ? (
              <View style={styles.item_icon_swipe}>
                <Image
                  source={{
                    uri: "https://img0.baidu.com/it/u=4232278629,1470839503&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=746",
                  }}
                  style={styles.item_icon}
                />
              </View>
            ) : null}
            <View style={styles.item_text_swipe}>
              <Text style={styles.item_text}>{item.text}</Text>
            </View>
          </View>
        </View>
      </TouchableOpacity>
    );
  };

  render() {
    const { items } = this.state;
    const renderHeaderView = (
      <View style={styles.aheader}>
        <Image
          source={{
            uri: "https://p7.itc.cn/mpbp/pro/20200929/650b94a7b8a542fda242a6575f51d74f.jpeg",
          }}
          style={styles.aheader_img}
        />
        <View style={styles.aheader_context}>
          <Text style={styles.aheader_title}>mochixuan</Text>
          <Text style={styles.aheader_desc}>
            Android, React-Native, Flutter, React, Web。Learn new knowledge and
            share new knowledge.
          </Text>
        </View>
      </View>
    );
    const renderBottomView = (
      <View style={styles.abottom}>
        <Text style={styles.abottom_desc}>yarn add react-native-drag-sort</Text>
      </View>
    );
    return (
      <>
        <View style={styles.header}>
          <Text style={styles.header_title}>AnySize</Text>
        </View>
        <AnySizeDragSortableView
          ref={this.sortableViewRef}
          dataSource={items}
          keyExtractor={(item) => item.text}
          renderItem={this._renderItem}
          onDataChange={(data, callback) => {
            this.setState({ items: data }, () => {
              callback();
              console.log("移动了");
            });
          }}
          renderHeaderView={renderHeaderView}
          headerViewHeight={headerViewHeight}
          renderBottomView={renderBottomView}
          bottomViewHeight={bottomViewHeight}
          movedWrapStyle={styles.item_moved}
          onDragEnd={() => console.log("Drag end")}
          scrollIndicatorInsets={{ top: 1, left: 1, bottom: 1, right: 1 }}
          autoThrottle={100}
          autoThrottleDuration={500}
          areaOverlapRatio={0.5}
          childMarginTop={10}
          childMarginBottom={10}
          childMarginLeft={10}
          childMarginRight={10}
        />
      </>
    );
  }
}

const styles = StyleSheet.create({
  item_wrap: {
    position: "relative",
    paddingLeft: 20,
    paddingTop: 20,
  },
  item: {
    justifyContent: "space-around",
    alignItems: "center",
    backgroundColor: "#f39c12",
    borderRadius: 4,
  },
  item_clear_wrap: {
    position: "absolute",
    left: 10,
    top: 10,
    width: 20,
    height: 20,
    zIndex: 999,
  },
  item_clear: {
    width: 20,
    height: 20,
  },
  item_moved: {
    opacity: 0.95,
    borderRadius: 4,
  },
  item_icon_swipe: {
    width: 50,
    height: 50,
    backgroundColor: "#fff",
    borderRadius: 50 * 0.5,
    justifyContent: "center",
    alignItems: "center",
  },
  item_icon: {
    width: 30,
    height: 30,
    resizeMode: "contain",
  },
  item_text_swipe: {
    backgroundColor: "#fff",
    width: 56,
    height: 30,
    borderRadius: 15,
    justifyContent: "center",
    alignItems: "center",
  },
  item_text: {
    color: "#444",
    fontSize: 20,
    fontWeight: "bold",
  },
  header: {
    height: 48,
    justifyContent: "center",
    alignItems: "center",
    borderBottomColor: "#2ecc71",
    borderBottomWidth: 2,
  },
  header_title: {
    color: "#333",
    fontSize: 24,
    fontWeight: "bold",
  },
  aheader: {
    height: headerViewHeight,
    flexDirection: "row",
    borderBottomColor: "#2ecc71",
    borderBottomWidth: 2,
    zIndex: 100,
    backgroundColor: "#fff",
  },
  aheader_img: {
    width: headerViewHeight * 0.6,
    height: headerViewHeight * 0.6,
    resizeMode: "cover",
    borderRadius: headerViewHeight * 0.3,
    marginLeft: 16,
    marginTop: 10,
  },
  aheader_context: {
    marginLeft: 8,
    height: headerViewHeight * 0.4,
    marginTop: 10,
  },
  aheader_title: {
    color: "#333",
    fontSize: 20,
    marginBottom: 10,
    fontWeight: "bold",
  },
  aheader_desc: {
    color: "#444",
    fontSize: 16,
    width: width - headerViewHeight * 0.6 - 32,
  },
  abottom: {
    justifyContent: "center",
    alignItems: "center",
    height: bottomViewHeight,
    backgroundColor: "#fff",
    zIndex: 100,
    borderTopColor: "#2ecc71",
    borderTopWidth: 2,
  },
  abottom_desc: {
    color: "#333",
    fontSize: 20,
    fontWeight: "bold",
  },
});
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-drag-sort Releases](https://github.com/react-native-oh-library/react-native-drag-sort/releases)

## 属性

### DragSortableView

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>

|           Name           |                               Description                               |   Type   | Required |  Platform   | HarmonyOS Support |
| :----------------------: | :---------------------------------------------------------------------: | :------: | :------: | :---------: | :---------------: |
|    **dataSource**        |                       DataSource array for list                         |  array   |   Yes    | iOS/Android |        Yes        |
|     **parentWidth**      |                              parent width                               |  number  |    No    | iOS/Android |        Yes        |
|  **childrenHeight**      |                            Each item height                             |  number  |   Yes    | iOS/Android |        Yes        |
|   **childrenWidth**      |                             Each item width                             |  number  |   Yes    | iOS/Android |        Yes        |
|  **marginChildrenTop**   | So the item's outermost view adds margin, you can only use this method. |  number  |    No    | iOS/Android |        Yes        |
| **marginChildrenBottom** |                           Item bottom margin                            |  number  |    No    | iOS/Android |        Yes        |
|  **marginChildrenLeft**  |                           Item left margin                              |  number  |    No    | iOS/Android |        Yes        |
| **marginChildrenRight**  |                           Item right margin                             |  number  |    No    | iOS/Android |        Yes        |
|       **sortable**       |                          Do not allow dragging                          |   bool   |    No    | iOS/Android |        Yes        |
|     **onClickItem**      |                                  click                                  | function |    No    | iOS/Android |        Yes        |
|     **onDragStart**      |                        Called after dragging starts                     | function |    No    | iOS/Android |        Yes        |
|      **onDragEnd**       |                        Called after dragging end                     | function |    No    | iOS/Android |        Yes        |
|     **onDataChange**     |           This method is called every time the data changes.            | function |    No    | iOS/Android |        Yes        |
|    **renderItem**        |                            render item view                             | function |   Yes    | iOS/Android |        Yes        |
|      **fixedItems**      |                                no remove                                |  array   |    No    | iOS/Android |        Yes        |
|     **keyExtractor**     |                           (item,index) => key                           | function |    No    | iOS/Android |        Yes        |
|    **delayLongPress**    |                            Long press delay                             |  number  |    No    | iOS/Android |        Yes        |
|     **isDragFreely**     |                     Whether to limit the drag space                     |   bool   |    No    | iOS/Android |        Yes        |
|      **onDragging**      |                          Called when dragging                           | function |    No    | iOS/Android |        Yes        |
|       **maxScale**       |                              max Scale                                  |  number  |    No    | iOS/Android |        Yes        |
|      **minOpacity**      |                              min Opacity                                |  number  |    No    | iOS/Android |        Yes        |
|      **scaleStatus**     |                              scale   status                                |  string  |    No    | iOS/Android |        Yes        |
|      **scaleDuration**   |                              scale duration                                |  number  |    No    | iOS/Android |        Yes        |
|      **slideDuration**   |                              slide Duration                               |  number  |    No    | iOS/Android |        Yes        |

### AutoDragSortableView

|           Name            |     Description         |                           Type                           | Required |  Platform   | HarmonyOS Support |
| :-----------------------: | :----------------------:| :------------------------------------------------------: | :------: | :---------: | :---------------: |
|    **dataSource**        |                       DataSource array for list                         |  array   |   Yes    | iOS/Android |        Yes        |
|     **parentWidth**      |                              parent width                               |  number  |    No    | iOS/Android |        Yes        |
|  **childrenHeight**      |                            Each item height                             |  number  |   Yes    | iOS/Android |        Yes        |
|   **childrenWidth**      |                             Each item width                             |  number  |   Yes    | iOS/Android |        Yes        |
|  **marginChildrenTop**   | So the item's outermost view adds margin, you can only use this method. |  number  |    No    | iOS/Android |        Yes        |
| **marginChildrenBottom** |                           Item bottom margin                            |  number  |    No    | iOS/Android |        Yes        |
|  **marginChildrenLeft**  |                           Item left margin                              |  number  |    No    | iOS/Android |        Yes        |
| **marginChildrenRight**  |                           Item right margin                             |  number  |    No    | iOS/Android |        Yes        |
|       **sortable**       |                          Do not allow dragging                          |   bool   |    No    | iOS/Android |        Yes        |
|     **onClickItem**      |                                  click                                  | function |    No    | iOS/Android |        Yes        |
|     **onDragStart**      |                        Called after dragging starts                     | function |    No    | iOS/Android |        Yes        |
|      **onDragEnd**       |                        Called after dragging end                     | function |    No    | iOS/Android |        Yes        |
|     **onDataChange**     |           This method is called every time the data changes.            | function |    No    | iOS/Android |        Yes        |
|    **renderItem**        |                            render item view                             | function |   Yes    | iOS/Android |        Yes        |
|      **fixedItems**      |                                no remove                                |  array   |    No    | iOS/Android |        Yes        |
|     **keyExtractor**     |                           (item,index) => key                           | function |    No    | iOS/Android |        Yes        |
|    **delayLongPress**    |                            Long press delay                             |  number  |    No    | iOS/Android |        Yes        |
|     **isDragFreely**     |                     Whether to limit the drag space                     |   bool   |    No    | iOS/Android |        Yes        |
|      **onDragging**      |                          Called when dragging                           | function |    No    | iOS/Android |        Yes        |
|       **maxScale**       |                              max Scale                                  |  number  |    No    | iOS/Android |        Yes        |
|      **minOpacity**      |                              min Opacity                                |  number  |    No    | iOS/Android |        Yes        |
|      **scaleStatus**     |                              scale   status                                |  string  |    No    | iOS/Android |        Yes        |
|      **scaleDuration**   |                              scale duration                                |  number  |    No    | iOS/Android |        Yes        |
|      **slideDuration**   |                              slide Duration                               |  number  |    No    | iOS/Android |        Yes        |
|     **autoThrottle**      |     auto  throttle      |                          number                          |    No    | iOS/Android |        Yes        |
| **autoThrottleDuration**  |   auto throttle duration|                          number                          |    No    | iOS/Android |        Yes        |
|   **renderHeaderView**    |    render header View   |                         element                          |    No    | iOS/Android |        Yes        |
|   **headerViewHeight**    |    header view height   |                          number                          |    No    | iOS/Android |        Yes        |
| **scrollIndicatorInsets** |    margin on scroll     | ({top:number, left:number, bottom:number, right:number}) |    No    | iOS |        NO        |
|   **renderBottomView**    |    render Bottom View   |                         element                          |    No    | iOS/Android |        Yes        |
|   **bottomViewHeight**    |    bottom view height   |                          number                          |    No    | iOS/Android |        Yes        |
|   **onScrollListener**    | Listening callback during scrolling|          (event: NativeSyntheticEvent) => void           |    No    | iOS/Android |        Yes        |
|      **onScrollRef**      |scroll reference callback|                    (ref: any) => void                    |    No    | iOS/Android |        Yes        |

### AnySizeDragSortableView

|           Name            |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
| :-----------------------: | :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|     **renderItem**         |                 render item view                  |                         function                         |   Yes    | iOS/Android |        Yes        |
|     **onDataChange**      | This method is called every time the data changes |                         function                         |   Yes    | iOS/Android |        Yes        |
|   **renderHeaderView**    |         render Header View                        |                         element                          |    No    | iOS/Android |        Yes        |
|   **headerViewHeight**    |         header view height                        |                          number                          |    No    | iOS/Android |        Yes        |
|   **renderBottomView**    |         render Bottom View                        |                         element                          |    No    | iOS/Android |        Yes        |
|   **bottomViewHeight**    |         bottom view height                        |                          number                          |    No    | iOS/Android |        Yes        |
|     **autoThrottle**      |          auto  throttle                           |                          number                          |    No    | iOS/Android |        Yes        |
| **autoThrottleDuration**  |         auto throttle duration                    |                          number                          |    No    | iOS/Android |        Yes        |
| **scrollIndicatorInsets** |         margin on scroll                          | ({top:number, left:number, bottom:number, right:number}) |    No    | iOS/Android |        No        |
|   **onScrollListener**    |Listening callback during scrolling                |          (event: NativeSyntheticEvent) => void           |    No    | iOS/Android |        Yes        |
|      **onScrollRef**      | scroll reference callback                         |                    (ref: any) => void                    |    No    | iOS/Android |        Yes        |
|   **areaOverlapRatio**    |             Must be greater than 0.5              |                          number                          |    No    | iOS/Android |        Yes        |
|    **movedWrapStyle**     |                       style                       |                        StyleProp                         |   Yes    | iOS/Android |        Yes        |
|    **childMarginTop**     |           Subpage top margin                      |                          number                          |    No    | iOS/Android |        Yes        |
|   **childMarginBottom**   |          Subpage bottom margin                    |                          number                          |    No    | iOS/Android |        Yes        |
|    **childMarginLeft**    |           Subpage left margin                     |                          number                          |    No    | iOS/Android |        Yes        |
|   **childMarginRight**    |           Subpage right margin                    |                          number                          |    No    | iOS/Android |        Yes        |
|       **onDragEnd**       |          Called after dragging end                |                         function                         |    Yes    | iOS/Android |        Yes        |
|     **dataSource**        |          DataSource array for list                |                          array                           |   Yes    | iOS/Android |        Yes        |
|     **keyExtractor**      |        item's unique key                          |                   (item,index) => key                    |   Yes    | iOS/Android |        Yes        |

## 遗留问题

- [ ] scrollIndicatorInsets属性不生效: [issue#179](https://github.com/mochixuan/react-native-drag-sort/issues/179)

## 其他

## 开源协议

本项目基于 [The Apache License (Apache)](https://github.com/mochixuan/react-native-drag-sort/blob/master/LICENSE) ，请自由地享受和参与开源。
