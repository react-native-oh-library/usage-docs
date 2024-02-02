# 简介

> 欢迎开始React-Native的旅程！如果你在找如何搭建环境的文档，请移步开发文档的[搭建开发环境](https://react-native-oh-library.gitee.io/docs/#/zh-cn/environment)章节。

## 概述

该文档旨在帮助开发者在 OpenHarmony 平台使用 React Native OpenHarmony 的第三方库，并呈现每个三方库的信息。

## RNOH 三方库总览

>[!tip] NPM 公仓坐标：@react-native-oh-tpl

>[!tip] NPM Github Packages 私仓坐标：@react-native-oh-library

| 序号 | 原库名 | 原库基线版本 | 原库是否支持新架构 | 鸿蒙化进度 | Releases | 文档链接 |
| :--: | :----: | :----------: | :----------------: | :--------: | :------: | :------: |
|  1  | [@react-native-async-storage/async-storage](https://github.com/react-native-async-storage/async-storage) |    1.21.1     | 是 | 100% | [@react-native-oh-tpl/async-storage](https://github.com/react-native-oh-library/async-storage/releases) | [链接](/zh-cn/react-native-async-storage-async-storage.md) |
|  2  | [@react-native-clipboard/clipboard](https://github.com/react-native-clipboard/clipboard) |     1.13.2     | 是 | 80% | [@react-native-oh-tpl/clipboard](https://github.com/react-native-oh-library/clipboard/releases) | [链接](/zh-cn/react-native-clipboard-clipboard.md) |
| 3 | [@react-native-community/datetimepicker](https://github.com/react-native-datetimepicker/datetimepicker) | 7.6.2 | 是 | 80% | [@react-native-oh-tpl/datetimepicker](https://github.com/react-native-oh-library/datetimepicker/releases) | [链接](/zh-cn/react-native-community-datetimepicker.md) |
| 4 | [@shopify/flash-list](https://github.com/Shopify/flash-list) | 1.6.3 | 否 | 80% | [@react-native-oh-tpl/flash-list](https://github.com/react-native-oh-library/flash-list/releases) | [链接](/zh-cn/shopify-flash-list.md) |
| 5 | [lottie-react-native](https://github.com/lottie-react-native/lottie-react-native) | 6.4.1 | 是 | 50% | [@react-native-oh-tpl/lottie-react-native](https://github.com/react-native-oh-library/lottie-react-native/releases) | [链接](/zh-cn/lottie-react-native.md) |
|  6  | [@react-native-picker/picker](https://github.com/react-native-picker/picker) |     2.5.1     | 否 | 90% | [@react-native-oh-tpl/picker](https://github.com/react-native-oh-library/picker/releases) | [链接](/zh-cn/react-native-picker-picker.md) |
|  7  | [@react-native-community/progress-bar-android](https://github.com/react-native-progress-view/progress-bar-android) |     1.0.4     | 是 | 90% | [@react-native-oh-tpl/progress-bar-android](https://github.com/react-native-oh-library/progress-bar-android/releases) | [链接](/zh-cn/react-native-community-progress-bar-android.md) |
|  8  | [@react-native-community/checkbox](https://github.com/react-native-checkbox/react-native-checkbox) |    0.5.16     | 否 | 100% | [@react-native-oh-tpl/react-native-checkbox](https://github.com/react-native-oh-library/react-native-checkbox/releases) | [链接](/zh-cn/react-native-community-checkbox.md) |
| 9 | [react-native-exception-handler](https://github.com/a7ul/react-native-exception-handler) | 2.10.10 | 否 | 100% | [@react-native-oh-tpl/react-native-exception-handler](https://github.com/react-native-oh-library/react-native-exception-handler/releases) | [链接](/zh-cn/react-native-exception-handler.md) |
| 10 | [react-native-fast-image](https://github.com/DylanVann/react-native-fast-image) | 8.6.3 | 否 | 70% | [@react-native-oh-tpl/react-native-fast-image](https://github.com/react-native-oh-library/react-native-fast-image/releases) | [链接](/zh-cn/react-native-fast-image.md) |
| 11 | [react-native-gesture-handler](https://github.com/software-mansion/react-native-gesture-handler) | 2.12.1 | 是 | 50% | [@react-native-oh-tpl/react-native-gesture-handler](https://github.com/react-native-oh-library/react-native-gesture-handler/releases) | [链接](/zh-cn/react-native-gesture-handler.md) |
| 12 | [react-native-image-picker](https://github.com/react-native-image-picker/react-native-image-picker) | 7.0.3 | 是 | 50% | [@react-native-oh-tpl/react-native-image-picker](https://github.com/react-native-oh-library/react-native-image-picker/releases) | [链接](/zh-cn/react-native-image-picker.md) |
| 13 | [react-native-linear-gradient](https://github.com/react-native-linear-gradient/react-native-linear-gradient) | 3.0.0-alpha.1 | 是 | 90% | [@react-native-oh-tpl/react-native-linear-gradient](https://github.com/react-native-oh-library/react-native-linear-gradient/releases) | [链接](/zh-cn/react-native-linear-gradient.md) |
| 14 | [@react-native-masked-view/masked-view](https://github.com/react-native-masked-view/masked-view) | 0.2.9 | 否 | 90% | [@react-native-oh-tpl/masked-view](https://github.com/react-native-oh-library/masked-view/releases) | [链接](/zh-cn/react-native-masked-view-masked-view.md) |
| 15 | [@react-native-community/netinfo](https://github.com/react-native-netinfo/react-native-netinfo) | 11.1.0 | 是 | 70% | [@react-native-oh-tpl/netinfo](https://github.com/react-native-oh-library/react-native-netinfo/releases) | [链接](/zh-cn/react-native-community-netinfo.md) |
| 16 | [react-native-pager-view](https://github.com/callstack/react-native-pager-view) | 6.2.2 | 是 | 100% | [@react-native-oh-tpl/react-native-pager-view](https://github.com/react-native-oh-library/react-native-pager-view/releases) | [链接](/zh-cn/react-native-pager-view.md) |
| 17 | [react-native-safe-area-context](https://github.com/th3rdwave/react-native-safe-area-context) | 4.7.4 | 是 |100% | [@react-native-oh-tpl/react-native-safe-area-context](https://github.com/react-native-oh-library/react-native-safe-area-context/releases) | [链接](/zh-cn/react-native-safe-area-context.md) |
| 18 | [react-native-screens](https://github.com/software-mansion/react-native-screens) | 3.29.0 | 是 | 0% | [react-native-screens](https://github.com/software-mansion/react-native-screens/releases) | [链接](/zh-cn/react-native-screens.md) |
|  19  | [@react-native-community/slider](https://github.com/callstack/react-native-slider) |     4.4.3     | 是 | 90% | [@react-native-oh-tpl/slider](https://github.com/react-native-oh-library/react-native-slider/releases) | [链接](/zh-cn/react-native-community-slider.md) |
| 20 | [react-native-SmartRefreshLayout](https://github.com/react-native-studio/react-native-SmartRefreshLayout) | 0.6.7 | 否 | 70% | [@react-native-oh-tpl/react-native-SmartRefreshLayout](https://github.com/react-native-oh-library/react-native-SmartRefreshLayout/releases) | [链接](/zh-cn/react-native-SmartRefreshLayout.md) |
| 21 | [react-native-svg](https://github.com/software-mansion/react-native-svg) | 13.14.0 | 是 | 10% | [@react-native-oh-tpl/react-native-svg](https://github.com/react-native-oh-library/react-native-svg/releases) | [链接](/zh-cn/react-native-svg.md) |
| 22 | [react-native-tab-view](https://github.com/react-navigation/react-navigation/tree/6.x/packages/react-native-tab-view) | 3.5.2 | - | 100% | [@react-native-oh-tpl/react-native-tab-view](https://github.com/react-native-oh-library/react-navigation/releases) | [链接](/zh-cn/react-native-tab-view.md) |
| 23 | [react-native-video](https://github.com/react-native-video/react-native-video) | 5.2.1 | 是 | 25% | [@react-native-oh-tpl/react-native-video](https://github.com/react-native-oh-library/react-native-video) | [链接](/zh-cn/react-native-video.md) |
| 24 | [react-native-webview](https://github.com/react-native-webview/react-native-webview) | 13.6.2 | 是 | 15% | [@react-native-oh-tpl/react-native-webview](https://github.com/react-native-oh-library/react-native-webview/releases) | [链接](/zh-cn/react-native-webview.md) |
| 25 | [@react-navigation/elements](https://github.com/react-navigation/react-navigation/tree/6.x/packages/elements) | 1.3.21 | - | 100% | [@react-native-oh-tpl/elements](https://github.com/react-native-oh-library/react-navigation/releases) | [链接](/zh-cn/react-navigation-elements.md) |
|  26  | [crypto-js](https://github.com/brix/crypto-js/tree/4.2.0) |    4.2.0     |  |  | [crypto-js](https://github.com/brix/crypto-js/tree/4.2.0) | [链接](/zh-cn/crypto-js.md) |
|  27  | [deepmerge](https://github.com/TehShrike/deepmerge) |     4.3.1     |  |  | [deepmerge](https://github.com/TehShrike/deepmerge/releases) | [链接](/zh-cn/deepmerge.md) |
| 28 | [htmlparser2](https://github.com/fb55/htmlparser2) | 9.1.0 |  |  | [htmlparser2](https://github.com/fb55/htmlparser2/releases) | [链接](/zh-cn/htmlparser2.md) |
| 29 | [js-beautify](https://github.com/beautifier/js-beautify) | 1.14.9 |  |  | [js-beautify](https://github.com/beautifier/js-beautify/releases) | [链接](/zh-cn/js-beautify) |
| 30 | [lodash](https://github.com/lodash/lodash/tree/4.17.21) | 4.17.21 |  |  | [lodash](https://github.com/lodash/lodash//releases) | [链接](/zh-cn/lodash.md) |
|  31  | [mobx-react](https://github.com/mobxjs/mobx/tree/mobx-react%407.6.0) |     7.6.0    |  |  | [mobx-react](https://github.com/mobxjs/mobx/tree/mobx-react%407.6.0) | [链接](/zh-cn/mobx-react.md) |
|  32  | [mobx](https://github.com/mobxjs/mobx/tree/mobx%406.10.0) |     6.10.0    |  |  | [mobx](https://github.com/mobxjs/mobx/tree/mobx%406.10.0) | [链接](/zh-cn/mobx.md) |
| 33 | [parse5](https://github.com/inikulin/parse5) | 7.1.2 |  |  | [parse5](https://github.com/inikulin/parse5/releases) | [链接](/zh-cn/parse5.md) |
|  34  | [prop-types](https://github.com/facebook/prop-types/tree/v15.8.1) |    15.8.1    |  |  | [prop-types](https://github.com/facebook/prop-types/tree/v15.8.1) | [链接](/zh-cn/prop-types.md) |
| 35 | [react-i18next](https://github.com/i18next/react-i18next) | 8.6.3 |  |  | [react-i18next](https://github.com/i18next/react-i18next/releases) | [链接](/zh-cn/react-i18next.md) |
| 36 | [react-native-action-button](https://github.com/mastermoo/react-native-action-button) |  |  |  | [react-native-action-button](https://github.com/mastermoo/react-native-action-button/releases) | [链接](/zh-cn/react-native-action-button.md) |
| 37 | [react-native-autoheight-webview](https://github.com/react-native-oh-library/react-native-autoheight-webview) |  |  |  | [@react-native-oh-tpl/react-native-autoheight-webview](https://github.com/react-native-oh-library/react-native-autoheight-webview/releases) | [链接](/zh-cn/react-native-autoheight-webview.md) |
| 38 | [@react-native-camera-roll/camera-roll](https://github.com/react-native-oh-library/react-native-cameraroll) |  |  |  | [@react-native-oh-tpl/camera-roll](https://github.com/react-native-oh-library/react-native-cameraroll/releases) | [链接](/zh-cn/react-native-cameraroll.md) |
| 39 | [@react-native-masked-view/masked-view](https://github.com/react-native-masked-view/masked-view) |  | |  | [@react-native-oh-tpl/masked-view](https://github.com/react-native-oh-library/masked-view/releases) | [链接](/zh-cn/react-native-masked-view-masked-view.md) |
| 40 | [@react-native-community/progress-view](https://github.com/react-native-progress-view/progress-view) |  |  |  | [@react-native-community/progress-view](https://github.com/react-native-oh-library/progress-view/releases) | [链接](/zh-cn/react-native-community-progress-view.md) |
| 41 | [@react-native-segmented-control/segmented-control](https://github.com/react-native-segmented-control/segmented-control) | 2.5.0 |  |  | [@react-native-segmented-control/segmented-control](https://github.com/react-native-segmented-control/segmented-control/releases) | [链接](/zh-cn/react-native-community-segmented-control.md) |
| 42 | [react-native-dotenv](https://github.com/goatandsheep/react-native-dotenv) | 3.4.9 |  | | [react-native-dotenv](https://github.com/goatandsheep/react-native-dotenv/releases) | [链接](/zh-cn/react-native-dotenv.md) |
| 43 | [@react-native-community/geolocation](https://github.com/michalchudziak/react-native-geolocation) |  |  |  | [@react-native-oh-tpl/react-native-geolocation](https://github.com/react-native-oh-library/react-native-geolocation/releases) | [链接](/zh-cn/react-native-geolocation.md) |
|  44  | [react-native-qrcode-svg](https://github.com/awesomejerry/react-native-qrcode-svg) |  |  |  | [@react-native-oh-tpl/react-native-qrcode-svg](https://github.com/react-native-oh-library/react-native-qrcode-svg/releases) | [链接](/zh-cn/react-native-qrcode-svg.md) |
| 45 | [react-native-reanimated](https://github.com/software-mansion/react-native-reanimated) |  |  |  | [@react-native-oh-tpl/react-native-reanimated](https://github.com/react-native-oh-library/react-native-reanimated/releases) | [链接](/zh-cn/react-native-reanimated.md) |
| 46 | [react-native-render-html](https://github.com/meliorence/react-native-render-html) |  |  |  | [react-native-render-html](https://github.com/meliorence/react-native-render-html/releases) | [链接](/zh-cn/react-native-render-html.md) |
| 47 | [react-native-section-list-get-item-layout](https://github.com/jsoendermann/rn-section-list-get-item-layout) | 2.2.3 | |  | [react-native-section-list-get-item-layout](https://github.com/jsoendermann/rn-section-list-get-item-layout/releases) | [链接](/zh-cn/react-native-section-list-get-item-layout.md) |
| 48 | [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons) | 10.0.3 |  |  | [react-native-vector-icons](https://github.com/oblador/react-native-vector-icons/releases) | [链接](/zh-cn/react-native-vector-icons.md) |
| 49 | [react-native-view-shot](https://github.com/gre/react-native-view-shot) |  |  |  | [@react-native-oh-tpl/react-native-view-shot](https://github.com/react-native-oh-library/react-native-view-shot/releases) | [链接](/zh-cn/react-native-view-shot.md) |
| 50 | [ @react-navigation/bottom-tabs](https://github.com/react-navigation/react-navigation/tree/6.x/packages/bottom-tabs) | 6.5.11 |  |  | [ @react-navigation/bottom-tabs](https://github.com/react-navigation/react-navigation/tree/6.x/packages/bottom-tabs) | [链接](/zh-cn/react-navigation-bottom-tabs.md) |
|  51  | [@react-navigation/native](https://github.com/react-navigation/react-navigation/tree/6.x/packages/native) |    6.1.9     |  |  | [@react-native-oh-tpl/async-storage](https://github.com/react-navigation/react-navigation/tree/6.x/packages/native/) | [链接](/zh-cn/react-navigation-native.md) |
|  52  | [@react-navigation/stack](https://github.com/react-navigation/react-navigation/tree/6.x/packages/stack) |     6.3.19     | 是 | 80% | [@react-navigation/stack](https://github.com/react-navigation/react-navigation/tree/6.x/packages/stack) | [链接](/zh-cn/react-navigation-stack.md) |
| 53 | [recyclerlistview](https://github.com/Flipkart/recyclerlistview) |  |  |  | [recyclerlistview](https://github.com/Flipkart/recyclerlistview/releases) | [链接](/zh-cn/recyclerListView.md) |
| 54 | [rn-placeholder](https://github.com/mfrachet/rn-placeholder) | 3.0.3 |  |  | [rn-placeholder](https://github.com/mfrachet/rn-placeholder/releases) | [链接](/zh-cn/rn-placeholder.md) |
| 55 | [styled-components](https://github.com/styled-components/styled-components) | 6.1.8 |  |  | [styled-components](https://github.com/styled-components/styled-components/releases) | [链接](/zh-cn/styled-components.md) |
|  56  | [styled-system](https://github.com/react-native-picker/picker) |    5.1.5    |  |  | [styled-system](https://github.com/styled-system/styled-system) | [链接](/zh-cn/styled-system.md) |

## 社区

[Github Organization: react-native-oh-library](https://github.com/react-native-oh-library)