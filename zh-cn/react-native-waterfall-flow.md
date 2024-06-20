> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-waterfall-flow</code> </h1>
</p>
<p align="center">
    <a href="https://www.npmjs.com/package/react-native-waterfall-flow">       
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/axerjs/react-native-waterfall-flow/blob/HEAD/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!tip]
>
>  [Github 地址](https://github.com/axerjs/react-native-waterfall-flow)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-waterfall-flow@1.1.5 --save
```

#### **yarn**

```bash
yarn add react-native-waterfall-flow@1.1.5 --save
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

<!-- {% raw %} -->
```js
import { PureComponent, Component } from 'react'
import { View, Dimensions, Image, Animated, ImageProps, ActivityIndicator, Text, Platform, TouchableOpacity, Alert } from 'react-native'
import WaterfallFlow from 'react-native-waterfall-flow'

const window = Dimensions.get('window')

export default class TestWaterfallFlowScreenTow extends Component {

  constructor(props) {
    super(props)

    this.state = {
      data: [],
      refreshing: false,
      noMore: false,
      inited: false
    }
    this.page = 1
    this.pageSize = 10
    this.loading = false
    this.listRef = null
  }

  componentDidMount() {

    this.loadData(1)

    setTimeout(() => {
      //this.listRef.scrollToIndex({ index: 6,viewPosition:1 })
      //this.listRef.scrollToEnd()
      // this.listRef.scrollToOffset({ offset: 200 })
    }, 3000)
  }

  loadData = (page = 1, refreshing) => {
    if (this.loading) {
      return
    }
    this.loading = true
    if (refreshing) {r
      this.setState({
        refreshing: true
      })
    } 
    setTimeout(() => { // mock request data
      const imgList = [
        {
          "thumbURL": "https://img1.baidu.com/it/u=2226443709,1655735334&fm=253&fmt=auto&app=120&f=JPEG?w=690&h=1226",
          "title": "尾页,好看的风景锁屏壁纸,唯美天空手机壁纸",
          "width": 690,
          "height": 1226
        },
        {
          "thumbURL": "https://img1.baidu.com/it/u=1864407977,4278108853&fm=253&fmt=auto&app=138&f=JPEG?w=333&h=499",
          "title": "唯美意境图片田园景色手机壁纸第一辑-风景-壁纸下载-美桌网",
          "width": 640,
          "height": 960
        },
        {
          "thumbURL": "https://img1.baidu.com/it/u=1884825806,3687074543&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=889",
          "title": "大自然唯美风景图片手机壁纸",
          "width": 1080,
          "height": 1920
        },
        {
          "thumbURL": "https://img2.baidu.com/it/u=241902442,933965745&fm=253&fmt=auto&app=120&f=JPEG?w=540&h=960",
          "title": "好看唯美的自然风光手机壁纸-风景-手机壁纸下载-美桌网",
          "width": 540,
          "height": 960
        },
        {
          "thumbURL": "https://img1.baidu.com/it/u=1605135781,4151997734&fm=253&fmt=auto&app=138&f=JPEG?w=281&h=499",
          "title": "唯美瀑布高清大自然风景图片壁纸",
          "width": 640,
          "height": 1137
        },
        {
          "thumbURL": "https://img0.baidu.com/it/u=1303418658,2016567117&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=889",
          "title": "手机动漫风景图片壁纸2",
          "width": 576,
          "height": 1024
        },
        {
          "thumbURL": "https://img1.baidu.com/it/u=1094974745,1772917056&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=750",
          "title": "清新的大海景色640x960唯美手机壁纸大图",
          "width": 640,
          "height": 960
        },
        {
          "thumbURL": "https://img0.baidu.com/it/u=2608390028,4097355289&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=751",
          "title": "高清风景图片竖屏最美(2)",
          "width": 500,
          "height": 751
        }]
      const newData = imgList.slice((page - 1) * this.pageSize, page * this.pageSize).map(img => {
        const { width, height } = img
        const cardWidth = Math.floor(window.width / 2)
        return {
          ...img, 
          width: cardWidth,
          height: Math.floor(height / width * cardWidth)
        }
      })
      const noMore = newData.length < this.pageSize
      this.loading = false
      this.page = refreshing ? 1 : page
      this.setState({
        data: refreshing ? newData : this.state.data.concat(newData),
        refreshing: false,
        noMore,
        inited: true
      })
    }, refreshing ? 1000 : 500)
  }

  onEndReached = () => {
    if (!this.state.noMore) {
      this.loadData(this.page + 1)
    }
  }

  render() {
    const { data, refreshing, noMore, inited } = this.state
    return (
      <WaterfallFlow
        ref={ref => this.listRef = ref}
        style={{ flex: 1 }}
        contentContainerStyle={{ backgroundColor: '#f9f9f9' }}
        ListHeaderComponent={<Header />}
        ListFooterComponent={<Footer noMore={noMore} inited={inited} isEmpty={data.length === 0}/>}
        ListEmptyComponent={<Empty inited={inited} />}
        data={data}
        numColumns={2}
        initialNumToRender={10}
        onEndReached={this.onEndReached}
        refreshing={refreshing}
        onRefresh={() => this.loadData(1, true)}
        renderItem={({ item, index, columnIndex }) => {
          return (
            <Card item={item} index={index} columnIndex={columnIndex}/>
          )
        }}
      />
    )
  }
}

class Card extends PureComponent {
  render() {
    const { item, index, columnIndex } = this.props
    return (
      <View style={{ flex: 1, overflow: 'hidden' }}>
        <TouchableOpacity 
          style={{ backgroundColor: '#fff', flex: 1 }} 
          activeOpacity={1}
        >
          <FadeImage 
            source={{ uri: item.thumbURL, width: item.width, height: item.height }} 
            resizeMode="cover" 
          />
        </TouchableOpacity>
      </View>
    )
  }
}

class Header extends PureComponent {
  render() {
    return (
      <FadeImage 
        resizeMode="cover"  
        source={{ 
          uri: 'https://img0.baidu.com/it/u=266597227,4250059863&fm=253&fmt=auto&app=138&f=JPEG?w=500&h=281', 
          width: window.width, 
          height: 281 / 500 * window.width 
        }}
      />
    )
  }
}

class Footer extends PureComponent {
  render() {
    const { noMore, inited, isEmpty } = this.props 
    if (!inited || isEmpty) {
      return null
    }
    return (
      <View style={{ flexDirection: 'row', alignItems: 'center', justifyContent: 'center', height: 60 }}>
        {!noMore && <ActivityIndicator color="red"/>}
        <Text style={{ color: '#999', marginLeft: 8 }}>{noMore ? '我是有底线的哦~' : '加载中...'}</Text>
      </View>
    )
  }
}


class Empty extends PureComponent {
  render() {
    const { inited } = this.props
    return (
      <View style={{ flexDirection: 'row', alignItems: 'center', justifyContent: 'center', height: 300 }}>
        {!inited && <ActivityIndicator color="red"/>}
        <Text style={{ color: '#999', marginLeft: 8 }}>{inited ? '这里空空的哦~' : '获取数据中...'}</Text>
      </View>
    )
  }
}

class FadeImage extends Component<ImageProps> {

  constructor(props) {
    super(props)
    this._animatedValue = new Animated.Value(0)
  }

  render() {
    const { style, onLoadEnd } = this.props
    if (Platform.OS === 'android') {
      return <Image {...this.props}/>
    }
    return (
      <Animated.Image 
        {...this.props}
        onLoadEnd={() => {
          Animated.timing(this._animatedValue, {
            toValue: 1,
            duration: 200,
            useNativeDriver: true
          }).start()
          onLoadEnd && onLoadEnd()
        }}
        style={[style, { opacity: this._animatedValue }]} 
      />
    )
  }
}
```
<!-- {% endraw %} -->



## 约束与限制

## 兼容性

本文档内容基于以下版本验证通过：

react-native-harmony：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 属性

> [!tip] 
>
> "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] 
>
> "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                                                            | Type     | default | Required | Platform | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- | ----------------- |
| `renderItem` | 用于将当前`item`渲染到列表中 | function |  | Yes       | All      | yes               |
| `data`     | 瀑布流数据源，可以是任意内容的数组            | array |  | Yes       | All      | yes               |
| `numColumns` | 瀑布流的列数，默认为2，即两列                    | number | 2 | No   | All      | yes               |
| `ListHeaderComponent` | 头部组件。可以是 React Component 或 render 函数。                          | component`, `function |  | No       | All      | yes               |
| `ListFooterComponent` | 尾部组件。可以是 React Component 或 render 函数。 | component`, `function |  | No       | All      | yes               |
| `ListEmptyComponent` | 列表为空时渲染该组件。可以是 React Component 或 render 函数 | component`, `function |  | No       | All      | yes               |
| `onEndReached`   | 当列表滚动到底部是调用            | function |  | No       | All      | yes               |
| `onRefresh`   | 如果设置了此选项，则会在列表头部添加一个标准的[`RefreshControl`](https://www.react-native.cn/docs/refreshcontrol) 控件，以便实现“下拉刷新”的功能。同时你需要正确设置`refreshing`属性。 | function |  | No       | All      | yes               |
| `refreshing` | 在等待加载新数据时将此属性设为 true，列表就会显示出一个正在加载的符号。                   | boolean | true | No       | All      | yes               |
| `style`     | 用于设置瀑布流外层样式，默认会有`{ flex: 1 }`的样式，即高度充满父容器             | [`view styles`](https://www.react-native.cn/docs/view-style-props) |  | No       | All      | yes               |
| `contentContainerStyle` | 瀑布流内容容器样式                           | [`view styles`](https://www.react-native.cn/docs/view-style-props) |   | No   | All      | yes               |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                       | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| -------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `scrollToEnd([params])`    | 滚动到瀑布流列表的底部                                       | object | No       | All      | yes               |
| `scrollToIndex([params])`  | 将位于指定位置的元素滚动到可视区的指定位置，当viewPosition 为 0 时将它滚动到屏幕顶部，为 1 时将它滚动到屏幕底部，为 0.5 时将它滚动到屏幕中央。 | object | Yes      | All      | yes               |
| `scrollToOffset([params])` | 滚动列表到指定的偏移（以像素为单位），等同于ScrollView的scrollTo方法。 | object | Yes      | All      | yes               |

## 遗留问题

 无

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/axerjs/react-native-waterfall-flow/blob/HEAD/LICENSE) ，请自由地享受和参与开源。
