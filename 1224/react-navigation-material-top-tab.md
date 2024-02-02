> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>@react-navigation/material-top-tabs</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/material-top-tabs">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/bottom-tabs/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->
#### **npm**

```bash
npm install @react-navigation/material-top-tabs@6.5.11
```

#### **yarn**

```bash
yarn add @react-navigation/material-top-tabs@6.6.5
```

<!-- tabs:end -->

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## 方法

| Name                            | Description              | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------- | ------------------------ | -------- | -------- | -------- | ----------------- |
| `createMaterialTopTabNavigator` | 创建 MaterialTopTab 组件 | function | no       | All      | yes               |

## 属性

以下属性已验证，更多属性详情请查看 [react-navigation/material-top-tab-navigator的文档介绍](https://reactnavigation.org/docs/material-top-tab-navigator/)

**Tab.Navigator**:

| Name                | Description                                                  | Type       | Required | Platform | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | ---------- | -------- | -------- | ----------------- |
| initialRouteName    | 第一次加载导航器时要渲染的路线的名称                         | string     | no       | All      | yes               |
| backBehavior        | 控制在导航器中调用 goBack 时发生的情况                       | string     | no       | All      | yes               |
| tabBar              | 返回一个 React 元素以显示为选项卡栏的函数。                  | function   | no       | All      | yes               |
| tabBarPosition      | 选项卡视图中选项卡栏的位置。可能的值为`'top'`和`'bottom'`。默认为`'top'` | string     | no       | All      | yes               |
| sceneContainerStyle | 包装屏幕内容的组件的样式对象                                 | ViewStyle  | no       | All      | yes               |
| screenOptions       | 用于导航器中屏幕的默认选项                                   | 自定义类型 | no       | All      | yes               |

**screenOptions**：

| Name                                         | Description                                                  | Type              | Required | Platform | HarmonyOS Support |
| -------------------------------------------- | ------------------------------------------------------------ | ----------------- | -------- | -------- | ----------------- |
| title                                        | 可用作 和 的后备的通用`headerTitle`标题`tabBarLabel`。       | string            | no       | All      | yes               |
| tabBarLabel                                  | 选项卡栏中显示的选项卡的标题字符串或给定对象返回 React.Node 的函数 | string\|Rect.Node | no       | All      | yes               |
| tabBarShowLabel                              | 选项卡标签是否可见。默认为`true`.                            | boolean           | no       | All      | yes               |
| tabBarIcon                                   | 给定的函数对象返回一个 React.Node，以显示在选项卡栏中。      | Rect.Node         | no       | All      | yes               |
| tabBarShowIcon                               | 选项卡图标是否可见。默认为`false`.                           | boolean           | no       | All      | yes               |
| tabBarBadge                                  | 返回一个 React 元素用作选项卡徽章的函数                      | Rect.Node         | no       | All      | yes               |
| tabBarIndicator                              | 返回 React 元素作为选项卡栏指示器的函数。                    | Rect.Node         | no       | All      | yes               |
| tabBarIndicatorStyle                         | 选项卡栏指示器的样式对象。                                   | Style             | no       | All      | yes               |
| tabBarIndicatorContainerStyle                | 包含选项卡栏指示器的视图的样式对象。                         | Style             | no       | All      | yes               |
| tabBarActiveTintColor                        | 活动选项卡中图标和标签的颜色。                               | string            | no       | All      | yes               |
| tabBarActiveTintColortabBarInactiveTintColor | 活动选项卡中图标和标签的颜色。非活动选项卡中图标和标签的颜色。 | string            | no       | All      | yes               |
| tabBarGap                                    | 选项卡栏中选项卡项目之间的间距。                             | number            | no       | All      | yes               |
| tabBarPressOpacity                           | 按下的选项卡的不透明度。                                     | number            | no       | All      | yes               |
| tabBarScrollEnabled                          | 布尔值，指示是否使选项卡栏可滚动。                           | boolean           | no       | All      | yes               |
| tabBarIconStyle                              | 选项卡图标容器的样式对象。                                   | Style             | no       | All      | yes               |
| tabBarLabelStyle                             | 选项卡标签的样式对象。                                       | Style             | no       | All      | yes               |
| tabBarStyle                                  | 选项卡栏的样式对象。                                         | Style             | no       | All      | yes               |
| swipeEnabled                                 | 布尔值，指示是否启用滑动手势。                               | boolean           | no       | All      | yes               |
| lazy                                         | 该屏幕是否应该延迟渲染。                                     | boolean           | no       | All      | yes               |
| lazyPreloadDistance                          | 此属性指定应提前预加载多少个相邻屏幕                         | number            | no       | All      | yes               |
| lazyPlaceholder                              | 如果此屏幕尚未渲染，则返回要渲染的 React 元素的函数。        | Rect.Node         | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/material-bottom-tabs/LICENSE) ，请自由地享受和参与开源。
