> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>@react-native-community/toolbar-android</code> </h1>
</p>

本项目基于 [@react-native-toolbar-android/toolbar-android@v0.2.1](https://github.com/react-native-toolbar-android/toolbar-android) 开发。

该第三方库的仓库已迁移至 Gitee，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/toolbar-android`，具体版本所属关系如下：

| Version         | Package Name                                      | Repository         | Release                    |
|-----------------| ------------------------------------------------- | ------------------ | -------------------------- |
| <= 0.2.1-0.0.4  | @react-native-oh-tpl/toolbar-android | [Github(deprecated)](https://github.com/react-native-oh-library/toolbar-android) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/toolbar-android/releases) |
| >= 0.2.2        | @react-native-ohos/toolbar-android   | [Gitee](https://gitee.com/openharmony-sig/rntpc_toolbar-android) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_toolbar-android/releases) |

## 1.安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/toolbar-android
```

#### yarn

```bash
yarn add @react-native-ohos/toolbar-android
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { StyleSheet, View, Text } from "react-native";
import ToolbarAndroid from "@react-native-community/toolbar-android";
function App({}): JSX.Element {
  const [state, setState] = useState<{
    message?: string;
  }>({
    message: undefined,
  });

  const { message } = state;

  return (
    <View style={styles.container}>
      <ToolbarAndroid
        navIcon={require("./assets/ic_menu_black_24dp.png")}
        logo={require("./assets/icon_app.png")}
        title={"ToolbarAndroid Example"}
        subtitle={"ToolbarAndroid Subtitle"}
        titleColor={"#FFFFFF"}
        subtitleColor={"#FF00FF"}
        contentInsetStart={10}
        contentInsetEnd={10}
        rtl={false}
        style={styles.toolbar}
        actions={[
          {
            title: "Action1",
            icon: require("./assets/icon_phone.png"),
            show: "ifRoom",
            showWithText: true,
          },
        ]}
        overflowIcon={require("./assets/relay.png")}
        onIconClicked={() => setState({ message: "Clicked nav icon" })}
        onActionSelected={(position: number) =>
          setState({ message: `Clicked Menu-${position}` })
        }
      />
      <View style={styles.centerContainer}>
        <Text style={styles.headText}>
          Click nav or action icon will trigger some events!
        </Text>
        <Text style={styles.contentText}>{message}</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  toolbar: {
    backgroundColor: "#E9EAED",
    height: 56,
  },
  centerContainer: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
  },
  headText: {
    fontSize: 16,
  },
  contentText: {
    fontSize: 18,
    fontWeight: "bold",
    color: "#ff681f",
  },
});

export default App;
```

## 2.Manual Link

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1.Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 2.2.引入原生端代码

目前有两种方法：

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@react-native-ohos/toolbar-android": "file:../../node_modules/@react-native-ohos/toolbar-android/harmony/toolbar_android.har"
  }
```

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 2.3.配置 CMakeLists 和引入 ToolbarAndroidPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/toolbar-android/src/main/cpp" ./toolbar-android)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_toolbar_android)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
...
+ #include "ToolbarAndroidPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      ...
+     std::make_shared<ToolbarAndroidPackage>(ctx),
    };
}
```

### 2.4.在 ArkTs 侧引入 RNCCheckBoxPackage

> [!TIP] 版本 v0.2.22 及以上需要

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {ToolbarAndroidPackage} from '@react-native-ohos/toolbar-android/src/main/ets/ToolbarAndroidPackage';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   return [new ToolbarAndroidPackage(ctx)];
  ];
}

```

### 2.5.在 ArkTs 侧引入 RNCToolbarAndroid 组件

找到 **function buildCustomRNComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RNCToolbarAndroid} from '@react-native-ohos/toolbar-android/src/main/ets/RNCToolbarAndroid'

  @Builder
  function buildCustomRNComponent(ctx: ComponentBuilderContext) {
    ...
+   if (ctx.componentName === RNCToolbarAndroid.NAME) {
+     RNCToolbarAndroid({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag
+     })
+   }
    ...
  }
  ...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  ...
+ RNCToolbarAndroid.NAME
];
```

### 2.6.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3.约束与限制

### 3.1兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/toolbar-android Releases](https://gitee.com/openharmony-sig/rntpc_toolbar-android/releases)

## 4.属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

Inherits [View Props](https://reactnative.dev/docs/view#props).

| Name              | Description                                                                                                                                                                                     | Type                                                                                                          | Required  | Platform | HarmonyOS Support |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |-----------| -------- | ----------------- |
| actions           | Sets possible actions on the toolbar as part of the action menu. These are displayed as icons or text on the right side of the widget. If they don't fit they are placed in an 'overflow' menu. | array of object: {title: string,icon: ImageSource,show: enum('always', 'ifRoom', 'never'),showWithText: bool} | No        | Android  | yes               |
| contentInsetStart | Sets the content inset for the toolbar starting edge.                                                                                                                                           | number                                                                                                        | No        | Android  | yes               |
| contentInsetEnd   | Sets the content inset for the toolbar ending edge.                                                                                                                                             | number                                                                                                        | No        | Android  | yes               |
| logo              | Sets the toolbar logo.                                                                                                                                                                          | ImageSource                                                                                                   | No        | Android  | yes               |
| navIcon           | Sets the navigation icon.                                                                                                                                                                       | ImageSource                                                                                                   | No        | Android  | yes               |
| onActionSelected  | Callback that is called when an action is selected. The only argument that is passed to the callback is the position of the action in the actions array.                                        | function                                                                                                      | No        | Android  | yes               |
| onIconClicked     | Callback called when the icon is selected.                                                                                                                                                      | function                                                                                                      | No        | Android  | yes               |
| overflowIcon      | Sets the overflow icon.                                                                                                                                                                         | ImageSource                                                                                                   | No        | Android  | yes               |
| rtl               | Used to set the toolbar direction to RTL.                                                                                                                                                       | bool                                                                                                          | No        | Android  | yes               |
| subtitle          | Sets the toolbar subtitle.                                                                                                                                                                      | string                                                                                                        | No        | Android  | yes               |
| subtitleColor     | Sets the toolbar subtitle color.                                                                                                                                                                | string                                                                                                        | No        | Android  | yes               |
| title             | Sets the toolbar title.                                                                                                                                                                         | string                                                                                                        | No        | Android  | yes               |
| titleColor        | Sets the toolbar title color.                                                                                                                                                                   | string                                                                                                        | No        | Android  | yes               |

#### 4.1.Props of ImageSource

| Name   | Description                                            | Type   | Required | Platform | HarmonyOS Support |
| ------ | ------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| uri    | load image from a url, e.g. require('./some_icon.png') | string | Yes      | android  | yes               |
| width  | the width of the image                                 | number | No       | android  | yes               |
| height | the height of the image                                | number | No       | android  | yes               |

## 5.遗留问题

## 6.其他

## 7.开源协议

本项目基于 [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_toolbar-android/blob/master/LICENSE) ，请自由地享受和参与开源。
