> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-largelist</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bolan9999/react-native-largelist">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bolan9999/react-native-largelist/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-largelist)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-largelist Releases](https://github.com/react-native-oh-library/react-native-largelist/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-largelist
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-largelist
```
<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
// Largelist
import React from "react";
import { StyleSheet, Text, View } from "react-native";
import { LargeList } from "react-native-largelist";

export class HeightEqualExample extends React.Component {
  _sectionCount = 10;
  _rowCount = 10;

  render() {
    const data = [];
    for (let section = 0; section < this._sectionCount; ++section) {
      const sContent = { items: [] };
      for (let row = 0; row < this._rowCount; ++row) {
        sContent.items.push(row);
      }
      data.push(sContent);
    }
    return (
      <LargeList
        style={styles.container}
        data={data}
        heightForSection={() => 50}
        renderSection={this._renderSection}
        heightForIndexPath={() => 50}
        renderIndexPath={this._renderIndexPath}
      />
    );
  }

  _renderSection = (section: number) => {
    return (
      <View style={styles.section}>
        <Text>
          Section {section}
        </Text>
      </View>
    );
  };

  _renderIndexPath = ({ section: section, row: row }) => {
    return (
      <View style={styles.row}>
        <Text>
          Section {section} Row {row}
        </Text>
        <View style={styles.line} />
      </View>
    );
  };
}

const styles = StyleSheet.create({
  container: {
    flex: 1
  },
  section: {
    flex: 1,
    backgroundColor: "gray",
    justifyContent: "center",
    alignItems: "center"
  },
  row: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center"
  },
  line: {
    position: "absolute",
    left: 0,
    right: 0,
    bottom: 0,
    height: 1,
    backgroundColor: "#EEE"
  }
});
```

