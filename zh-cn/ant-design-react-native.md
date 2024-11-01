> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@ant-design/react-native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ant-design/ant-design-mobile-rn">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ant-design/ant-design-mobile-rn/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/ant-design/ant-design-mobile-rn)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @ant-design/react-native@5.2.2
```

#### **yarn**

```bash
yarn add @ant-design/react-native@5.2.2
```

> [!TIP] 本库还依赖了[@react-native-oh-tpl/slider](/zh-cn/react-native-community-slider.md)、[@react-native-oh-tpl/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)、[@react-native-oh-tpl/react-native-modal-popover](/zh-cn/react-native-modal-popover.md)、[@react-native-oh-tpl/react-native-reanimated](/zh-cn/react-native-reanimated.md)和[react-native-community/segmented-control](/zh-cn/react-native-community-segmented-control.md)

> **Warning:**
> @bang88/react-native-ultimate-listview 这个依赖库还没鸿蒙化，会影响到里面的一个 ListView 组件，如果想暂时解决掉这个报错的话，可以在 node_modules\@bang88\react-native-ultimate-listview\src 目录下添加一个 refreshableScrollView.js 文件。

## 链接字体图标

```bash
// 配置根目录下的 `react-native.config.js` 文件
module.exports = {
  assets: ['node_modules/@ant-design/icons-react-native/fonts'],
};
```

然后

```bash
# 手动执行命令
npm install react-native-asset && npx react-native-asset
```

### 在 ArkTs 侧引入和注册字体文件

> [!WARNING] 使用时 import 的库名不变。

步骤一：
复制字体文件到 `\entry\src\main\resources\rawfile\fonts` 目录下(没有 fonts 文件夹就新建一个，如使用了外部字体文件，需要将\*.ttf 文件复制过来)

步骤二：
打开 `entry/src/main/ets/pages/Index.ets`，添加以下代码

```diff

    @Entry
    @Component
    struct Index {
        //...
        if (this.rnohCoreContext && this.shouldShow) {
        if (this.rnohCoreContext?.isDebugModeEnabled) {
          RNOHErrorDialog({ ctx: this.rnohCoreContext })
        }
        RNApp({
          rnInstanceConfig: {
            createRNPackages,
            enableNDKTextMeasuring: true,
            enableBackgroundExecutor: false,
            enableCAPIArchitecture: true,
            arkTsComponentNames: [SLIDER_TYPE],
            fontResourceByFontFamily: {
+              'antoutline': $rawfile("fonts/antoutline.ttf"),
+              "antfill": $rawfile('fonts/antfill.ttf'),
            }
          },
        //...
         )
    }
```

> [!TIP] Demo 中字体属于 IconFont 文件；自定义字体也需要用统一的方法在此注册。

下面的代码展示了这个库的基本使用场景：

```jsx
import React from "react";
import { ScrollView, View } from "react-native";
import { Badge, WhiteSpace } from "@ant-design/react-native";
export default class BasicTagExample extends React.Component {
  render() {
    return (
      <ScrollView
        style={{ flex: 1 }}
        automaticallyAdjustContentInsets={false}
        showsHorizontalScrollIndicator={false}
        showsVerticalScrollIndicator={false}
      >
        <View style={{ padding: 20 }}>
          <Badge text={9}>
            <View
              style={{
                width: 52,
                height: 52,
                backgroundColor: "rgba(255, 140, 101, 0.15)",
              }}
            />
          </Badge>

          <WhiteSpace size="lg" />

          <Badge text={109} overflowCount={100}>
            <View
              style={{
                width: 52,
                height: 52,
                backgroundColor: "rgba(255, 140, 101, 0.15)",
              }}
            />
          </Badge>

          <WhiteSpace size="lg" />

          <Badge text={109}>
            <View
              style={{
                width: 52,
                height: 52,
                backgroundColor: "rgba(255, 140, 101, 0.15)",
              }}
            />
          </Badge>

          <WhiteSpace size="lg" />

          <Badge text="new">
            <View
              style={{
                width: 52,
                height: 52,
                backgroundColor: "rgba(255, 140, 101, 0.15)",
              }}
            />
          </Badge>

          <WhiteSpace size="lg" />

          <Badge text={109} dot>
            <View
              style={{
                width: 52,
                height: 52,
                backgroundColor: "rgba(255, 140, 101, 0.15)",
              }}
            />
          </Badge>

          <WhiteSpace size="lg" />

          <Badge text={33} corner>
            <View
              style={{
                width: 52,
                height: 52,
                backgroundColor: "rgba(255, 140, 101, 0.15)",
              }}
            />
          </Badge>
        </View>
      </ScrollView>
    );
  }
}
```

## Link

> [!TIP] @react-native-oh-tpl/react-native-gesture-handler 安装 v2.14.7 版本配套使用

> [!TIP] @react-native-oh-tpl/slider 安装 v4.4.3-0.3.2 版本配套使用

> [!TIP] @react-native-oh-tpl/react-native-modal-popover 安装 v2.1.3-0.0.1 版本配套使用

> [!TIP] @react-native-oh-tpl/react-native-reanimated 安装 v3.6.2 版本配套使用

本库 HarmonyOS 侧实现依赖 @react-native-oh-tpl/slider、@react-native-oh-tpl/react-native-gesture-handler 、@react-native-oh-tpl/react-native-reanimated 和@react-native-oh-tpl/react-native-modal-popover 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照文档进行引入

- [@react-native-oh-tpl/slider 引入方法](/zh-cn/react-native-community-slider.md)

- [@react-native-oh-tpl/react-native-gesture-handler 引入方法](/zh-cn/react-native-gesture-handler.md)

- [@react-native-oh-tpl/react-native-modal-popover 引入方法](/zh-cn/react-native-modal-popover.md)

- [@react-native-oh-tpl/react-native-reanimated](/zh-cn/react-native-reanimated.md)

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;

## 组件

详细请查看 [ant-design-mobile-rn 的文档介绍](http://rn.mobile.ant.design/docs/react/introduce-cn)

以下为目前已支持的组件属性：

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Accordion**：手风琴组件，可以折叠/展开的内容区域。

|       Name        |              Description               |           Type            | Required | Platform | HarmonyOS Support |
| :---------------: | :------------------------------------: | :-----------------------: | :------: | :------: | :---------------: |
| onChange(indexes) |    当 section(s)发生变化的时候执行     | (indexes: number[])=>void |    No    |   All    |        Yes        |
|  activeSections   | 初始化选中 sections ，留空关闭所有面板 |         number[]          |    No    |   All    |        Yes        |

更多自定义属性请参考 https://github.com/oblador/react-native-collapsible#properties-1

**Accordion.Panel**：Accordion 子组件。

|  Name  |  Description   |          Type           | Required | Platform | HarmonyOS Support |
| :----: | :------------: | :---------------------: | :------: | :------: | :---------------: |
|  key   | 对应 activeKey |         String          |    No    |   All    |        Yes        |
| header |   面板头内容   | React.Element or String |   Yes    |   All    |        Yes        |

**ActionSheet**：动作面板组件，从底部弹出的模态框，提供和当前场景相关的 2 个以上的操作动作，也支持提供标题和描述。

|          Name          |                 Description                  |          Type           | Required | Platform | HarmonyOS Support |
| :--------------------: | :------------------------------------------: | :---------------------: | :------: | :------: | :---------------: |
|        options         |             按钮标题列表 (必须)              |     Array 或 String     |   Yes    |   All    |        Yes        |
|   cancelButtonIndex    |         按钮列表中取消按钮的索引位置         |         Number          |    No    |   All    |        Yes        |
| destructiveButtonIndex | 按钮列表中破坏性按钮（一般为删除）的索引位置 |         Number          |    No    |   All    |        Yes        |
|         title          |                   顶部标题                   |         String          |    No    |   All    |        Yes        |
|        message         |             顶部标题下的简要消息             | String 或 React.element |    No    |   All    |        Yes        |

**Card**：卡片组件，用于组织信息和操作，通常也作为详细信息的入口。

| Name | Description |  Type   | Required | Platform | HarmonyOS Support |
| :--: | :---------: | :-----: | :------: | :------: | :---------------: |
| full |  是否通栏   | boolean |    No    |   All    |        Yes        |

**Card.Header**：卡片子组件。

|    Name    |   Description    |         Type          | Required | Platform | HarmonyOS Support |
| :--------: | :--------------: | :-------------------: | :------: | :------: | :---------------: |
|   title    |     卡片标题     | React.Element、String |    No    |   All    |        Yes        |
|   thumb    |   卡片标题图片   | String、React.Element |    No    |   All    |        Yes        |
| thumbStyle |   标题图片样式   |        Object         |    No    |   All    |        Yes        |
|   extra    | 卡片标题辅助内容 | React.Element、String |    No    |   All    |        Yes        |

**Card.Footer**：卡片子组件。

|  Name   | Description  |         Type          | Required | Platform | HarmonyOS Support |
| :-----: | :----------: | :-------------------: | :------: | :------: | :---------------: |
| content |   尾部内容   | React.Element、String |    No    |   All    |        Yes        |
|  extra  | 尾部辅助内容 | React.Element、String |    No    |   All    |        Yes        |

**Icon**：图标组件。

| Name  |     Description     |                Type                | Required | Platform | HarmonyOS Support |
| :---: | :-----------------: | :--------------------------------: | :------: | :------: | :---------------: |
| name  | OutlineGlyphMapType |               string               |   Yes    |   All    |        Yes        |
| size  |      图标大小       | 'xxs'/'xs'/'sm'/'md'/'lg' / number |    No    |   All    |        Yes        |
| color |      图标颜色       |               Color                |    No    |   All    |        Yes        |

**List**：列表组件，单个连续模块垂直排列，显示当前的内容、状态和可进行的操作。eg：联系人列表。

|     Name     |   Description    |                                                              Type                                                              | Required | Platform | HarmonyOS Support |
| :----------: | :--------------: | :----------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
| renderHeader |    list heder    |                                                            (): void                                                            |    No    |   All    |        Yes        |
| renderFooter |   list footer    |                                                            (): void                                                            |    No    |   All    |        Yes        |
|    styles    | 语义化结构 style | [ListStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/list/index.zh-CN.md#liststyle-语义化样式) |    No    |   All    |        Yes        |

**List.Item**：列表子组件。

|     Name     |                                         Description                                         |                                                                                      Type                                                                                      | Required | Platform | HarmonyOS Support |
| :----------: | :-----------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|    thumb     |                           缩略图(当为 string 类型时作为 img src)                            |                                                                             String、React.Element                                                                              |    No    |   All    |        Yes        |
|    extra     |                                          右边内容                                           |                                                                             String 、React.Element                                                                             |    No    |   All    |        Yes        |
|    arrow     | 箭头方向(右,上,下), 可选 horizontal,up,down,empty，如果是 empty 则存在对应的 dom,但是不显示 |                                                                                     String                                                                                     |    No    |   All    |        Yes        |
|    align     |                           子元素垂直对齐，可选 top,middle,bottom                            |                                                                                     String                                                                                     |    No    |   All    |        Yes        |
|   onPress    |                                     点击事件的回调函数                                      |       同[TouchableHighlightProps['onPress']](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.0-rc.0/components/list/index.zh-CN.md#touchablehighlightprops)        |    No    |   All    |        Yes        |
| multipleLine |                                            多行                                             |                                                                                    Boolean                                                                                     |    No    |   All    |        Yes        |
|     wrap     |                          是否换行，默认情况下，文字超长会被隐藏，                           |                                                                                    Boolean                                                                                     |    No    |   All    |        Yes        |
|    styles    |                                      语义化结构 style                                       | [ListItemStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.0-rc.0/components/list/index.zh-CN.md#listitemstyle-%E8%AF%AD%E4%B9%89%E5%8C%96%E6%A0%B7%E5%BC%8F) |    No    |   All    |        Yes        |

**List.Item.Brief**：列表辅助说明组件。

**ListView**：列表 Experimental 组件，当你需要一个 infinite scroll 列表时，请使用 ListView。[更多文档](https://github.com/gameboyVito/react-native-ultimate-listview)

**Modal**：对话框组件，用作显示系统的重要信息，并请求用户进行操作反馈，eg：删除某个重要内容时，弹出 Modal 进行二次确认。

|      Name      |                                                                     Description                                                                      |          Type           | Required | Platform | HarmonyOS Support |
| :------------: | :--------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------: | :------: | :------: | :---------------: |
|    visible     |                                                                    对话框是否可见                                                                    |         Boolean         |    No    |   All    |        Yes        |
|    closable    |                                                                   是否显示关闭按钮                                                                   |         Boolean         |    No    |   All    |        Yes        |
|  maskClosable  |                                                                 点击蒙层是否允许关闭                                                                 |         Boolean         |    No    |   All    |        Yes        |
|    onClose     |                                                                 点击 x 或 mask 回调                                                                  |        (): void         |    No    |   All    |        Yes        |
|  transparent   |                                                                     是否背景透明                                                                     |         Boolean         |    No    |   All    |        Yes        |
|     popup      |                                                                     是否弹窗模式                                                                     |         Boolean         |    No    |   All    |        Yes        |
| animationType  |                                                                可选: 'fade' / 'slide'                                                                |         String          |    No    |   All    |        Yes        |
|     title      |                                                                         标题                                                                         |      React.Element      |    No    |   All    |        Yes        |
|     footer     |                                                                       底部内容                                                                       | Array [{text, onPress}] |    No    |   All    |        Yes        |
| onRequestClose | onRequestClose 回调会在用户按下 Android 设备上的后退按键或是 Apple TV 上的菜单键时触发。返回 true 时会在 modal 处于开启状态时阻止 BackHandler 事件。 |       (): boolean       |    No    |   All    |        No         |

**Modal.alert(title, message, actions?, platform?)**：对话框组件。

|     Name      |                             Description                             |          Type           | Required | Platform | HarmonyOS Support |
| :-----------: | :-----------------------------------------------------------------: | :---------------------: | :------: | :------: | :---------------: |
|     title     |                                标题                                 | String 或 React.Element |    No    |   All    |        Yes        |
|    message    |                              提示信息                               | String 或 React.Element |    No    |   All    |        Yes        |
|    actions    |                  按钮组, [{text, onPress, style}]                   |          Array          |    No    |   All    |        Yes        |
| onBackHandler | 返回键的回调(非必须)，返回 true 则关闭 modal，false 阻止 modal 关闭 |       (): boolean       |    No    |   All    |        Yes        |

**Modal.prompt(title, message, callbackOrActions, type?, defaultValue?, placeholders?, platform?)**：对话框组件。

|       Name        |                             Description                             |                     Type                      | Required | Platform | HarmonyOS Support |
| :---------------: | :-----------------------------------------------------------------: | :-------------------------------------------: | :------: | :------: | :---------------: |
|       title       |                                标题                                 |            String 或 React.Element            |    No    |   All    |        Yes        |
|      message      |                              提示信息                               |            String 或 React.Element            |    No    |   All    |        Yes        |
| callbackOrActions |                 按钮组 [{text, onPress}] 或回调函数                 |               Array or Function               |    No    |   All    |        Yes        |
|       type        |                            prompt 的样式                            | String (default, secure-text, login-password) |    No    |   All    |        Yes        |
|   defaultValue    |                默认值(input 为 password 类型不支持)                 |                    String                     |    No    |   All    |        Yes        |
|   placeholders    |                              ['', '']                               |                   String[]                    |    No    |   All    |        Yes        |
|   onBackHandler   | 返回键的回调(非必须)，返回 true 则关闭 modal，false 阻止 modal 关闭 |                  (): boolean                  |    No    |   All    |        No         |

**Modal.operation(actions?, onBackHandler?)**：对话框组件。

|     Name      |                             Description                             |    Type     | Required | Platform | HarmonyOS Support |
| :-----------: | :-----------------------------------------------------------------: | :---------: | :------: | :------: | :---------------: |
|    actions    |                  按钮组, [{text, onPress, style}]                   |    Array    |    No    |   All    |        Yes        |
| onBackHandler | 返回键的回调(非必须)，返回 true 则关闭 modal，false 阻止 modal 关闭 | (): boolean |    No    |   All    |        Yes        |

**Portal**：Portal 组件，注意：源码复制自 react-native-paper 更多信息请移步https://callstack.github.io/react-native-paper/portal.html。

**Result**：结果页组件，在整张页面中组织插画、图标、文字等内容，向用户反馈操作结果。

|     Name      |          Description          |           Type            | Required | Platform | HarmonyOS Support |
| :-----------: | :---------------------------: | :-----------------------: | :------: | :------: | :---------------: |
|    imgUrl     |           插图 url            | string / Image Source(rn) |    No    |   All    |        Yes        |
|      img      | 插图元素 , 会覆盖 imgUrl 设置 |         ReactNode         |    No    |   All    |        Yes        |
|     title     |          title 文案           |         ReactNode         |    No    |   All    |        Yes        |
|    message    |         message 文案          |         ReactNode         |    No    |   All    |        Yes        |
|  buttonText   |           按钮文案            |          string           |    No    |   All    |        Yes        |
|  buttonType   |     请参考 button 的配置      |          string           |    No    |   All    |        Yes        |
| onButtonClick |         按钮回调函数          |     (e: Object): void     |    No    |   All    |        Yes        |

**Toast**：轻提示组件，一种轻量级反馈/提示，可以用来显示不会打断用户操作的内容，适合用于页面转场、数据交互的等场景中。

|   Name    |          Description           |                                                               Type                                                                | Required | Platform | HarmonyOS Support |
| :-------: | :----------------------------: | :-------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|  content  |            提示内容            |                                                              String                                                               |   Yes    |   All    |        Yes        |
| duration  |     自动关闭的延时，单位秒     |                                                              number                                                               |    No    |   All    |        Yes        |
|   icon    |              图标              |                                                            `'success'`                                                            |    No    |   All    |        Yes        |
| position  |        垂直方向显示位置        |                                                              `'top'`                                                              |    No    |   All    |        Yes        |
|  onClose  |           关闭后回调           |                                                             Function                                                              |    No    |   All    |        Yes        |
|   mask    | 是否显示透明蒙层，防止触摸穿透 |                                                              Boolean                                                              |    No    |   All    |        Yes        |
| stackable |        是否允许叠加显示        |                                                              Boolean                                                              |    No    |   All    |        Yes        |
|  styles   |        语义化结构 style        | [ToastStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/toast/index.zh-CN.md#toaststyle-语义化样式) |    No    |   All    |        Yes        |

**Toast API**

- Toast.success(props)
- Toast.fail(props)
- Toast.info(props)
- Toast.loading(props)
- Toast.offline(props)
- Toast.show(props)

**Toast.removeAll**: 关闭所有显示中的 `Toast`。

**ActivityIndicator**：活动指示器组件，表明某个任务正在进行中。

|   Name    |          Description           |  Type   | Required | Platform | HarmonyOS Support |
| :-------: | :----------------------------: | :-----: | :------: | :------: | :---------------: |
| animating |            显隐状态            | boolean |    No    |   All    |        Yes        |
|   size    | spinner 大小，可选 small/large | string  |    No    |   All    |        Yes        |
|   toast   |        loading 样式类型        | boolean |    No    |   All    |        Yes        |
|   text    |          loading 文本          | string  |    No    |   All    |        Yes        |
|   color   |          spinner 颜色          | string  |    No    |   All    |        Yes        |

**Badge**：徽标数组件，图标右上角的红点、数字或者文字。用于告知用户，该区域的状态变化或者待处理任务的数量。

|     Name      |        Description         |       Type       | Required | Platform | HarmonyOS Support |
| :-----------: | :------------------------: | :--------------: | :------: | :------: | :---------------: |
|     size      |   大小，可选 large small   |      string      |    No    |   All    |        Yes        |
|     text      |      展示的数字或文案      | string 或 number |    No    |   All    |        Yes        |
|    corner     |          置于角落          |     boolean      |    No    |   All    |        Yes        |
|      dot      | 不展示数字，只有一个小红点 |     boolean      |    No    |   All    |        Yes        |
| overflowCount |      展示封顶的数字值      |      number      |    No    |   All    |        Yes        |

**Button**：按钮组件，点击后会触发一个操作。

|      Name       |                     Description                      |       Type        | Required | Platform | HarmonyOS Support |
| :-------------: | :--------------------------------------------------: | :---------------: | :------: | :------: | :---------------: |
|      type       |  按钮类型，可选值为 primary/ghost/warning 或者不设   |      string       |    No    |   All    |        Yes        |
|      size       |           按钮大小，可选值为 large、small            |      string       |    No    |   All    |        Yes        |
|   activeStyle   | 点击反馈的自定义样式 (设为 false 时表示禁止点击反馈) |     {}/false      |    No    |   All    |        Yes        |
| activeClassName |                 点击反馈的自定义类名                 |      string       |    No    |   All    |        No         |
|    disabled     |                       设置禁用                       |      boolean      |    No    |   All    |        Yes        |
|     onPress     |                点击按钮的点击回调函数                | (e: Object): void |    No    |   All    |        Yes        |
|      style      |                      自定义样式                      |      Object       |    No    |   All    |        Yes        |
|    onPressIn    |          同 RN TouchableHighlight onPressIn          | (e: Object): void |    No    |   All    |        Yes        |
|   onPressOut    |         同 RN TouchableHighlight onPressOut          | (e: Object): void |    No    |   All    |        Yes        |
| onShowUnderlay  |       同 RN TouchableHighlight onShowUnderlay        | (e: Object): void |    No    |   All    |        Yes        |
| onHideUnderlay  |       同 RN TouchableHighlight onHideUnderlay        | (e: Object): void |    No    |   All    |        Yes        |

**Carousel**：走马灯组件。

|       Name       |      Description       |            Type            | Required | Platform | HarmonyOS Support |
| :--------------: | :--------------------: | :------------------------: | :------: | :------: | :---------------: |
|  selectedIndex   | 手动设置当前显示的索引 |           number           |    No    |   All    |        Yes        |
|       dots       |   是否显示面板指示点   |          Boolean           |    No    |   All    |        Yes        |
|     vertical     |        垂直显示        |          Boolean           |    No    |   All    |        Yes        |
|     autoplay     |      是否自动切换      |          Boolean           |    No    |   All    |        Yes        |
| autoplayInterval |   自动切换的时间间隔   |           Number           |    No    |   All    |        Yes        |
|     infinite     |      是否循环播放      |          Boolean           |    No    |   All    |        Yes        |
|   afterChange    |  切换面板后的回调函数  |  (current: number): void   |    No    |   All    |        Yes        |
|     dotStyle     |       指示点样式       |         ViewStyle          |    No    |   All    |        Yes        |
|  dotActiveStyle  |  当前激活的指示点样式  |         ViewStyle          |    No    |   All    |        Yes        |
|    pageStyle     |       轮播页样式       |         ViewStyle          |    No    |   All    |        Yes        |
|    pagination    |   自定义 pagination    | (props) => React.ReactNode |    No    |   All    |        Yes        |

**Carousel methods**

| Name |  Description   |                   Type                    | Required | Platform | HarmonyOS Support |
| :--: | :------------: | :---------------------------------------: | :------: | :------: | :---------------: |
| goTo | 跳转到指定位置 | (index: number, animated?: boolean): void |    No    |   All    |        Yes        |

**Checkbox**：复选框组件。

|      Name      |               Description               |        Type        | Required | Platform | HarmonyOS Support |
| :------------: | :-------------------------------------: | :----------------: | :------: | :------: | :---------------: |
| defaultChecked |              初始是否选中               |      Boolean       |    No    |   All    |        Yes        |
|    checked     |            指定当前是否选中             |      Boolean       |    No    |   All    |        Yes        |
|    disabled    |                  禁用                   |      Boolean       |    No    |   All    |        Yes        |
| indeterminate  | 设置 indeterminate 状态，只负责样式控制 |      Boolean       |    No    |   All    |        Yes        |
|    onChange    |        change 事件触发的回调函数        | (e: Event) => void |    No    |   All    |        Yes        |

**Checkbox.CheckboxItem**：基于 List.Item 对 Checkbox 进行封装,List.Item 的 thumb 属性固定传入 Checkbox,其他属性和 List.Item 一致。 其他 API 和 Checkbox 相同。

**Checkbox.AgreeItem**：用于同意协议这种场景的复选框。

**DatePicker**：日期选择组件，用于选择日期或者时间。

|     Name      |                                           Description                                            |                                            Type                                             | Required | Platform | HarmonyOS Support |
| :-----------: | :----------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|   precision   |                                               精度                                               |                                          Precision                                          |    No    |   All    |        Yes        |
|     value     |                                           当前选中时间                                           |                                            Date                                             |    No    |   All    |        Yes        |
| defaultValue  |                                           默认选中时间                                           |                                            Date                                             |    No    |   All    |        Yes        |
|    minDate    |                                           最小可选日期                                           |                                            Date                                             |    No    |   All    |        Yes        |
|    maxDate    |                                           最大可选日期                                           |                                          Precision                                          |    No    |   All    |        Yes        |
|   onChange    |                                      时间发生变化的回调函数                                      |                                    (value: Date) => void                                    |    No    |   All    |        Yes        |
| onValueChange |                                     每列 picker 改变时的回调                                     |                            (value: Date, index: number) => void                             |    No    |   All    |        Yes        |
|  renderLabel  | 自定义渲染每列展示的内容。其中 type 参数为 precision 中的任意值或 now，data 参数为默认渲染的数字 |                     (type:Precision / 'now', data: number) => ReactNode                     |    No    |   All    |        Yes        |
|    locale     |                             国际化，可覆盖全局 LocaleProvider 的配置                             | Object: {okText, dismissText, extra, DatePickerLocale:{ year,month,day,hour,minute,am,pm }} |    No    |   All    |        Yes        |
|    filter     |                                        过滤可供选择的时间                                        |                                      DatePickerFilter                                       |    No    |   All    |        Yes        |

**DatePickerView**：日期选择器组件，atePickerView 的功能类似于 DatePicker ，但它是直接渲染在区域中，而不是弹出窗口。

|     Name      |                                           Description                                            |                        Type                         | Required | Platform | HarmonyOS Support |
| :-----------: | :----------------------------------------------------------------------------------------------: | :-------------------------------------------------: | :------: | :------: | :---------------: |
|   precision   |                                               精度                                               |                      Precision                      |    No    |   All    |        Yes        |
|     value     |                                           当前选中时间                                           |                        Date                         |    No    |   All    |        Yes        |
| defaultValue  |                                           默认选中时间                                           |                        Date                         |    No    |   All    |        Yes        |
|    minDate    |                                           最小可选日期                                           |                        Date                         |    No    |   All    |        Yes        |
|    maxDate    |                                           最大可选日期                                           |                      Precision                      |    No    |   All    |        Yes        |
|   onChange    |                                      时间发生变化的回调函数                                      |                (value: Date) => void                |    No    |   All    |        Yes        |
| onValueChange |                                     每列 picker 改变时的回调                                     |        (value: Date, index: number) => void         |    No    |   All    |        Yes        |
|  renderLabel  | 自定义渲染每列展示的内容。其中 type 参数为 precision 中的任意值或 now，data 参数为默认渲染的数字 | (type:Precision / 'now', data: number) => ReactNode |    No    |   All    |        Yes        |
|    filter     |                                        过滤可供选择的时间                                        |                  DatePickerFilter                   |    No    |   All    |        Yes        |

**InputItem**：文本输入组件，用于接受单行文本。

|           Name           |                                                                                                                     Description                                                                                                                     |        Type         | Required | Platform | HarmonyOS Support |
| :----------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------: | :------: | :------: | :---------------: |
|           type           |                                       可以是银行卡 bankCard; 手机号 phone(此时最大长度固定为 11,maxLength 设置无效); 密码 password; 数字 number; digit(表示原生的 number 类型); 以及其他标准 input type 类型                                        |       String        |    No    |   All    |        Yes        |
|          value           |                                                                                       value 值(受控与否参考https://facebook.github.io/react/docs/forms.html)                                                                                        |       String        |    No    |   All    |        Yes        |
|       defaultValue       |                                                                                                                   设置初始默认值                                                                                                                    |       String        |    No    |   All    |        Yes        |
|       placeholder        |                                                                                                                     placeholder                                                                                                                     |       String        |    No    |   All    |        Yes        |
|         editable         |                                                                                                                     是否可编辑                                                                                                                      |        bool         |    No    |   All    |        Yes        |
|         disabled         |                                                                                                                      是否禁用                                                                                                                       |        bool         |    No    |   All    |        Yes        |
|          clear           | 是否带清除功能(仅 editable 为 true,disabled 为 false 才生效)。在 Android 中, 处于编辑状态(focus)时 icon 才会出现, 且此组件被 ScrollView 包裹时, 设置 ScrollView 的 keyboardShouldPersistTaps 属性为 handled 或 always 时, icon 才会正确响应点击事件 |        bool         |    No    |   All    |        Yes        |
|        maxLength         |                                                                                                                      最大长度                                                                                                                       |       number        |    No    |   All    |        Yes        |
|         onChange         |                                                                                                              change 事件触发的回调函数                                                                                                              | (val: string): void |    No    |   All    |        Yes        |
|          onBlur          |                                                                                                               blur 事件触发的回调函数                                                                                                               | (val: string): void |    No    |   All    |        Yes        |
|         onFocus          |                                                                                                              focus 事件触发的回调函数                                                                                                               | (val: string): void |    No    |   All    |        Yes        |
|          error           |                                                                                                                      报错样式                                                                                                                       |        bool         |    No    |   All    |        Yes        |
|       onErrorClick       |                                                                                                            点击报错 icon 触发的回调函数                                                                                                             |  (e: Object): void  |    No    |   All    |        Yes        |
|          extra           |                                                                                                                      右边注释                                                                                                                       |   string or node    |    No    |   All    |        Yes        |
|       onExtraClick       |                                                                                                            extra 点击事件触发的回调函数                                                                                                             |  (e: Object): void  |    No    |   All    |        Yes        |
| onVirtualKeyboardConfirm |                                                                                                            虚拟键盘点击确认时的回调函数                                                                                                             | (val: string): void |    No    |   All    |        No         |
|       labelNumber        |                                                                                                         标签的文字个数，可用 2-7 之间的数字                                                                                                         |       number        |    No    |   All    |        Yes        |
|           last           |                                                                                           如果是最后一项，则将移除 borderBottom（默认拥有 borderBottom）                                                                                            |        bool         |    No    |   All    |        Yes        |
|          locale          |                                                                                                国际化, 当 type 为 money，可以自定义确认按钮的文案。                                                                                                 |        bool         |    No    |   All    |        No         |

**Picker**：选择器组件，在一组预设数据中进行选择，e.g. 省市区选择。

|        Name        |                                                           Description                                                            |                                       Type                                       | Required | Platform | HarmonyOS Support |
| :----------------: | :------------------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|        data        |                                                              数据源                                                              |                        `PickerColumn` / `PickerColumn[]`                         |    No    |   All    |        Yes        |
|       value        |                                                              选中项                                                              |                                 `PickerValue[]`                                  |    No    |   All    |        Yes        |
|    defaultValue    |                                                            默认选中项                                                            |                                 `PickerValue[]`                                  |    No    |   All    |        Yes        |
|      cascade       |                                            是否级联。子级来自`data`参数内的`children`                                            |                                     Boolean                                      |    No    |   All    |        Yes        |
|        cols        |                                                               列数                                                               |                                      Number                                      |    No    |   All    |        Yes        |
|      onChange      |                                                           选中后的回调                                                           |           `(value: PickerValue[], extend: PickerValueExtend) => void`            |    No    |   All    |        Yes        |
|   onPickerChange   |                                                   每列数据选择变化后的回调函数                                                   |                 `(value: PickerValue[], index: number) => void`                  |    No    |   All    |        Yes        |
|  onVisibleChange   |                                                     当显隐状态变化时回调函数                                                     |                             `(visible: bool): void`                              |    No    |   All    |        Yes        |
|    renderLabel     |                                                     自定义渲染每列展示的内容                                                     | `(item: PickerColumnItem, index: number) => ReactNode` 或 `(item) => item.label` |    No    |   All    |        Yes        |
|       title        |                                                              大标题                                                              |                                    ReactNode                                     |    No    |   All    |        Yes        |
|       okText       |                                                            选中的文案                                                            |                                      String                                      |    No    |   All    |        Yes        |
|    dismissText     |                                                          取消选中的文案                                                          |                                      String                                      |    No    |   All    |        Yes        |
|        onOk        |                                                       点击选中时执行的回调                                                       |           `(value: PickerValue[], extend: PickerValueExtend) => void`            |    No    |   All    |        Yes        |
|     onDismiss      |                                                       点击取消时执行的回调                                                       |                                     (): void                                     |    No    |   All    |        Yes        |
|   okButtonProps    |                                                          ok 按钮 props                                                           |    [TouchableHighlightProps](https://reactnative.dev/docs/touchablehighlight)    |    No    |   All    |        Yes        |
| dismissButtonProps |                                                        dismiss 按钮 props                                                        |    [TouchableHighlightProps](https://reactnative.dev/docs/touchablehighlight)    |    No    |   All    |        Yes        |
|      visible       |                                                          是否显示选择器                                                          |                                     Boolean                                      |    No    |   All    |        Yes        |
|      loading       |                                                         是否处于加载状态                                                         |                                     Boolean                                      |    No    |   All    |        Yes        |
|   loadingContent   |                                                       加载状态下展示的内容                                                       |                                    ReactNode                                     |    No    |   All    |        Yes        |
|   indicatorStyle   |                                                      默认 Indicator 的样式                                                       |                                      Object                                      |    No    |   All    |        No         |
|       locale       | 国际化，可覆盖全局[Provider](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/provider-cn)的`locale`配置 |                       Object: {okText, dismissText, extra}                       |    No    |   All    |        Yes        |

**Picker 自定义样式**

|     Name      |                                         Description                                          |          Type          | Required | Platform | HarmonyOS Support |
| :-----------: | :------------------------------------------------------------------------------------------: | :--------------------: | :------: | :------: | :---------------: |
|     style     |                                           外部样式                                           | `StyleProp<ViewStyle>` |    No    |   All    |        Yes        |
|    styles     |                                        内部组件样式集                                        |   `PickerViewStyle`    |    No    |   All    |        Yes        |
|   itemStyle   |                                           每列样式                                           | `StyleProp<TextStyle>` |    No    |   All    |        Yes        |
|  itemHeight   | 每列固定高度，未设值时会根据`numberOfLines`动态计算；`itemStyle`属性设置`{height}`值是无效的 |         Number         |    No    |   All    |        Yes        |
| numberOfLines |                                       允许每列显示行数                                       |         Number         |    No    |   All    |        Yes        |

**Picker 遮罩层**
还支持自定义遮罩样式，如使用渐变组件`<LinearGradient />`。当前默认为白色半透明。

|       Name       |       Description        |                                             Type                                             | Required | Platform | HarmonyOS Support |
| :--------------: | :----------------------: | :------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|  renderMaskTop   | 自定义渲染上半部分遮罩层 | `()=> ReactNode` 或 `<View style={{ flex: 1, backgroundColor: 'rgba(255,255,255,0.8)' }} />` |    No    |   All    |        Yes        |
| renderMaskBottom | 自定义渲染下半部分遮罩层 | `()=> ReactNode` 或 `<View style={{ flex: 1, backgroundColor: 'rgba(255,255,255,0.8)' }} />` |    No    |   All    |        Yes        |

**Picker 的 Children**
通常是 [List.Item](/components/list-cn/#List.Item) ，以下属性也是围绕着`List.Item`展开：

|    Name     |                  Description                  |          Type           | Required | Platform | HarmonyOS Support |
| :---------: | :-------------------------------------------: | :---------------------: | :------: | :------: | :---------------: |
|  children   |      Picker 占位组件，通常是`List.Item`       |        ReactNode        |    No    |   All    |        Yes        |
|    extra    | Picker children 的`extra`属性，无选中项时展示 |         String          |    No    |   All    |        Yes        |
| triggerType |                 按钮事件名称                  |         String          |    No    |   All    |        Yes        |
|  disabled   |                  是否不可用                   |         Boolean         |    No    |   All    |        Yes        |
|   format    |  格式化选中值的函数，用于回显在 extra 属性上  | (labels: string[]): any |    No    |   All    |        Yes        |

**PickerView**：PickerView 的功能类似于 Picker ，但它是直接渲染在区域中，而不是弹出窗口。

|      Name      |                              Description                               |                                       Type                                       | Required | Platform | HarmonyOS Support |
| :------------: | :--------------------------------------------------------------------: | :------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|      data      |                                 数据源                                 |                        `PickerColumn` / `PickerColumn[]`                         |    No    |   All    |        Yes        |
|     value      |                                 选中项                                 |                                 `PickerValue[]`                                  |    No    |   All    |        Yes        |
|  defaultValue  |                               默认选中项                               |                                 `PickerValue[]`                                  |    No    |   All    |        Yes        |
|    cascade     |             是否级联。子级来自`data`参数内的`children`属性             |                                     Boolean                                      |    No    |   All    |        Yes        |
|      cols      |                                  列数                                  |                                      Number                                      |    No    |   All    |        Yes        |
|    onChange    | 选中后的回调，可使用[rc-form](https://github.com/react-component/form) |           `(value: PickerValue[], extend: PickerValueExtend) => void`            |    No    |   All    |        Yes        |
|  renderLabel   |                        自定义渲染每列展示的内容                        | `(item: PickerColumnItem, index: number) => ReactNode` 或 `(item) => item.label` |    No    |   All    |        Yes        |
|    loading     |                            是否处于加载状态                            |                                     Boolean                                      |    No    |   All    |        Yes        |
| loadingContent |                          加载状态下展示的内容                          |                                    ReactNode                                     |    No    |   All    |        Yes        |
| indicatorStyle |                         默认 Indicator 的样式                          |                                      Object                                      |    No    |   All    |        No         |

**PickerView 自定义样式**

|     Name      |                                         Description                                          |          Type          | Required | Platform | HarmonyOS Support |
| :-----------: | :------------------------------------------------------------------------------------------: | :--------------------: | :------: | :------: | :---------------: |
|     style     |                                           外部样式                                           | `StyleProp<ViewStyle>` |    No    |   All    |        Yes        |
|    styles     |                                        内部组件样式集                                        |   `PickerViewStyle`    |    No    |   All    |        Yes        |
|   itemStyle   |                                           每列样式                                           | `StyleProp<TextStyle>` |    No    |   All    |        Yes        |
|  itemHeight   | 每列固定高度，未设值时会根据`numberOfLines`动态计算；`itemStyle`属性设置`{height}`值是无效的 |         Number         |    No    |   All    |        Yes        |
| numberOfLines |                                       允许每列显示行数                                       |         Number         |    No    |   All    |        Yes        |

**PickerView 遮罩层**

还支持自定义遮罩样式，如使用渐变组件`<LinearGradient />`。当前默认为白色半透明。

|       Name       |       Description        |                                             Type                                             | Required | Platform | HarmonyOS Support |
| :--------------: | :----------------------: | :------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|  renderMaskTop   | 自定义渲染上半部分遮罩层 | `()=> ReactNode` 或 `<View style={{ flex: 1, backgroundColor: 'rgba(255,255,255,0.8)' }} />` |    No    |   All    |        Yes        |
| renderMaskBottom | 自定义渲染下半部分遮罩层 | `()=> ReactNode` 或 `<View style={{ flex: 1, backgroundColor: 'rgba(255,255,255,0.8)' }} />` |    No    |   All    |        Yes        |

**Progress**：进度条组件，表明某个任务的当前进度。

|   Name   |                        Description                         |  Type   | Required | Platform | HarmonyOS Support |
| :------: | :--------------------------------------------------------: | :-----: | :------: | :------: | :---------------: |
| percent  |                         进度百分比                         | number  |    No    |   All    |        Yes        |
| position | 进度条的位置，fixed 将浮出固定在最顶层，可选: fixed normal | string  |    No    |   All    |        Yes        |
| unfilled |                    是否显示未填充的轨道                    | boolean |    No    |   All    |        Yes        |
|  style   |                         进度条样式                         | object  |    No    |   All    |        Yes        |
| barStyle |                          进度样式                          | object  |    No    |   All    |        Yes        |

**Pagination**：分页器组件。

|   Name   |                Description                 |             Type             | Required | Platform | HarmonyOS Support |
| :------: | :----------------------------------------: | :--------------------------: | :------: | :------: | :---------------: |
|   mode   |      形态，可选 button,number,pointer      |            string            |    No    |   All    |        Yes        |
| current  |                  当前页号                  |            number            |    No    |   All    |        Yes        |
|  total   |                  数据总数                  |            number            |    No    |   All    |        Yes        |
|  simple  |                是否隐藏数值                |           boolean            |    No    |   All    |        Yes        |
| disabled |                  禁用状态                  |           boolean            |    No    |   All    |        No         |
|  locale  | 国际化, 可以覆盖全局 LocaleProvider 的配置 | Object：{prevText, nextText} |    No    |   All    |        Yes        |
| onChange |         change 事件触发的回调函数          |      (e: Object): void       |    No    |   All    |        Yes        |

**Radio**：单选框组件。

|      Name      |          Description          |                     Type                      | Required | Platform | HarmonyOS Support |
| :------------: | :---------------------------: | :-------------------------------------------: | :------: | :------: | :---------------: |
| defaultChecked |         初始是否选中          |                    Boolean                    |    No    |   All    |        Yes        |
|    checked     |       指定当前是否选中        |                    Boolean                    |    No    |   All    |        Yes        |
|    disabled    |             禁用              |                    Boolean                    |    No    |   All    |        Yes        |
|    onChange    |   change 事件触发的回调函数   | (e: { target: { checked: boolean } }) => void |    No    |   All    |        Yes        |
|     value      | 携带的标识值，用于 Group 模式 |                  RadioValue                   |    No    |   All    |        Yes        |

**Radio.RadioItem**
基于 List.Item 对 Radio 进行封装,List.Item 的 extra 属性固定传入 Radio,其他属性和 List.Item 一致。 其他 API 和 Radio 相同。

**Radio.Group**：单选框子组件。

|     Name     |        Description        |                                       Type                                        | Required | Platform | HarmonyOS Support |
| :----------: | :-----------------------: | :-------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
| defaultValue |       默认选中的值        |                                    RadioValue                                     |    No    |   All    |        Yes        |
|   options    |   以配置形式设置子元素    | string[] 或 number[] 或 Array<{ label: string value: string disabled?: boolean }> |    No    |   All    |        Yes        |
|   disabled   |           禁用            |                                      Boolean                                      |    No    |   All    |        Yes        |
|   onChange   | change 事件触发的回调函数 |                   (e: { target: { checked: boolean } }) => void                   |    No    |   All    |        Yes        |
|    value     |   用于设置当前选中的值    |                                    RadioValue                                     |    No    |   All    |        Yes        |

**Stepper**：步进器，用作增加或者减少当前数值。

|       Name       |                                                      Description                                                      |                                    Type                                    | Required | Platform | HarmonyOS Support |
| :--------------: | :-------------------------------------------------------------------------------------------------------------------: | :------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|    allowEmpty    |                                                   是否允许内容为空                                                    |                                 `boolean`                                  |    No    |   All    |        Yes        |
|      digits      |          格式化到小数点后固定位数，设置为 `0` 表示格式化到整数。配置 `formatter` 时展示会以 `formatter` 为准          |                                  `number`                                  |    No    |   All    |        Yes        |
|    formatter     |                                                    格式化展示数值                                                     |                        `(value?: number) => string`                        |    No    |   All    |        Yes        |
|      parser      |                                    将输入解析为对应数字，一般配合 `formatter` 使用                                    |                          (text: string) => number                          |    No    |   All    |        Yes        |
| minusButtonProps |                                                   minus 按钮 props                                                    | [TouchableHighlightProps](https://reactnative.dev/docs/touchablehighlight) |    No    |   All    |        Yes        |
| plusButtonProps  |                                                    plus 按钮 props                                                    | [TouchableHighlightProps](https://reactnative.dev/docs/touchablehighlight) |    No    |   All    |        Yes        |
|       min        |                                                        最小值                                                         |                                   Number                                   |    No    |   All    |        Yes        |
|       max        |                                                        最大值                                                         |                                   Number                                   |    No    |   All    |        Yes        |
|      value       |                                                        当前值                                                         |                                   Number                                   |    No    |   All    |        Yes        |
|       step       |                                               每次改变步数，可以为小数                                                |                              Number or String                              |    No    |   All    |        Yes        |
|   defaultValue   |                                                        初始值                                                         |                                   Number                                   |    No    |   All    |        Yes        |
|     onChange     |                                                    变化时回调函数                                                     |                                  (): void                                  |    No    |   All    |        Yes        |
|     disabled     |                                                         禁用                                                          |                                  Boolean                                   |    No    |   All    |        Yes        |
|     readOnly     |                                                      input 只读                                                       |                                  Boolean                                   |    No    |   All    |        Yes        |
|      styles      |                                                 react native 组件样式                                                 |                           ReactNative StyleSheet                           |    No    |   All    |        Yes        |
|    stringMode    | 字符值模式，开启后支持高精度小数。开启后 `defaultValue`、`value`、`min`、`max`、`onChange` 等都将转换为 `string` 类型 |                                 `boolean`                                  |    No    |   All    |        Yes        |
|    inputStyle    |                                               react native 显示数字样式                                               |                           ReactNative StyleSheet                           |    No    |   All    |        Yes        |

**Steps**：步骤条组件，显示一个任务的进度；或者引导用户完成某个复杂任务。

|   Name    |                                 Description                                 |               Type                | Required | Platform | HarmonyOS Support |
| :-------: | :-------------------------------------------------------------------------: | :-------------------------------: | :------: | :------: | :---------------: |
|  current  | 指定当前步骤，从 0 开始记数。在子 Step 元素中，可以通过 status 属性覆盖状态 |              number               |    No    |   All    |        Yes        |
|   size    |                         尺寸，支持设置小尺寸 small                          |              string               |    No    |   All    |        Yes        |
|  status   |             指定当前步骤的状态，可选 wait process finish error              |              string               |    No    |   All    |        Yes        |
| direction |                     step 样式( RN 目前只支持 vertical )                     | Enum { 'vertical', 'horizontal' } |    No    |   All    |        Yes        |

**Steps.Step**：步骤条组件，步骤条内的每一个步骤。

|    Name     |                             Description                              |                                         Type                                          | Required | Platform | HarmonyOS Support |
| :---------: | :------------------------------------------------------------------: | :-----------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|   status    | 指定状态。当不配置该属性时，会使用 Steps 的 current 来自动指定状态。 |                     Enum { 'wait', 'process', 'finish', 'error' }                     |    No    |   All    |        Yes        |
|    title    |                                 标题                                 |                                     React.Element                                     |    No    |   All    |        Yes        |
| description |                         步骤的详情描述，可选                         |                                     React.Element                                     |    No    |   All    |        Yes        |
|    icon     |                            步骤图标，可选                            |                                 object/React.Element                                  |    No    |   All    |        Yes        |
| renderIcon  |                         自定义步骤图标，可选                         | (params: { starting: boolean; waiting: boolean; error: boolean; }) => React.ReactNode |    No    |   All    |        Yes        |

**Switch**：滑动开关组件，在两个互斥对象进行选择，eg：选择开或关。

|       Name        |                       Description                       |                  Type                   | Required | Platform | HarmonyOS Support |
| :---------------: | :-----------------------------------------------------: | :-------------------------------------: | :------: | :------: | :---------------: |
|      checked      |                      是否默认选中                       |                 Boolean                 |    No    |   All    |        Yes        |
|  defaultChecked   |                      初始是否打开                       |                 Boolean                 |    No    |   All    |        Yes        |
|     disabled      |                      是否不可修改                       |                 boolean                 |    No    |   All    |        Yes        |
|      loading      |                      加载中的开关                       |                 Boolean                 |    No    |   All    |        Yes        |
|     onChange      | 变化时的回调函数，当返回 Promise 时，会自动显示加载状态 | (val: boolean) => void 或 Promise<void> |    No    |   All    |        Yes        |
|       color       |                    开关打开后的颜色                     |                 String                  |    No    |   All    |        Yes        |
|  checkedChildren  |                      选中时的内容                       |                ReactNode                |    No    |   All    |        Yes        |
| unCheckedChildren |                     非选中时的内容                      |                ReactNode                |    No    |   All    |        Yes        |

**Tabs**：标签页组件，用于让用户在不同的视图中进行切换。

|            Name            |        Description         |                          Type                          | Required | Platform | HarmonyOS Support |
| :------------------------: | :------------------------: | :----------------------------------------------------: | :------: | :------: | :---------------: |
|            tabs            |          tab 数据          |                    Models.TabData[]                    |   Yes    |   All    |        Yes        |
|       tabBarPosition       |        TabBar 位置         |                   'top' 或 'bottom'                    |    No    |   All    |        Yes        |
|        renderTabBar        |        替换 TabBar         | ((props: TabBarPropsType) => React.ReactNode) 或 false |    No    |   All    |        Yes        |
|        initialPage         |  初始化 Tab, index or key  |                    number 或 string                    |    No    |   All    |        Yes        |
|            page            |   当前 Tab, index or key   |                    number 或 string                    |    No    |   All    |        Yes        |
|         swipeable          |    是否可以滑动内容切换    |                        boolean                         |    No    |   All    |        Yes        |
|          useOnPan          |        使用跟手滚动        |                        boolean                         |    No    |   All    |        Yes        |
| prerenderingSiblingsNumber |    预加载两侧 Tab 数量     |                         number                         |    No    |   All    |        Yes        |
|          animated          |      是否开启切换动画      |                        boolean                         |    No    |   All    |        Yes        |
|          onChange          |       tab 变化时触发       |      (tab: Models.TabData, index: number) => void      |    No    |   All    |        Yes        |
|         onTabClick         |      tab 被点击的回调      |      (tab: Models.TabData, index: number) => void      |    No    |   All    |        Yes        |
|     destroyInactiveTab     |      销毁超出范围 Tab      |                        boolean                         |    No    |   All    |        Yes        |
|    distanceToChangeTab     |   滑动切换阈值(宽度比例)   |                         number                         |    No    |   All    |        Yes        |
|          usePaged          |      是否启用分页模式      |                        boolean                         |    No    |   All    |        Yes        |
|    tabBarUnderlineStyle    |     tabBar 下划线样式      |               React.CSSProperties 或 any               |    No    |   All    |        Yes        |
|   tabBarActiveTextColor    |  tabBar 激活 Tab 文字颜色  |                         string                         |    No    |   All    |        Yes        |
|   tabBarBackgroundColor    |       tabBar 背景色        |                         string                         |    No    |   All    |        Yes        |
|      tabBarTextStyle       |      tabBar 文字样式       |               React.CSSProperties 或 any               |    No    |   All    |        Yes        |
|  tabBarInactiveTextColor   | tabBar 非激活 Tab 文字颜色 |                         string                         |    No    |   All    |        Yes        |
|         renderTab          |     替换 TabBar 的 Tab     |        (tab: Models.TabData) => React.ReactNode        |    No    |   All    |        Yes        |
|      renderUnderline       |      renderUnderline       |            (style: any) => React.ReactNode             |    No    |   All    |        Yes        |

**Tabs.DefaultTabBar**

|    Name    |    Description     |                     Type                     | Required | Platform | HarmonyOS Support |
| :--------: | :----------------: | :------------------------------------------: | :------: | :------: | :---------------: |
|  goToTab   |      跳转 Tab      |          (index: number) => boolean          |    No    |   All    |        Yes        |
|    tabs    |      tab 数据      |               Models.TabData[]               |   Yes    |   All    |        Yes        |
| activeTab  | 当前激活 Tab 索引  |                    number                    |    No    |   All    |        Yes        |
|  animated  |    是否使用动画    |                   boolean                    |    No    |   All    |        Yes        |
| renderTab  | 替换 TabBar 的 Tab |   (tab: Models.TabData) => React.ReactNode   |    No    |   All    |        Yes        |
|    page    |    Tab 分页尺寸    |                    number                    |    No    |   All    |        Yes        |
| onTabClick |  tab 被点击的回调  | (tab: Models.TabData, index: number) => void |    No    |   All    |        Yes        |

**Tag**：标签组件，进行标记和分类的小标签，用于标记事物的属性和维度，以及进行分类。

|    Name     |            Description             |          Type          | Required | Platform | HarmonyOS Support |
| :---------: | :--------------------------------: | :--------------------: | :------: | :------: | :---------------: |
|    small    |              小号标签              |        Boolean         |    No    |   All    |        Yes        |
|  disabled   |             是否不可用             |        Boolean         |    No    |   All    |        Yes        |
|  closable   | 是否关闭（非 disabled small 状态） |        Boolean         |    No    |   All    |        Yes        |
|  selected   |            是否默认选中            |        Boolean         |    No    |   All    |        Yes        |
|  onChange   |          切换选中回调函数          | (selected: bool): void |    No    |   All    |        Yes        |
|   onClose   |         点关闭时的回调函数         |        (): void        |    No    |   All    |        Yes        |
| afterClose  |            关闭后的回调            |        (): void        |    No    |   All    |        Yes        |
| onLongPress |             长按的回调             |        (): void        |    No    |   All    |        Yes        |

**TextareaItem**：多行输入组件。

|     Name     |                                                            Description                                                             |        Type         | Required | Platform | HarmonyOS Support |
| :----------: | :--------------------------------------------------------------------------------------------------------------------------------: | :-----------------: | :------: | :------: | :---------------: |
|    value     |                                                              value 值                                                              |       String        |    No    |   All    |        Yes        |
| defaultValue |                                                           设置初始默认值                                                           |       String        |    No    |   All    |        Yes        |
| placeholder  |                                                            placeholder                                                             |       String        |    No    |   All    |        Yes        |
|   editable   |                                                             是否可编辑                                                             |        bool         |    No    |   All    |        Yes        |
|   disabled   |                                                              是否禁用                                                              |        bool         |    No    |   All    |        Yes        |
|    clear     |                                    是否带清除功能(仅 editable 为 true,disabled 为 false 才生效)                                    |        bool         |    No    |   All    |        Yes        |
|    count     |                                         计数功能,兼具最大长度,默认为 0,代表不开启计数功能                                          |       number        |    No    |   All    |        Yes        |
|     rows     |                                                              显示几行                                                              |       number        |    No    |   All    |        Yes        |
|   onChange   |                                                     change 事件触发的回调函数                                                      | (val: string): void |    No    |   All    |        Yes        |
|    error     |                                                              报错样式                                                              |        bool         |    No    |   All    |        Yes        |
| onErrorClick |                                                      点击报错 icon 触发的回调                                                      |      (): void       |    No    |   All    |        Yes        |
|  autoHeight  |                                              高度自适应, autoHeight 和 rows 请二选一                                               |        bool         |    No    |   All    |        Yes        |
| labelNumber  | 定宽枚举值：num \* @input-label-width: 34px，可用 2-7 之间的数字，一般(不能保证全部)能对应显示出相应个数的中文文字(不考虑英文字符) |       number        |    No    |   All    |        Yes        |
|     last     |                                   如果是最后一项，则将移除 borderBottom（默认拥有 borderBottom）                                   |        bool         |    No    |   All    |        Yes        |

**Flex**：布局组件，Flex 是 CSS flex 布局的一个封装。

|   Name    |                               Description                               |  Type  | Required | Platform | HarmonyOS Support |
| :-------: | :---------------------------------------------------------------------: | :----: | :------: | :------: | :---------------: |
| direction |                  项目定位方向，值可以为 `row`,`column`                  | String |    No    |   All    |        Yes        |
|   wrap    |                  子元素的换行方式，可选`nowrap`,`wrap`                  | String |    No    |   All    |        Yes        |
|  justify  | 子元素在主轴上的对齐方式，可选`start`,`end`,`center`,`between`,`around` | String |    No    |   All    |        Yes        |
|   align   |    子元素在交叉轴上的对齐方式，可选`start`,`end`,`center`,`stretch`     | String |    No    |   All    |        Yes        |

**Grid**：宫格组件，在水平和垂直方向，将布局切分成若干等大的区块。

|      Name      |              Description               |               Type                | Required | Platform | HarmonyOS Support |
| :------------: | :------------------------------------: | :-------------------------------: | :------: | :------: | :---------------: |
|      data      |             传入的菜单数据             |    `Array<{icon, text}>` 或 []    |    No    |   All    |        Yes        |
|    onPress     |         点击每个菜单的回调函数         | (el: Object, index: number): void |    No    |   All    |        Yes        |
|   columnNum    |                  列数                  |              number               |    No    |   All    |        Yes        |
|    hasLine     |               是否有边框               |              boolean              |    No    |   All    |        Yes        |
|   isCarousel   |               是否跑马灯               |              boolean              |    No    |   All    |        Yes        |
| carouselProps  |               跑马灯属性               |           CarouselProps           |    No    |   All    |        Yes        |
| carouselMaxRow | 如果是跑马灯, 一页跑马灯需要展示的行数 |              number               |    No    |   All    |        Yes        |
|   renderItem   |     自定义每个 grid 条目的创建函数     |     (el, index) => React.Node     |    No    |   All    |        Yes        |
|   itemStyle    |           每个格子自定义样式           |              object               |    No    |   All    |        Yes        |

`isCarousel = true` 模式时，还可以传递 [carousel](https://mobile.ant.design/components/carousel) 相关的 API。

**国际化和皮肤配置**：为组件内建文案提供统一的国际化支持。

|  Name  |                                                                               Description                                                                                |  Type  | Required | Platform | HarmonyOS Support |
| :----: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :----: | :------: | :------: | :---------------: |
| locale |                                             语言包配置，语言包可到 `@ant-design/react-native/lib/locale-provider/`目录下寻找                                             | object |    No    |   All    |        Yes        |
| theme  | 主题样式配置，可根据需要覆盖部分或者全部变量，具体变量请查看 [theme](https://github.com/ant-design/ant-design-mobile-rn/blob/master/components/style/themes/default.tsx) | object |    No    |   All    |        Yes        |

**View**：基础组件，更安全的 View 基础组件。

|   Name   | Description |                     Type                     | Required | Platform | HarmonyOS Support |
| :------: | :---------: | :------------------------------------------: | :------: | :------: | :---------------: |
| children |   子组件    |      React.ReactNode 或 React.ReactText      |    No    |   All    |        Yes        |
|  style   |    样式     | StyleProp<ViewStyle> 或 StyleProp<TextStyle> |    No    |   All    |        Yes        |

**WhiteSpace**：上下留白组件。

| Name |             Description             |  Type  | Required | Platform | HarmonyOS Support |
| :--: | :---------------------------------: | :----: | :------: | :------: | :---------------: |
| size | 上下留白的间距，可选 xs,sm,md,lg,xl | string |    No    |   All    |        Yes        |

**WingBlank**：两翼留白组件。

| Name |            Description             |  Type  | Required | Platform | HarmonyOS Support |
| :--: | :--------------------------------: | :----: | :------: | :------: | :---------------: |
| size | 两翼留白的间距，可选`sm`,`md`,`lg` | string |    No    |   All    |        Yes        |

**NoticeBar**：通告栏组件，在导航栏下方，一般用作系统提醒、活动提醒等通知。

|     Name     |                   Description                   |                                                                      Type                                                                      | Required | Platform | HarmonyOS Support |
| :----------: | :---------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|     mode     |        提示类型，可选 `closable`,`link`         |                                                                     String                                                                     |    No    |   All    |        Yes        |
|     icon     |               在开始位置设置图标                |                                                                   ReactNode                                                                    |    No    |   All    |        Yes        |
|   children   |                     子组件                      |                                                                   ReactNode                                                                    |    No    |   All    |        Yes        |
|   onPress    |         点击关闭或者操作区域的回调函数          |                                                                    (): void                                                                    |    No    |   All    |        Yes        |
| marqueeProps |                  marquee 参数                   |                                                                     Object                                                                     |    No    |   All    |        Yes        |
|    action    |            用于替换操作 icon 的文案             |                                                                  ReactElement                                                                  |    No    |   All    |        Yes        |
|   onClose    | 点击关闭的回调函数。仅当`mode="closable"`时生效 |                                                                   () => void                                                                   |    No    |   All    |        Yes        |
|    style     |                   最外层样式                    |                                                              StyleProp<ViewStyle>                                                              |    No    |   All    |        Yes        |
|    styles    |                语义化结构 style                 | [NoticeBarStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/notice-bar/index.zh-CN.md#noticebarstyle-语义化样式) |    No    |   All    |        Yes        |

**NoticeBar.MarqueeProps**

|      Name       |                                 Description                                 |                   Type                   | Required | Platform | HarmonyOS Support |
| :-------------: | :-------------------------------------------------------------------------: | :--------------------------------------: | :------: | :------: | :---------------: |
|    autoFill     |              是否自动用 children 的副本填充字幕框中的空白区域               |                `Boolean`                 |    No    |   All    |        Yes        |
|    direction    |                               字幕滑动的方向                                | `'left'` 或`'right'` 或`'up'` 或`'down'` |    No    |   All    |        Yes        |
|       fps       |                       滚动速度，单位 `pixels/second`                        |                 `Number`                 |    No    |   All    |        Yes        |
|     leading     |                    渲染后动画延迟的时间（以毫秒为单位）                     |                 `Number`                 |    No    |   All    |        Yes        |
|      loop       |                    字幕循环的次数, `true`或`0`表示无限次                    |           `Boolean` 或`Number`           |    No    |   All    |        Yes        |
|    onFinish     |          当字幕结束滚动时的回调。仅当`loop={false}`或`非零`时调用           |               `() => void`               |    No    |   All    |        Yes        |
| onCycleComplete | 当字幕完成循环时的回调。如果达到最大循环次数，则不会调用（改用 `onFinish`） |               `() => void`               |    No    |   All    |        Yes        |
|      play       |                             播放或暂停滚动字幕                              |                `Boolean`                 |    No    |   All    |        Yes        |
|     spacing     |               重复字幕之间的间距。仅当`autoFill={true}`时有效               |                 `Number`                 |    No    |   All    |        Yes        |
|      style      |                                  字幕样式                                   |               `TextStyle`                |    No    |   All    |        Yes        |
|    trailing     |             上一次循环后到下一次动画的延迟时间（以毫秒为单位）              |                 `Number`                 |    No    |   All    |        Yes        |
|    wrapStyle    |                           Marquee 组件外部 style                            |               `ViewStyle`                |    No    |   All    |        Yes        |

**SearchBar**：搜索栏组件，一般可位于 NavBar 下方，通过『取消按钮』退出激活状态。

|       Name       |                  Description                  |        Type         | Required | Platform | HarmonyOS Support |
| :--------------: | :-------------------------------------------: | :-----------------: | :------: | :------: | :---------------: |
|   defaultValue   |                搜索框的默认值                 |       String        |    No    |   All    |        Yes        |
|      value       |                搜索框的当前值                 |       String        |    No    |   All    |        Yes        |
|   placeholder    |                  placeholder                  |       String        |    No    |   All    |        Yes        |
|     onSubmit     |        submit 事件 (点击键盘的 enter)         | (val: string): void |    No    |   All    |        Yes        |
|     onChange     |               change 事件的回调               | (val: string): void |    No    |   All    |        Yes        |
|     onFocus      |               focus 事件的回调                |      (): void       |    No    |   All    |        Yes        |
|      onBlur      |                blur 事件的回调                |      (): void       |    No    |   All    |        Yes        |
|     onCancel     | 点击`取消`按钮触发 (不再自动清除输入框的文字) | (val: string): void |    No    |   All    |        Yes        |
| showCancelButton |            是否一直显示`取消`按钮             |        bool         |    No    |   All    |        Yes        |
|    cancelText    |             定制`取消`按钮的文字              |       String        |    No    |   All    |        Yes        |
|     disabled     |                   设置禁用                    |        bool         |    No    |   All    |        Yes        |

**TabBar**：标签栏组件，位于 APP 底部，方便用户在不同功能模块之间进行快速切换。

|        Name         |   Description    |  Type  | Required | Platform | HarmonyOS Support |
| :-----------------: | :--------------: | :----: | :------: | :------: | :---------------: |
|    barTintColor     |  tabbar 背景色   | String |    No    |   All    |        Yes        |
|      tintColor      |  选中的字体颜色  | String |    No    |   All    |        Yes        |
| unselectedTintColor | 未选中的字体颜色 | String |    No    |   All    |        Yes        |

**TabBar.Item**：TabBar 子组件。
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :----------: | :---------------------------------------------------: | :-------------: | :--------------: | :------: | :---------------: |
| badge | 徽标数 | Number \ String | No | All | Yes |
| onPress | bar 点击触发，需要自己改变组件 state & selecte={true} | Function | No | All | Yes |
| selected | 是否选中 | Boolean | No | All | Yes |
| icon | 默认展示图片 | `Image Source  | React.ReactNode` | No | All | Yes |
| selectedIcon | 选中后的展示图片 | `Image Source  | React.ReactNode` | No | All | Yes |
| title | 标题文字 | String | No | All | Yes |
| key | 唯一标识 | String | No | All | Yes |
| iconStyle | icon 样式 | String | No | All | Yes |

**Slider**：滑动输入条组件，允许用户在一个区间中选择特定值，eg：控制屏幕的显示亮度。

|     Name      |                                                                   Description                                                                    |                                                                 Type                                                                 | Required | Platform | HarmonyOS Support |
| :-----------: | :----------------------------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|      min      |                                                                      最小值                                                                      |                                                                Number                                                                |    No    |   All    |        Yes        |
|      max      |                                                                      最大值                                                                      |                                                                Number                                                                |    No    |   All    |        Yes        |
|     step      | 步长，取值必须大于 0，并且可被 (max - min) 整除。当 `marks` 不为空对象时，可以设置 `step` 为 `null`，此时 Slider 的可选值仅有 marks 标出来的部分 |                                                            Number or null                                                            |    No    |   All    |        Yes        |
|     ticks     |                                                                   是否显示刻度                                                                   |                                                              `boolean`                                                               |    No    |   All    |        Yes        |
|     range     |                                                                   是否为双滑块                                                                   |                                                              `boolean`                                                               |    No    |   All    |        Yes        |
|     icon      |                                                                    滑块的图标                                                                    |                                                             `ReactNode`                                                              |    No    |   All    |        Yes        |
|    styles     |                                                                 语义化结构 style                                                                 | [SliderStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/slider/index.zh-CN.md#sliderstyle-语义化样式) |    No    |   All    |        Yes        |
|     style     |                                                                  最外层容器样式                                                                  |                                                        `StyleProp<ViewStyle>`                                                        |    No    |   All    |        Yes        |
|     marks     |                                                                     刻度标记                                                                     |                                                 `{ [key: number]: React.ReactNode }`                                                 |    No    |   All    |        Yes        |
|     value     |                                                                  设置当前取值。                                                                  |                                                                Number                                                                |    No    |   All    |        Yes        |
| defaultValue  |                                                                  设置初始取值。                                                                  |                                                                Number                                                                |    No    |   All    |        Yes        |
|   disabled    |                                                                  滑块为禁用状态                                                                  |                                                               Boolean                                                                |    No    |   All    |        Yes        |
|   onChange    |                                    当 Slider 的值发生改变时，会触发 onChange 事件，并把改变后的值作为参数传入                                    |                                                               Function                                                               |    No    |   All    |        Yes        |
| onAfterChange |                                                与 `ontouchend` 触发时机一致，把当前值作为参数传入                                                |                                                               Function                                                               |    No    |   All    |        Yes        |

**Popover**：气泡组件，在点击控件或者某个区域后，浮出一个气泡菜单来做更多的操作。 如果设置了遮罩层，建议通过点击遮罩层的任一位置，进行退出。

|          Name          |                                    Description                                    |                                                            Type                                                             | Required | Platform | HarmonyOS Support |
| :--------------------: | :-------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|        overlay         |                                    弹出层内容                                     |                                                          ReactNode                                                          |    No    |   All    |        Yes        |
|       placement        |                                    弹出层位置                                     |                                          'top 或 right 或 bottom 或 left 或 auto'                                           |    No    |   All    |        Yes        |
|        onSelect        |                              选中某选项时的回调函数                               |                                                     (value: any): void                                                      |    No    |   All    |        Yes        |
|      triggerStyle      |                               触发元素外围容器样式                                |                                                          ViewStyle                                                          |    No    |   All    |        Yes        |
| renderOverlayComponent | 自定义弹出层的外围组件，默认是`ScrollView`，示例`(nodes) => <View>{nodes}</View>` |                                         (node: React.ReactNode) => React.ReactNode                                          |    No    |   All    |        Yes        |
|        duration        |                                     动画时长                                      |                                                           number                                                            |    No    |   All    |        Yes        |
|         easing         |                                     动画效果                                      | (show: boolean) => (value: number) => number 或 show => show ? Easing.out(Easing.back(1.70158)) : Easing.inOut(Easing.quad) |    No    |   All    |        Yes        |
|    useNativeDriver     |                            动画是否使用 Native Driver                             |                                                           boolean                                                           |    No    |   All    |        Yes        |
|       onDismiss        |                             Popover 关闭后的回调函数                              |                                                          function                                                           |    No    |   All    |        No         |

**Popover.Item**：气泡子组件。

|   Name   |     Description     |   Type    | Required | Platform | HarmonyOS Support |
| :------: | :-----------------: | :-------: | :------: | :------: | :---------------: |
| disabled |      是否禁用       |  Boolean  |    No    |   All    |        Yes        |
|  style   |      item 样式      | ViewStyle |    No    |   All    |        Yes        |
|  value   | 可作为选中的条目 ID |    any    |   Yes    |   All    |        Yes        |

**SwipeAction**：滑动操作组件。

|        Name         |         Description          |                                                                   Type                                                                   | Required | Platform | HarmonyOS Support |
| :-----------------: | :--------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|        left         |          左侧按钮组          |                                                                  Array                                                                   |   Yes    |   All    |        Yes        |
|        right        |          右侧按钮组          |                                                                  Array                                                                   |   Yes    |   All    |        Yes        |
|   onSwipeableOpen   |        打开时回调函数        |                                                                 (): void                                                                 |    No    |   All    |        Yes        |
|  onSwipeableClose   |        关闭时回调函数        |                                                                 (): void                                                                 |    No    |   All    |        Yes        |
|    closeOnAction    |    点击按钮后自动隐藏按钮    |                                                                `boolean`                                                                 |    No    |   All    |        Yes        |
| closeOnTouchOutside | 是否在点击其他区域时自动归位 |                                                                `boolean`                                                                 |    No    |   All    |        Yes        |
|       styles        |       语义化结构 style       | [SwipeActionStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/swipe-action-cn#swipeactionstyle-语义化样式) |    No    |   All    |        Yes        |

**SwipeAction.Button**：滑动操作组件内的 Button。

|       Name        |  Description   |                                                      Type                                                      | Required | Platform | HarmonyOS Support |
| :---------------: | :------------: | :------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|  backgroundColor  |     背景色     |                                                    `string`                                                    |    No    |   All    |        Yes        |
|     disabled      |    是否禁用    |                                                   `boolean`                                                    |    No    |   All    |        Yes        |
|       text        |    按钮文案    |                                                     String                                                     |    No    |   All    |        Yes        |
|       color       |    字体颜色    |                                                    `string`                                                    |    No    |   All    |        Yes        |
|       style       |    按钮样式    |                                                     Object                                                     |    No    |   All    |        Yes        |
|      onPress      |  按钮点击事件  |                                                    (): void                                                    |    No    |   All    |        Yes        |
| actionButtonProps | 其他额外 props | [RectButtonProps](https://docs.swmansion.com/react-native-gesture-handler/docs/components/buttons/#rectbutton) |    No    |   All    |        Yes        |

**Collapse**：折叠面板组件， 可以折叠/展开的内容区域。

|       Name       |                          Description                          |                                                                                                                        Type                                                                                                                        | Required | Platform | HarmonyOS Support |
| :--------------: | :-----------------------------------------------------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|    accordion     |                      是否开启手风琴模式                       |                                                                                                                     `Boolean`                                                                                                                      |    No    |   All    |        Yes        |
|    activeKey     |                     当前展开面板的 `key`                      |                                                                                                                手风琴模式：`string`                                                                                                                |    No    |   All    |        Yes        |
|    arrowIcon     | 自定义箭头图标， 如果是 ReactNode，会自动为你增加旋转动画效果 |                                                                                                                    `ReactNode`                                                                                                                     |    No    |   All    |        Yes        |
| defaultActiveKey |                     默认展开面板的 `key`                      |                                                                                                                手风琴模式：`string`                                                                                                                |    No    |   All    |        Yes        |
|     onChange     |                        切换面板时触发                         |                                                                                                         手风琴模式：`(activeKey: string)`                                                                                                          |    No    |   All    |        Yes        |
|      styles      |                       语义化结构 style                        | 同 [ListStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/list-cn#liststyle-语义化样式) & [ListItemStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/list-cn#listitemstyle-语义化样式) |    No    |   All    |        Yes        |

**Collapse.Panel**：折叠面板子组件。

|      Name      |         Description         |                                                             Type                                                              | Required | Platform | HarmonyOS Support |
| :------------: | :-------------------------: | :---------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|   arrowIcon    |       自定义箭头图标        |                                                          `ReactNode`                                                          |    No    |   All    |        Yes        |
| destroyOnClose | 不可见时是否销毁 `DOM` 结构 |                                                           `Boolean`                                                           |    No    |   All    |        Yes        |
|    disabled    |       是否为禁用状态        |                                                           `Boolean`                                                           |    No    |   All    |        Yes        |
|  forceRender   | 被隐藏时是否渲染 `DOM` 结构 |                                                           `Boolean`                                                           |    No    |   All    |        Yes        |
|      key       |         唯一标识符          |                                                           `String`                                                            |    No    |   All    |        Yes        |
|    onPress     |      标题栏的点击事件       |                                           `(event: GestureResponderEvent) => void`                                            |    No    |   All    |        Yes        |
|     styles     |      语义化结构 style       | 同 [ListItemStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/list-cn#listitemstyle-语义化样式) |    No    |   All    |        Yes        |
|     title      |       标题栏左侧内容        |                                                          `ReactNode`                                                          |    No    |   All    |        Yes        |

**Input**：文本输入组件，通过键盘输入内容，是最基础的表单域包装。

|     Name     |                                               Description                                               |                                                               Type                                                                | Required | Platform | HarmonyOS Support |
| :----------: | :-----------------------------------------------------------------------------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|  allowClear  |                                        可以点击清除图标删除内容                                         |                                                             `boolean`                                                             |    No    |   All    |        Yes        |
| defaultValue |                                             输入框默认内容                                              |                                                              string                                                               |    No    |   All    |        Yes        |
|   disabled   |                                       是否禁用状态，默认为 false                                        |                                                              boolean                                                              |    No    |   All    |        Yes        |
|  maxLength   |                                                最大长度                                                 |                                                              number                                                               |    No    |   All    |        Yes        |
|    prefix    |                                          带有前缀图标的 input                                           |                                                             ReactNode                                                             |    No    |   All    |        Yes        |
|  showCount   |                                              是否展示字数                                               |                                                             `boolean`                                                             |    No    |   All    |        Yes        |
|    status    |                                              设置校验状态                                               |                                                       'error' \| 'warning'                                                        |    No    |   All    |        Yes        |
|  inputStyle  |                                             TextInput style                                             |                                                      `StyleProp<TextStyle>`                                                       |    No    |   All    |        Yes        |
|    style     |                                           容器(container)样式                                           |                                                      `StyleProp<ViewStyle>`                                                       |    No    |   All    |        Yes        |
|    styles    |                                            语义化结构 style                                             | [InputStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/input/index.zh-CN.md#inputstyle-语义化样式) |    No    |   All    |        Yes        |
|    suffix    |                                          带有后缀图标的 input                                           |                                                             ReactNode                                                             |    No    |   All    |        Yes        |
|     type     | 声明 Input 类型，同原生 [`keyboardType`](https://reactnative.dev/docs/textinput.html#keyboardtype) 属性 |                                      'text' \| 'number' \|'password' \| KeyboardTypeOptions                                       |    No    |   All    |        Yes        |
|    value     |                                               输入框内容                                                |                                                              string                                                               |    No    |   All    |        Yes        |
|   onChange   |                         输入框内容变化时的回调，额外支持`e.target.value`的返回                          |                                  `(e: NativeSyntheticEvent<TextInputChangeEventData>) => void;`                                   |    No    |   All    |        Yes        |

**Input.TextArea**

同 `Input` 属性，外加：

|   Name   |            Description            |                                                               Type                                                                | Required | Platform | HarmonyOS Support |
| :------: | :-------------------------------: | :-------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
| autoSize |  自适应内容高度，可设置为 `true`  |                                           `false` 或对象：`{ minRows: 2, maxRows: 6 }`                                            |    No    |   All    |        Yes        |
|   rows   | 固定显示几行，`autoSize` 优先级高 |                                                              number                                                               |    No    |   All    |        Yes        |
|  styles  |         语义化结构 style          | [InputStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/input/index.zh-CN.md#inputstyle-语义化样式) |    No    |   All    |        Yes        |

**Form**

表单组件，高性能表单控件，自带数据域管理。包含数据录入、校验以及对应样式。

|       Name       |                                                               Description                                                               |                                                                      Type                                                                      |  Required  | Platform | HarmonyOS Support |
| :--------------: | :-------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------------------------------------------------------------------------------------------------: | :--------: | :------: | :---------------: |
|     disabled     |                                     设置表单组件禁用，仅对 `@ant-design/react-native` 内置组件有效                                      |                                                                    boolean                                                                     |     No     |   All    |        Yes        |
|    component     |                                         设置 Form 渲染元素，为 `false` 则不创建 ReactNode 节点                                          |                                                                     number                                                                     |     No     |   All    |        Yes        |
|      fields      |                                      通过状态管理（如 redux）控制表单字段，如非强需求不推荐使用。                                       |             [ FieldData](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#fielddata)[]             |     No     |   All    |        Yes        |
|       form       |                                      经 `Form.useForm()` 创建的 form 控制实例，不提供时会自动创建                                       |           [FormInstance](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#forminstance)            |     No     |   All    |        Yes        |
|  feedbackIcons   |                                          当 `Form.Item` 有 `hasFeedback` 属性时可以自定义图标                                           |          [FeedbackIcons](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#feedbackicons)           |     No     |   All    |        Yes        |
|  initialValues   |                                                  表单默认值，只有初始化以及重置时生效                                                   |                                                                     object                                                                     |     No     |   All    |        Yes        |
|    labelStyle    |                                                            label 标签的样式                                                             |                                                                   `ViewStyle                                                                   | TextStyle` |    No    |        All        | Yes |
|      layout      |                                                                表单布局                                                                 |                                                                  `horizontal`                                                                  |     No     |   All    |        Yes        |
|       name       |                                                 表单名称，会作为表单字段 `id` 前缀使用                                                  |                                                                     string                                                                     |     No     |   All    |        Yes        |
|     preserve     |                              当字段被删除时保留字段值。你可以通过 `getFieldsValue(true)` 来获取保留字段值                               |                                                                    boolean                                                                     |     No     |   All    |        Yes        |
|   requiredMark   |                            必选样式，可以切换为必选或者可选展示样式。此为 Form 配置，Form.Item 无法单独配置                             |                            boolean \| `optional` \| ((label: ReactNode, info: { required: boolean }) => ReactNode)                             |     No     |   All    |        Yes        |
| validateMessages | 验证提示模板，说明[见下](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#validatemessages) | [ValidateMessages](https://github.com/ant-design/ant-design/blob/6234509d18bac1ac60fbb3f92a5b2c6a6361295a/components/locale/en_US.ts#L88-L134) |     No     |   All    |        Yes        |
| validateTrigger  |                                                       统一设置字段触发验证的时机                                                        |                                                               string \| string[]                                                               |     No     |   All    |        Yes        |
|   wrapperStyle   |                                       需要为输入控件设置布局样式时，使用该属性，用法同 labelStyle                                       |                                                                  `ViewStyle`                                                                   |     No     |   All    |        Yes        |
|  onFieldsChange  |                                                         字段更新时触发回调事件                                                          |                                                       function(changedFields, allFields)                                                       |     No     |   All    |        Yes        |
|     onFinish     |                                                    提交表单且数据验证成功后回调事件                                                     |                                                                function(values)                                                                |     No     |   All    |        Yes        |
|  onFinishFailed  |                                                    提交表单且数据验证失败后回调事件                                                     |                                                  function({ values, errorFields, outOfDate })                                                  |     No     |   All    |        Yes        |
|  onValuesChange  |                                                        字段值更新时触发回调事件                                                         |                                                       function(changedValues, allValues)                                                       |     No     |   All    |        Yes        |
|      styles      |                                                            语义化结构 style                                                             |             同 [ListStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/list-cn#liststyle-语义化样式)              |     No     |   All    |        Yes        |

**Form.Item**

|       Name        |                                                                                Description                                                                                 |                                                                                                                                            Type                                                                                                                                             | Required | Platform | HarmonyOS Support |
| :---------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|   dependencies    |                    设置依赖字段，说明[见下](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#dependencies)                     |                                                                                     [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath)[]                                                                                     |    No    |   All    |        Yes        |
| getValueFromEvent |                                                                     设置如何将 event 的值转换成字段值                                                                      |                                                                                                                                   (..args: any[]) => any                                                                                                                                    |    No    |   All    |        Yes        |
|   getValueProps   |                                       为子元素添加额外的属性 (不建议通过 `getValueProps` 生成动态函数 prop，请直接将其传递给子组件)                                        |                                                                                                                             (value: any) => Record<string, any>                                                                                                                             |    No    |   All    |        Yes        |
|    hasFeedback    |                          配合 `validateStatus` 属性使用，展示校验状态图标，建议只配合 Input 组件使用 此外，它还可以通过 Icons 属性获取反馈图标。                           |                                                                      boolean \| { icons: [FeedbackIcons](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#feedbackicons) }                                                                      |    No    |   All    |        Yes        |
|       help        |                                                                提示信息，如不设置，则会根据校验规则自动生成                                                                |                                                                                                                                           boolean                                                                                                                                           |    No    |   All    |        Yes        |
|      hidden       |                                                                    是否隐藏字段（依然会收集和校验字段）                                                                    |                                                                                                                                           boolean                                                                                                                                           |    No    |   All    |        Yes        |
|   initialValue    |                                                    设置子元素默认值，如果与 Form 的 `initialValues` 冲突则以 Form 为准                                                     |                                                                                                                                           string                                                                                                                                            |    No    |   All    |        Yes        |
|       label       |                                                                             `label` 标签的文本                                                                             |                                                                                                                                          ReactNode                                                                                                                                          |    No    |   All    |        Yes        |
|    labelStyle     |                          label 标签的样式。你可以通过 Form 的 `labelStyle` 进行统一设置，不会作用于嵌套 Item。当和 Form 同时设置时，以 Item 为准                           |                                                                                                                                              -                                                                                                                                              |    No    |   All    |        Yes        |
| messageVariables  |                                                                             默认验证字段的信息                                                                             |                                                                                                                                   Record<string, string>                                                                                                                                    |    No    |   All    |        Yes        |
|       name        |                                                                              字段名，支持数组                                                                              |                                                                                      [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath)                                                                                      |    No    |   All    |        Yes        |
|     normalize     |                                                              组件获取值后进行转换，再放入 Form 中。不支持异步                                                              |                                                                                                                            (value, prevValue, prevValues) => any                                                                                                                            |    No    |   All    |        Yes        |
|      noStyle      |             为 `true` 时不带样式，作为纯字段控件使用。当自身没有 `validateStatus` 而父元素存在有 `validateStatus` 的 Form.Item 会继承父元素的 `validateStatus`             |                                                                                                                                           boolean                                                                                                                                           |    No    |   All    |        Yes        |
|     preserve      |                                                                          当字段被删除时保留字段值                                                                          |                                                                                                                                           boolean                                                                                                                                           |    No    |   All    |        Yes        |
|     required      |                                                              必填样式设置。如不设置，则会根据校验规则自动生成                                                              |                                                                                                                                           boolean                                                                                                                                           |    No    |   All    |        Yes        |
|       rules       |                             校验规则，设置字段的校验逻辑。点击[此处](https://ant.design/components/form-cn#components-form-demo-basic)查看示例                             |                                                                                         [Rule](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#rule)[]                                                                                         |    No    |   All    |        Yes        |
|   shouldUpdate    |                 自定义字段更新逻辑，说明[见下](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#shouldupdate)                  |                                                                                                                         boolean \| (prevValue, curValue) => boolean                                                                                                                         |    No    |   All    |        Yes        |
|      styles       |                                                                              语义化结构 style                                                                              | [FormItemStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#formitemstyle-语义化样式) & [ValidateStatusStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#validatestatusstyle-语义化样式) |    No    |   All    |        Yes        |
|      trigger      |                     设置收集字段值变更的时机。点击[此处](https://ant.design/components/form-cn#components-form-demo-customized-form-controls)查看示例                      |                                                                                                                                           string                                                                                                                                            |    No    |   All    |        Yes        |
|   validateFirst   |                                               当某一规则校验不通过时，是否停止剩下的规则的校验。设置 `parallel` 时会并行校验                                               |                                                                                                                                     boolean 或 parallel                                                                                                                                     |    No    |   All    |        Yes        |
| validateDebounce  |                                                                       设置防抖，延迟毫秒数后进行校验                                                                       |                                                                                                                                           number                                                                                                                                            |    No    |   All    |        Yes        |
|  validateStatus   |                                        校验状态，如不设置，则会根据校验规则自动生成，可选：'success' 'warning' 'error' 'validating'                                        |                                                                                                                                           string                                                                                                                                            |    No    |   All    |        Yes        |
|  validateTrigger  |                                                                             设置字段校验的时机                                                                             |                                                                                                                                     string \| string[]                                                                                                                                      |    No    |   All    |        Yes        |
|   valuePropName   | 子节点的值的属性。注意：Switch、Checkbox 的 valuePropName 应该是 `checked`，否则无法获取这个两个组件的值。该属性为 `getValueProps` 的封装，自定义 `getValueProps` 后会失效 |                                                                                                                                           string                                                                                                                                            |    No    |   All    |        Yes        |
|   wrapperStyle    |    需要为输入控件设置布局样式时，使用该属性，用法同 `labelStyle`。你可以通过 Form 的 `wrapperCol` 进行统一设置，不会作用于嵌套 Item。当和 Form 同时设置时，以 Item 为准    |                                                                                                                                         `ViewStyle`                                                                                                                                         |    No    |   All    |        Yes        |

**Form.List**

|     Name     |                                                                                                           Description                                                                                                            |                                                       Type                                                        | Required | Platform | HarmonyOS Support |
| :----------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|   children   |                                                                                                             渲染函数                                                                                                             |             (fields: Field[], operation: { add, remove, move }, meta: { errors }) => React.ReactNode              |   Yes    |   All    |        Yes        |
| initialValue |                                                                               设置子元素默认值，如果与 Form 的 `initialValues` 冲突则以 Form 为准                                                                                |                                                       any[]                                                       |    No    |   All    |        Yes        |
|     name     | 字段名，支持数组。List 本身也是字段，因而 `getFieldsValue()` 默认会返回 List 下所有值，你可以通过[参数](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#getfieldsvalue)改变这一行为 | [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath) |    No    |   All    |        Yes        |
|    rules     |                             校验规则，仅支持自定义规则。需要配合 [ErrorList](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#formerrorlist) 一同使用。                              |                                             { validator, message }[]                                              |    No    |   All    |        Yes        |

**Form.ErrorList**

|  Name  |   Description    |                                                                        Type                                                                        | Required | Platform | HarmonyOS Support |
| :----: | :--------------: | :------------------------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
| errors |     错误列表     |                                                                    ReactNode[]                                                                     |    No    |   All    |        Yes        |
| styles | 语义化结构 style | [ValidateStatusStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#validatestatusstyle-语义化样式) |    No    |   All    |        Yes        |

**Form.Provider**

|     Name     |     Description      |                            Type                            | Required | Platform | HarmonyOS Support |
| :----------: | :------------------: | :--------------------------------------------------------: | :------: | :------: | :---------------: |
| onFormChange | 子表单字段更新时触发 | function(formName: string, info: { changedFields, forms }) |    No    |   All    |        Yes        |
| onFormFinish |   子表单提交时触发   |    function(formName: string, info: { values, forms })     |    No    |   All    |        Yes        |

**FormInstance**

|       Name        |                                                                                  Description                                                                                   |                                                                                                                                        Type                                                                                                                                         | Required | Platform | HarmonyOS Support |
| :---------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|   getFieldError   |                                                                            获取对应字段名的错误信息                                                                            |                                                                        (name: [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath)) => string[]                                                                        |    No    |   All    |        Yes        |
|  getFieldsError   |                                                                  获取一组字段名对应的错误信息，返回为数组形式                                                                  |                                                                  (nameList?: [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath)[]) => FieldError[]                                                                   |    No    |   All    |        Yes        |
| getFieldInstance  |                                                                                获取对应字段实例                                                                                |                                                                          (name: [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath)) => any                                                                           |    No    |   All    |        Yes        |
|  getFieldsValue   |                                   获取一组字段名对应的值，会按照对应结构返回。默认返回现存字段值，当调用 `getFieldsValue(true)` 时返回所有值                                   |                                                                            [GetFieldsValue](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#getfieldsvalue)                                                                            |    No    |   All    |        Yes        |
|   getFieldValue   |                                                                               获取对应字段名的值                                                                               |                                                                          (name: [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath)) => any                                                                           |    No    |   All    |        Yes        |
|  isFieldsTouched  |                                               检查一组字段是否被用户操作过，`allTouched` 为 `true` 时检查是否所有字段都被操作过                                                |                                                          (nameList?: [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath)[], allTouched?: boolean) => boolean                                                          |    No    |   All    |        Yes        |
|  isFieldTouched   |                                                                          检查对应字段是否被用户操作过                                                                          |                                                                        (name: [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath)) => boolean                                                                         |    No    |   All    |        Yes        |
| isFieldValidating |                                                                            检查对应字段是否正在校验                                                                            |                                                                        (name: [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath)) => boolean                                                                         |    No    |   All    |        Yes        |
|    resetFields    |                                                                         重置一组字段到 `initialValues`                                                                         |                                                                       (fields?: [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath)[]) => void                                                                        |    No    |   All    |        Yes        |
|   setFieldValue   |                                   设置表单的值（该值将直接传入 form store 中并且**重置错误信息**。如果你不希望传入对象被修改，请克隆后传入）                                   |                                                                    (name: [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath), value: any) => void                                                                    |    No    |   All    |        Yes        |
|  setFieldsValue   | 设置表单的值（该值将直接传入 form store 中并且**重置错误信息**。如果你不希望传入对象被修改，请克隆后传入）。如果你只想修改 Form.List 中单项值，请通过 `setFieldValue` 进行指定 |                                                                                                                                  (values) => void                                                                                                                                   |    No    |   All    |        Yes        |
|      submit       |                                                                     提交表单，与点击 `submit` 按钮效果相同                                                                     |                                                                                                                                     () => void                                                                                                                                      |    No    |   All    |        Yes        |
|  validateFields   |                                                           触发表单验证，设置 `recursive` 时会递归校验所有包含的路径                                                            | (nameList?: [NamePath](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#namepath)[], config?: [ValidateConfig](https://github.com/ant-design/ant-design-mobile-rn/blob/5.2.2/components/form/index.zh-CN.md#validateFields)) => Promise |    No    |   All    |        Yes        |

**Tooltip**：气泡组件，在点击控件或者某个区域后，浮出一个气泡菜单来做更多的操作。

|      Name       |         Description          |                                                  Type                                                   | Required | Platform | HarmonyOS Support |
| :-------------: | :--------------------------: | :-----------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|    children     |    触发 `Tooltip` 的元素     |                                          `React.ReactElement`                                           |   Yes    |   All    |        Yes        |
|     content     |           弹出内容           |                                            `React.ReactNode`                                            |    No    |   All    |        Yes        |
| defaultVisible  |         默认是否显隐         |                                                `boolean`                                                |    No    |   All    |        Yes        |
|      mode       |   设置亮色模式或者黑色模式   |                                                `'light'`                                                |    No    |   All    |        Yes        |
| onVisibleChange |        显示隐藏的回调        |                                      `(visible: boolean) => void`                                       |    No    |   All    |        Yes        |
|    placement    |          气泡框位置          |                                                 `'top'`                                                 |    No    |   All    |        Yes        |
|     styles      |       语义化结构 style       | [TooltipStyle](https://github.com/ant-design/ant-design-mobile-rn/blob/master/#tooltipstyle-语义化样式) |    No    |   All    |        Yes        |
|     trigger     |           触发方式           |                                               `'onPress'`                                               |    No    |   All    |        Yes        |
|     visible     | 受控模式下，是否展示弹出内容 |                                                `boolean`                                                |    No    |   All    |        Yes        |

**Tooltip.Menu**

|   Name   |             Description              |           Type           | Required | Platform | HarmonyOS Support |
| :------: | :----------------------------------: | :----------------------: | :------: | :------: | :---------------: |
| actions  | 菜单列表，当弹出内容为标准菜单时使用 |        `Action[]`        |   Yes    |   All    |        Yes        |
| maxCount | 菜单列表最大个数，超出则隐藏进行滚动 |         `number`         |    No    |   All    |        Yes        |
| onAction |   当使用菜单列表时，选中菜单的回调   | `(item: Action) => void` |    No    |   All    |        Yes        |

**Tooltip.Menu.Action**

|   Name   |             Description              |     Type     | Required | Platform | HarmonyOS Support |
| :------: | :----------------------------------: | :----------: | :------: | :------: | :---------------: |
| disabled |               是否禁用               |  `boolean`   |    No    |   All    |        Yes        |
|   icon   |             菜单项的图标             | `ReactNode`  |    No    |   All    |        Yes        |
|   key    |  菜单的唯一标识, 缺省时即为 `index`  |   `string`   |    No    |   All    |        Yes        |
| onPress  |              点击时触发              | `() => void` |    No    |   All    |        Yes        |
|   text   | 菜单列表，当弹出内容为标准菜单时使用 | `ReactNode`  |    No    |   All    |        Yes        |

## 遗留问题

- [ ] PickerView 组件在 harmony 暂不支持，待ArkUI规格升级之后再重新适配
- [ ] Input.TextArea 组件在 harmony 暂不支持，待ArkUI规格升级之后再重新适配

## 其他

- Drawer 组件暂时无法支持，与 Android/IOS 一致[issue#1352](https://github.com/ant-design/ant-design-mobile-rn/issues/1352)、[issue#1338](https://github.com/ant-design/ant-design-mobile-rn/issues/1338)。
- Tooltip 组件气泡位置异常展示，与 Android/IOS 一致[issue#1376](https://github.com/ant-design/ant-design-mobile-rn/issues/1376)。
- Radio 组件的 defaultCheck 属性无法正常生效，与 Android/IOS 一致[issue#1380](https://github.com/ant-design/ant-design-mobile-rn/issues/1380)。
- Picker 组件的 defaultValue 属性无法正常生效，与 Android/IOS 一致[issue#1381](https://github.com/ant-design/ant-design-mobile-rn/issues/1381)。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ant-design/ant-design-mobile-rn/blob/master/LICENSE)，请自由地享受和参与开源。

