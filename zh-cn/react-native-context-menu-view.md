> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-context-menu-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mpiannucci/react-native-context-menu-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mpiannucci/react-native-context-menu-view/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-context-menu-view)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-context-menu-view Releases](https://github.com/react-native-oh-library/react-native-context-menu-view/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-context-menu-view
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-context-menu-view
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import ContextMenu from "react-native-context-menu-view";

const Example = () => {
  return (
    <ContextMenu
      actions={[{ title: "Title 1" }, { title: "Title 2" }]}
      onPress={(e) => {
        console.warn(
          `Pressed ${e.nativeEvent.name} at index ${e.nativeEvent.index}`
        );
      }}
    >
      <View style={styles.yourOwnStyles} />
    </ContextMenu>
  );
};
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-context-menu-view": "file:../../node_modules/@react-native-oh-tpl/react-native-context-menu-view/harmony/context_menu.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.配置 CMakeLists 和引入 ContextMenuPackage

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

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-context-menu-view/src/main/cpp" ./context_menu)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_context_menu)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ContextMenuPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ContextMenuPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 ContextMenuPackage

打开 `entry/src/main/ets/RNPackagesFactory.ets`，添加：

```diff
  ...
+ import {ContextMenuPackage} from '@react-native-oh-tpl/react-native-context-menu-view/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ContextMenuPackage(ctx)
  ];
}
```

### 5.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-context-menu-view Releases](https://github.com/react-native-oh-library/react-native-context-menu-view/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                   | Description                                                  | Type     | Required | Platform               | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | -------- | -------- | ---------------------- | ----------------- |
| title                  | The title above the popup menu.                              | string   | no       | Android/iOS            | yes               |
| actions                | Menu props.                                                  | array    | no       | Android(partially)/iOS | partially         |
| previewBackgroundColor | The background color of the preview.                         | string   | no       | NA                     | no                |
| dropdownMenuMode       | When set to true, the context menu is triggered with a single tap instead of a long press. | boolean  | no       | Android/iOS            | yes               |
| disabled               | Disable menu interaction.                                    | boolean  | no       | Android/iOS            | yes               |
| onPress                | When the popup is opened and the user picks an option.       | callback | no       | Android/iOS            | yes               |
| onPreviewPress         | When the context menu preview is tapped.                     | callback | no       | iOS                    | yes               |
| onCancel               | When the popup is opened and the user cancels.               | callback | no       | Android/iOS            | yes               |

## actions

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name           | Description                                                  | Type    | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| title          | the title of the action                                      | string  | no       | Android/iOS | yes               |
| subtitle       | the subtitle of the action                                   | string  | no       | iOS 15+     | yes               |
| systemIcon     | refers to an icon name within [SF Symbols](https://developer.apple.com/design/human-interface-guidelines/sf-symbols/overview/) | string  | no       | iOS         | yes               |
| icon           | Custom Icons.                                                | string  | no       | Android/iOS | yes               |
| iconColor      | will change the color of the icon provided to the `icon` prop and has no effect on `systemIcon` (default: black) | string  | no       | Android/iOS | yes               |
| destructive    | items are rendered in red                                    | boolean | no       | iOS         | yes               |
| selected       | items have a checkmark next to them                          | boolean | no       | iOS         | yes               |
| disabled       | marks whether the action is disabled or not                  | boolean | no       | Android/iOS | yes               |
| inlineChildren | marks whether its children (if any) should be rendered inline instead of in their own child menu | boolean | no       | iOS         | partially         |
| actions        | will provide a one level deep nested menu                    | array   | no       | Android/iOS | partially         |

## 遗留问题

## 其他

1.previewBackgroundColor属性，经过验证在iOS和Android均无效果。

2.actions属性是个结构体函数，所以包含其他上文列举属性，例如previewBackgroundColor等。所以，属于部分支持

3.该库的具体逻辑实现，在不同平台，均为调用平台对应的底层Menu接口进行相关操作。所以，不同平台上，动效展示等会有所不同。

4.onPress方法的callback参考：{ nativeEvent: { index, indexPath, name } }. 

5.当systemIcon和icon同时配置的时候，在Harmony Next平台上，systemIcon的优先级高于icon

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mpiannucci/react-native-context-menu-view/blob/main/LICENSE) ，请自由地享受和参与开源。
