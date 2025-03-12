> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-search-bar</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/umhan35/react-native-search-bar">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/umhan35/react-native-search-bar/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-search-bar)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-search-bar Releases](https://github.com/react-native-oh-library/react-native-search-bar/releases).

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-search-bar
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-search-bar
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useRef  } from 'react';
import { StyleSheet , Text, View } from 'react-native';
import SearchBar from 'react-native-search-bar';


const SearchBarDemo = () => {
  const search1 = React.createRef();

  return (
      <ScrollView contentContainerStyle={styles.inset}>
        <Text style={styles.header}>Dark Style</Text>
		
        <SearchBar
		  style={{marginTop:20,marginBottom:30}}
          ref={search1}
		  barStyle="default"
		  placeholder="Search"
		  returnKeyType="Done"
		  keyboardType="phone-padd"
		  onChange={(e)=>{
			  console.log('search-bar -----------> JS Demo onchange:' + e.nativeEvent.text)
		  }}
		  onChangeText={(text)=>{

		  }}
		  onFocus={()=>{

		  }}
		  onBlur={()=>{

		  }}
		  onSearchButtonPress={(text)=>{
			  search1.current.clearText();
		  }}
		  onCancelButtonPress={()=>{
			  search1.current.blur();
		  }}
        />
		
      </ScrollView>
  );
};

const styles = StyleSheet.create({
  inset: {
    flex: 1,
  },
  header: {
    textAlign: 'center',
    marginTop: 35,
    fontSize: 18,
    fontWeight: 'bold',
  },
});

export default SearchBarDemo;
```

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

    "@react-native-oh-tpl/react-native-search-bar": "file:../../node_modules/@react-native-oh-tpl/react-native-search-bar/harmony/search_bar.har",
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

### 3. Configuring CMakeLists and Introducing SearchBarPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-search-bar/src/main/cpp" ./search-bar)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_search_bar)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "SearchBarPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SearchBarPackage>(ctx),
    };
}
```

### 4.Introducing RNCSearchBar Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
    ...
+ import { RNCSearchBar } from "@react-native-oh-tpl/react-native-search-bar"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
    ...
+   if (ctx.componentName === RNCSearchBar.NAME) {
+     RNCSearchBar({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag,
+     })
+   }
...
  }
...
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ RNCSearchBar.NAME
  ];
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-search-bar Releases](https://github.com/react-native-oh-library/react-native-search-bar/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                                                                                                                                                                                   | Type     | Required | Platform    | HarmonyOS Support |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| -------- | -------- |-------------|------------------|
| `placeholder`  | Text for the placeholder.                                                                            | string | No       | Android、iOS | yes              |
| `textColor`   | Textfield text color.                                                                                                                             | string   | No       | Android、iOS | yes              |
| `barTintColor` | Background color of the search bar.                                                                              | string | No       | Android、iOS | yes              |
| `tintColor` | Color of the Cancel button, highlight and cursor.                                                                                                   | string | No       | Android、iOS | yes              |
| `text`     | Text in the search bar.                                                                                                                  | string | No       | Android、iOS | yes              |
| `textFieldBackgroundColor` | Textfield background color.                                                                                   | string | No       | Android、iOS | yes              |
| `returnKeyType` | Return key type for the keyboard. | string | No       | IOS     | yes              |
| `keyboardType` | The type of keyboard to display.                    | string | No       | IOS     | yes              |
| `showsCancelButtonWhileEditing` | Only shows the cancel button while the search bar has focus.                                                                                                        | boolean | No       | IOS     | yes              |
| `hideBackground` | Indicates whether just to show the text input only.                                                                          | boolean | No       | Android、iOS | yes            |
| `barStyle`   | Style of the bar.                                                                                                                | string | No       | Android、iOS | yes           |
| `editable` | Toggles if the user can interact with the search bar.                                                                | boolean | No       | Android、iOS | yes           |
| `showsCancelButton` | Toggles whether to show the cancel button or not.                                                                    | boolean | No       | Android、iOS | yes           |
| `searchBarStyle` | Style of the search bar.                                                                                                            | string | No       | Android、iOS | yes           |
| `cancelButtonText` | String for the cancel button.                                                                                 | string | No       | Android、iOS | yes           |
| `onBlur` | Event fired the input is blurred.                                                 | Function | No       | Android、iOS | yes           |
| `onChange` | Event fired when.                                                                 | Function | No       | Android、iOS | yes           |
| `onChangeText` | Event fired when the text in the input changes.                                   | Function | No       | Android、iOS | yes           |
| `onFocus` | Event fired when the text input is focused.                                       | Function | No       | Android、iOS | yes           |
| `onSearchButtonPress` | Event fired when the search button is pressed.                                    | Function | No       | Android、iOS | yes           |
| `onCancelButtonPress` | Event fired when the cancel button is pressed.                                    | Function | No       | Android、iOS | yes           |
| `keyboardAppearance` | The appearance of the keyboard.      | 'default' 、 'dark' 、 'light' | No       | iOS          | no          |
| `enablesReturnKeyAutomatically` | Indicates whether the Return key is automatically enabled when the user is entering text. | boolean | No       | Android、iOS | no          |
| `autoCorrect` | If autoCorrect is enabled.           | boolean | No       | iOS | no         |
| `spellCheck` | If red underline is shown for misspelt words. | boolean | No       | iOS | no         |
| `autoCapitalize` | The auto-capitalization behavior.    | 'none' 、 'sentences' 、 'words' 、 'characters' | No       | iOS | no         |                                                                                                                      | 'stroke' or 'fill' or 'bounce' or 'flat' or 'one-stroke' or 'fade'   | No       | iOS     | No              |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name        | Description         | Type     | Required | Platform     | HarmonyOS Support |
| ----------- | ------------------- | -------- | -------- | ------------ | ----------------- |
| `focus`     | Get focus.          | function | No       | Android、iOS | yes               |
| `blur`      | Lose focus.         | function | No       | Android、iOS | yes               |
| `unFocus`   | Lose focus.         | function | No       | Android、iOS | yes               |
| `clearText` | Clean up the input. | function | No       | Android、iOS | yes               |

## Known Issues

- [ ] autoCapitalize属性，该属性用来控制自动大写风格，单词首字母/句子首字母/整体大写，ArkUI 不支持此属性: [issue#2](https://github.com/react-native-oh-library/react-native-search-bar/issues/2)
- [ ] spellCheck属性，该属性用来控制错误的单词，是否显示红色下划线，ArkUI 不支持此属性: [issue#3](https://github.com/react-native-oh-library/react-native-search-bar/issues/3)
- [ ] autoCorrect属性，该属性用来控制是否开启错误单词自动更正功能，ArkUI 不支持此属性: [issue#4](https://github.com/react-native-oh-library/react-native-search-bar/issues/4)
- [ ] enablesReturnKeyAutomatically属性，该属性用来控制编辑时键盘返回键是否显示，ArkUI 不支持此属性: [issue#5](https://github.com/react-native-oh-library/react-native-search-bar/issues/5)
- [ ] keyboardAppearance属性，该属性用来控制键盘主题风格，ArkUI 不支持此属性: [issue#6](https://github.com/react-native-oh-library/react-native-search-bar/issues/6)

## Others

## License


This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-search-bar/blob/master/LICENSE).
