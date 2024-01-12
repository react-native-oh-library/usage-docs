> 模板版本：v0.1.2

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

```bash
yarn add @react-navigation/native@6.1.9
```

#### **npm**

```bash
npm install @react-navigation/native@6.1.9
```

<!-- tabs:end -->

## 兼容性

在下述版本验证通过：

1. DevEco Studio: 4.0.3.700; SDK: OpenHarmony(API10) 4.0.10.15; 测试设备: Mate 40 Pro(NOH-AN00); ROM: 4.0.0.66(SP3C00E73R1P14log); RNOH: 0.72.10
2. DevEco Studio: 4.1.3.313; SDK: OpenHarmony(API11) 4.1.0.52; 测试设备: Mate 40 Pro(NOH-AN00); ROM: 2.0.0.51(SP22C00E52R1P17log); RNOH: 0.72.11
3. DevEco Studio: 4.1.3.313; SDK: OpenHarmony(API11) 4.1.0.52; 测试设备: Mate 40 Pro(NOH-AN00); ROM: 2.0.0.52(SP22C00E52R1P17log); RNOH: 0.72.11

## 属性

以下属性已验证，更多属性详情请查看 [react-navigation/native 的文档介绍](https://reactnavigation.org/docs/navigation-container)

**NavigationContainer**：

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| theme | 主题 | Theme | no      | All      | yes      |
| independent | 此导航容器是否应独立于父容器 | boolean | no      | All      | yes      |
| documentTitle | 文档标题 | function | no      | All      | yes      |


**NavigationHelpersContext.Provider**：navigation提供者，用于保存导航器

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/native/LICENSE) ，请自由地享受和参与开源。