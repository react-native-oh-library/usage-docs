> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-waterflow-list</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ZakZheng/react-native-waterflow-list">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ZakZheng/react-native-waterflow-list/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/ZakZheng/react-native-waterflow-list)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm i react-native-waterflow-list@1.2.3
```

#### **yarn**

```bash
yarn add react-native-waterflow-list@1.2.3
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from 'react';
import { Dimensions, Image, RefreshControl, Text, View } from 'react-native';
import { IColumnsHandles } from 'react-native-waterflow-list/src/Columns';
import WaterFlow from 'react-native-waterflow-list/src/';

const width = Math.round((Dimensions.get('screen').width - 30) / 2);

const getItemData = (() => {
  let id = 0;
  return () => {
    id++;
    const height = Math.ceil(Math.random() * 1000);
    return {
      id,
      text: Math.random(),
      image_path: `https://picsum.photos/${width}/${height}/?random`,
      height,
      width,
    };
  };
})();

const sleep = (ms: number) => {
  return new Promise(resolve => setTimeout(resolve, ms));
};

const itemDataFactory = () =>
  Array(10)
    .fill('')
    .map(() => getItemData());

interface IItem {
  id: number
  [index: string]: any
}

export default () => {
  const [data, setData] = React.useState<IItem[]>([]);
  const [loading, setLoading] = React.useState(false)

  const WaterFlowRef = React.useRef<IColumnsHandles>()
  const onLoadMore = React.useCallback(async () => {
    setLoading(true)
    await sleep(1000);
    setLoading(false)
    return setData(data.concat(itemDataFactory()));
  }, [data]);
  const loadData = React.useCallback(async () => {
    await sleep(1000);
    return setData(itemDataFactory());
  }, [data])

  React.useEffect(() => {
    setData(itemDataFactory());
  }, []);

  return (
    <WaterFlow
      ref={WaterFlowRef}
      data={data}
      keyForItem={item => item.id}
      numColumns={2}
      onEndReached={onLoadMore}
      //Custom Scroll Listener(if needed)
      onScroll={(e) => {console.log(e)}}
      columnFlatListProps={{
        style: { marginHorizontal: 5, },
      }}
      columnsFlatListProps={{
        ListHeaderComponent: () => <View><Text>Hello</Text></View>,
        refreshControl: <RefreshControl
          style={{ zIndex: 10 }}
          refreshing={loading}
          onRefresh={() => {
            WaterFlowRef.current?.clear()
            loadData()
          }}
          tintColor={'gray'}
        />
        ,
        style: { marginHorizontal: 10, },
      }}
      renderItem={({ item, index }) => {
        return renderItem(item);
      }}
    />
  );
};

```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH:0.72.29; SDK:HarmonyOS NEXT Developer Beta6 SDK; IDE:DevEco Studio 5.0.3.706; ROM:NEXT.0.0.60;
1. RNOH: 0.72.33; SDK: Openharmony 5.0.0.71(API Version 12 Release); IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> 详情见 [react-native-waterflow-list 源库地址](https://github.com/ZakZheng/react-native-waterflow-list)

| Name                      | Description                                                                                              | Type                                                         | Required | Platform                  | HarmonyOS Support |
| :-------------------------- | :------------------------------------------------------------------------------------------------ | :------------------------------------------------------------: | :--------: | :---------------------: |:--------------:|
| **data**           | 列表数据, 数据类型必须为 `Object`              | Object[]                                              | Yes | All                   | Yes          |
| **numColumns**           | 列数                    | number                                              | No | All                   | Yes          |
| **keyForItem**                   | 用以检测是否以渲染该数据                                                                      | string                                        | Yes    | All                   | Yes          |
| **heightForItem**                  | 如 renderItem 高度已知,则传入以提高性能和加载速度 | number                                                  | No       | All                   | Yes          |
| **asyncHeightForItem**                 | 如item的高度为异步获取的,则通过该函数返回item的真实高度 | Promise(number)                                      | No       | All | Yes           |
| **renderItem**                    | 渲染列表条目 | JSX.Element                        | Yes    | All  | Yes           |
| **onEndReached**       | 上拉加载, 若传入 Promise 对象, 则须等待 Promise 事件回调后方能再次触发此事件. 若其他则不作处理 | function                                            | No       | All  | Yes           |
| **columnsFlatListProps** | 外层 FlatList 参数           | FlatListProps                                      | No       | All  | Yes           |
| **columnFlatListProps**                 | 列 FlatList 参数 | FlatListProps                                          | No       | All  | Yes           |

## Static Methods
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ----- | :-----------| :--: |:--------:| :------: |:-----------------:|
| **clear** | 清空渲染列表, 一般用于下拉刷新获取到数据化,清空之前的数据 | function |    No    | All |        Yes        |


## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ZakZheng/react-native-waterflow-list/blob/master/LICENSE).