> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-mmkv-storage</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ammarahm-ed/react-native-mmkv-storage">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ammarahm-ed/react-native-mmkv-storage/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-mmkv-storage)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-mmkv-storage Releases](https://github.com/react-native-oh-library/react-native-mmkv-storage/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-mmkv-storage@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-mmkv-storage@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import React, {useCallback} from 'react';
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
} from 'react-native';
import {MMKVLoader, create} from 'react-native-mmkv-storage';

const storage = new MMKVLoader().withEncryption().initialize();

const storage2 = new MMKVLoader().withInstanceID('storage2').initialize();

const useStorage = create(storage);
const useStorage2 = create(storage2);

const App = () => {
  const [user, setUser] = useStorage('user', 'robert');
  const [age, setAge] = useStorage2('age', 24);

  const getUser = useCallback(() => {
    let users = ['andrew', 'robert', 'jack', 'alison'];
    let _user =
      users[
        users.indexOf(user) === users.length - 1 ? 0 : users.indexOf(user) + 1
      ];
    return _user;
  }, [user]);

  const buttons = [
    {
      title: 'setString',
      onPress: () => {
        storage.setString('user', getUser());
      },
    },
    {
      title: 'setMulti',
      onPress: () => {
        const user = getUser();
        console.log('setting user to', user);
        storage.setMultipleItemsAsync([['user', user]], 'string');
      },
    },
    {
      title: 'getMulti',
      onPress: async () => {
        console.log(await storage.getMultipleItemsAsync(['user'], 'string'));
      },
    },
    {
      title: 'setUser',
      onPress: () => {
        setUser(getUser());
      },
    },
    {
      title: 'setAge',
      onPress: () => {
        setAge((age: number) => {
          return age + 1;
        });
      },
    },
    {
      title: 'clearAll',
      onPress: () => {
        storage.clearStore();
      },
    },
    {
      title: 'removeByKeys',
      onPress: async () => {
        const keys = await storage.indexer.getKeys();
        console.log(keys);
        storage.removeItems(keys);
        storage.clearStore();
        console.log(await storage.indexer.getKeys());
      },
    },
  ];

  return (
    <>
      <StatusBar barStyle="dark-content" />
      <SafeAreaView style={styles.container}>
        <View style={styles.header}>
          <Text style={styles.headerText}>
            I am {user} and I am {age} years old.
          </Text>
        </View>
        <ScrollView
          style={{
            width: '100%',
            paddingHorizontal: 12,
          }}>
          {buttons.map(item => (
            <Button
              key={item.title}
              title={item.title}
              onPress={item.onPress}
            />
          ))}
        </ScrollView>
      </SafeAreaView>
    </>
  );
};

const Button = ({title, onPress}: {title: string; onPress: () => void}) => {
  return (
    <TouchableOpacity style={styles.button} onPress={onPress}>
      <Text style={{color: 'white'}}>{title}</Text>
    </TouchableOpacity>
  );
};

export default App;

const styles = StyleSheet.create({
  container: {
    alignItems: 'center',
    flex: 1,
    backgroundColor: 'white',
  },
  header: {
    width: '100%',
    backgroundColor: '#f7f7f7',
    marginBottom: 20,
    justifyContent: 'center',
    alignItems: 'center',
    paddingVertical: 50,
  },
  button: {
    width: '100%',
    height: 50,
    backgroundColor: 'orange',
    justifyContent: 'center',
    alignItems: 'center',
    borderRadius: 10,
    marginBottom: 10,
  },
  headerText: {fontSize: 40, textAlign: 'center', color: 'black'},
});
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
    "@react-native-oh-tpl/react-native-mmkv-storage": "file:../../node_modules/@react-native-oh-tpl/react-native-mmkv-storage/harmony/mmvk-storage.har"
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

### 3.配置 CMakeLists 和引入 RNOHMMKVStoragePackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-mmkv-storage/src/main/cpp" ./mmkv-storage)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_mmkv_storage)
# RNOH_END: manual_package_linking_2

