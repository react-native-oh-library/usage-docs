> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-text-input-mask</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-text-input-mask/react-native-text-input-mask">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-text-input-mask/react-native-text-input-mask/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-text-input-mask)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-text-input-mask Releases](https://github.com/react-native-oh-library/react-native-text-input-mask/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-text-input-mask
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-text-input-mask
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useState, useRef } from "react";
import {
  StyleSheet,
  Text,
  View,
  ScrollView,
  Button,
  TextInput,
} from "react-native";
import TextInputMask, {
  mask,
  unmask,
  setMask,
} from "react-native-text-input-mask";
import { Colors } from "react-native/Libraries/NewAppScreen";
export const TextInputTest = () => {
  const [maskTest, maskValue] = useState("");
  const maskDemo = () => {
    mask("+1 ([000]) [000] [00] [00]", "13343469915", true)
      .then((res) => {
        maskValue(res);
      })
      .catch((err) => {
        console.log("error", err);
      });
  };

  const [unmaskTest, unmaskValue] = useState("");
  const unmaskDemo = () => {
    unmask("+1 ([000]) [000] [00] [00]", "13343469915", true)
      .then((res) => {
        unmaskValue(res);
      })
      .catch((err) => {
        console.log("error", err);
      });
  };
  const customNotations = [
    { character: "s", characterSet: "$€", isOptional: true },
  ];
  const [onChangeTextTest_formatted, setonChangeTextValue_formatted] =
    useState("");
  const [onChangeTextTest_extracted, setonChangeTextValue_extracted] =
    useState("");
  const componentDemo = (formatted: string, extracted: string | undefined) => {
    console.log("formatted", formatted);
    setonChangeTextValue_formatted(formatted);
    console.log("extracted", extracted);
    if (extracted) {
      setonChangeTextValue_extracted(extracted);
    }
  };
  return (
    <ScrollView style={{ flex: 1 }}>
      <View style={styles.container}>
        <TextInputMask
          rightToLeft={true}
          onChangeText={componentDemo}
          affinityCalculationStrategy="CAPACITY"
          style={styles.input}
          autocomplete={true}
          customNotations={customNotations}
          mask={"[s][9999]"}
          placeholder="Enter phone number"
        />
        <Text style={styles.input}>{onChangeTextTest_formatted}</Text>
        <Text style={styles.input}>{onChangeTextTest_extracted}</Text>
      </View>
      <View style={styles.container}>
        <Text style={styles.label}>Phone Number:</Text>
        <Button title="mask" onPress={maskDemo} />
        <Text style={styles.input}>{maskTest}</Text>
      </View>
      <View style={styles.container}>
        <Text style={styles.label}>Phone Number:</Text>
        <Button title="unmask" onPress={unmaskDemo} />
        <Text style={styles.input}>{unmaskTest}</Text>
      </View>
    </ScrollView>
  );
};
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    padding: 16,
  },
  label: {
    color: Colors.white,
    fontSize: 16,
    marginBottom: 8,
  },
  input: {
    height: 40,
    color: Colors.white,
    borderColor: "#ccc",
    borderWidth: 1,
    paddingHorizontal: 8,
  },
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
    "@react-native-oh-tpl/react-native-text-input-mask": "file:../../node_modules/@react-native-oh-tpl/react-native-text-input-mask/harmony/text_input_mask.har"
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

### 3. Configuring CMakeLists and Introducing RNTextInputMaskPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(RNOH_CPP_DIR "${OH_MODULE_DIR}/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")

file(GLOB GENERATED_CPP_FILES "${CMAKE_CURRENT_SOURCE_DIR}/generated/*.cpp")

set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
add_compile_definitions(WITH_HITRACE_SYSTRACE)
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use

add_subdirectory("${RNOH_CPP_DIR}" ./rn)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-text-input-mask/src/main/cpp" ./RNTextInputMask)

add_library(rnoh_app SHARED
   ${GENERATED_CPP_FILES}
   "./PackageProvider.cpp"
   "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)


target_link_libraries(rnoh_app PUBLIC rnoh)
+ target_link_libraries(rnoh_app PUBLIC text_input_mask)
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "RNTextInputMaskPackage.h"
 using namespace rnoh;

 std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
     return {std::make_shared<RNOHGeneratedPackage>(ctx),
+            std::make_shared<RNTextInputMaskPackage>(ctx)
     };
 }
