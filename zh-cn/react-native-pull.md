> 模板版本：v0.2.0

<p align="center">
<h1 align="center"> <code>react-native-pull</code> </h1>
</p>
<p align="center">
 <a href="https://github.com/react-native-oh-library/react-native-pull">
     <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
 </a>
     <a href="https://github.com/react-native-oh-library/react-native-pull/blob/main/LICENSE">
     <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
 </a>
</p>


> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-pull)

## 简介

react-native-pull包含两个（`PullView` & `PullList`）可以实现`下拉刷新`的react native组件，可支持android & ios，简单易用！

纯js代码，基于`ScrollView` & `FlatList`封装. 比scrollview & FlatList更强大，有三个下拉状态: **pulling**, **pullok**, **pullrelease**. `PullView`可以让你使用refreshControl或提供的相关属性实现类似于scrollview的pull-to-refresh. `PullList`可以让你使用`FlatList`的所有属性。你也可以使用`topIndicatorRender `和`onPushing`方法实现带有动画效果的自定义的topIndicator头部。

## 安装与使用

请到三方库的地址查看配套的版本信息：[@react-native-oh-tpl/react-native-pull/releases](https://github.com/react-native-oh-library/react-native-pull/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-pull@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-pull@file:#
```

<!-- tabs:end -->

下面的demo代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

**PullViewDemo**

![img](https://raw.githubusercontent.com/greatbsky/react-native-pull-demo/master/PullViewDemo/image/demo.gif)

> 代码示例

```js
import React, { Component, useState } from 'react';
import {
StyleSheet,
Text,
View,
ActivityIndicator,
Dimensions,
} from 'react-native';

import {PullView} from 'react-native-pull';

const PullViewDemo = () => {

const [count, setCount] = useState(0);
let testObj = {
 pulling:null,
 pullok:null,
 pullrelease:null,
 pushing:null,
 refresh:null,
 isPullEnd:null
};
const [data, setData] = useState(testObj);
const onPulling = () => {
   testObj.pulling='pulling--------->'
   setData(testObj)
};
const onPullOk = () => {
   testObj.pullok='pullok--------->'
   setData(testObj)
};
const onPullRelease = (resolve) => {
     //do something
     testObj.pullrelease='pullrelease--------->'
     setData(testObj)
     setTimeout(() => {
         resolve();
     }, 3000);
 };
 const onPushing = (gesturePosition) => {
     testObj.pushing= 'x:' + gesturePosition.x + '------' + 'y：' + gesturePosition.y
     setData(testObj)
 };
	const topIndicatorRender = (pulling, pullok, pullrelease) => {
     if (pulling) {
         setCount('下拉刷新pulling...')
     } else if (pullok) {
         setCount('松开刷新pullok......')
     } else if (pullrelease) {
         setCount('玩命刷新中pullrelease......')
     }
		return (
         <View style={{flexDirection: 'row', justifyContent: 'center', alignItems: 'center', height: 60}}>
             <ActivityIndicator size="small" color="gray" />
             {pulling ? <Text>{count}</Text> : null}
             {pullok ? <Text>{count}</Text> : null}
             {pullrelease ? <Text>{count}</Text> : null}
 		</View>
     );
	};

 return (
   <View style={[styles.container]}>
		<PullView style={{width: Dimensions.get('window').width}}
           onPulling={onPulling}
           onPullOk={onPullOk}
           isPullEnd={true}
           onPullRelease={onPullRelease}
           onPushing={onPushing}
           topIndicatorRender={topIndicatorRender}
           topIndicatorHeight={60}>
			<View style={{backgroundColor: '#eeeeee'}}>
			    <Text>1***************</Text>
             <Text>onPulling:{testObj.pulling}</Text>
             <Text>3</Text>
             <Text>onPullOk:{testObj.pullok}</Text>
             <Text>5</Text>
             <Text>onPullRelease:{testObj.pullrelease}</Text>
             <Text>7</Text>
             <Text>onPushing:{testObj.pushing}</Text>
             <Text>9</Text>
         </View>
     </PullView>
   </View>
 );
           > };
export default PullViewDemo;
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
});
```

**PullListDemo**

![img](https://raw.githubusercontent.com/greatbsky/react-native-pull-demo/master/PullListDemo/image/demo.gif)

> 代码示例

```jsx
import React, { Component, useState } from 'react';
import {
  StyleSheet,
  Text,
  View,
  ActivityIndicator,
  Dimensions,
} from 'react-native';
import {PullList} from 'react-native-pull';

