> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-bindingx</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/alibaba/bindingx">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/alibaba/bindingx/blob/master/LICENSE.md">
       <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-bindingx)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-bindingx Releases](https://github.com/react-native-oh-library/react-native-bindingx/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-bindingx
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-bindingx
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, {Component} from 'react';
import {
  StyleSheet,
  View,
  Text,
  findNodeHandle,
  TouchableHighlight,
  PanResponder
} from 'react-native';

import bindingx from 'react-native-bindingx';

export default class App extends Component {

  _panResponder = PanResponder.create({
    onStartShouldSetPanResponder: (evt, gestureState) => true,
    onPanResponderGrant: (evt, gestureState) => {
      this.onBind();
    }
  });

  _x = 0;
  _y = 0;

  componentDidMount() {
    let anchor = findNodeHandle(this.refs._anchor);
    bindingx.prepare({
      eventType: 'pan',
      anchor: anchor
    });
  }

  onPanEnd = (e) => {
    if (e.state === 'end') {
      this._x += e.deltaX;
      this._y += e.deltaY;
    }
  }

  onBind() {

    let expression_x_origin = "x+" + this._x;

    let expression_y_origin = "y+" + this._y;

    let anchor = findNodeHandle(this.refs._anchor);
    let token = bindingx.bind({
      eventType: 'pan',
      anchor: anchor,
      props: [
        {
          element: anchor,
          property: 'transform.translateX',
          expression: expression_x_origin
        },
        {
          element: anchor,
          property: 'transform.translateY',
          expression: expression_y_origin
        }
      ]
    },this.onPanEnd);
  }

  render() {
    return (
      <View style={styles.container}>
        <View
          ref="_anchor"
          style={styles.anchor}
          {...this._panResponder.panHandlers}
        />

      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#F5FCFF',
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 10,
  },
  text: {
    textAlign: 'center',
    color: '#ffffff',
  },
  wrapper: {
    backgroundColor: '#0000ff',
    height: 48,
    alignItems: 'center',
    justifyContent: 'center'
  },
  margin: {
    marginTop: 20
  },
  anchor: {
    width: 80,
    height: 80,
    backgroundColor: '#ff0000',
    marginTop: 48
  }
});

```

## Link

目前HarmonyOS暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`

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
    "@react-native-oh-tpl/react-native-bindingx": "file:../../node_modules/@react-native-oh-tpl/react-native-bindingx/harmony/bindingx.har"
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

### 3.配置 CMakeLists 和引入 ReactBindingXPackge

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-bindingx/src/main/cpp" ./bindingx)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_bindingx)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ReactBindingXPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ReactBindingXPackage>(ctx),
    };
}
...
```


### 4.在 ArkTs 侧引入 ReactBindingXPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {ReactBindingXPackage} from '@react-native-oh-tpl/react-native-bindingx/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ReactBindingXPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-bindingx Releases](https://github.com/react-native-oh-library/react-native-bindingx/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                                                                                                                                                                   | Type            | Required | Platform        | HarmonyOS Support  |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- | -------- | ----------------| ------------------ |
| bind              | Build a specific event type of binding instance. When the event is triggered, corresponding expression will be executed and touch off transform in specified element.         | string          | yes      | iOS/Android     |      yes           |
| unbind            | unbind specified binding instance.                                                                                                                                            | void            | yes      | iOS/Android     |      yes           |
| unbindAll         | unbind all binding instance                                                                                                                                                   | void            | yes      | iOS/Android     |      yes           |
| prepare           | launch bind. This method is only useful for pan type binding.                                                                                                                 | void            | yes      | iOS/Android     |      yes           |
| getComputedStyle  | get styles of specified view.                                                                                                                                                 | Promise<string> | yes      | iOS/Android     |      yes           |

## 遗留问题

## 其他

## 开源协议

本项目基于 [Apache License2.0](https://github.com/alibaba/bindingx/blob/master/LICENSE.md) ，请自由地享受和参与开源。
