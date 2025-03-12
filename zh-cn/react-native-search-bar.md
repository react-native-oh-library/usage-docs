> 模板版本：v0.2.2

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


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-search-bar)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-search-bar Releases](https://github.com/react-native-oh-library/react-native-search-bar/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：



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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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
		  placeholder="占位符"
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

    "@react-native-oh-tpl/react-native-search-bar": "file:../../node_modules/@react-native-oh-tpl/react-native-search-bar/harmony/search_bar.har",
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

### 3.配置 CMakeLists 和引入 SearchBarPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 4.在 ArkTs 侧引入 RNCSearchBar 组件

找到 `function buildCustomComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

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

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ RNCSearchBar.NAME
  ];
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-search-bar Releases](https://github.com/react-native-oh-library/react-native-search-bar/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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
| `autoCapitalize` | The auto-capitalization behavior.    | 'none' 、 'sentences' 、 'words' 、 'characters' | No       | iOS | no         |
## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name        | Description         | Type     | Required | Platform     | HarmonyOS Support |
| ----------- | ------------------- | -------- | -------- | ------------ | ----------------- |
| `focus`     | Get focus.          | function | No       | Android、iOS | yes               |
| `blur`      | Lose focus.         | function | No       | Android、iOS | yes               |
| `unFocus`   | Lose focus.         | function | No       | Android、iOS | yes               |
| `clearText` | Clean up the input. | function | No       | Android、iOS | yes               |

## 遗留问题
- [ ] autoCapitalize属性，该属性用来控制自动大写风格，单词首字母/句子首字母/整体大写，ArkUI 不支持此属性: [issue#2](https://github.com/react-native-oh-library/react-native-search-bar/issues/2)
- [ ] spellCheck属性，该属性用来控制错误的单词，是否显示红色下划线，ArkUI 不支持此属性: [issue#3](https://github.com/react-native-oh-library/react-native-search-bar/issues/3)
- [ ] autoCorrect属性，该属性用来控制是否开启错误单词自动更正功能，ArkUI 不支持此属性: [issue#4](https://github.com/react-native-oh-library/react-native-search-bar/issues/4)
- [ ] enablesReturnKeyAutomatically属性，该属性用来控制编辑时键盘返回键是否显示，ArkUI 不支持此属性: [issue#5](https://github.com/react-native-oh-library/react-native-search-bar/issues/5)
- [ ] keyboardAppearance属性，该属性用来控制键盘主题风格，ArkUI 不支持此属性: [issue#6](https://github.com/react-native-oh-library/react-native-search-bar/issues/6)

  
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-search-bar/blob/master/LICENSE) ，请自由地享受和参与开源。