<p align="center">
  <h1 align="center"> <code>@react-native-masked-view/masked-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-masked-view/masked-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://opensource.org/license/mit/">
        <img src="https://img.shields.io/npm/l/@react-native-masked-view/masked-view.svg?style=flat-square" alt="License" />
    </a>
</p>



## 安装与使用

> [!tip] 目前 React-Native-OpenHarmony(RNOH) 三方库的 npm 包部署在私仓，需要通过 github token 来获取访问权限。

在与 `package.json` 文件相同的目录中，创建或编辑 `.npmrc` 文件以包含指定 GitHub Packages URL 和托管包的命名空间的行。 将 TOKEN 替换为 RNOH 三方库指定的 token。

```bash
@react-native-oh-library:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=TOKEN
```

进入到工程目录并输入以下命令：

```bash
yarn add @react-native-masked-view/masked-view@npm:@react-native-oh-library/masked-view
```

或者

```bash
npm install @react-native-masked-view/masked-view@npm:@react-native-oh-library/masked-view
```

下面的代码展示了这个库的基本使用场景：

```js
import MaskedView from '@react-native-masked-view/masked-view';

<MaskedView
      style={{ flex: 1, flexDirection: 'row', height: '100%' }}
      maskElement={
        <View
          style={{
            // Transparent background because mask is based off alpha channel.
            backgroundColor: 'transparent',
            flex: 1,
            justifyContent: 'center',
            alignItems: 'center',
          }}
        >
          <Text
            style={{
              fontSize: 60,
              color: 'black',
              fontWeight: 'bold',
            }}
          >
            Basic Mask
          </Text>
        </View>
      }
    >
      {/* Shows behind the mask, you can put anything here, such as an image */}
      <View style={{ flex: 1, height: '100%', backgroundColor: '#324376' }} />
      <View style={{ flex: 1, height: '100%', backgroundColor: '#F5DD90' }} />
      <View style={{ flex: 1, height: '100%', backgroundColor: '#F76C5E' }} />
      <View style={{ flex: 1, height: '100%', backgroundColor: '#e1e1e1' }} />
    </MaskedView>
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入
打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-masked-view": "file:../../node_modules/@react-native-masked-view/masked-view/harmony/masked_view.har",
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码
打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-masked-view": "file:../../node_modules/@react-native-masked-view/masked-view/harmony/masked_view"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 MaskedPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-masked-view/src/main/cpp" ./masked-view)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_masked_view)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "MaskedPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<MaskedPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 MaskedView 组件

打开 `entry/src/main/ets/pages/index.ets`，添加：

```diff
import {
  RNApp,
  ComponentBuilderContext,
  RNAbility,
  AnyJSBundleProvider,
  MetroJSBundleProvider,
  ResourceJSBundleProvider,
} from 'rnoh'
import { SampleView, SAMPLE_VIEW_TYPE, PropsDisplayer } from "rnoh-sample-package"
import { createRNPackages } from '../RNPackagesFactory'
+ import { MaskedView, MASKED_VIEW_TYPE } from "rnoh-masked-view"

  @Builder
  function CustomComponentBuilder(ctx: ComponentBuilderContext) {
    if (ctx.descriptor.type === SAMPLE_VIEW_TYPE) {
      SampleView({
        ctx: ctx.rnohContext,
        tag: ctx.descriptor.tag,
        buildCustomComponent: CustomComponentBuilder
      })
    }
+   else if (ctx.descriptor.type === MASKED_VIEW_TYPE) {
+     MaskedView({
+       ctx: ctx.rnohContext,
+       tag: ctx.descriptor.tag,
+       buildCustomComponent: CustomComponentBuilder
+     })
+   }
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

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

| `@react-native-oh-library/masked-view` Version | Required React Native Version | Required RNOH Version | Required DevEco Studio Version | Required ROM Version  |
| ----------------------------------------- | ----------------------------- | --------------------- | ------------------------------ | --------------------- |
| `0.2.9-0.0.1`                             | `0.72.5`                      | `0.72.10`             | `4.0.3.601`                    | `OpenHarmony 4.10.10` |

## 属性

| 名称                    | 说明                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | 类型                                         | 是否必填 | 原库平台     | 鸿蒙支持 |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- | -------- | ------------ | -------- |
| `maskElement`                 | 遮罩元素                                                                                                                                                                                                                                                                                                                                                                               | element                                   | yes       | All          | yes      |
`androidRenderingMode`                 | 安卓渲染模式                                                                                                                                                                                                                                                                                                                                                                               | software, hardware                                   | no       | android          | no      |



## 遗留问题

- [ ] 鸿蒙侧未实现遮罩效果[issue#1](https://github.com/react-native-oh-library/masked-view/issues/1)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-masked-view/masked-view/blob/master/LICENSE) ，请自由地享受和参与开源。