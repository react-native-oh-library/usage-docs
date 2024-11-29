
> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-custom-keyboard</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/reactnativecn/react-native-custom-keyboard">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-custom-keyboard)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-custom-keyboard Releases](https://github.com/react-native-oh-library/react-native-custom-keyboard/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-custom-keyboard
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-custom-keyboard
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';  
import {  
  StyleSheet,  
  Text,  
  View,  
  TouchableOpacity,  
} from 'react-native';  

import {  
  CustomTextInput,  
  register,  
  insertText,  
  backSpace,  
} from 'react-native-custom-keyboard';  

/**  
 * Custom Keyboard Component  
 */  
const MyKeyboard = ({ tag }) => {  
  const onPress = (value) => {  
    insertText(tag, value);  
  };  

  return (  
    <View style={styles.keyboard}>  
      {[[1, 2, 3], [4, 5, 6], [7, 8, 9]].map((row, rowIndex) => (  
        <View style={styles.row} key={`row-${rowIndex}`}>  
          {row.map((num) => (  
            <View style={styles.button} key={num}>  
              <TouchableOpacity onPress={() => onPress(num.toString())}>  
                <Text style={styles.buttonLabel}>{num}</Text>  
              </TouchableOpacity>  
            </View>  
          ))}  
        </View>  
      ))}  
      <View style={styles.row}>  
        <View style={styles.button}>  
          <TouchableOpacity onPress={() => onPress('0')}>  
            <Text style={styles.buttonLabel}>0</Text>  
          </TouchableOpacity>  
        </View>  
        <View style={styles.button}>  
          <TouchableOpacity onPress={() => onPress('.')}>  
            <Text style={styles.buttonLabel}>.</Text>  
          </TouchableOpacity>  
        </View>  
        <View style={styles.button}>  
          <TouchableOpacity onPress={() => backSpace(tag)}>  
            <Text style={styles.buttonLabel}>←</Text>  
          </TouchableOpacity>  
        </View>  
      </View>  
    </View>  
  );  
};  

register('price', () => MyKeyboard);  

/**  
 * Main Application Component  
 */  
const App = () => {  
  return (  
    <View style={styles.container}>  
      <CustomTextInput  
        customKeyboardType="price"  
        style={styles.input}  
      />  
    </View>  
  );  
};  

export default App;  

/**  
 * Style Definition  
 */  
const styles = StyleSheet.create({  
  container: {  
    flex: 1,  
    justifyContent: 'center',  
    alignItems: 'center',  
    backgroundColor: '#F5FCFF',  
  },  
  input: {  
    backgroundColor: '#ffffff',  
    borderWidth: 1,  
    borderColor: 'grey',  
    width: 270,  
    fontSize: 19,  
  },  
  keyboard: {  
    backgroundColor: 'white',  
  },  
  row: {  
    flexDirection: 'row',  
  },  
  button: {  
    width: '33.3333%',  
  },  
  buttonLabel: {  
    borderWidth: 0.5,  
    borderColor: '#d6d7da',  
    paddingVertical: 13,  
    textAlign: 'center',  
    fontSize: 20,  
  },  
});   
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
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

1. Use the HAR file(recommended)；
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-custom-keyboard": "file:../../node_modules/@react-native-oh-tpl/react-native-custom-keyboard/harmony/custom_keyboard.har"
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

### 3.Configuring CMakeLists and Introducing rnoh_custom_keyboard_package Package

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-custom-keyboard/src/main/cpp" ./custom-keyboard)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_custom_keyboard_package)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "CustomKeyboardPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<CustomKeyboardPackage>(ctx),
    };
}
```

### 4.Introducing RNCustomKeyboardPackage Package to ArkTS 

Open `entry/src/main/ets/RNPackagesFactory.ts` and add the following code:

```diff
  ...
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';
+import {RNCustomKeyboardPackage}  from '@react-native-oh-tpl/react-native-custom-keyboard/ts';


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new RNCustomKeyboardPackage(ctx)
  ];
}
```

### 5.Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-custom-keyboard Releases](https://github.com/react-native-oh-library/react-native-custom-keyboard/releases)

## Properties (If Any)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                       | Type   | Required | Platform | HarmonyOS Support |
| ------------------ | --------------------------------- | ------ | -------- | -------- | ----------------- |
| customKeyboardType | Use a registered custom keyboard. | string | no       | All      | yes               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                                                                                                                                                                   | Type     | Required | Platform | HarmonyOS Support |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| register             | Register a custom keyboard type.                                                                                                                                                              | function | no       | All      | yes               |
| install              | Install custom keyboard to a TextInput.  Generally you can use CustomTextInput instead of this. But you can use this API to install/change custom keyboard dynamically.                       | function | no       | All      | yes               |
| uninstall            | Uninstall custom keyboard from a TextInput dynamically.                                                                                                                                       | function | no       | All      | yes               |
| insertText           | Use in a custom keyboard, insert text to TextInput.                                                                                                                                           | function | no       | All      | yes               |
| backSpace            | Use in a custom keyboard, delete selected text or the charactor before cursor.                                                                                                                | function | no       | All      | yes               |
| doDelete             | Use in a custom keyboard, delete selected text or the charactor after cursor.                                                                                                                 | function | no       | All      | yes               |
| moveLeft             | Use in a custom keyboard, move cursor to selection start or move cursor left.                                                                                                                 | function | no       | All      | yes               |
| moveRight            | Use in a custom keyboard, move cursor to selection end or move cursor right.                                                                                                                  | function | no       | All      | yes               |
| switchSystemKeyboard | Use in a custom keyboard. Switch to system keyboard.Next time user press or focus on the TextInput, custom keyboard will appear again. To keep using system keyboard, call uninstall instead. | function | no       | All      | yes               |

## Others

## Known Issues

## License

This project is licensed under [The MIT License (MIT)](https://www.mit-license.org).