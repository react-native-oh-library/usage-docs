> Template version: v0.2.2

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



> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-mmkv-storage)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package:[@react-native-oh-tpl/react-native-mmkv-storage Releases](https://github.com/react-native-oh-library/react-native-mmkv-storage/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-mmkv-storage": "file:../../node_modules/@react-native-oh-tpl/react-native-mmkv-storage/harmony/mmvk-storage.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

### 3. Configuring CMakeLists and Introducing xxx Package

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
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

```
> [!Tip] Note: NODE_MODULES is the installation path of the source database. You can define NODE_MODULES based on the installation path of the source database.
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4. Introducing RNMMKVStoragePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import {RNMMKVStoragePackage} from '@react-native-oh-tpl/react-native-mmkv-storage'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNMMKVStoragePackage(ctx),
  ];
}

```

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-mmkv-storage Releases](https://github.com/react-native-oh-library/react-native-mmkv-storage/releases)

### Permission Requirements

Some functions and interfaces of this library require the Store Persistent Data permission ohos.permission.STORE_PERSISTENT_DATA. The permission must be configured in the module.json5 file in entry/src/main.

####  Add permissions to the module.json5 file in the entry directory.

Open `entry/src/main/module.json5` and add the following information:
```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.STORE_PERSISTENT_DATA",
+  },
+  
]
```

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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
| initialize                   | Initialize the MMKV Instance with the selected properties. Returns an MMKV Instance that you can use. | Function | no       | All      | yes               |
| withInstanceID               | Specifies that the MMKV Instance should be created with the given ID. This way multiple intances can be created. | Function | no       | All      | yes               |
| withEncryption               | Encrypt the MMKV instance on initialization.                 | Function | no       | All      | yes               |
| encryptWithCustomKey         | You can also specify your own password to encrypt the storage. | Function | no       | All      | yes               |
| setAccessibleMode (iOS only) | Choose the accessibility mode for secure key storage (IOS ONLY); | Function | no       | iOS      | no                |
| withServiceName (iOS only)   | Sets the [kSecAttrService](https://developer.apple.com/documentation/security/ksecattrservice) option for secure key storage (IOS ONLY); | Function | no       | iOS      | no                |
| removeItem                   | Remove an item for a given key.                              | Function | no       | All      | yes               |
| clearStore                   | Clear the storage.                                           | Function | no       | All      | yes               |
| clearMemoryCache             | Clear the storage from memory.                               | Function | no       | All      | yes               |
| getCurrentMMKVInstances      | get the currently initialized instance IDs.                  | Function | no       | All      | yes               |
| hasKey                       | Check if any data exists for a given key.                    | Function | no       | All      | yes               |
| getKey                       | get the encryption key for the current MMKV instance         | Function | no       | All      | yes               |

## HOOKS

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name           | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| useIndex       | take an array of keys and returns an array of values for those keys | Function | no       | All      | yes               |
| useMMKVRef     | A persisted ref that will always write every change to it's `current` value to storage. It doesn't matter if you reload the app or restart it. Everything will be in place on app load. | Function | no       | All      | yes               |
| useMMKVStorage | always write every change in storage and update your app UI instantly | Function | no       | All      | yes               |



## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ammarahm-ed/react-native-mmkv-storage/blob/master/LICENSE). 