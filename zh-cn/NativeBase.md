> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>NativeBase</code> </h1>
</p>
<p align="center">
   <a href="https://github.com/GeekyAnts/NativeBase">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/GeekyAnts/NativeBase/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/NativeBase)

## 安装与使用



请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/native-base Releases](https://github.com/react-native-oh-library/NativeBase/releases)，并下载适用版本的 tgz 包。


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/native-base@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/native-base@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
// NativeBaseProvider 是一个使主题可在整个应用中使用的组件。它使用 React 的 Context API。将 NativeBaseProvider 添加到应用的根目录并更新 App.js,要按如下所示使用.
import React from "react";
import { SafeAreaView, View } from "react-native";
import { NativeBaseProvider } from "native-base";

function App() {
  return (
    <NativeBaseProvider>
      <View style={{ backgroundColor: "white" }}>
        <SafeAreaView></SafeAreaView>
      </View>
    </NativeBaseProvider>
  );
}
export default App;
```

```tsx
import { StyleSheet, View } from "react-native";
import { Text } from "native-base";

export function TextTest() {
  return (
    <View style={styles.container}>
      <Text fontSize="xs">xs</Text>
      <Text fontSize="sm">sm</Text>
      <Text fontSize="md">md</Text>
      <Text fontSize="lg">lg</Text>
      <Text fontSize="xl">xl</Text>
      <Text fontSize="2xl">2xl</Text>
      <Text fontSize="3xl">3xl</Text>
      <Text fontSize="4xl">4xl</Text>
      <Text fontSize="5xl">5xl</Text>
      <Text fontSize="6xl">6xl</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    justifyContent: "center",
    alignItems: "center",
    padding: 10,
    margin: 25,
    borderRadius: 5,
    borderWidth: 3,
  },
});
```
## Link

本库依赖以下三方库，请查看对应文档：
+ [@react-native-oh-tpl/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)
+ [@react-native-oh-tpl/react-native-reanimated](/zh-cn/react-native-reanimated.md)
+ [@react-native-oh-library/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)
+ [@react-native-oh-tpl/react-native-svg](/zh-cn/react-native-svg.md)
+ [@react-native-oh-tpl/react-navigation-drawer](/zh-cn/react-navigation-drawer.md)
+ [@react-native-oh-tpl/react-native-tab-view](/zh-cn/react-native-tab-view.md)
+ [@react-native-oh-tpl/react-native-vector-icons](/zh-cn/react-native-vector-icons.md)
+ [@react-native-oh-tpl/react-native-pager-view](/zh-cn/react-native-pager-view.md)
+ [@react-native-oh-tpl/react-native-swipe-list-view](/zh-cn/react-native-swipe-list-view.md)

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-gesture-handler、@react-native-oh-tpl/react-native-reanimated、@react-native-oh-library/react-native-safe-area-context、@react-native-oh-tpl/react-native-svg、@react-native-oh-tpl/react-navigation-drawer、@react-native-oh-tpl/react-native-tab-view、@react-native-oh-tpl/react-native-vector-icons、@react-native-oh-tpl/react-native-pager-view的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档的 Link 章节](/zh-cn/react-native-gesture-handler.md#link)、[@react-native-oh-tpl/react-native-reanimated 文档的 Link 章节](/zh-cn/react-native-reanimated.md#link)、[@react-native-oh-library/react-native-safe-area-context 文档的 Link 章节](/zh-cn/react-native-safe-area-context.md#link)、[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](/zh-cn/react-native-svg.md#link)、[@react-native-oh-tpl/react-navigation-drawer 文档的 Link 章节](/zh-cn/react-navigation-drawer.md#link)、[@react-native-oh-tpl/react-native-tab-view 文档的 Link 章节](/zh-cn/react-native-tab-view.md#link)、[@react-native-oh-tpl/react-native-vector-icons 文档的 Link 章节](/zh-cn/react-native-vector-icons.md#link)、[@react-native-oh-tpl/react-native-pager-view 文档的 Link 章节](/zh-cn/react-native-pager-view.md#link)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-oh-tpl-native-base Releases](https://github.com/react-native-oh-library/NativeBase/releases)


## 组件

组件使用详情见 [NativeBase 的文档介绍](https://docs.nativebase.io)

以下为目前已支持的组件属性：

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 Yes 表示 HarmonyOS 平台支持该属性；No 则表示不支持；Web 表示仅Web支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**AspectRatio**: AspectRatio 控制节点或子组件未定义维度的大小
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        ratio         |        容器的纵横比。例如 `16/9`、`16/10`、`9/16`、`4/3`        |        Object         |    No    |   All    |        Yes        |

**Box**: 这是一个满足低级布局需求的通用组件。它类似于div在HTML中。 
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        children         |        将组件渲染为 Box 子项。接受 React.Element 或 JSX.Element 数组。 |        React.element         |    No    |   All    |        Yes        |
|        _text         |       用于为 Box 内的文本提供参数 |        Any         |    No    |   All    |        Yes        |
|        bg         |   简写设置背景    |        String         |    No    |   All    |        Yes        |
|        background         |    可以接受各种背景相关的设置，如颜色、图像、渐变等   |        String        |    No    |   All    |        Yes        |
|        bgColor         |     明确用于设置背景颜色  |        String         |    No    |   All    |        Yes        |
|        backgroundColor    |   与bgColor类似，专门用于设置背景颜色   |        String         |    No    |   All    |        Yes        |  

**Center**: 布局组件中心对齐
[继承了React Native中View参数](https://reactnative.dev/docs/view#props)

**Container**: 容器根据当前断点限制内容的宽度，同时保持尺寸的流动性。
[Container实现了Box的功能，所以所有Box的属性都能传给Container]

**Flex**: 布局组件，Flex 是 CSS flex 布局的一个封装
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        direction          |        项目定位方向，值可以为 column,column-reverse,row,row-reverse   |         String       |    No    |   All    |        Yes        |
|        wrap           |        子元素的换行方式nowrap,wrap,wrap-reverse     |         String       |    No    |   All    |        Yes        |
|        align           |         子元素在交叉轴上的对齐方式，可选baseline,normal,stretch      |         String       |    No    |   All    |        Yes        |
|        justify           |         子元素在主轴上的对齐方式，可选left,normal,right       |         String       |    No    |   All    |        Yes        |
|        basis           |         可选-moz-fit-content,-moz-max-content,-moz-min-content,-webkit-auto,auto,content,fit-content,max-content,min-contents       |         String       |    No    |   All    |        Yes        |
|        grow           |        可选Globals ,(number & {}) , (string & {})       |         Number       |    No    |   All    |        Yes        |
|        shrink           |         可选Globals , (number & {}) , (string & {});       |         Number       |    No    |   All    |        Yes        |

**HStack / Row**: HStack / Row 布局组件水平对齐
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        direction         |           堆叠项目的方向，可选row,column,column-reverse,row-reverse     |        String         |    No    |   All    |        Yes        |

**Stack**: 根据方向属性， Stack垂直或水平对齐项目
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        divider         |           元素之间使用的分隔元素。     |        ReactElement	         |    No    |   All    |        Yes        |
|        space         |           每个堆栈项之间的空间。接受响应值 sm,2xs,xs,md,xl,lg,2xl,gutter,SpaceType    |        ReactElement	         |    No    |   All    |        Yes        |
|        reversed         |           确定是否反转堆叠项目的方向。     |        Boolean	         |    No    |   All    |        Yes        |
|        direction        |           堆叠项目的方向,可选row，column，column-reverse，row-reverse    |        String	         |    No    |   All    |        Yes        |
|        isHovered         |           是否悬停     |        Boolean	         |    No    |   Web    |        No        |
|        isFocused         |           是否聚焦     |        Boolean	         |    No    |   No    |        No        |
|        isDisabled         |           是否禁用     |        Boolean	         |    No    |   No    |        No        |
|        isInvalid         |           是否无效     |        Boolean	         |    No    |   No    |        No        |
|        isReadOnly         |           是否只读,如果为 true，则阻止编辑子项的值。与 FormControls 一起使用     |        Boolean	         |    No    |   No    |        No        |

**VStack / Column**: VStack / Column 布局组件垂直对齐
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        direction         |           堆叠项目的方向，可选row,column,column-reverse,row-reverse      |        String         |    No    |   All    |        Yes        |

**ZStack**: ZStack将元素与 z 轴对齐
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        reversed         |           堆叠项目的方向，是否反转      |        Boolean         |    No    |   All    |        Yes        |

**Button**: 按钮
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        variant         |           风格，可选link，subtle，solid，ghost，outline，unstyled     |       String          |    No    |   All    |        Yes        |
|        colorScheme         |           主题      |        String         |    No    |   All    |        Yes        |
|        size         |           按钮大小，可选sm（小尺寸）、md（中等尺寸）、lg（大尺寸）      |        String         |    No    |   All    |        Yes        |
|        isLoading         |           是否加载中      |        Boolean         |    No    |   All    |        Yes        |
|        isHovered         |           是否悬停      |        Boolean         |    No    |   Web    |        No        |
|        isPressed         |           是否按下     |        Boolean         |    No    |   All    |        Yes        |
|        isFocused         |           是否被聚焦      |        Boolean         |    No    |   All    |        Yes        |
|        isFocusVisible         |           是否展示焦环      |        Boolean         |    No    |   No    |        No        |
|        startIcon         |           开始图标元素      |        React.element         |    No    |   All    |        Yes        |
|        endIcon         |           结束图标元素      |        React.element         |    No    |   All    |        Yes        |
|        isLoadingText         |           正在加载文本      |         String        |    No    |   All    |        Yes        |
|        spinner         |           加载中传入的元素      |        JSX.Element         |    No    |   All    |        Yes        |
|        isDisabled         |           是否禁用      |        Boolean         |    No    |   All    |        Yes        |
|        _text        |          用于为框内的文本提供参数      |        Object         |    No    |   All    |        Yes        |
|        _stack         |           要传递给按钮内部使用的 HStack 的参数      |        Object         |    No    |   All    |        Yes        |
|        _icon         |            传递给按钮内部使用的图标的参数      |        Object         |    No    |   All    |        Yes        |
|        spinnerPlacement         |          指定加载指示器（spinner）的位置，可选start，end    |        String         |    No    |   All    |        Yes        |
|        _loading         |           当按钮加载中时传递的参数     |        Object         |    No    |   All    |        Yes        |
|        _isDisabled         |           当按钮禁用时传递给按钮的参数      |        Object         |    No    |   All    |        Yes        |
|        _spinner         |           当按钮加载中时传递给按钮的参数      |        Object         |    No    |   All    |        Yes        |
|        _hover        |           当按钮悬停时传递给按钮的参数     |        Object         |    No    |   Web    |        No        |
|        _pressed        |            当按钮按下时传递给按钮的参数      |        Object         |    No    |   All    |        Yes        |
|        _focus        |           当按钮获得焦点时传递给按钮的参数      |        Object         |    No    |   All    |        Yes        |
|        rightIcon        |           按钮中使用的右侧图标元素      |        React.element         |    No    |   All    |        Yes        |
|        leftIcon        |           按钮中使用的左侧图标元素      |        React.element         |    No    |   All    |        Yes        |
|        direction        |           堆叠项目的方向，可选row,column     |        String         |    No    |   All    |        Yes        |
|        children        |           将组件渲染为 Box 子项。接受 JSX.Element 或 JSX.Element 数组。      |        React.element         |    No    |   All    |        Yes        |
|        isAttached        |           如果为真，按钮将会连接在一起      |       Boolean       |    No    |   All    |        Yes        |

**Pressable**: 创建可触摸交互的元素。
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        onHoverIn         |           鼠标移入调用      |        () => void         |    No    |   Web    |        No        |
|        onHoverOut         |           鼠标移出调用      |        () => void         |    No    |   Web    |        No        |
|        onFocus         |           聚焦时调用      |        () => void         |    No    |   No    |        No        |
|        onBlur         |           失焦时调用      |        () => void         |    No    |   No    |        No        |
|        _hover         |           悬停参数      |        Object         |    No    |   Web    |        No        |
|        _pressed         |           按下时参数      |        Object         |    No    |   All    |        Yes        |
|        _focus         |           获得焦点时参数      |        Object         |    No    |   All    |        Yes        |
|        _disabled         |           禁用时参数      |        Object         |    No    |   All    |        Yes        |
|        isDisabled         |           是否禁用     |        Boolean         |    No    |   All    |        Yes        |
|        isHovered         |           是否悬停      |        Boolean         |    No    |   Web    |        No        |
|        isPressed         |           是否按下      |        Boolean         |    No    |   All    |        Yes        |
|        isFocused         |          是否聚焦      |        Boolean         |    No    |   No    |        No        |
|        isFocusVisible         |           是否展示焦环      |        Boolean         |    No    |   All    |        Yes        |
|        _focusVisible         |           焦点可见时应用的样式属性。这些样式仅在用户使用键盘与应用交互时应用。（仅限 Web）      |        Object         |    No    |   Web    |        No        |
|        children         |           将组件渲染为 Box 子项。接受 JSX.Element 或 JSX.Element 数组。      |        React.element         |    No    |   All    |        Yes        |

**CheckBox**: 复选框。
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        id         |           唯一标识      |        String         |    No    |   All    |        Yes        |
|        value         |           复选框的值      |        String         |    No    |   All    |        Yes        |
|        defaultValue         |           复选框组的初始值      |        String         |    No    |   All    |        Yes        |
|        colorScheme         |           主题，可选danger，info，orange，purple    |        String         |    No    |   All    |        Yes        |
|        size         |            按钮大小，可选sm（小尺寸）、md（中等尺寸）、lg（大尺寸）      |        String         |    No    |   All    |        Yes        |
|        onChange         |           选中事件      |        () => void         |    No    |   All    |        Yes        |
|        _checkbox         |           选中复选框时传递的参数      |        Object        |    No    |   All    |        Yes        |

**FormControl**: 表单控件
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        nativeID         |           本地ID      |        String         |    No    |   All    |        Yes        |
|        isInvalid         |           是否无效    |        Boolean         |    No    |   All    |        Yes        |
|        isRequired         |            是否必须      |        Boolean         |    No    |   All    |        Yes        |
|        isDisabled         |           是否禁用      |        Boolean         |    No    |   No    |        No        |
|        isReadOnly         |           是否只读      |        Boolean        |    No    |   All    |        Yes        |
|        _disabled         |           禁用状态下传递参数      |        Object        |    No    |   All    |        Yes        |
|        htmlFor         |           反映“for”内容属性的值      |        String        |    No    |   Web    |        No        |
|        _astrick         |           应用于 astric 文本的道具      |        Object        |    No    |   Web    |        No        |
|        rightIcon         |           表单中使用的左侧侧图标元素      |        React.element        |    No    |   All    |        Yes        |
|        leftIcon         |           表单中使用的右侧图标元素      |        React.element        |    No    |   All    |        Yes        |
|        startIcon         |           开始图标元素      |        React.element        |    No    |   All    |        Yes        |
|        endIcon         |           结束图标元素      |        React.element        |    No    |   All    |        Yes        |
|        _stack         |           要传递给 FormControl.ErrorMessage 内部使用的 HStack 的参数      |        Object        |    No    |   All    |        Yes        |
|        _invalid         |           无效状态下传递参数      |        Object        |    No    |   All    |        Yes        |

**IconButton**: 图标按钮
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        colorScheme         |            主题，可选primary，green，red      |        String         |    No    |   All    |        Yes        |
|        variant         |           风格，可选link，unstyled，solid，ghost，subtle      |        String         |    No    |   All    |        Yes        |
|        size         |            按钮大小，可选xs（微小尺寸）、sm（小尺寸）、md（中等尺寸）、lg（大尺寸）      |        String         |    No    |   All    |        Yes        |
|        isDisabled         |           是否禁用    |        Boolean         |    No    |   All    |        Yes        |
|        icon         |           要使用的图标      |         React.element         |    No    |   All    |        Yes        |
|        _icon         |           要传递给IconButton内部使用的图标的参数      |        Object        |    No    |   All    |        Yes        |
|        _hover         |           要传递给IconButton内部使用的悬停的参数      |        Object        |    No    |   Web    |        No        |
|        _pressed         |           要传递给IconButton内部使用的按压的参数      |        Object        |    No    |   All    |        Yes        |
|        _focus         |           要传递给IconButton内部使用的聚焦的参数      |        Object        |    No    |   All    |        Yes        |

**Input**: 输入框
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        isInvalid         |            是否无效      |        Boolean         |    No    |   All    |        Yes        |
|        variant         |           风格，可选outline，filled，underlined，unstyled，rounded     |        String         |    No    |   All    |        Yes        |
|        isDisabled         |            是否禁用      |        Boolean         |    No    |   All    |        Yes        |
|        isHovered         |           是否悬停    |        Boolean         |    No    |   Web    |        No        |
|        isFocused         |           是否聚焦      |         Boolean         |    No    |   All    |        Yes        |
|        size         |           输入框尺寸，可选sm（小尺寸）、md（中等尺寸）、lg（大尺寸）      |        String        |    No    |   All    |        Yes        |
|        isRequired         |           是否必传      |        Boolean        |    No    |   No    |        No        |
|        isReadOnly         |           是否只读      |        Boolean        |    No    |   All    |        Yes        |
|        InputLeftElement         |           输入框内部左侧元素      |        React.element        |    No    |   All    |        Yes        |
|        leftElement         |           输入框外部左侧元素      |        React.element        |    No    |   All    |        Yes        |
|        InputRightElement         |           输入框内部右侧元素      |        React.element        |    No    |   All    |        Yes        |
|        rightElement         |           输入框外部右侧元素      |        React.element        |    No    |   All    |        Yes        |
|        type         |           类型，可选text，password      |        String        |    No    |   All    |        Yes        |
|        isFullWidth         |           沾满元素      |        Boolean        |    No    |   No    |        No        |
|        wrapperRef         |           获取节点     |        Any        |    No    |   No    |        No        |
|        _hover         |           要传递给Input内部使用的悬停的参数      |        Object        |    No    |   Web    |        NO        |
|        _focus         |           要传递给Input内部使用的聚焦的参数      |        Object        |    No    |   All    |        Yes        |
|        _disabled         |           要传递给Input内部使用的禁用的参数      |        Object        |    No    |   All    |        Yes        |
|        _readOnly         |           要传递给Input内部使用的只读的参数      |        Object        |    No    |   All    |        Yes        |
|        _invalid         |           无效状态下传递参数      |        Object        |    No    |   All    |        Yes        |
|        _input         |           传递给InputBase组件参数      |        Object        |    No    |   All    |        Yes        |
|        _stack         |            要传递给按钮内部使用的 HStack 的参数      |        Object        |    No    |   All    |        Yes        |
|        focusOutlineColor         |           当输入框获得焦点时，该属性指定输入框的轮廓颜色      |        String        |    No    |   All    |        Yes        |
|        invalidOutlineColor         |           当输入框中的内容被认为是无效时，该属性指定输入框的轮廓颜色      |        String        |    No    |   All    |        Yes        |
|        ref         |           节点      |        Any        |    No    |   All    |        Yes        |

**TextArea**: 文本域
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        isInvalid         |            是否无效      |        Boolean         |    No    |   All    |        Yes        |
|        variant         |           风格，可选outline，filled，underlined，unstyled，rounded     |        String         |    No    |   All    |        Yes        |
|        isDisabled         |            是否禁用      |        Boolean         |    No    |   All    |        Yes        |
|        isHovered         |           是否悬停    |        Boolean         |    No    |   Web    |        No        |
|        isFocused         |           是否聚焦      |         Boolean         |    No    |   All    |        Yes        |
|        size         |           输入框尺寸，可选sm（小尺寸）、md（中等尺寸）、lg（大尺寸）      |        String        |    No    |   All    |        Yes        |
|        isRequired         |           是否必传      |        Boolean        |    No    |   No    |        No        |
|        isReadOnly         |           是否只读      |        Boolean        |    No    |   All    |        Yes        |
|        InputLeftElement         |           输入框内部左侧元素      |        React.element        |    No    |   All    |        Yes        |
|        leftElement         |           输入框外部左侧元素      |        React.element        |    No    |   All    |        Yes        |
|        InputRightElement         |           输入框内部右侧元素      |        React.element        |    No    |   All    |        Yes        |
|        rightElement         |           输入框外部右侧元素      |        React.element        |    No    |   All    |        Yes        |
|        type         |           类型，可选text，password      |        String        |    No    |   All    |        Yes        |
|        isFullWidth         |           沾满元素      |        Boolean        |    No    |   No    |        No        |
|        wrapperRef         |           获取节点     |        Any        |    No    |   All    |        Yes        |
|        _hover         |           要传递给Input内部使用的悬停的参数      |        Object        |    No    |   Web    |        NO        |
|        _focus         |           要传递给Input内部使用的聚焦的参数      |        Object        |    No    |   All    |        Yes        |
|        _disabled         |           要传递给Input内部使用的禁用的参数      |        Object        |    No    |   All    |        Yes        |
|        _readOnly         |           要传递给Input内部使用的只读的参数      |        Object        |    No    |   All    |        Yes        |
|        _invalid         |           无效状态下传递参数      |        Object        |    No    |   All    |        Yes        |
|        _stack         |            要传递给按钮内部使用的 HStack 的参数      |        Object        |    No    |   All    |        Yes        |
|        focusOutlineColor         |           当输入框获得焦点时，该属性指定输入框的轮廓颜色      |        Boolean        |    No    |   All    |        Yes        |
|        invalidOutlineColor         |           当输入框中的内容被认为是无效时，该属性指定输入框的轮廓颜色      |        Boolean        |    No    |   All    |        Yes        |
|        placeholder           |            提示文本      |        String         |    No    |   All    |        Yes        |

**Link**: 超链接
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        href         |            连接地址      |        String         |    No    |   All    |        Yes        |
|        size         |           超连接尺寸2xl，xl，lg，md，sm，xsm     |        String         |    No    |   All    |        Yes        |
|        isUnderlined         |            是否有下横线     |        Boolean         |    No    |   All    |        Yes        |
|        isHovered         |           是否悬停    |        Boolean         |    No    |   Web    |        No        |
|        onPress         |           按压事件      |          () => void          |    No    |   All    |        Yes        |
|        isExternal         |           是否直接打开web端      |        String        |    No    |   No    |        No        |
|        _hover         |          悬停参数      |        Object        |    No    |   Web    |        No        |
|        wrapperRef         |           获取节点      |        Any        |    No    |   All    |        Yes        |

**Radio**: 单选框
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        value           |            单选框的值      |        String         |    No    |   All    |        Yes        |
|        colorScheme         |            主题，可选yellow，green，red      |        String         |    No    |   All    |        Yes        |
|        isDisabled         |            是否禁用     |        Boolean         |    No    |   All    |        Yes        |
|        isHovered         |           是否悬停    |        Boolean         |    No    |   Web    |        No        |
|        isPressed         |           是否按压      |         Boolean         |    No    |   All    |        Yes        |
|        isFocused         |           是否聚焦      |        Boolean        |    No    |   All    |        Yes        |
|        isInvalid         |           是否失效      |        Boolean        |    No    |   All    |        Yes        |
|        onChange         |          改变事件      |          () => void          |    No    |   All    |        Yes        |
|        isFocusVisible         |           焦点是否可见      |        Boolean        |    No    |   No    |        No        |
|        size         |           单选框尺寸lg，md，sm     |        String        |    No    |   All    |        Yes        |
|        icon         |           接收图标     |         React.element          |    No    |   All    |        Yes        |
|        wrapperRef         |           获取节点     |        Any        |    No    |   All    |        Yes        |
|        _stack         |           要传递给单选框内部使用的 HStack 的参数     |        Object        |    No    |   All    |        Yes        |
|        _disabled         |           当禁用时传递给单选框的参数     |        Object        |    No    |   All    |        Yes        |
|        _checked         |           当选中时传递给单选框的参数     |        Object        |    No    |   All    |        Yes        |
|        _focus         |           当聚焦时传递给单选框的参数     |        Object        |    No    |   All    |        Yes        |
|        _hover         |           当悬停时传递给单选框的参数     |        Object        |    No    |   Web    |        No        |
|        _invalid         |           当失效时传递给单选框的参数     |        Object        |    No    |   All    |        Yes        |
|        _pressed         |           当按压时传递给单选框的参数     |        Object        |    No    |   All    |        Yes        |
|        _icon         |           当传递图标时传递给单选框的参数     |        Object        |    No    |   All    |        Yes        |
|        _readOnly         |           当只读时传递给单选框的参数     |        Object        |    No    |   All    |        Yes        |
|        _interactionBox         |           当交互时传递给按钮的参数     |        Object        |    No    |   All    |        Yes        |
|        ref         |           获取节点数据     |        Object        |    No    |   All    |        Yes        |

**Select**: 下拉框
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        placeholder           |            提示文本      |        String         |    No    |   All    |        Yes        |
|        color         |            选中颜色      |        String         |    No    |   No    |        Yes        |
|        placeholderTextColor         |            提示文本颜色     |        String         |    No    |   iOS    |        No        |
|        _item         |           每个选项的参数    |        Object         |    No    |   All    |        Yes        |
|        _selectedItem         |           选中选项的参数      |         Object         |    No    |   All    |        Yes        |
|        selectedValue         |           选中值      |        String        |    No    |   All    |        Yes        |
|        defaultValue         |           初始值      |        String        |    No    |   All    |        Yes        |
|        onValueChange         |           单选事件     |         () => void         |    No    |   All    |        Yes        |
|        isDisabled         |           是否禁用     |         Boolean          |    No    |   All    |        Yes        |
|        isHovered         |           是否悬停     |        Boolean        |    No    |   Web    |        No        |
|        isFocused         |           是否聚焦     |        Boolean        |    No    |   All    |        Yes        |
|        isFocusVisible         |           焦点是否可见     |        Boolean        |    No    |   No    |        No        |
|        dropdownIcon         |           原有图标     |        React.element        |    No    |   All    |        Yes        |
|        dropdownOpenIcon         |           打开图标     |        React.element        |    No    |   All    |        Yes        |
|        dropdownCloseIcon         |           关闭图标     |        React.element        |    No    |   All    |        Yes        |
|        variant         |           风格，可选outline，filled，underlined，unstyled，rounded    |        String        |    No    |   All    |        Yes        |
|        onOpen         |           打开下拉事件     |        () => void        |    No    |   All    |        Yes        |
|        onClose         |           关闭下拉事件     |        () => void        |    No    |   All    |        Yes        |
|        _actionSheet         |           传递给遮罩层的参数样式     |        Object        |    No    |   All    |        Yes        |
|        _actionSheetContent         |           传递给内容的参数样式     |        Object        |    No    |   All    |        Yes        |
|        _actionSheetBody         |           传递给内容Body的参数     |        Object        |    No    |   All    |        Yes        |
|        wrapperRef         |           获取节点    |        Any        |    No    |   No    |        No        |
|        accessibilityLabel         |           当用户与元素交互时读取的文本    |        String        |    No    |   No    |        No        |

**Select.Item**: 下拉框子集
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        label         |            选择提示文本      |        String         |    No    |   All    |        Yes        |
|        value         |           选中值     |        String         |    No    |   All    |        Yes        |

**Switch**: 开关
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        size         |            开关尺寸，可选lg，md，sm      |        String         |    No    |   All    |        Yes        |
|        isDisabled         |           是否禁用     |        Boolean         |    No    |   All    |        Yes        |
|        isHovered         |            是否悬停     |        Boolean         |    No    |   Web    |        No        |
|        name         |          表单中使用开关的别名      |          String          |    No    |   All    |        Yes        |
|        onToggle         |           开关事件      |        () => void        |    No    |   All    |        Yes        |
|        isChecked         |           是否开启      |        Boolean        |    No    |   All    |        Yes        |
|        defaultIsChecked         |           是否默认开启    |        Boolean        |    No    |   All    |        Yes        |
|        isInvalid         |           是否失效      |        Boolean        |    No    |   All    |        Yes        |
|        onTrackColor         |            打开时轨道的颜色      |        Object        |    No    |   All    |        Yes        |
|        offTrackColor         |           关闭时轨道的颜色      |        Object        |    No    |   All    |        Yes        |
|        onThumbColor         |           打开时按钮的颜色      |        Object        |    No    |   All    |        Yes        |
|        offThumbColor         |           关闭时按钮的颜色      |        Object        |    No    |   All    |        Yes        |
|        colorScheme         |           主题      |        String        |    No    |   All    |        Yes        |
|        _hover         |           悬停参数      |        String        |    No    |   Web    |        No        |

**Slider**: 滑块
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        value         |            值      |        Number         |    No    |   All    |        Yes        |
|        defaultValue         |           默认值     |        Number         |    No    |   All    |        Yes        |
|        onChange         |          滑块事件      |          () => void          |    No    |   All    |        Yes        |
|        colorScheme         |           主题      |        String        |    No    |   All    |        Yes        |
|        orientation         |           展示方向，可选horizontal，vertical'     |        String        |    No    |   All    |        Yes        |
|        accessibilityLabel         |           滑块文本描述      |        String        |    No    |   No    |        No        |
|        isReversed         |           是否反转      |        Boolean        |    No    |   All    |        Yes        |
|        isDisabled         |           是否禁用      |        Boolean        |    No    |   All    |        Yes        |
|        onChangeEnd         |          松开停止移动事件      |         () => void        |    No    |   All    |        Yes        |
|        minValue         |           最小值      |        Number        |    No    |   All    |        Yes        |
|        maxValue         |           最大值      |        Number        |    No    |   All    |        Yes        |
|        step         |           每次用移动的步数      |        Number        |    No    |   All    |        Yes        |
|        isReadOnly         |           是否只读      |        Boolean        |    No    |   All    |        Yes        |
|        _disabled         |           禁用时启用      |        Object        |    No    |   All    |        Yes        |
|        _readOnly         |           只读时启用      |        Object        |    No    |   All    |        Yes        |
|        sliderTrackHeight         |           轨道高度      |        Number        |    No    |   All    |        Yes        |
|        thumbSize         |           滑块大小      |        Number        |    No    |   All    |        Yes        |
|        _interactionBox         |           交互样式      |        Object        |    No    |   All    |        Yes        |

**Badge**: 小标识小标签
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        variant         |            风格      |        String         |    No    |   All    |        Yes        |
|        colorScheme         |           主题,可选success，danger，info，coolGray     |        String         |    No    |   All    |        Yes        |
|        rightIcon         |          组件右侧图标      |          React.element         |    No    |   All    |        Yes        |
|        leftIcon         |          组件左侧图标      |          React.element          |    No    |   All    |        Yes        |
|        startIcon         |          开始图标      |          React.element          |    No    |   All    |        Yes        |
|        endIcon         |          结束图标      |          React.element         |    No    |   All    |        Yes        |
|        _text         |          组件内的文本提供参数       |          Object         |    No    |   All    |        Yes        |
|        _icon         |          组件内的图标提供参数      |          Object        |    No    |   All    |        Yes        |

**Divider**: 分割线
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        orientation         |            方向,可选vertical，horizontal      |        Number         |    No    |   All    |        Yes        |
|        thickness         |           分割线宽度    |        String         |    No    |   All    |        Yes        |

**Alert**: 状态提示框
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        status         |            状态,可选info，warning，success，error      |        String         |    No    |   All    |        Yes        |
|        variant         |           风格    |        String         |    No    |   All    |        Yes        |
|        colorScheme         |           主题    |        String         |    No    |   All    |        Yes        |

**Progress**: 进度条
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        value         |            数值     |        Number         |    No    |   All    |        Yes        |
|        size         |           尺寸    |        String         |    No    |   All    |        Yes        |
|        colorScheme         |           主题    |        String         |    No    |   All    |        Yes        |
|        _filledTrack         |           填充的轨道提供参数   |        Object         |    No    |   All    |        Yes        |
|        min         |           最小值    |        Number         |    No    |   All    |        Yes        |
|        max         |            最大值   |        Number         |    No    |   All    |        Yes        |


**Skeleton**: 组件的加载状态
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        fadeDuration         |            加载时长     |        Number         |    No    |   All    |        Yes        |
|        isLoaded         |           是否加载中    |        Boolean         |    No    |   All    |        Yes        |
|        speed         |           加载速度    |        Number         |    No    |   All    |        Yes        |
|        startColor         |           开始颜色   |        String         |    No    |   All    |        Yes        |
|        endColor         |           结束颜色    |        String         |    No    |   All    |        Yes        |
|        size         |            尺寸   |        String         |    No    |   All    |        Yes        |

**Skeleton.Text**: 组件的加载状态文字组件
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        fadeDuration         |            加载时长     |        Number         |    No    |   All    |        Yes        |
|        isLoaded         |           是否加载中    |        Boolean         |    No    |   All    |        Yes        |
|        speed         |           加载速度    |        Number         |    No    |   All    |        Yes        |
|        startColor         |           开始颜色   |        String         |    No    |   All    |        Yes        |
|        endColor         |           结束颜色    |        String         |    No    |   All    |        Yes        |
|        lines         |            文本中的行数   |        Number         |    No    |   All    |        Yes        |
|        _line         |            文本中的行数样式参数   |        String         |    No    |   All    |        Yes        |
|        _stack         |            要传递给按钮内部使用的 HStack 的参数    |        String         |    No    |   No    |        No        |

**Spinner**: 加载等待中
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        color         |            颜色     |        String         |    No    |   All    |        Yes        |
|        size         |            尺寸，可选lg，md，sm   |        String         |    No    |   All    |        Yes        |

**Toast**: 轻提示
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        show         |            消息体     |        Object         |    No    |   All    |        Yes        |
|        close         |            关闭单个   |       (id: any) => void;        |    No    |   All    |        Yes        |
|        closeAll         |            关闭所有   |        () => void         |    No    |   All    |        Yes        |
|        isActive         |            防抖设计   |        (id: any) => boolean;        |    No    |   All    |        Yes        |

**Toast.show**: 轻提示消息体
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        title         |            标题   |       ReactNode        |    No    |   All    |        Yes        |
|        description         |            内容描述   |      ReactNode         |    No    |   All    |        Yes        |
|        duration         |            显示时长   |       Number 或 null        |    No    |   All    |        Yes        |
|        id         |            唯一标识   |       any        |    No    |   All    |        Yes        |
|        onCloseComplete         |            显示完成关闭回调   |       () => void        |    No    |   All    |        Yes        |
|        placement         |            位置，可选top，top-right，top-left，bottom，bottom-left，bottom-right   |      String        |    No    |   All    |        Yes        |
|        render         |            接收子组件   |      (props: any) => ReactNode       |    No    |   All    |        Yes        |
|        _title         |            标题样式参数   |       Object       |    No    |   All    |        Yes        |
|        _description         |            描述样式参数   |       Object        |    No    |   All    |        Yes        |
|        accessibilityAnnouncement         |            Toast 打开时屏幕阅读器播报的文本   |       String       |    No    |   Android     |        No        |
|        accessibilityLiveRegion         |            Toast 打开时屏幕阅读器播报的文本位置   |       String        |    No    |   Android     |        No        |
|        avoidKeyboard         |         键盘打开，则 Toast 将向上移动相当于键盘高度   |       Boolean        |    No    |   iOS    |        No        |

**Text**: 文本
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        children         |            子集     |        JSX.Element         |    No    |   All    |        Yes        |
|        fontSize         |            字号   |       String        |    No    |   All    |        Yes        |
|        letterSpacing         |            间距   |       String         |    No    |   All    |        Yes        |
|        lineHeight         |            行高   |        String        |    No    |   All    |        Yes        |
|        fontWeight         |            字宽   |        String        |    No    |   All    |        Yes        |
|        Fonts         |            字型   |        String        |    No    |   No    |        No        |
|        noOfLines         |            行数   |        Number        |    No    |   All    |        Yes        |
|        bold         |            加粗   |        Number        |    No    |   All    |        Yes        |
|        isTruncated         |            超出省略   |        Boolean        |    No    |   All    |        Yes        |
|        italic         |            斜体   |        Boolean        |    No    |   All    |        Yes        |
|        underline         |            下横线   |        Boolean        |    No    |   All    |        Yes        |
|        strikeThrough         |            删除线   |        Boolean        |    No    |   All    |        Yes        |
|        sub         |            字体缩小（副标题或者辅助说明的文本）   |        Boolean        |    No    |   All    |        Yes        |
|        highlight         |            突出显示   |        Boolean        |    No    |   All    |        Yes        |

**Heading**: 标题(继承了Text属性)
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        size         |            尺寸，可选lg，md，sm    |       String        |    No    |   All    |        Yes        |

**AlertDialog**: 警告对话框
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        isOpen         |           是否打开    |       Boolean        |    No    |   All    |        Yes        |
|        onClose         |           关闭事件    |       () => void        |    No    |   All    |        Yes        |
|        defaultIsOpen         |           是否打开    |       Boolean        |    No    |   All    |        Yes        |
|        size         |           尺寸    |       Number        |    No    |   All    |        Yes        |
|        leastDestructiveRef         |           最小元素节点    |       Object        |    No    |   No    |        No        |
|        initialFocusRef         |           打开时焦点元素节点    |       Object        |    No    |   All    |        Yes        |
|        finalFocusRef         |           关闭时焦点元素节点    |       Object        |    No    |   All    |        Yes        |
|        avoidKeyboard         |           键盘打开，则 AlertDialog 将向上移动相当于键盘高度     |       Boolean        |    No    |   iOS    |        No        |
|        closeOnOverlayClick         |           点击关闭    |       Boolean        |    No    |   All    |        Yes        |
|        isKeyboardDismissable         |           Esc关闭    |       Boolean        |    No    |   No    |        No        |
|        overlayVisible         |           背景元素是否可见    |       Boolean        |    No    |   All    |        Yes        |
|        backdropVisible         |           背景元素是否可见    |       Boolean        |    No    |   All    |        Yes        |
|        _backdrop         |           遮罩参数用样式    |       Any        |    No    |   All    |        Yes        |
|        _backdropFade         |           遮罩动画的参数样式    |       Object        |    No    |   All    |        Yes        |
|        _fade         |           子集褪色动画的参数样式    |       Object        |    No    |   All    |        Yes        |
|        _slide         |           子集幻灯片动画的参数样式    |       Object        |    No    |   All    |        Yes        |
|        animationPreset         |           动画类型    |       String        |    No    |   All    |        Yes        |

**Menu**: 菜单
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        trigger         |            手动触发显示的元素  |        () => void        |    Yes    |   All    |        Yes        |
|        onOpen         |            打开事件    |        () => void        |    No    |   All    |        Yes        |
|        onClose         |           关闭事件    |        () => void        |    No    |   All    |        Yes        |
|        closeOnSelect         |             选择时菜单是否自动关闭    |        Boolean        |    No    |   All    |        Yes        |
|        defaultIsOpen         |            默认打开   |        Boolean        |    No    |   All    |        Yes        |
|        isOpen         |            是否打开    |        Boolean       |    No    |   All    |        Yes        |
|        crossOffset         |            控制菜单相对于触发元素的偏移量    |        Number       |    No    |   All    |        Yes        |
|        offset         |            菜单弹出位置的偏移量    |        Number       |    No    |   All    |        Yes        |
|        shouldOverlapWithTrigger         |            控制菜单是否与触发元素重叠显示。    |        boolean       |    No    |   All    |        Yes        |
|        placement         |            位置，可选top,bottom,left,right等    |        String       |    No    |   All    |        Yes        |
|        _overlay         |            菜单的覆盖层参数    |        Object       |    No    |   All    |        Yes        |
|        _presenceTransition         |            出现和消失过渡效果参数    |        Object       |    No    |   All    |        Yes        |
|        _backdrop         |            背景遮罩参数    |        Object       |    No    |   All    |        Yes        |
|        shouldFlip         |             没有空间时元素是否翻转    |   Boolean            |    No    |   All    |        Yes        |

**Menu.Item**: 菜单子项
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        children         |             子元素    |   JSX.Element             |    No    |   All    |        Yes        |
|        isDisabled         |             是否禁用    |   Boolean             |    No    |   All    |        Yes        |
|        _text         |            传给文字的参数    |   Object             |    No    |   All    |        Yes        |
|        textValue         |             预设的值    |   String             |    No    |   All    |        Yes        |

**Menu.Option**: 菜单选项
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        value         |             值    |   String             |    No    |   All    |        Yes        |
|        _stack         |             传递给stack的参数    |   Object             |    No    |   All    |        Yes        |
|        _icon         |             传递给图标的参数    |   Object             |    No    |   All    |        Yes        |
|        _text         |            传给文字的参数    |   Object             |    No    |   All    |        Yes        |

**Menu.MenuGroup**: 菜单组
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        title         |             标题    |   String             |    No    |   All    |        Yes        |
|        children         |             子元素    |   JSX.Element             |    No    |   All    |        Yes        |
|        _title         |            传给标题的参数    |   Object             |    No    |   All    |        Yes        |

**Menu.MenuOptionGroup**: 菜单选项组
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        type         |            类型（可选radio，checkbox）    |   String             |    No    |   All    |        Yes        |
|        defaultValue         |             默认值    |   String             |    No    |   All    |        Yes        |
|        value         |            值    |   String             |    No    |   All    |        Yes        |
|        onChange         |            改变事件    |   () => void             |    No    |   All    |        Yes        |

**Modal**: 弹框
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        isOpen         |            是否打开    |        Boolean        |    No    |   All    |        Yes        |
|        onClose         |           关闭事件    |        () => void        |    No    |   All    |        Yes        |
|        defaultIsOpen         |             默认打开    |        Boolean        |    No    |   All    |        Yes        |
|        size         |            尺寸   |        String        |    No    |   All    |        Yes        |
|        initialFocusRef         |            模态框打开时最初获得焦点的元素节点    |        Any       |    No    |   All    |        Yes        |
|        finalFocusRef         |            模态框关闭时最终获得焦点的元素节点    |        Any       |    No    |   All    |        Yes        |
|        avoidKeyboard         |            键盘打开，则 Modal 将向上移动相当于键盘高度      |        Boolean       |    No    |   iOS    |        No        |
|        isKeyboardDismissable         |            控制是否可以通过触摸屏幕外部或按下系统返回键来关闭键盘和模态框    |        Boolean       |    No    |   All    |        Yes        |
|        overlayVisible         |            控制模态框的背景覆盖层（overlay）是否可见    |        Boolean       |    No    |   All    |        Yes        |
|        backdropVisible         |            控制模态框的背景遮罩是否可见    |        Boolean       |    No    |   All    |        Yes        |
|        animationPreset         |            动画效果    |        String       |    No    |   All    |        Yes        |
|        _backdrop         |            背景遮罩参数    |        Object       |    No    |   All    |        Yes        |
|        _fade         |            动画参数    |        Object       |    No    |   All    |        Yes        |
|        _slide         |            幻灯片动画参数    |        Object       |    No    |   All    |        Yes        |
|        _overlay         |            背景覆盖层参数    |        Object       |    No    |   All    |        Yes        |
|        useRNModal         |          是否使用 React Native 的原生Modal组件来实现模态框      |        Boolean       |    No    |   All    |        Yes        |
|        _backdropFade         |            背景遮罩参数    |        Object       |    No    |   All    |        Yes        |
|        closeOnOverlayClick         |            点击关闭    |        () => void       |    No    |   All    |        Yes        |

**Popover**: 局部弹框
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        isOpen         |            是否打开    |        Boolean        |    No    |   All    |        Yes        |
|        onClose         |           关闭事件    |        () => void        |    No    |   All    |        Yes        |
|        onOpen         |           打开事件    |        () => void        |    No    |   All    |        Yes        |
|        placement         |           位置    |        String        |    No    |   All    |        Yes        |
|        defaultIsOpen         |             默认打开    |        Boolean        |    No    |   All    |        Yes        |
|        initialFocusRef         |            模态框打开时最初获得焦点的元素节点    |        Any       |    No    |   All    |        Yes        |
|        finalFocusRef         |            模态框关闭时最终获得焦点的元素节点    |        Any       |    No    |   All    |        Yes        |
|        isKeyboardDismissable         |            控制是否可以通过触摸屏幕外部或按下系统返回键来关闭键盘和模态框    |        Boolean       |    No    |   All    |        Yes        |
|        useRNModal         |            是否使用 React Native 的原生Modal组件来实现局部弹框     |        Boolean       |    No    |   All    |        Yes        |
|        trigger         |            手动触发显示的元素  |        () => void        |    No    |   All    |        Yes        |
|        trapFocus         |            是否应该捕获焦点  |        Boolean        |    No    |   No    |        No        |
|        crossOffset         |            x轴偏移量  |       Number        |    No    |   All    |        Yes        |
|        offset         |            y轴偏移量  |       Number        |    No    |   All    |        Yes        |
|        shouldOverlapWithTrigger         |            控制菜单是否与触发元素重叠显示。    |        boolean       |    No    |   All    |        Yes        |
|        children         |             子元素    |   JSX.Element             |    No    |   All    |        Yes        |
|        shouldFlip         |             元素渲染位置不够是否反转    |   Boolean             |    No    |   All    |        Yes        |

**Avatar**: 显示用户头像或图像
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        source         |            图片地址参数    |        Object        |    No    |   All    |        Yes        |
|        size         |           尺寸    |        String        |    No    |   All    |        Yes        |
|        _image         |           图片参数    |        Object       |    No    |   All    |        Yes        |
|        wrapperRef         |             获取节点    |        Any        |    No    |   All    |        Yes        |

**Icon**: 展示图标
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        as         |            接收矢量图标    |        Any        |    No    |   All    |        Yes        |
|        size         |           尺寸    |        String        |    No    |   All    |        Yes        |
|        color         |           颜色    |        String       |    No    |   All    |        Yes        |
|        name         |             名称    |   String            |    No    |   All    |        Yes        |
|        viewBox         |             icon盒子参数    |   String            |    No    |   All    |        Yes        |
|        path         |             icon地址    |   JSX.Element[]            |    No    |   All    |        Yes        |
|        d         |             SVG图标的路径    |   String            |    No    |   All    |        Yes        |

**Image**: 图片
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        source         |            图片地址参数    |        Object        |    No    |   All    |        Yes        |
|        alt         |            未展示文字    |         String       |    No    |   All    |        Yes        |
|        _alt         |            未展示文字样式参数    |         Object       |    No    |   All    |        Yes        |
|        size         |           尺寸    |        String        |    No    |   All    |        Yes        |
|        src         |             图片地址    |   String             |    No    |   All    |        Yes        |
|        fallbackSource         |             指定当主图像源无法加载时显示的备用图像源    |   String            |    No    |   All    |        Yes        |
|        ignoreFallback         |             是否忽略备用图像源    |   Boolean            |    No    |   All    |        Yes        |
|        fallbackElement         |             指定当主图像源无法加载时显示的备用元素    |   JSX.Element            |    No    |   All    |        Yes        |

**ActionSheet**: 操作表
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        isOpen         |            是否打开    |        Boolean        |    No    |   All    |        Yes        |
|        onClose         |            关闭事件    |         () => void       |    No    |   All    |        Yes        |
|        disableOverlay         |            是否有遮罩    |         Boolean       |    No    |   All    |        Yes        |
|        hideDragIndicator         |           是否有拖动    |        Boolean        |    No    |   All    |        Yes        |
|        _backdrop         |           遮罩参数用样式    |        any       |    No    |   All    |        Yes        |
|        useRNModal         |             是否使用 React Native 的原生Modal组件来实现ActionSheet   |   Boolean             |    No    |   All    |        Yes        |

**Actionsheet.Content**: 操作表内容
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        _dragIndicatorWrapperOffSet         |            在操作表内容上方区域内容参数    |        Object        |    No    |   All    |        Yes        |
|        _dragIndicatorWrapper         |            在操作表内容周围区域内容参数    |         Object      |    No    |   All    |        Yes        |
|        _dragIndicator         |            拖动指示器的参数    |         Object       |    No    |   All    |        Yes        |

**PresenceTransition**: 组件的出现和消失添加动画过渡效果
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        onTransitionComplete         |            过渡完成事件    |         () => void         |    No    |   All    |        Yes        |
|        initial         |            动画初始状态的属性    |        Object       |    No    |   All    |        Yes        |
|        animate         |            动画最终状态的属性    |         Object       |    No    |   All    |        Yes        |
|        exit         |           组件在隐藏时的状态    |        Boolean        |    No    |   All    |        Yes        |
|        visible         |           是否打开    |        Boolean       |    No    |   All    |        Yes        |
|        children         |             子集   |   any             |    No    |   All    |        Yes        |
|        as         |             包裹在过渡效果中的元素的类型   |   any             |    No    |   All    |        Yes        |

**Stagger**: 交错动画效果组件
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        initial         |            动画初始状态的属性    |        Object       |    No    |   All    |        Yes        |
|        animate         |            动画最终状态的属性    |         Object       |    No    |   All    |        Yes        |
|        exit         |           组件在隐藏时的状态    |        Object        |    No    |   All    |        Yes        |
|        visible         |           是否打开    |        Boolean       |    No    |   All    |        Yes        |

**Slide**: 实现滑动动画
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        in         |            显示隐藏    |        Boolean       |    No    |   All    |        Yes        |
|        duration         |            动画时长    |         Number       |    No    |   All    |        Yes        |
|        placement         |           位置    |        String        |    No    |   All    |        Yes        |

**FAB**: 浮动按钮
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        placement         |            位置    |        String       |    No    |   All    |        Yes        |
|        label         |            文本参数    |         String       |    No    |   All    |        Yes        |
|        icon         |           图标    |        React.Element        |    No    |   All    |        Yes        |
|        renderInPortal         |           是否将 FAB 渲染在一个 Portal(Portal 是一种在 React 中用于将子组件渲染到父组件以外的 DOM 节点中的技术)    |        Boolean        |    No    |   All    |        Yes        |

**Hidden**: 根据colorMode或平台响应性地切换子组件的可见性值
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        from         |            屏幕尺寸的起点，当屏幕尺寸大于等于这个起点时，组件将被隐藏    |        String       |    No    |   All    |        Yes        |
|        till         |             屏幕尺寸的终点，当屏幕尺寸小于这个终点时，组件将被隐藏    |         String       |    No    |   All    |        Yes        |
|        only         |           指定一个或多个特定的屏幕尺寸，只有在这些尺寸下组件才会显示，其他尺寸下将被隐藏    |        String        |    No    |   All    |        Yes        |
|        colorMode         |           组件在不同颜色模式下的显示状态。NativeBase 通常支持多种颜色模式，如 light（浅色模式）、dark（深色模式）等。    |        React.Element        |    No    |   No    |        No        |
|        platform         |           系统平台    |        React.Element        |    No    |   All    |        Yes        |
|        children         |           子元素    |        React.Element        |    No    |   All    |        Yes        |
|        isSSR         |           组件是否在服务器端渲染（SSR）环境中    |       Boolean        |    No    |   No    |        No        |

**KeyboardAvoidingView**: 拉起键盘视图向上移动的垂直偏移量
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        children        |           将组件渲染为 KeyboardAvoidingView 子项。接受 JSX.Element 或 JSX.Element 数组。      |        React.element         |    No    |   All    |        Yes        |

**Scrollview**: 滚动
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        children        |           将组件渲染为 Scrollview 子项。接受 JSX.Element 或 JSX.Element 数组。      |        React.element         |    No    |   All    |        Yes        |
|        _contentContainerStyle        |         传递给内容容器样式      |        Object         |    No    |   All    |        Yes        |

**View**: 视图
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        children        |           将组件渲染为 Scrollview 子项。接受 JSX.Element 或 JSX.Element 数组。      |        React.element         |    No    |   All    |        Yes        |

**FlatList**: 滚动
|         Name         |                         Description                          |         Type          | Required | Platform | HarmonyOS Support |
| :------------------: | :----------------------------------------------------------: | :-------------------: | :------: | :------: | :---------------: |
|        _contentContainerStyle        |           传递给内容容器样式      |        Object         |    No    |   All    |        Yes        |
|            ref   |         获取节点数据      |        Object         |    No    |   All    |        Yes        |


**Other**：包含hooks和外用组件
| Name                   | Description | Required | Platform | HarmonyOS Support |
| ---------------------- | ----------- | -------- | ----------------- | ----------------- |
| useDisclose     | 处理常见的打开、关闭或切换场景，并可以控制反馈组件，如Modal、AlertDialog、Drawer等。 | NO        | All              | YES               |
| useBreakpointValue     | 用于呈现分段列表的高性能接口 | NO        | NO               | NO               |
| SectionList     | 导出的是RN原生的SectionList，可直接用RN的SectionList | NO        | All              | YES               |
| useClipboard     | 使用剪贴板控件并控制将内容复制到剪贴板 | NO        | All               | YES               |
| useMediaQuery     | 检测单个媒体查询或多个媒体查询之间的匹配。React Native本身不支持媒体查询，因此useMediaQuery仍然有限 | NO        | All               | YES               |
| useToken     | 解析主题中的设计标记. | NO        | All              | YES               |
| useColorMode     |设置或检索颜色模式 | NO        | NO               | NO               |
| useTheme     |从上下文调用主题对象 | NO        | All               | YES               |
| useColorModeValue     | 基于活动颜色模式值传递的参数中检索值 | NO        | NO              | NO               |
| useContrastText     | 提供与作为参数传递的背景颜色的颜色对比文本颜色（lightText或darkText） | NO        | All               | YES               |
| useAccessibleColors  | 更新您的颜色配置，以在应用程序中获得更好的颜色和对比度可访问性。默认情况下，可访问的颜色是关闭的如果您想继续使用可访问的文本颜色，可以使用此挂钩。您还可以使用extendTheme在NativeBaseProvider的配置中传递它 | NO        | All               | YES               |
| Todo-List     | 用本库的组件写的案例，如有业务需要可自行编写适合的组件 | NO        | All              | YES               |
| AppBar     | 用本库的组件写的案例，如有业务需要可自行编写适合的组件 | NO        | All               | YES               |
| Card     |用本库的组件写的案例，如有业务需要可自行编写适合的组件| NO        | All               | YES               |
| Drawer Navigation    | 快速地使用 [@react-native-oh-tpl/react-navigation-drawer](/zh-cn/react-navigation-drawer.md) | NO        | All               | YES               |
| Tab View     | 快速地使用 [@react-native-oh-tpl/react-native-tab-view 文档](/zh-cn/react-native-tab-view.md) in NB | NO        | All               | YES               |
| Swipe List    | 快速地使用 [@react-native-oh-tpl/react-native-swipe-list-view](/zh-cn/react-native-swipe-list-view.md) | NO        | All              | YES               |
| Form with Validation    | 用本库的组件写的案例，如有业务需要可自行编写适合的组件 | NO        | All              | YES               |
| Login/Signup Forms     | 用本库的组件写表单登录的案例，如有业务需要可自行编写适合的组件| NO        | All               | YES               |
| SearchBar     | 用本库的组件写的搜索案例，如有业务需要可自行编写适合的组件 | NO        | All               | YES               |
| App drawer     | 使用FlatList创建类似应用程序抽屉的布局非常常见，如有业务需要可自行编写适合的组件 | NO        | All               | YES               |
| Footer     |用本库的组件写的Footer案例，如有业务需要可自行编写适合的组件 | NO        | All               | YES               |

## 遗留问题
- [ ] FormControl组件isDisabled属性无效: [issue#1](https://github.com/GeekyAnts/NativeBase/issues/5707)
- [ ] Select组件placeholderTextColor属性无效: [issue#16](https://github.com/react-native-oh-library/NativeBase/issues/16)
- [ ] Modal,AlertDialog,组件avoidKeyboard属性无效: [issue#17](https://github.com/react-native-oh-library/NativeBase/issues/17)

## 其他

- 网站文档图标要用@expo/vector-icons（需要用到expo脚手架才可以），如果没有用到expo脚手架的可以用[react-native-vector-icons 文档](/zh-cn/react-native-vector-icons.md)平替
- Tooltip 当用户与元素交互时，工具提示会提供简短的信息性消息。工具提示的启动方法包括：通过鼠标悬停手势或键盘悬停手势。这个组件是在web端用的

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/GeekyAnts/NativeBase/blob/master/LICENSE) ，请自由地享受和参与开源。
