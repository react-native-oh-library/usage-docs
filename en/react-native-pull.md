> Template version: v0.2.2

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



> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-pull)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-pull/releases](https://github.com/react-native-oh-library/react-native-pull/releases). For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


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

The following code shows the basic use scenario of the repository:

> [!WARNING] The library name imported during use remains unchanged.

**PullViewDemo**

> code example

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
     testObj.pushing = 'x:' + gesturePosition.x + '------' + 'y: ' + gesturePosition.y
     setData(testObj)
 };
	const topIndicatorRender = (pulling, pullok, pullrelease) => {
     if (pulling) {
         setCount('Pull-to-refresh: pulling...')
     } else if (pullok) {
         setCount('Release-to-refresh: pullok...')
     } else if (pullrelease) {
         setCount('Refreshing: pullrelease...')
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

> code example

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
        testObj.pushing = 'x:' + gesturePosition.x + '------' + 'y: ' + gesturePosition.y
        setData(testObj)
    };

    const topIndicatorRender = (pulling, pullok, pullrelease) => {
      if (pulling) {
          setCount('Current PullList state: pulling...')
      } else if (pullok) {
          setCount('Current PullList state: pullok...')
      } else if (pullrelease) {
          setCount('Current PullList state: pullrelease...')
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
      // Logic for loading data
      setRefreshing(true)
      // After data loading is completed
      setTimeout(() => {
        setRefreshing(false)
      }, 2000); // Assuming that data loading takes 2 seconds
    };
    const refreshControl = (
      <RefreshControl
        refreshing={refreshing}
        onRefresh={onRefresh}
        tintColor="#ff0000" // Optional, set the color of the refresh indicator
        title="Loading..." // Optional, set the text displayed when refreshing
        colors={['#ff0000', '#00ff00', '#0000ff']} // Optional, set the color array for the refresh indicator
        progressBackgroundColor="#ffffff" // Optional, set progress background color
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
                scrollEventThrottle: 16, // Reduce the delay of scrolling events and improve the responsiveness of scrolling
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

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-pull/releases](https://github.com/react-native-oh-library/react-native-pull/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**`PullView` & `PullList` Pull down effect attribute**

| Name                 | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| `style`              | Sets the component style, such as width, height, and background color. | Style    | no       | android,ios | yes               |
| `onPulling`          | Called when the component is in the **pulling** state.       | function | no       | android,ios | yes               |
| `onPullOk`           | Called when the component is in the **pullok** state.        | function | no       | android,ios | yes               |
| `onPullRelease`      | Called when the component is in the **pullrelease** state. This function contains the **resolve **parameter. You should call **resolve()** at the end. | function | no       | android,ios | yes               |
| `onPushing`          | Called when the component is in the **pushing** state. This function contains the **gesturePosition** parameter, which is a **{x, y}** object in JSON format. When the component is pulled from top to bottom, the value of **gesturePosition.y** is greater than 0. When the object is pushed from bottom to top, the value of **gesturePosition.y** is less than 0. | function | no       | android,ios | yes               |
| `topIndicatorRender` | Renders the top indicator component. This function contains four parameters: **ispulling**, **ispullok**, **ispullrelease** and **gesturePosition**. You can use **gesturePosition** to define the animation header. | function | no       | android,ios | yes               |
| `topIndicatorHeight` | Specifies the height of the top indicator component. This property is necessary when **topIndicatorRender** is defined. | number   | no       | android,ios | yes               |
| `isPullEnd`          | Indicates whether the pull-down ends. If the value is **true**, the top indicator component is hidden. This parameter is optional. | boolean  | no       | android,ios | yes               |
| `onRefresh`          | Called when the refresh starts.                              | function | no       | android,ios | yes               |
| `refreshing`         | Indicates whether the component is being refreshed.          | function | no       | android,ios | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/greatbsky/react-native-pull/blob/master/LICENSE).