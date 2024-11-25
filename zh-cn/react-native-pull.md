> 模板版本：v0.2.2

<p align="center">
<h1 align="center"> <code>react-native-pull</code> </h1>
</p>
<p align="center">
 <a href="https://github.com/greatbsky/react-native-pull/blob/master">
     <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
 </a>
     <a href="https://github.com/greatbsky/react-native-pull/blob/master/LICENSE">
     <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
 </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-pull)

## 安装与使用

请到三方库的地址查看配套的版本信息：[@react-native-oh-tpl/react-native-pull/releases](https://github.com/react-native-oh-library/react-native-pull/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-pull
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-pull
```

<!-- tabs:end -->

下面的demo代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

**PullViewDemo**

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

> 代码示例

```jsx
import React, { Component, useState } from 'react';
import {
  StyleSheet,
  Text,
  View,
  ActivityIndicator,
  Dimensions,
  RefreshControl
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
    const [stateList, setStateList] = useState(
         [
                 {
                   id: 1,
                   title: '------>Item1',
                 },
                 {
                   id: 2,
                   title: '------>Item2',
                 },
                 {
                   id: 3,
                   title: '------>Item3',
                 },
                 {
                   id: 4,
                   title: '------>Item4',
                 },
                 {
                   id: 5,
                   title: '------>Item5',
                 },
                 {
                   id: 6,
                   title: '------>Item6',
                 },
                 {
                   id: 7,
                   title: '------>Item7',
                 },
                 {
                   id: 8,
                   title: '------>Item8',
                 },
                 {
                   id: 9,
                   title: '------>Item9',
                 },
                  {
                    id: 10,
                    title: '------>Item10',
                  },
                  {
                    id: 11,
                    title: '------>Item11',
                  },
                  {
                    id: 12,
                    title: '------>Item12',
                  },
               ]
    );

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
         setStateList([
                                       {
                                         id: 1,
                                         title: '------>Item1',
                                       },
                                       {
                                         id: 2,
                                         title: '------>Item2',
                                       },
                                       {
                                         id: 3,
                                         title: '------>Item3',
                                       },
                                       {
                                         id: 4,
                                         title: '------>Item4',
                                       },
                                       {
                                         id: 5,
                                         title: '------>Item5',
                                       },
                                       {
                                         id: 6,
                                         title: '------>Item6',
                                       },
                                       {
                                         id: 7,
                                         title: '------>Item7',
                                       },
                                       {
                                         id: 8,
                                         title: '------>Item8',
                                       },
                                       {
                                         id: 9,
                                         title: '------>Item9',
                                       },
                                        {
                                          id: 10,
                                          title: '------>Item10',
                                        },
                                        {
                                          id: 11,
                                          title: '------>Item11',
                                        },
                                        {
                                          id: 12,
                                          title: '------>Item12',
                                        },
                                     ]);
            resolve();
        }, 3000);
    };


    const onPushing = (gesturePosition) => {
        testObj.pushing= 'x:' + gesturePosition.x + '------' + 'y：' + gesturePosition.y
        setData(testObj)
    };

    const topIndicatorRender = (pulling, pullok, pullrelease) => {
      if (pulling) {
          setCount('当前PullList状态: pulling...')
      } else if (pullok) {
          setCount('当前PullList状态: pullok......')
      } else if (pullrelease) {
          setCount('当前PullList状态: pullrelease......')
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
      const list = []
      const num = stateList.length
        for(var i = 0; i < 5; i++) {
            list.push({
                id: (i + 1 + num) + '',
                title: `------>Item${(i+num+1)}`,
            })
        }
       setTimeout(() => {
          setStateList([...stateList,...list]);
        }, 1000);
    }

    const [refreshing, setRefreshing] = useState(false)
    const onRefresh = () => {
      // 加载数据的逻辑
      setRefreshing(true)
      // 数据加载完成后
      setTimeout(() => {
        setRefreshing(false)
      }, 2000); // 假设数据加载需要2秒
    };
    const refreshControl = (
      <RefreshControl
        refreshing={refreshing}
        onRefresh={onRefresh}
        tintColor="#ff0000" // 可选，设置刷新指示器的颜色
        title="Loading..." // 可选，设置刷新时显示的文本
        colors={['#ff0000', '#00ff00', '#0000ff']} // 可选，设置刷新指示器的颜色数组
        progressBackgroundColor="#ffffff" // 可选，设置进度背景色
      />
    );

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
            scrollViewProps={{
                scrollEventThrottle: 16, // 减少滚动事件的延迟，提高滚动的响应性
              }}
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
    flexDirection: 'column',
    backgroundColor: '#F5FCFF',
    width:'100%',
    height:'100%',
    overflow: 'scroll'
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});

export default PullListDemo;

```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-pull/releases](https://github.com/react-native-oh-library/react-native-pull/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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

本项目基于 [The MIT License (MIT)](https://github.com/greatbsky/react-native-pull/blob/master/LICENSE) ，请自由地享受和参与开源。
