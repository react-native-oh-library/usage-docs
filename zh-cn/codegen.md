
# Codegen 使用指导

## 简介

`CodeGen` 是 React Native 中的一项工具，用于简化和自动化代码生成。它可以帮助开发者生成桥接代码，使得 React Native 应用能够更方便地与原生代码进行交互。

在 Harmony OS RN 中已支持 codegen，并且大部分 Arkts 三方库已支持，因此在使用这些三方库之前需要通过 codegen 生成桥接代码，否则可能会出现如下报错：

```
cannot find module '@rnoh/react-native-openharmony/generated/ts' or its corresponding type declarations.
```

## 使用方式

### 运行 RN 工程 `MyProject/package.json` 的 codegen 脚本

> [!TIP] 运行前请确保三方库已经正确安装！

配置 codegen 脚本：

```json
...
  "scripts": {
    ...
  "codegen": "react-native codegen-harmony --cpp-output-path ./harmony/entry/src/main/cpp/generated --rnoh-module-path ./harmony/entry/oh_modules/@rnoh/react-native-openharmony"
  },
  ...
```

codegen-harmony 参数介绍：

- `rnoh-module-path`: Native 工程内， RNOH SDK 模块的相对路径（如果通过 har 包安装，则需指向安装后的地址，如：xxx/oh_modules/@rnoh/react-native-openharmony）
- `cpp-output-path`:` 指定⽤于存储⽣成的 C++ 文件的输出⽬录的相对路径，默认./harmony/entry/src/main/cpp/generated
- `project-root-path`: Native 工程根⽬录的相对路径

执行 codegen

```bash
npm run codegen
```

运行后，会在 `cpp-output-path` 参数指定的路径下生成 C++ 代码（若未指定则生成至默认路径），在 `rnoh-module-path`路径下生成 ArkTS/TS 代码（必须生成在 RN SDK 下）。

**注意事项**

脚本生成的代码需在项目工程中，否则会报如下错误：

```
[ERROR] Tried to remove files in path/generated and that path is outside current working directory
```

因此建议将原生工程置于 `RN` 工程内

```
.
├── ReactNativeProject // RN 工程
│   ├── android
│   ├── ios
│   ├── harmony // HarmonyOS 原生工程
```

### 配置 CMakeLists 和引入 RNOHGeneratedPackage（C++）

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
...
# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("${OH_MODULE_DIR}/rnoh-sample-package/src/main/cpp" ./sample-package)
# RNOH_END: add_package_subdirectories

+ file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")
add_library(rnoh_app SHARED
+ ${GENERATED_CPP_FILES}
 "./PackageProvider.cpp"
 "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)
# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
# RNOH_END: link_packages
...
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
+ #include "generated/RNOHGeneratedPackage.h"

using namespace rnoh;
std::vector<std::shared_ptr<Package>>
PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<RNOHGeneratedPackage>(ctx),
    };
}
```

