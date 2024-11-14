> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>realm-js</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/realm/realm-js>">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/realm/realm-js/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/realm-js)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/realm-js Releases](https://github.com/react-native-oh-library/realm-js/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:


Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/realm": "file:../../node_modules/@react-native-oh-tpl/realm/binding/harmony/realm.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing RealmPackage Package

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4. Introducing RNRealmPackage Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/realm-js Releases](https://github.com/react-native-oh-library/realm-js/releases)



## APIs (TurboModules, If Any)

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

- [ ] The realm-js library can currently only be used on rooted phones. [issue#2](https://github.com/react-native-oh-library/realm-js/issues/2)

## Others

## License

This project is licensed under [Apache License (Apache)](https://github.com/realm/realm-js/blob/main/LICENSE).

