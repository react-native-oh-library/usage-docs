<!-- {% raw %} -->
> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>@react-navigation/bottom-tabs</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/bottom-tabs">
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
npm install @react-navigation/bottom-tabs@6.5.11
```

#### **yarn**

```bash
yarn add @react-navigation/bottom-tabs@6.5.11
```

<!-- tabs:end -->

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## 方法

| Name                       | Description          | Type     | Required | Platform | HarmonyOS Support |
| -------------------------- | -------------------- | -------- | -------- | -------- | ----------------- |
| `createBottomTabNavigator` | 创建 BottomTabs 组件 | function | no       | All      | yes               |

## 属性

以下属性已验证，更多属性详情请查看 [react-navigation/bottom-tabs 的文档介绍](https://reactnavigation.org/docs/bottom-tab-navigator)

**Navigator**：

| Name                | Description                               | Type       | Required | Platform | HarmonyOS Support |
| ------------------- | ----------------------------------------- | ---------- | -------- | -------- | ----------------- |
| initialRouteName    | 第一次加载导航器时要渲染的路线的名称      | string     | no       | All      | yes               |
| backBehavior        | 控制在导航器中调用 goBack 时发生的情况    | string     | no       | All      | yes               |
| tabBar              | 函数，返回一个 React 元素用来显示选项卡栏 | function   | no       | All      | yes               |
| sceneContainerStyle | 包装屏幕内容的组件的样式对象              | ViewStyle  | no       | All      | yes               |
| screenOptions       | 用于导航器中屏幕的默认选项                | 自定义类型 | no       | All      | yes               |

**Screen**：

| Name    | Description                            | Type       | Required | Platform | HarmonyOS Support |
| ------- | -------------------------------------- | ---------- | -------- | -------- | ----------------- |
| name    | 屏幕显示的 自定义类型名称              | string     | no       | All      | yes               |
| options | 用于配置如何在导航器中显示屏幕的选项。 | 自定义类型 | no       | All      | yes               |

**BottomTabBarHeightCallBackContext.Provider**：标签栏高度回调函数提供者

**BottomTabBarHeightContext.Provider**：标签栏高度提供者

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/bottom-tabs/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->