```

### 4. Introducing RNTextInputMaskPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNTextInputMaskPackage } from '@react-native-oh-tpl/react-native-text-input-mask/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+    new RNTextInputMaskPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-text-input-mask Releases](https://github.com/react-native-oh-library/react-native-text-input-mask/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name          | Description                                                                                                               | Type      | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------------------------------------------------------------------- | --------- | ----------- | ----------------- |
| mask          | Format a string,Return the formatted string                                                                               | function  | Android/iOS | yes               |
| unmask        | Restore the formatted string,Return the restored string                                                                   | function  | Android/iOS | yes               |
| setMask       | Set a listener for a component,Format the input content of a text box,Use in conjunction with the TextInputMask component | function  | Android/iOS | yes               |
| TextInputMask | Text input component                                                                                                      | component | Android/iOS | yes               |

#### mask

```js
mask(mask: string, value: string, autocomplete: boolean) : Promise<string>
```

| Name         | Description                    | Type    | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------ | ------- | -------- | ----------- | ----------------- |
| mask         | Format for string formatting   | string  | yes      | iOS/Android | yes               |
| value        | Characters to be formatted     | string  | yes      | iOS/Android | yes               |
| autocomplete | Automatic character completion | boolean | no       | iOS/Android | yes               |

#### unmask

```json
unmask(mask: string, value: string, autocomplete: boolean) : Promise<string>
```

| Name         | Description                    | Type    | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------ | ------- | -------- | ----------- | ----------------- |
| mask         | Format for string formatting   | string  | yes      | iOS/Android | yes               |
| value        | Characters to be restored      | string  | yes      | iOS/Android | yes               |
| autocomplete | Automatic character completion | boolean | no       | iOS/Android | yes               |

#### setMask

```
setMask (reactNode: number, primaryFormat: string, options?: MaskOptions) : void
```

| Name          | Description                   | Type        | Required | Platform    | HarmonyOS Support |
| :------------ | ----------------------------- | ----------- | -------- | ----------- | ----------------- |
| reactNode     | Component ID                  | string      | yes      | iOS/Android | yes               |
| primaryFormat | Formatting format             | string      | yes      | iOS/Android | yes               |
| options       | Formatting-related properties | MaskOptions | no       | iOS/Android | yes               |

##### MaskOptions

| Name                        | Description                          | Type                             | Required | Platform    | HarmonyOS Support |
| --------------------------- | ------------------------------------ | -------------------------------- | -------- | ----------- | ----------------- |
| affineFormats               | Alternate format                     | string[]                         | no       | iOS/Android | yes               |
| customNotations             | Custom escape characters             | Natation[]                       | no       | iOS/Android | yes               |
| affinityCalculationStrategy | Affinity calculation strategy        | AffinityCalculationStrategy 枚举 | no       | iOS/Android | yes               |
| autocomplete                | Whether to automatically complete    | boolean                          | no       | iOS/Android | yes               |
| autoskip                    | Whether to automatically skip        | boolean                          | no       | iOS/Android | yes               |
| rightToLeft                 | Whether to format from right to left | boolean                          | no       | iOS/Android | yes               |

##### Natation

| Name         | Description                                              | Type    | Required | Platform    | HarmonyOS Support |
| ------------ | -------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| character    | Symbols in the format string                             | string  | yes      | iOS/Android | yes               |
| characterSet | Associated character set for acceptable input characters | string  | yes      | iOS/Android | yes               |
| isOptional   | Whether the symbol is optional or mandatory              | boolean | yes      | iOS/Android | yes               |

##### AffinityCalculationStrategy

| Name                     | Description                                                                                                                                         | Type   | Required | Platform    | HarmonyOS Support |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| WHOLE_STRING             | Default calculation strategy                                                                                                                        | string | no       | iOS/Android | yes               |
| PREFIX                   | Find the longest common prefix between the original text and the identical text                                                                     | string | no       | iOS/Android | yes               |
| CAPACITY                 | Affinity is the tolerance between the length of the input and the total amount of text that the current mask can accommodate.                       | string | no       | iOS/Android | yes               |
| EXTRACTED_VALUE_CAPACITY | Affinity is the tolerance between the length of the extracted value and the total length of extracted values that the current mask can accommodate. | string | no       | iOS/Android | yes               |

## Others

## License

This project is licensed under[The MIT License(MIT)](https://github.com/react-native-text-input-mask/react-native-text-input-mask/blob/master/LICENSE).