const PullListDemo = () => {
  let testObj = {
    pulling:null,
    pullok:null,
    pullrelease:null,
    pushing:null,
    refresh:null,
    isPullEnd:null
   };

   const [count, setCount] = useState(0);
   const [data, setData] = useState(testObj);
    const [stateList, setStateList] = useState([
      {
        id: 'bd7acbea-c1b1-46c2-aed5-3ad53abb2cba',
        title: 'First Item1',
      },
      {
        id: '3ac68afc-c605-48d3-a4f8-fbd91a397f63',
        title: 'Second Item2',
      },
      {
        id: '58694a0f-3da1-471f-bd96-145573e29d72',
        title: 'Third Item3',
      },
      {
        id: 'bd7acbea-c1b1-26c2-aed5-3ad53abb2cba',
        title: 'First Item4',
      },
      {
        id: '3ac68afc-c605-4843-a4f8-fbd91a397f63',
        title: 'Second Item5',
      },
      {
        id: '58694a0f-3da1-451f-bd96-145573e29d72',
        title: 'Third Item6',
      },
    ]);

   const onPulling = () => {
      testObj.pulling='pulling--------->'
      setData(testObj)
   };

   const onPullOk = () => {
      testObj.pullok='pullok--------->'
      setData(testObj)
   };

   const onPullRelease = (resolve) => {
        //do something
        testObj.pullrelease='pullrelease--------->'
        setData(testObj)
        setTimeout(() => {
            resolve();
        }, 3000);
    };


    const onPushing = (gesturePosition) => {
        testObj.pushing= 'x:' + gesturePosition.x + '------' + 'y：' + gesturePosition.y
        setData(testObj)
    };

    const topIndicatorRender = (pulling, pullok, pullrelease) => {
      if (pulling) {
          setCount('下拉刷新pulling...')
      } else if (pullok) {
          setCount('松开刷新pullok......')
      } else if (pullrelease) {
          setCount('玩命刷新中pullrelease......')
      }

  return (
      <View style={{flexDirection: 'row', justifyContent: 'center', alignItems: 'center', height: 60}}>
          <ActivityIndicator size="small" color="gray" />
          {pulling ? <Text>{count}</Text> : null}
          {pullok ? <Text>{count}</Text> : null}
          {pullrelease ? <Text>{count}</Text> : null}
      </View>
  );
};


    const renderHeader = () => {
      return (
          <View style={{height: 50, backgroundColor: '#eeeeee', alignItems: 'center', justifyContent: 'center'}}>
              <Text style={{fontWeight: 'bold'}}>This is header</Text>
          </View>
      );
    }

   const renderRow = ({item}) => {
     console.log('renderRow', item.title)
      return (
          <View style={{height: 50, backgroundColor: '#fafafa', alignItems: 'center', justifyContent: 'center'}}>
              <Text>{item.title}</Text>
          </View>
      );
    }

   const renderFooter = () => {
      return (
          <View style={{height: 100}}>
              <ActivityIndicator />
          </View>
      );
    }

   const loadMore = () => {
      const list = [ {
        id: 'bd7acbea-c1b1-46c2-aed5-3ad53abb28ba',
        title: 'First Item',
      }]
        for(var i = 0; i < 5; i++) {
            list.push({
                id: (i + 1) + '',
                title: `this is ${i}`,
            })
        }
        setTimeout(() => {
          setStateList([...stateList,...list]);
        }, 1000);
    }
    return (
      <View style={[styles.container]}>
		<PullList style={{width: Dimensions.get('window').width}}
          onPulling={onPulling}
          onPullOk={onPullOk}
          isPullEnd={true}
          onPullRelease={onPullRelease}
          onPushing={onPushing}
          topIndicatorRender={topIndicatorRender}
          topIndicatorHeight={60}
          pageSize={5}
          initialListSize={5}
          onEndReached={loadMore}
          onEndReachedThreshold={60}
          renderItem={renderRow}
          ListFooterComponent={renderFooter}
          ListHeaderComponent={renderHeader}
          data={stateList}
          keyExtractor={(item:any) => item.id}
        />
      </View>
    );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
});

export default PullListDemo;

```

## 约束与限制

### 兼容性
本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.21;

请到三方库相应的发布地址查看版本信息：[@react-native-oh-tpl/react-native-pull/releases](https://github.com/react-native-oh-library/react-native-pull/releases)

## 属性配置项

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**`PullView` & `PullList` 下拉效果属性**

| Name                 | Description                                                                                                                                                                | Type     | Required | Platform    | HarmonyOS Support |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| `style`              | 设置组件样式，比如可以设置width/height/backgroudColor等                                                                                                                    | Style    | no       | android,ios | yes               |
| `onPulling`          | 处于`pulling`状态时执行的方法                                                                                                                                              | function | no       | android,ios | yes               |
| `onPullOk`           | 处于`pullok`状态时执行的方法                                                                                                                                               | function | no       | android,ios | yes               |
| `onPullRelease`      | 处于`pullrelease`状态时执行的方法，接受一个参数：`resolve`，最后执行完操作后应该调用`resolve()`。                                                                          | function | no       | android,ios | yes               |
| `onPushing`          | 当从下往上推时执行的方法，接受一个参数：`gesturePosition`。gesturePosition是json格式{x, y}对象，当从上往下拉时gesturePosition.y > 0，当从下往上推时gesturePosition.y < 0。 | function | no       | android,ios | yes               |
| `topIndicatorRender` | 顶部刷新指示组件的渲染方法, 接受4个参数: `ispulling`, `ispullok`, `ispullrelease`，`gesturePosition`，你可以使用`gesturePosition`定义动画头部。                            | function | no       | android,ios | yes               |
| `topIndicatorHeight` | 顶部刷新指示组件的高度, 若定义了topIndicatorRender则同时需要此属性                                                                                                         | number   | no       | android,ios | yes               |
| `isPullEnd`          | 是否已经下拉结束，若为true则隐藏顶部刷新指示组件，非必须                                                                                                                   | boolean  | no       | android,ios | yes               |
| `onRefresh`          | 开始刷新时调用的方法                                                                                                                                                       | function | no       | android,ios | yes               |
| `refreshing`         | 指示是否正在刷新                                                                                                                                                           | function | no       | android,ios | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-pull/blob/main/LICENSE) ，请自由地享受和参与开源。
