<p align="center">
  <h1 align="center"> <code>@react-native-community/checkbox</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-native-checkbox">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-checkbox/react-native-checkbox/blob/develop/LICENSE">
        <img src="https://img.shields.io/npm/l/@react-native-community/checkbox.svg" alt="License" />
    </a>
</p>

## 安装与使用

目前 React-Native-OpenHarmony(RNOH) 三方库的npm包部署在私仓，需要通过github token来获取访问权限。

在与 `package.json` 文件相同的目录中，创建或编辑 `.npmrc` 文件以包含指定 GitHub Packages URL 和托管包的命名空间的行。 将TOKEN替换为RNOH三方库指定的token。
```json
@react-native-oh-library:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=TOKEN
```

进入到工程目录并输入以下命令：

```bash
yarn add @react-native-community/checkbox@npm:@react-native-oh-library/checkbox
```

或者

```bash
npm install @react-native-community/checkbox@npm:@react-native-oh-library/checkbox
```

下面的代码展示了这个库的基本使用场景：

```js
import CheckBox from '@react-native-community/checkbox';

<CheckBox
                disabled={false}
                value={toggleCheckBox}
                style={{ width: 70, height: 70 }}
                tintColor={'red'}
                onCheckColor={'green'}
                onChange={(event) => {
                    console.log("" + event.nativeEvent.value)
                    setMsg2("onChange" + event.nativeEvent.target)
                    setValue(event.nativeEvent.value)
                }}
                markSize={70}
                strokeColor={'yellow'}
                strokeWidth={5}
                onValueChange={(newValue) => {
                    setToggleCheckBox(newValue)
                    setMsg("onValueChange----")
                }}
            />
```

## Link

目前鸿蒙暂不支持 AutoLink，所以Link步骤需要手动配置。

首先需要使用DevEco Studio打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入
打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-checkbox": "file:../../node_modules/@react-native-community/checkbox/harmony/checkbox.har"
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
    "rnoh-checkbox": "file:../../node_modules/@react-native-community/checkbox/harmony/checkbox"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置CMakeLists和引入CheckboxPackge

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-checkbox/src/main/cpp" ./checkbox)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_checkbox)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "CheckboxPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<CheckboxPackage>(ctx)
    };
}
```


### 在ArkTs侧引入 Checkbox 组件

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
+ import { RNCCheckbox, CHECKBOX_TYPE } from "rnoh-checkbox"

  @Builder
  function CustomComponentBuilder(ctx: ComponentBuilderContext) {
    if (ctx.descriptor.type === SAMPLE_VIEW_TYPE) {
      SampleView({
        ctx: ctx.rnohContext,
        tag: ctx.descriptor.tag,
        buildCustomComponent: CustomComponentBuilder
      })
    } 
+   else if (ctx.descriptor.type === CHECKBOX_TYPE) {
+     RNCCheckbox({
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
要使用此库，需要使用正确的React-Native和RNOH版本。另外，还需要使用配套的 DevEco Studio 和 手机ROM。

| `@react-native-oh-library/checkbox` Version | Required React Native Version | Required RNOH Version | Required DevEco Studio Version | Required ROM Version |
| ---------------------------------------- | ----------------------------- | ----------------------------- | ----------------------------- | ----------------------------- |
| `0.5.16-0.0.2`                                  | `>=0.72.5`                    | `>=0.72.6` | `>=4.0.3.501`                    | `>=OpenHarmony 4.10.10` |


## 属性


| 名称                    | 说明                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | 类型                                         | 是否必填 | 原库平台     | 鸿蒙支持 |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- | -------- | ------------ | -------- |
| `onChange`              | Invoked on change with the native event.                                                                                                                                                                                                                                                                                                                                                                                                     | function                                         | No       | All          | yes      |
| `onValueChange`              | Invoked with the new boolean value when it changes.                                                                                                                                                                                                                                                                                                                                                                                                     | function                                         | No       | All          | yes      |
| `value`              |  The value of the checkbox. If true the checkbox will be turned on. Default value is false.                                                                                                                                                                                                                                                                                                                                                                                                    | boolean                                         | No       | All          | yes      |
| `testID`              | Used to locate this view in end-to-end tests.                                                                                                                                                                                                                                                                                                                                                                                                     | string                                         | No       | All          | yes      |
| `disabled`              | If true the user won't be able to toggle the checkbox. Default value is false.                                                                                                                                                                                                                                                                                                                                                                                                     | bool                                         | No       | All          | yes      |
| `onCheckColor`              | Color of the check box when it is selected.                                                                                                                                                                                                                                                                                                                                                                                                     | Color                                         | No       | ios & harmony          | yes      |
| `tintColor`              | Border color of the check box when it is not selected.                                                                                                                                                                                                                                                                                                                                                                                                     | Color                                         | No       | ios & harmony          | yes      |
| `markSize`              | Size of the internal mark. The default size is the same as the width of the check box.This parameter cannot be set in percentage. If it is set to an invalid value, the default value is used.                                                                                                                                                                                                                                                                                                                                                                                                     | number                                         | No       | harmony          | yes      |
| `strokeWidth`              | Stroke width of the internal mark. This parameter cannot be set in percentage. If it is set to an invalid value, the default value is used.                                                                                                                                                                                                                                                                                                                                                                                                     | number                                         | No       | harmony          | yes      |
| `strokeColor`              | Color of the internal mark.                                                                                                                                                                                                                                                                                                                                                                                                     | Color                                         | No       | harmony          | yes      |

## 遗留问题

## 其他

## 开源协议
本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-checkbox/blob/harmony/LICENSE) ，请自由地享受和参与开源。