更多示例可以查看[largelistExample](https://github.com/bolan9999/react-native-largelist/tree/master/Examples)

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-spring-scrollview 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-spring-scrollview 文档的 Link 章节](/zh-cn/react-native-spring-scrollview.md#link)进行引入

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-largelist Releases](https://github.com/react-native-oh-library/react-native-largelist/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Largelist:
| Name                           | Description                                                                                                                                                                                                                           | Type                                                                                                          | Required | Platform    | HarmonyOS Support |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| bounces                        | 滑动超出内容视图后是否可以弹性地继续滑动（iOS & Android，如果为true，水平方向内容视图如果没有超过SpringScrollView则不会有弹性，垂直方向始终具有弹性）                                                                                 | boolean                                                                                                       | no       | Android/iOS | yes               |
| scrollEnabled                  | 是否可以滚动                                                                                                                                                                                                                          | boolean                                                                                                       | no       | Android/iOS | yes               |
| initialContentOffset           | 初始化偏移，仅第一次初始化有效，后期更改无效（已支持x方向）                                                                                                                                                                           | {x:number, y:number}                                                                                          | no       | Android/iOS | yes               |
| showsVerticalScrollIndicator   | 显示垂直滚动指示器                                                                                                                                                                                                                    | boolean                                                                                                       | no       | Android/iOS | no               |
| showsHorizontalScrollIndicator | 显示水平滚动指示器（内容视图超出LargeList视口才有用）                                                                                                                                                                                 | boolean                                                                                                       | no       | Android/iOS | no               |
| tapToHideKeyboard              | 点击LargeList是否收起键盘                                                                                                                                                                                                             | boolean                                                                                                       | no       | Android/iOS | yes               |
| data                           | 列表的数据源                                                                                                                                                                                                                          | { items: any[] }[]                                                                                            | no       | Android/iOS | yes               |
| heightForSection               | 返回列表每一组组头高度的函数                                                                                                                                                                                                          | (section: number) => number                                                                                   | no       | Android/iOS | yes               |
| renderSection                  | 每一组组头的render函数                                                                                                                                                                                                                | `(section: number) => React.ReactElement <any>`                                                               | no       | Android/iOS | yes               |
| heightForIndexPath             | 返回列表每一行高度的函数                                                                                                                                                                                                              | (indexPath: IndexPath) => number                                                                              | no       | Android/iOS | yes               |
| renderIndexPath                | 每一行的render函数, mediaWrapperParam是用于大图片或视频优化选项。                                                                                                                                                                     | `(indexPath: IndexPath, mediaWrapperParam:Object) => React.ReactElement <any>`                                | no       | Android/iOS | yes               |
| renderHeader                   | 列表的头部组件函数                                                                                                                                                                                                                    | `()=> React.ReactElement <any>`                                                                               | no       | Android/iOS | yes               |
| renderFooter                   | 列表的尾部组件函数                                                                                                                                                                                                                    | `()=> React.ReactElement <any>`                                                                               | no       | Android/iOS | yes               |
| inverted                       | 翻转滚动方向，适配聊天App                                                                                                                                                                                                             | boolean                                                                                                       | no       | Android/iOS | yes               |
| onRefresh                      | 下拉刷新的回调函数,如果设置了此属性，则会在顶部加一个刷新Header                                                                                                                                                                       | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| refreshHeader                  | 选择下拉刷新的组件，用户如果不希望高度自定义，则可以不设定直接使用NormalHeader,如果需要高度自定义，请参考自定义下拉刷新                                                                                                                       | [RefreshHeader](https://github.com/bolan9999/react-native-spring-scrollview/blob/master/src/RefreshHeader.js) | no       | Android/iOS | yes               |
| onLoading                      | 上拉加载的回调函数,如果设置了此属性，则会在底部加一个加载组件                                                                                                                                                                         | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| allLoaded                      | 数据是否加载完成。                                                                                                                                                                                                                    | boolean                                                                                                       | no       | Android/iOS | yes               |
| loadingFooter                  | 上拉加载组件，用户如果不希望自定义，则可以使用NormalFooter,如果需要高度自定义，请参考自定义上拉加载                                                                                                                                          | [LoadingFooter](https://github.com/bolan9999/react-native-spring-scrollview/blob/master/src/LoadingFooter.js) | no       | Android/iOS | yes               |
| onScroll                       | 监听列表滑动（JavaScript端）                                                                                                                                                                                                          | ({nativeEvent:{contentOffset:{x, y}}})=>any                                                                   | no       | Android/iOS | yes               |
| onNativeContentOffsetExtract   | 使用原生动画值监听滑动偏移，可以用作插值动画                                                                                                                                                                                          | {x?:Animated.Value, y?:Animated.Value}                                                                        | no       | Android/iOS | yes               |
| onTouchBegin                   | 手指按下时回调                                                                                                                                                                                                                        | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| onTouchEnd                     | 手指抬起时回调                                                                                                                                                                                                                        | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| onMomentumScrollBegin          | 松手后减速开始的回调                                                                                                                                                                                                                  | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| onMomentumScrollEnd            | 减速结束回调                                                                                                                                                                                                                          | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| textInputRefs                  | 将TextInput的引用传入，让SpringScrollView自动管理键盘遮挡问题。                                                                                                                                                                       | TextInput[]                                                                                                   | no       | Android/iOS | yes               |
| dragToHideKeyboard             | 滑动屏幕时是否隐藏键盘                                                                                                                                                                                                                | boolean                                                                                                       | no       | Android/iOS | yes               |
| inputToolBarHeight             | 不同的系统，不同的三方输入法，键盘的工具栏高度是不确定的，并且官方没有给出获取工具栏高度的办法，这个属性用以给用户小幅调整键盘弹起时，组件偏移的位置                                                                                  | number                                                                                                        | no       | Android/iOS | yes               |
| groupCount                     | 优化参数，LargeList将各行进行分组（不是Section，这个视独立的组），groupCount表示总共渲染4组，每组至少渲染groupMinHeight高度，值越大预渲染的行数越多，对应的初始化越慢。请注意groupCount * groupMinHeight必须大于LargeList的视口高度。 | number                                                                                                        | no       | Android/iOS | yes               |
| groupMinHeight                 | 优化参数，每组的高度                                                                                                                                                                                                                  | number                                                                                                        | no       | Android/iOS | yes               |
| updateTimeInterval             | 更新延时，值越小请求更新的频率越高，但是React Native是异步的，请求更新过多会导致更新不过来；值越大越容易让用户看到新的Item替换旧的Item的现象。                                                                                        | number                                                                                                        | no       | Android/iOS | yes               |


### WaterfallList:
| Name              | Description                                                                                                                                                                                       | Type                                                | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- | -------- | ----------- | ----------------- |
| data              | 数据源，数组的个数决定了Item的数量                                                                                                                                                                | any[]                                               | no       | Android/iOS | yes               |
| heightForItem     | 一个高度函数，用以返回每个Item的高度                                                                                                                                                              | (item:any,index:number)=> number                    | no       | Android/iOS | yes               |
| renderItem        | 每个Item的render函数                                                                                                                                                                              | `(item:any,index:number)=> React.ReactElement<any>` | no       | Android/iOS | yes               |
| preferColumnWidth | 每个Item的理想宽度， 它会影响实际列数，实际列数等于WaterfallList除以理想宽度向下取整，实际宽度是组件宽度除以实际列数（目前只支持等宽的Item）.(preferColumnWidth 和 numColumns 至少需要指定一个. ) | number                                              | no       | Android/iOS | yes               |
| numColumns        | 固定列数. (preferColumnWidth 和 numColumns 至少需要指定一个. )                                                                                                                                    | number                                              | no       | Android/iOS | yes               |
| renderHeader      | 头部组件函数                                                                                                                                                                                      | `()=> React.ReactElement <any>	`                    | no       | Android/iOS | yes               |
| renderFooter      | 尾部组件函数                                                                                                                                                                                      | `()=> React.ReactElement <any>	`                    | no       | Android/iOS | yes               |


### StickyForm:
| Name                   | Description                                                  | Type    | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| ...LargeList           | 支持所有的LargeList属性（含刷新及加载）。                    | -       | no       | Android/iOS | yes               |
| directionalLockEnabled | 当此属性为true时，它会试着锁定只在水平或垂直一个方向上滚动。 | boolean | no       | Android/iOS | no               |
| headerStickyEnabled    | 将头部吸在StickForm的顶部，Section跟着吸在头部的下边。       | boolean | no       | Android/iOS | no               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/bolan9999/react-native-largelist/blob/master/LICENSE) ，请自由地享受和参与开源。

