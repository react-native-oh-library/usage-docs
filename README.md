# 简介

> 欢迎开始React-Native的旅程！如果你在找如何搭建环境的文档，请移步开发文档的[搭建开发环境](https://react-native-oh-library.gitee.io/docs/#/zh-cn/environment)章节。

## 概述

该文档旨在帮助开发者在 OpenHarmony 平台使用 React Native OpenHarmony 的第三方库，并呈现每个三方库的信息。

## RNOH 三方库总览

>[!tip] NPM 公仓坐标：@react-native-oh-tpl

>[!tip] NPM Github Packages 私仓坐标：@react-native-oh-library

| 序号 | 原库名 | 原库基线版本 | 原库是否支持新架构 | 鸿蒙化进度 | Releases | 文档链接 |
| :--: | :----: | :----------: | :----------------: | :--------: | :------: | :------: |
|  1  | [@react-native-async-storage/async-storage](https://github.com/react-native-async-storage/async-storage) |    1.19.5     | 是 | 100% | [@react-native-oh-library/async-storage](https://github.com/react-native-oh-library/async-storage/releases) | [链接](zh-cn/async-storage.md) |
|  2  | [@react-native-clipboard/clipboard](https://github.com/react-native-clipboard/clipboard) |     1.12.1     | 是 | 80% | [@react-native-oh-library/clipboard](https://github.com/react-native-oh-library/clipboard/releases) | [链接](zh-cn/clipboard.md) |
| 3 | [@react-native-community/datetimepicker](https://github.com/react-native-datetimepicker/datetimepicker) | x | x | x | [@react-native-oh-tpl/datetimepicker](https://github.com/react-native-oh-library/datetimepicker) | [链接](zh-cn/datetimepicker.md) |
| 4 | [@shopify/flash-list](https://github.com/Shopify/flash-list) | 1.6.3 | 否 | 80% | [@react-native-oh-tpl/flash-list](https://github.com/react-native-oh-library/flash-list/tree/harmony) | [链接](zh-cn/flash-list.md) |
| 5 | [lottie-react-native](https://github.com/lottie-react-native/lottie-react-native) | 6.4.1 | 是 | 50% | [@react-native-oh-tpl/lottie-react-native](https://github.com/react-native-oh-library/lottie-react-native/releases) | [链接](zh-cn/lottie-react-native.md) |
|  6  | [@react-native-picker/picker](https://github.com/react-native-picker/picker) |     2.5.1     | 否 | 90% | [@react-native-oh-library/picker](https://github.com/react-native-oh-library/picker/releases) | [链接](zh-cn/picker.md) |
|  7  | [@react-native-community/progress-bar-android](https://github.com/react-native-progress-view/progress-bar-android) |     1.0.4     | 是 | 90% | [@react-native-oh-library/progress-bar-android](https://github.com/react-native-oh-library/progress-bar-android/releases) | [链接](zh-cn/progress-bar-android.md) |
|  8  | [@react-native-community/checkbox](https://github.com/react-native-checkbox/react-native-checkbox) |    0.5.16     | 否 | 100% | [@react-native-oh-library/checkbox](https://github.com/react-native-oh-library/react-native-checkbox/releases) | [链接](zh-cn/react-native-checkbox.md) |
| 9 | [react-native-exception-handler](https://github.com/a7ul/react-native-exception-handler) | 2.10.10 | 否 | 100% | [@react-native-oh-tpl/react-native-exception-handler](https://github.com/react-native-oh-library/react-native-exception-handler/releases) | [链接](zh-cn/react-native-exception-handler.md) |
| 10 | [react-native-fast-image](https://github.com/DylanVann/react-native-fast-image) | 8.6.3 | 否 | 70% | [@react-native-oh-tpl/react-native-fast-image](https://github.com/react-native-oh-library/react-native-fast-image/releases) | [链接](zh-cn/react-native-fast-image.md) |
| 11 | [react-native-gesture-handler](https://github.com/software-mansion/react-native-gesture-handler) | 2.12.1 | 是 | 50% | [@react-native-oh-tpl/react-native-gesture-handler](https://github.com/react-native-oh-library/react-native-gesture-handler/releases) | [链接](zh-cn/react-native-gesture-handler.md) |
| 12 | [react-native-image-picker](https://github.com/react-native-image-picker/react-native-image-picker) | 7.0.3 | 是 | 50% | [@react-native-oh-tpl/react-native-image-picker](https://github.com/react-native-oh-library/react-native-image-picker/releases) | [链接](zh-cn/react-native-image-picker.md) |
| 13 | [react-native-linear-gradient](https://github.com/react-native-linear-gradient/react-native-linear-gradient) | 3.0.0-alpha.1 | 是 | 90% | [@react-native-oh-tpl/react-native-linear-gradient](https://github.com/react-native-oh-library/react-native-linear-gradient/releases) | [链接](zh-cn/react-native-linear-gradient.md) |
| 14 | [@react-native-masked-view/masked-view](https://github.com/react-native-masked-view/masked-view) | 0.2.9 | 否 | 90% | [@react-native-oh-tpl/masked-view](https://github.com/react-native-oh-library/masked-view/releases) | [链接](zh-cn/react-native-masked-view.md) |
| 15 | [@react-native-community/netinfo](https://github.com/react-native-netinfo/react-native-netinfo) | 11.1.0 | 是 | 70% | [@react-native-oh-library/netinfo](https://github.com/react-native-oh-library/react-native-netinfo/releases) | [链接](zh-cn/react-native-netinfo.md) |
| 16 | [react-native-pager-view](https://github.com/callstack/react-native-pager-view) | 6.2.2 | 是 | 100% | [@react-native-oh-tpl/react-native-pager-view](https://github.com/react-native-oh-library/react-native-pager-view/releases) | [链接](zh-cn/react-native-pager-view.md) |
| 17 | [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context) | 4.7.4 | 是 |100% | [@react-native-oh-tpl/react-native-safe-area-context](https://github.com/react-native-oh-library/react-native-safe-area-context/releases) | [链接](zh-cn/react-native-safe-area-context.md) |
| 18 | [react-native-screens](https://github.com/software-mansion/react-native-screens) | 3.29.0 | 是 | 0% | [react-native-screens](https://github.com/software-mansion/react-native-screens/releases) | [链接](zh-cn/react-native-screens.md) |
|  19  | [@react-native-community/slider](https://github.com/callstack/react-native-slider) |     4.4.3     | 是 | 90% | [@react-native-oh-library/slider](https://github.com/react-native-oh-library/react-native-slider/releases) | [链接](zh-cn/react-native-slider.md) |
| 20 | [react-native-SmartRefreshLayout](https://github.com/react-native-studio/react-native-SmartRefreshLayout) | 0.6.7 | 否 | 70% | [@react-native-oh-tpl/react-native-SmartRefreshLayout](https://github.com/react-native-oh-library/react-native-SmartRefreshLayout/releases) | [链接](zh-cn/react-native-SmartRefreshLayout.md) |
| 21 | [react-native-svg](https://github.com/software-mansion/react-native-svg) | 13.14.0 | 是 | 10% | [@react-native-oh-tpl/react-native-svg](https://github.com/react-native-oh-library/react-native-svg/releases) | [链接](zh-cn/react-native-svg.md) |
| 22 | [react-native-tab-view](https://github.com/react-navigation/react-navigation/tree/6.x/packages/react-native-tab-view) | 3.5.2 | - | 100% | [@react-native-oh-tpl/react-native-tab-view](https://github.com/react-native-oh-library/react-navigation/releases) | [链接](zh-cn/react-native-tab-view.md) |
| 23 | [react-native-video](https://github.com/react-native-video/react-native-video) | 5.2.1 | 是 | 25% | [@react-native-oh-tpl/react-native-video](https://github.com/react-native-oh-library/react-native-video) | [链接](zh-cn/react-native-video.md) |
| 24 | [react-native-webview](https://github.com/react-native-webview/react-native-webview) | 13.6.2 | 是 | 15% | [@react-native-oh-tpl/react-native-webview](https://github.com/react-native-oh-library/react-native-webview/releases) | [链接](zh-cn/react-native-webview.md) |
| 25 | [@react-navigation/elements](https://github.com/react-navigation/react-navigation/tree/6.x/packages/elements) | 1.3.21 | - | 100% | [@react-native-oh-tpl/elements](https://github.com/react-native-oh-library/react-navigation/releases) | [链接](zh-cn/react-navigation-elements.md) |

## 社区

[Github Organization: react-native-oh-library](https://github.com/react-native-oh-library)