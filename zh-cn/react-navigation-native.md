> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>@react-navigation/native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/native">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/native/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-navigation/native@6.1.9
```

#### **yarn**

```bash
yarn add @react-navigation/native@6.1.9
```

<!-- tabs:end -->

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## 属性

以下属性已验证，更多属性详情请查看 [react-navigation/native 的文档介绍](https://reactnavigation.org/docs/navigation-container)

**NavigationContainer**：

| Name          | Description                  | Type     | Required | Platform | HarmonyOS Support |
| ------------- | ---------------------------- | -------- | -------- | -------- | ----------------- |
| theme         | 主题                         | Theme    | no       | All      | yes               |
| independent   | 此导航容器是否应独立于父容器 | boolean  | no       | All      | yes               |
| documentTitle | 文档标题                     | function | no       | All      | yes               |

**NavigationHelpersContext.Provider**：navigation 提供者，用于保存导航器

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/native/LICENSE) ，请自由地享受和参与开源。
