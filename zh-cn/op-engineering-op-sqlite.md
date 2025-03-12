模板版本：v0.2.2

<p align="center">
  <h1 align="center"> 
    <code>@op-engineering/op-sqlite</code> 
  </h1>
</p>

<p align="center">
    <a href="https://github.com/OP-Engineering/op-sqlite">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/OP-Engineering/op-sqlite/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/op-sqlite)


## 安装与使用


请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/op-sqlite Releases](https://github.com/react-native-oh-library/op-sqlite/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/op-sqlite
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/op-sqlite
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。


```js

import React, { useEffect, useState } from 'react';
import {
    SafeAreaView,
    Text,
    TouchableOpacity,
    View,
} from 'react-native';

import {
    open,
    type DB
} from '@op-engineering/op-sqlite';
import { HARMONY_DATABASE_PATH } from '@react-native-oh-tpl/op-sqlite';

export default function OpSqliteExample() {
    
    return (
        <SafeAreaView style={{ flex: 1, backgroundColor: '#fff' }}>
            <View style={{ flex: 1, backgroundColor: '#fff' }}>
                <TouchableOpacity
                    style={{ padding: 5 }}
                    onPress={() => {
                        let db:DB = open({
                            name: 'helloDb.sqlite',
                            encryptionKey: 'test',
                            location: HARMONY_DATABASE_PATH
                        });
                    }}>
                    <Text style={{ color: 'red' }}>
                       tap to {'openDB'}
                    </Text>
                </TouchableOpacity>
            </View>

        </SafeAreaView>
    );
}


```

详细参考[源库文档地址](https://ospfranco.notion.site/OP-SQLite-Documentation-a279a52102464d0cb13c3fa230d2f2dc?pvs=4)


## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1. 在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/op-sqlite": "file:../../node_modules/@react-native-oh-tpl/op-sqlite/harmony/rn_op_sqlite.har"
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

### 3. 配置 CMakeLists 和引入 RNOpSqlitePackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/op-sqlite/src/main/cpp" ./rn_op_sqlite)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_rn_op_sqlite)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNOpSqlitePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNOpSqlitePackage>(ctx)
    };
}
```

### 4. 在 ArkTs 侧引入 RNOpSqlitePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，或者`entry/src/main/ets/rn/RNPackagesFactory.ts`，添加：

```diff
+ import { RNOpSqlitePackage } from '@react-native-oh-tpl/op-sqlite/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNOpSqlitePackage(ctx),
  ];
}
```
### 5.在ide的工程根目录创建package.json文件,并配置参数

```diff
{
...
  "op-sqlite": {
    ...
    "sqlcipher": false,
    "libsql": false, //此处设置为ture即为远程数据库模式
  },
}
```

### 6. 在 ArkTs 侧引入 opSqlitePlugin

打开 `entry/hvigorfile.ts`，添加：

```diff
+ import { hapTasks, OhosHapContext, OhosPluginId, Target } from '@ohos/hvigor-ohos-plugin';
+ import { HvigorPlugin, HvigorNode, getNode } from '@ohos/hvigor';
+ import { opSqlitePlugin } from './oh_modules/@react-native-oh-tpl/op-sqlite/hvigorfile.ts';

+const path = require('path');
+const rootRNPackagePath = path.join(__dirname, '../package.json'); //此处根据实际package路径来进行配置

export default {
    system: hapTasks,
+   plugins: [opSqlitePlugin(rootRNPackagePath)]
}
```

### 6. 运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/op-sqlite Releases](https://github.com/react-native-oh-library/op-sqlite/releases)


### 应用权限申请

#### 在 entry 目录下的module.json5中添加权限
在 `YourProject/entry/src/main/module.json5`补上配置

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

    "requestPermissions": [
+     { "name": "ohos.permission.INTERNET" },
    ]
  }
}
```


## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| getConstants  | Return the corresponding database/file storage sandbox path.         |  () => {IOS_DOCUMENT_PATH,IOS_LIBRARY_PATH,ANDROID_DATABASE_PATH,ANDROID_FILES_PATH,ANDROID_EXTERNAL_FILES_PATH,HARMONY_DATABASE_PATH,HARMONY_FILES_PATH,}  | no | all      | yes |
| openSync  | Synchronize the local database to the remote database and open the database.         | (options: {url: string;authToken: string;name: string;location?: string;}) => DB; | no | all      | yes |
| openRemote  | Open the remote database. | (options: { url: string; authToken: string }) => DB;  | no | all      | yes |
| open  | Open the database.encryptionKey indicates the key string required for using sqlcipher.After sqlcipher is enabled, encryptionKey is supported.         | (options: {name: string;location?: string;encryptionKey?: string;}) => DB;  | no | all      | yes |
| isSQLCipher  | Whether SQL cipher is enabled.(SQLCipher is an open source SQLite extension that provides transparent 256-bit AES full database encryption.)         | () => boolean;  | no | all      | yes |
| isLibsql  | Indicates whether to enable isLibsql. After isLibsql is enabled, the remote database and database synchronization interface can be enabled         | () => boolean;  | no | all      | yes |
| moveAssetsDatabase  | Copy the database to the specified path.         | async (args: {filename: string;path?: string;overwrite?: boolean;}) => Promise<boolean>  | no | all      | yes |

### DB

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| close  | Shut down the database.         | () => void;  | no | all      | yes |
| delete  | Deleting a database         | (location?: string) => void;  | no | all      | yes |
| attach  | Attaching other databases to the primary database by aliasing          | (mainDbName: string,dbNameToAttach: string,alias: string,location?: string) => void;  | no | all      | yes |
| detach  | Detaching Other Databases from the Primary Database by Alias         | (mainDbName: string, alias: string) => void;  | no | all      | yes |
| transaction  | Operate through database transactions         | (fn: (tx: Transaction) => Promise<void>) => Promise<void>;  | no | all      | yes |
| execute  | Execute SQL statements in the database.         | (query: string, params?: any[]) => QueryResult;  | no | all      | yes |
| executeWithHostObjects  | The database query statement is used to quickly query a large amount of data. However, the return attribute access speed is slow.         | (query: string,params?: any[]) => Promise<QueryResult>;  | no | all      | yes |
| executeBatch  | Query and execute a large number of statements.         | (commands: SQLBatchTuple[]) => BatchQueryResult;  | no | all      | yes |
| loadFile  | Load the local SQL file.         | (location: string) => Promise<FileLoadResult>;  | no | all      | yes |
| updateHook  | Database update hook callback         | (callback?:((params: \{table: string;operation: UpdateHookOperation;row?: any;rowId: number;}) => void) \| null) => void;  | no | all      | yes |
| commitHook  | Database commit hook callback.         | (callback?: (() => void) \| null) => void;  | no | all      | yes |
| rollbackHook  | Database rollback hook callback.         | (callback?: (() => void) \| null) => void;  | no | all      | yes |
| prepareStatement  | You can reuse a query statement, use bind to change parameters, and execute the execution result.        | (query: string) => PreparedStatementObj;  | no | all      | yes |
| loadExtension  | Load SQL extension.         | (path: string, entryPoint?: string) => void;  | no | all      | yes |
| executeRaw  | If you do not care about the key, you can use this API to simplify the execution and return a component array.This should be much faster than the normal operation because you don't need to create objects with the same key.         | (query: string,params?: any[]) => Promise<any[]>;  | no | all      | yes |
| getDbPath  | Obtaining the Database Path.         | (location?: string) => string;  | no | all      | yes |
| reactiveExecute  | Responsive statement query         | (params: {query: string;arguments: any[];fireOn: {table: string;ids?: number[];}[];callback: (response: any) => void;}) => () => void;  | no | all      | yes |
| sync  | Database synchronization operation, which is supported after isLibsql is enabled.         | () => void | no | all      | yes |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/OP-Engineering/op-sqlite/blob/main/LICENSE) ，请自由地享受和参与开源。
