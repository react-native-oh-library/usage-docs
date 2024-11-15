> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>realm-js</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/realm/realm-js">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/realm/realm-js/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache-green.svg" alt="License" /> 
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/react-native-oh-library/realm-js)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/realm-js Releases](https://github.com/react-native-oh-library/realm-js/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install @react-native-oh-tpl/realm
npm install @react-native-oh-tpl/realm-react
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/realm
yarn add @react-native-oh-tpl/realm-react
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { SafeAreaView, View, Text, TextInput, FlatList, Pressable } from "react-native";
import { Realm, RealmProvider, useRealm, useQuery } from '@realm/react'

class Task extends Realm.Object {
  _id!: Realm.BSON.ObjectId;
  description!: string;
  isComplete!: boolean;
  createdAt!: Date;

  static generate(description: string) {
    return {
      _id: new Realm.BSON.ObjectId(),
      description,
      createdAt: new Date(),
    };
  }

  static schema = {
    name: 'Task',
    primaryKey: '_id',
    properties: {
      _id: 'objectId',
      description: 'string',
      isComplete: { type: 'bool', default: false },
      createdAt: 'date'
    },
  };
}

export default function AppWrapper() {
  return (
    <RealmProvider schema={[Task]}><TaskApp /></RealmProvider>
  )
}

function TaskApp() {
  const realm = useRealm();
  const tasks = useQuery(Task);
  const [newDescription, setNewDescription] = useState("")

  return (
    <SafeAreaView>
      <View style={{ flexDirection: 'row', justifyContent: 'center', margin: 10 }}>
        <TextInput
          value={newDescription}
          placeholder="Enter new task description"
          onChangeText={setNewDescription}
        />
        <Pressable
          onPress={() => {
            realm.write(() => {
              realm.create("Task", Task.generate(newDescription));
            });
            setNewDescription("")
          }}><Text>➕</Text></Pressable>
      </View>
      <FlatList data={tasks.sorted("createdAt")} keyExtractor={(item) => item._id.toHexString()} renderItem={({ item }) => {
        return (
          <View style={{ flexDirection: 'row', justifyContent: 'center', margin: 10 }}>
            <Pressable
              onPress={() =>
                realm.write(() => {
                  item.isComplete = !item.isComplete
                })
              }><Text>{item.isComplete ? "✅" : "☑️"}</Text></Pressable>
            <Text style={{ paddingHorizontal: 10 }} >{item.description}</Text>
            <Pressable
              onPress={() => {
                realm.write(() => {
                  realm.delete(item)
                })
              }} ><Text>{"🗑️"}</Text></Pressable>
          </View>
        );
      }} ></FlatList>
    </SafeAreaView >
  );
}
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
    "@react-native-oh-tpl/realm": "file:../../node_modules/@react-native-oh-tpl/realm/binding/harmony/realm.har"
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

### 3.配置 CMakeLists 和引入 RealmPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
+ set(CMAKE_CXX_STANDARD 17)
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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/realm/src/main/cpp" ./realm)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_realm)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RealmPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RealmPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNRealmPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNRealmPackage} from '@react-native-oh-tpl/realm/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNRealmPackage(ctx),
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/realm-js Releases](https://github.com/react-native-oh-library/realm-js/releases)

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- |-------- | -------- | ------------------ |
| useRealm() | Returns the instance of the Realm opened by the `RealmProvider` | function  |No       | All      | Yes      |
| useQuery() | Returns a Realm.Collection of Realm.Objects from a given type | function  |No       | All      | Yes      |
| new Realm(): Realm | Create a new Realm instance, at the default path | function  |No | All | Yes |
| new Realm(path): Realm | Create a new Realm instance at the provided path | function  |No | All | Yes |
| new Realm(config): Realm | Create a new Realm instance using the provided  config | function  |No | All | Yes |
| setLogLevel(level, category?): void | Sets the log level | function  |No | All | Yes |
| shutdown(): void | Closes all Realms, cancels all pendingRealm.open calls, clears internal caches, resets the logger and collects garbage. | function  |No | All | Yes |
| exists(path:): boolean | Checks if the Realm already exists on disk | function  |No | All | Yes |
| exists(config): boolean | Checks if the Realm already exists on disk | function  |No | All | Yes |
| deleteFile(config): void | Delete the Realm file for the given configuration | function  |No | All | Yes |
| open(): ProgressRealmPromise | Open the default Realm asynchronously with a promise | function  |No | All | Yes |
| open(path): ProgressRealmPromise | Open a Realm asynchronously with a promise | function  |No | All | Yes |
| open(config): ProgressRealmPromise | Open a Realm asynchronously with a promise | function  |No | All | Yes |
| isEmpty(): boolean | Indicates if this Realm contains any objects                 | function  |No | All | Yes |
| path(): string | The path to the file where this Realm is stored | function  |No | All | Yes |
| isReadOnly(): boolean | Indicates if this Realm was opened as read-only | function  |No | All | Yes |
| isInMemory(): boolean | Indicates if this Realm was opened in-memory | function  |No | All | Yes |
| schema(): CanonicalObjectSchema[] | A normalized representation of the schema provided in the Configuration when this Realm was constructed | function  |No | All | Yes |
| schemaVersion(): number | The current schema version of the Realm | function  |No | All | Yes |
| isInTransaction(): boolean | Indicates if this Realm is in a write transaction | function  |No | All | Yes |
| isInMigration(): boolean | Indicates if this Realm is in migration | function  |No | All | Yes |
| isClosed(): boolean | Indicates if this Realm has been closed | function  |No | All | Yes |
| close(): void | Closes this Realm so it may be re-opened with a newer schema version | function  |No | All | Yes |
| create() | Create a new RealmObject of the given type and with the specified properties | function  |No | All | Yes |
| delete() | Deletes the provided Realm object, or each one inside the provided collection | function |No | All | Yes |
| deleteAll(): void | This will delete **all** objects in the Realm! | function |No | All | Yes |
| objectForPrimaryKey() | Searches for a Realm object by its primary key | function |No | All | Yes |
| objects() | Returns all objects of the given type in the Realm | function |No | All | Yes |
| write(callback) | Synchronously call the provided callback inside a write transaction | function |No | All | Yes |
| writeCopyTo(config): void | Writes a compacted copy of the Realm with the given configuration | function |No | All | Yes |

## 遗留问题

- [ ] realm-js库目前只能在root后的手机上使用。[issue#2](https://github.com/react-native-oh-library/realm-js/issues/2)

## 其他

## 开源协议

本项目基于 [The Apache License (Apache)](https://github.com/realm/realm-js/blob/main/LICENSE) ，请自由地享受和参与开源。