```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "MMKVNativePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
    	std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RNOHMMKVStoragePackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNMMKVStoragePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
+ import {RNMMKVStoragePackage} from '@react-native-oh-tpl/react-native-mmkv-storage'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNMMKVStoragePackage(ctx),
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-mmkv-storage Releases](https://github.com/react-native-oh-library/react-native-mmkv-storage/releases)


## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                         | Description                                                  | type     | Required | Platform | HarmonyOS Support |
| ---------------------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| setString                    | Sets a string value in storage for the given key.            | Function | no       | All      | yes               |
| getString                    | Gets a string value for a given key.                         | Function | no       | All      | yes               |
| setInt                       | Sets a number value in storage for the given key.            | Function | no       | All      | yes               |
| getInt                       | Gets a number value for a given key.                         | Function | no       | All      | yes               |
| setBool                      | Sets a boolean value in storage for the given key.           | Function | no       | All      | yes               |
| getBool                      | Gets a boolean value for a given key.                        | Function | no       | All      | yes               |
| setMap                       | Sets an object to storage for the given key.                 | Function | no       | All      | yes               |
| getMap                       | Gets an object from storage.                                 | Function | no       | All      | yes               |
| setArray                     | Sets an array to storage for the given key.                  | Function | no       | All      | yes               |
| getArray                     | Gets an array from storage.                                  | Function | no       | All      | yes               |
| getMultipleItems             | Retrieve multiple Objects for a given array of keys. Currently will work only if data for all keys is an Object | Function | no       | All      | yes               |
| setStringAsync               | Sets a string value in storage for the given key.            | Function | no       | All      | yes               |
| getStringAsync               | Gets a string value for a given key.                         | Function | no       | All      | yes               |
| setIntAsync                  | Sets a number value in storage for the given key.            | Function | no       | All      | yes               |
| getIntAsync                  | Gets a number value for a given key.                         | Function | no       | All      | yes               |
| setBoolAsync                 | Sets a boolean value in storage for the given key.           | Function | no       | All      | yes               |
| getBoolAsync                 | Gets a boolean value for a given key.                        | Function | no       | All      | yes               |
| setMapAsync                  | Sets an object to storage for the given key.                 | Function | no       | All      | yes               |
| getMapAsync                  | Gets an object from storage.                                 | Function | no       | All      | yes               |
| setArrayAsync                | Sets an array to storage for the given key.                  | Function | no       | All      | yes               |
| getArrayAsync                | Sets an array to storage for the given key.                  | Function | no       | All      | yes               |
| setMultipleItemsAsync        | Sets multiple Objects for a given array of keys. Currently will work only if data for all keys is an Object. | Function | no       | All      | yes               |
| getMultipleItemsAsync        | Retrieve multiple Objects for a given array of keys. Currently will work only if data for all keys is an Object. | Function | no       | All      | yes               |
| withInstanceID               | Specifies that the MMKV Instance should be created with the given ID. This way multiple intances can be created. | Function | no       | All      | yes               |
| setAccessibleMode (iOS only) | Choose the accessibility mode for secure key storage (IOS ONLY); | Function | no       | iOS      | no                |
| withServiceName (iOS only)   | Sets the [kSecAttrService](https://developer.apple.com/documentation/security/ksecattrservice) option for secure key storage (IOS ONLY); | Function | no       | iOS      | no                |
| removeItem                   | Remove an item for a given key.                              | Function | no       | All      | yes               |
| clearStore                   | Clear the storage.                                           | Function | no       | All      | yes               |
| clearMemoryCache             | Clear the storage from memory.                               | Function | no       | All      | yes               |
| getAllMMKVInstanceIDs        | Returns a list of all the MMKV Instance IDs created.         | Function | no       | All      | yes               |
| getCurrentMMKVInstances      | get the currently initialized instance IDs.                  | Function | no       | All      | yes               |
| hasKey                       | Check if any data exists for a given key.                    | Function | no       | All      | yes               |
| getKey                       | get the encryption key for the current MMKV instance         | Function | no       | All      | yes               |

## HOOKS

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name           | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| useIndex       | take an array of keys and returns an array of values for those keys | Function | no       | All      | yes               |
| useMMKVRef     | A persisted ref that will always write every change to it's `current` value to storage. It doesn't matter if you reload the app or restart it. Everything will be in place on app load. | Function | no       | All      | yes               |
| useMMKVStorage | always write every change in storage and update your app UI instantly | Function | no       | All      | yes               |



## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ammarahm-ed/react-native-mmkv-storage/blob/master/LICENSE) ，请自由地享受和参与开源。