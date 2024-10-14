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

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/realm-js Releases](https://github.com/react-native-oh-library/realm-js/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

#### **npm**

```bash
npm install @react-native-oh-tpl/realm@file:#
npm install @react-native-oh-tpl/realm-react@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/realm@file:#
yarn add @react-native-oh-tpl/realm-react@file:#
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

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

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

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

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
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| useRealm() | Returns the instance of the Realm opened by the `RealmProvider` | function  | yes | All      | yes |
| useObject(type, primaryKey) | Returns a Realm.Object from a given type and value of primary key | function  | yes | All      | yes |
| useQuery() | Returns a Realm.Collection of Realm.Objects from a given type. | function  | yes | All      | yes |
| useUser() | Hook to access the currently authenticated Realm user from the UserProvider context.| function  | yes | All      | yes |
| useAuth() | Hook providing operations and corresponding state for authenticating with an Atlas App. | function  | yes | All      | yes |
| logIn(credentials) | Log in with a Realm.Credentials instance. This allows login with any authentication mechanism supported by Realm. | function  | yes | All      | yes |
| logInWithAnonymous() | Log in with the Anonymous authentication provider | function  | yes | All      | yes |
| logInWithApiKey(key) | Log in with an API key. | function  | yes | All      | yes |
| logInWithEmailPassword(credentials) | Log in with Email / Password.| function  | yes | All      | yes |
| logInWithJWT(credentials) | Log in with a JSON Web Token (JWT). | function  | yes | All      | yes |
| logInWithGoogle(credentials) | Log in with Google. | function  | yes | All      | yes |
| logInWithApple(idToken) | Log in with Apple. | function  | yes | All      | yes |
| logInWithFacebook(accessToken) | Log in with Facebook. |function  | yes | All      | yes |
| logInWithFunction(payload) | Log in with a custom function. | function  | yes | All      | yes |
| logOut() | Log out the current user. | function  | yes | All      | yes |
| useEmailPasswordAuth() | Hook providing operations and corresponding state for authenticating with an Atlas App with Email/Password. | function  | yes | All      | yes |
| logIn(credentials) | Convenience function to log in a user with an email and password - users. | function  | yes | All      | yes |
| logOut() | Log out the current user.| function  | yes | All      | yes |
| register(args) | Register a new user. | function  | yes | All      | yes |
| Confirm(args) | Confirm a user's account by providing the `token` and `tokenId` received. | function  | yes | All      | yes |
| resendConfirmationEmail(args) | Resend a user's confirmation email. | function  | yes | All      | yes |
| retryCustomConfirmation(args) | Retry the custom confirmation function for a given user. | function  | yes | All      | yes |
| sendResetPasswordEmail(args) | Send a password reset email for a given user. | function  | yes | All      | yes |
| resetPassword(args) | Complete resetting a user's password. | function  | yes | All      | yes |
| callResetPasswordFunction(args, restArgs) | Call the configured password reset function, passing in any additional arguments to the function. | function  | yes | All      | yes |
| useApp() | Hook to access the current Realm.App from the AppProvider context. | function  | yes | All      | yes |

## Known Issues
- [ ] Problem with the get_synchronized_realm, sync_session and get_latest_subscription_set methods in the Realm-js library: Currently unavailable, support will need to be provided by the dependent realm-core third-party library before implementation. [issue#1](https://github.com/react-native-oh-library/realm-js/issues/1)
- [ ] The realm-js library can currently only be used on rooted phones. [issue#2](https://github.com/react-native-oh-library/realm-js/issues/2)

## Others

## License

This project is licensed under [Apache License (Apache)](https://github.com/realm/realm-js/blob/main/LICENSE).

