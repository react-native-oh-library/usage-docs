> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>@react-native-oh-tpl/toolbar-android</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/toolbar-android">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/toolbar-android/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/toolbar-android/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-tpl/toolbar-android> Releases](https://github.com/react-native-oh-library/toolbar-android/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/toolbar-android@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/toolbar-android@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useState } from 'react';
import { StyleSheet, View, Text } from 'react-native';
import ToolbarAndroid from '@react-native-oh-tpl/toolbar-android';
function App({ }): JSX.Element {
  const [state, setState] = useState<{
    message?: string
  }>({
    message: undefined
  })

  const { message } = state

  return (
    <View style={styles.container}>
      <ToolbarAndroid
        navIcon={require('./assets/ic_menu_black_24dp.png')}
        logo={require('./assets/icon_app.png')}
        title={"ToolbarAndroid Example"}
        subtitle={'ToolbarAndroid Subtitle'}
        titleColor={'#FFFFFF'}
        subtitleColor={'#FF00FF'}
        contentInsetStart={10}
        contentInsetEnd={10}
        rtl={false}
        style={styles.toolbar}
        actions={[
          { title: 'Action1', icon: require('./assets/icon_phone.png'), show: 'ifRoom', showWithText: true }
        ]}
        overflowIcon={require('./assets/relay.png')}
        onIconClicked={() => setState({ message: 'Clicked nav icon' })}
        onActionSelected={(position: number) => setState({ message: `Clicked Menu-${position}` })} />
      <View style={styles.centerContainer}>
        <Text style={styles.headText}>
          Click nav or action icon will trigger some events!
        </Text>
        <Text style={styles.contentText}>
          {message}
        </Text>
      </View>

    </View>
  )
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  toolbar: {
    backgroundColor: '#E9EAED',
    height: 56,
  },
  centerContainer: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  headText: {
    fontSize: 16
  },
  contentText: {
    fontSize: 18,
    fontWeight: 'bold',
    color: '#ff681f'
  }
});

export default App;
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-toolbar-android": "file:../../node_modules/@react-native-oh-tpl/toolbar-android/harmony/toolbar_android.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-toolbar-android": "file:../../node_modules/@react-native-oh-tpl/toolbar-android/harmony/toolbar_android"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

###  配置 CMakeLists 和引入 ToolbarAndroidPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
txtproject(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-toolbar-android/src/main/cpp" ./toolbar-android)
# RNOH_END: add_package_subdirectories

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
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ToolbarAndroidPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ToolbarAndroidPackage>(ctx),
    };
}
```

### 在 ArkTs 侧引入 RNCToolbarAndroid组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import { RNCToolbarAndroid, RNC_TOOLBAR_ANDROID_TYPE, RNCToolbarAndroidDescriptor } from 'rnoh-toolbar-android/src/main/ets/RNCToolbarAndroid'

  @Builder
  function buildCustomComponent(ctx: ComponentBuilderContext) {
    if (ctx.componentName === SAMPLE_VIEW_TYPE) {
      SampleView({
        ctx: ctx.rnComponentContext,
        tag: ctx.tag,
        buildCustomComponent: buildCustomComponent
      })
    }
+  else if (ctx.componentName === RNC_TOOLBAR_ANDROID_TYPE) {
+    RNCToolbarAndroid({
+      ctx: ctx.rnohContext,
+      tag: ctx.tag,
+      descriptor: ctx.descriptor as RNCToolbarAndroidDescriptor
+    })
+  }
    ...
  }
  ...

```

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[<@react-native-oh-tpl/toolbar-android> Releases](https://github.com/react-native-oh-library/toolbar-android/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

Inherits [View Props](https://reactnative.dev/docs/view#props).

| Name           | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| actions          | Sets possible actions on the toolbar as part of the action menu. These are displayed as icons or text on the right side of the widget. If they don't fit they are placed in an 'overflow' menu.                            | array of object: {title: string,icon: object: {uri:object,height?:number,width?:number},show: enum('always', 'ifRoom', 'never'),showWithText: bool} | No       | Android     | yes               |
| contentInsetStart         | Sets the content inset for the toolbar starting edge.                     | number | No       | Android | yes               |
| contentInsetEnd       | Sets the content inset for the toolbar ending edge.                | number | No       | Android | yes               |
| logo | Sets the toolbar logo. | object: {uri:object,height?:number,width?:number} | No       | Android     | yes               |
| navIcon      | Sets the navigation icon.                         | object: {uri:object,height?:number,width?:number} | No       | Android | yes               |
| onActionSelected     | Callback that is called when an action is selected. The only argument that is passed to the callback is the position of the action in the actions array.                         | function | No       | Android | yes               |
| onIconClicked       | Callback called when the icon is selected.         | function | No       | Android         | yes               |
| overflowIcon         | Sets the overflow icon.                              | object: {uri:object,height?:number,width?:number} | No       | Android | yes               |
| rtl         | Used to set the toolbar direction to RTL.                              | bool | No       | Android | yes               |
| subtitle         | Sets the toolbar subtitle.                              | string | No       | Android | yes               |
| subtitleColor         | Sets the toolbar subtitle color.                              | string | No       | Android | yes               |
| title         | Sets the toolbar title.                              | string | Yes       | Android | yes               |
| titleColor         | Sets the toolbar title color.                              | string | No       | Android | yes               |

#### types of uri

| Usage                                                        | Description                                                  | Platform    | HarmonyOS Support |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- | ----------------- |
| {require("./test.png")}                                    | load image from a url                                          | android | yes               |

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-toolbar-android/toolbar-android/blob/master/LICENSE) ，请自由地享受和参与开源。