> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-keyboard-controller</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/kirillzyusko/react-native-keyboard-controller">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/kirillzyusko/react-native-keyboard-controller/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-keyboard-controller)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-keyboard-controller Releases](https://github.com/react-native-oh-library/react-native-keyboard-controller/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-keyboard-controller@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-keyboard-controller@file:#
```

<!-- tabs:end -->

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-reanimated. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [react-native-reanimated docs](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-reanimated.md) to add it to your project.

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { Text, View, TextInput, TouchableOpacity } from "react-native";
import {
  KeyboardAvoidingView,
  KeyboardProvider,
} from "react-native-keyboard-controller";

function App() {
  return (
    <KeyboardProvider>
      <KeyboardAvoidingView
        style={{
          padding: 22,
          flex: 1,
          justifyContent: "space-between",
        }}
      >
        <Text
          style={{
            color: "black",
            fontSize: 25,
            marginTop: 100,
            fontWeight: "500",
          }}
        >
          react-native-keyboard-controller
        </Text>
        <View>
          <TextInput
            placeholder="Username"
            placeholderTextColor="#7C7C7C"
            style={{
              height: 45,
              borderColor: "#000000",
              borderWidth: 1,
              borderRadius: 10,
              marginBottom: 36,
              paddingLeft: 10,
            }}
          />
          <TextInput
            placeholder="Password"
            placeholderTextColor="#7C7C7C"
            style={{
              height: 45,
              borderColor: "#000000",
              borderWidth: 1,
              borderRadius: 10,
              marginBottom: 36,
              paddingLeft: 10,
            }}
          />
          <TouchableOpacity
            style={{
              marginTop: 40,
              height: 45,
              borderRadius: 10,
              backgroundColor: "rgb(40, 64, 147)",
              justifyContent: "center",
              alignItems: "center",
            }}
          >
            <Text
              style={{
                fontWeight: "500",
                fontSize: 16,
                color: "white",
              }}
            >
              Submit
            </Text>
          </TouchableOpacity>
        </View>
      </KeyboardAvoidingView>
    </KeyboardProvider>
  );
}
export default App;
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
    "@react-native-oh-tpl/react-native-keyboard-controller": "file:../../node_modules/@react-native-oh-tpl/react-native-keyboard-controller/harmony/keyboard_controller.har"
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

### 3. Configuring CMakeLists and Introducing RNKeyboardControllerPackage，RNStatusBarManagerCompatPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-keyboard-controller/src/main/cpp" ./keyboard-controller)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_keyboard_controller)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "keyboardControllerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<KeyboardControllerPackage>(ctx),
    };
}
```

### 4. Introducing RNKeyboardControllerPackage，RNStatusBarManagerCompatPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import {RNKeyboardControllerPackage,RNStatusBarManagerCompatPackage} from  "@react-native-oh-tpl/react-native-keyboard-controller/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNKeyboardControllerPackage(ctx),
+   new RNStatusBarManagerCompatPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-keyboard-controller Releases](https://github.com/react-native-oh-library/react-native-keyboard-controller/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**Hooks**:键盘控制器相关的钩子函数
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| useKeyboardAnimation | 获取键盘动画值的钩子函数 | function | no | iOS,Android | yes |
| useReanimatedKeyboardAnimation | 获取键盘动画值的钩子函数 | function | no | iOS,Android | yes |
| useKeyboardHandler | 设置键盘回调事件的钩子函数 | function | no | iOS,Android | yes |
| useKeyboardController | 设置是否启动键盘监听事件的钩子函数 |function | no | iOS,Android | yes |
| useFocusedInputHandler | 设置监听输入框回调事件的钩子函数 | function | no | iOS,Android |partially |
| useReanimatedFocusedInput | 当前聚焦的输入控件文本变化事件回调的钩子函数 | function | no | iOS,Android |no |

**KeyboardController**: 键盘控制器

| Name                                     | Description          | Type     | Required | Platform    | HarmonyOS Support |
| ---------------------------------------- | -------------------- | -------- | -------- | ----------- | ----------------- |
| setInputMode(mode: number): void         | 设置键盘显示默认模式 | function | no       | Android     | no                |
| setDefaultMode(): void                   | 设置键盘显示默认模式 | function | no       | Android     | no                |
| dismiss(): void                          | 设置键盘隐藏         | function | no       | iOS,Android | yes               |
| setFocusTo(direction: string): void      | 设置聚焦的方式       | function | no       | iOS,Android | no                |
| addListener: (eventName: string) => void | 添加键盘的监听事件   | function | no       | iOS,Android | yes               |
| removeListeners: (count: number) => void | 删除键盘的监听事件   | function | no       | iOS,Android | yes               |

**StatusBarManagerCompat**: 状态栏控制器

| Name                                             | Description          | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------------------------ | -------------------- | -------- | -------- | -------- | ----------------- |
| setHidden(hidden: boolean): void                 | 设置状态栏隐藏不可见 | function | no       | Android  | yes               |
| setColor(color: number, animated: boolean): void | 设置状态栏背景颜色   | function | no       | Android  | yes               |
| setTranslucent(translucent: boolean): void       | 设置状态栏是否透明   | function | no       | Android  | yes               |
| setStyle(style: string): void                    | 设置状态栏的内容颜色 | function | no       | Android  | yes               |

**KeyboardEvents**:监听键盘事件

| Name             | Description      | Type   | Required | Platform    | HarmonyOS Support |
| ---------------- | ---------------- | ------ | -------- | ----------- | ----------------- |
| keyboardWillShow | 键盘将要显示事件 | string | no       | iOS,Android | no                |
| keyboardDidShow  | 键盘已经显示事件 | string | no       | iOS,Android | yes               |
| keyboardWillHide | 键盘将要隐藏事件 | string | no       | iOS,Android | no                |
| keyboardDidHide  | 键盘已经隐藏事件 | string | no       | iOS,Android | yes               |

**FocusedInputEvents**:监听聚焦输入框事件

| Name        | Description        | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------ | ------ | -------- | ----------- | ----------------- |
| focusDidSet | 聚焦输入框事件类型 | string | no       | iOS,Android | no                |

**WindowDimensionsEvents**:监听窗口布局变化事件

| Name            | Description  | Type   | Required | Platform | HarmonyOS Support |
| --------------- | ------------ | ------ | -------- | -------- | ----------------- |
| windowDidResize | 监听窗口事件 | string | no       | Android  | no                |

## 组件

**KeyboardControllerView**: 键盘控制器

| Name                                                                                    | Description                      | Type        | Required | Platform    | HarmonyOS Support |
| --------------------------------------------------------------------------------------- | -------------------------------- | ----------- | -------- | ----------- | ----------------- |
| enabled                                                                                 | 是否开启键盘监听事件             | boolean     | no       | iOS,Android | yes               |
| statusBarTranslucent                                                                    | 状态栏是否透明                   | boolean     | no       | Android     | no                |
| navigationBarTranslucent                                                                | 导航栏是否透明                   | boolean     | no       | Android     | no                |
| onKeyboardMoveStart?: DirectEventHandler < KeyboardMoveEvent >                          | 键盘开始移动的监听事件           | function    | no       | iOS,Android | no                |
| onKeyboardMove?: DirectEventHandler< KeyboardMoveEvent >                                | 键盘移动中的监听事件             | function    | no       | iOS,Android | no                |
| onKeyboardMoveEnd?: DirectEventHandler< KeyboardMoveEvent >                             | 键盘移动结束的监听事件           | function    | no       | iOS,Android | yes               |
| onKeyboardMoveInteractive?: DirectEventHandler< KeyboardMoveEvent >                     | 键盘移动交互的监听事件           | function    | no       | iOS,Android | no                |
| onFocusedInputLayoutChanged?: DirectEventHandler < FocusedInputLayoutChangedEvent >     | 聚焦输入框位置坐标变化的监听事件 | function    | no       | iOS,Android | no                |
| onFocusedInputTextChanged?: DirectEventHandler< FocusedInputTextChangedEvent>           | 聚焦输入框文本变化的监听事件     | function    | no       | iOS,Android | yes               |
| onFocusedInputSelectionChanged?: DirectEventHandler< FocusedInputSelectionChangedEvent> | 聚焦输入框文本选择的监听事件     | function    | no       | iOS,Android | no                |
| children                                                                                | JSX element 子组件               | JSX.Element | no       | iOS,Android | yes               |

**KeyboardGestureArea**: 手势控制键盘组件

| Name                 | Description                  | Type                 | Required | Platform | HarmonyOS Support |
| -------------------- | ---------------------------- | -------------------- | -------- | -------- | ----------------- |
| showOnSwipeUp        | 键盘随手势向上滑动显示       | boolean              | no       | Android  | no                |
| enableSwipeToDismiss | 键盘随手势向下滑动隐藏       | boolean              | no       | Android  | no                |
| interpolator         | 设置键盘随手势滑动的动画模式 | linear / ios/ linear | no       | Android  | no                |

**KeyboardAvoidingView**: 键盘控制器的容器组件

| Name                   | Description                                                    | Type                                                   | Required | Platform    | HarmonyOS Support |
| ---------------------- | -------------------------------------------------------------- | ------------------------------------------------------ | -------- | ----------- | ----------------- |
| behavior               | 指定如何对键盘的存在做出反应                                   | "height" / "position" / "padding"                      | no       | iOS,Android | yes               |
| contentContainerStyle  | 当`behavior`为 position 时，内容容器的样式                     | [ ViewStyle ](https://reactnative.dev/docs/view#props) | no       | Android     | yes               |
| enabled                | 控制这个`KeyboardAvodingView`实例是否应该生效,默认为 true      | boolean                                                | no       | Android     | yes               |
| keyboardVerticalOffset | 用户屏幕顶部和 React Native 视图之间的距离,默认为`0`           | number                                                 | no       | iOS,Android | yes               |
| onLayout               | 在安装和布局更改时的回调函数(event: LayoutChangeEvent) => void | function/undefined                                     | no       | iOS,Android | yes               |
| style                  | `KeyboardAvodingView`的 CSS 属性                               | [ ViewStyle ](https://reactnative.dev/docs/view#props) | no       | iOS,Android | yes               |
| children               | JSX element 子组件                                             | JSX.Element                                            | no       | iOS,Android | yes               |

**KeyboardAwareScrollView**: 滚动键盘控制器的容器组件

| Name                        | Description                                                             | Type                                                   | Required | Platform    | HarmonyOS Support |
| --------------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------ | -------- | ----------- | ----------------- |
| bottomOffset                | 显示键盘时，键盘与焦点`TextInput`之间的距离。默认值为“0”                | number                                                 | no       | iOS,Android | yes               |
| enabled                     | 控制此`KeyboardAwareScrollView`实例是否应生效。默认值为`true`           | boolean                                                | no       | Android     | yes               |
| disableScrollOnKeyboardHide | 防止键盘隐藏时`ScrollView`自动滚动，保持当前屏幕位置。默认值为`false`。 | boolean                                                | no       | Android     | yes               |
| extraKeyboardSpace          | 用户屏幕顶部和 React Native 视图之间的距离,默认为 0                     | number                                                 | no       | iOS,Android | yes               |
| onLayout                    | 在安装和布局更改时的回调函数(event: LayoutChangeEvent) => void          | function/undefined                                     | no       | iOS,Android | yes               |
| style                       | `KeyboardAwareScrollView`的 CSS 属性                                    | [ ViewStyle ](https://reactnative.dev/docs/view#props) | no       | iOS,Android | yes               |
| children                    | JSX element 子组件                                                      | JSX.Element                                            | no       | iOS,Android | yes               |

**KeyboardStickyView**: 滚动键盘控制器的容器组件

| Name     | Description                        | Type                                                   | Required | Platform    | HarmonyOS Support |
| -------- | ---------------------------------- | ------------------------------------------------------ | -------- | ----------- | ----------------- |
| offset   | 为给定的键盘状态指定视图的附加偏移 | {closed?: number;opened?: number;}                     | no       | iOS,Android | yes               |
| style    | `KeyboardStickyView`的 CSS 属性    | [ ViewStyle ](https://reactnative.dev/docs/view#props) | no       | iOS,Android | yes               |
| children | JSX element 子组件                 | JSX.Element                                            | no       | iOS,Android | yes               |

**KeyboardToolbar**: 是显示在键盘上方的组件，带有`Prev`/`Next`和
\*“完成”按钮。

| Name                        | Description                                            | Type                         | Required | Platform    | HarmonyOS Support |
| --------------------------- | ------------------------------------------------------ | ---------------------------- | -------- | ----------- | ----------------- |
| theme                       | 工具栏组件使用的一组深色/浅色主题                      | {light: Theme; dark: Theme;} | no       | iOS,Android | yes               |
| content                     | 显示在工具栏中间的元素                                 | JSX.Element                  | no       | iOS,Android | yes               |
| doneText                    | 完成按钮的自定义文本                                   | React.ReactNode              | no       | iOS,Android | yes               |
| button                      | 工具栏的自定义可触摸组件（用于 prev/next/done 按钮）   | React.ReactNode              | no       | iOS,Android | yes               |
| icon                        | 用于显示 next/prev 按钮的自定义图标组件                | React.ReactNode              | no       | iOS,Android | yes               |
| showArrows                  | 是否显示下一个和上一个按钮                             | boolean                      | no       | iOS,Android | yes               |
| blur                        | 对工具栏应用模糊效果的组件                             | JSX.Element                  | no       | iOS,Android | yes               |
| opacity                     | 十六进制格式的容器不透明度值（例如`ff`）。默认值为`ff` | HEX                          | no       | iOS,Android | yes               |
| onNextCallback?: () => void | 当用户按下“下一步”按钮时调用的回调以及默认操作。       | function                     | no       | iOS,Android | no                |
| onPrevCallback?: () => void | 用户按下“上一步”按钮时调用的回调以及默认操作。         | function                     | no       | iOS,Android | no                |
| onDoneCallback?: () => void | 当用户按下“完成”按钮时调用的回调以及默认操作。         | function                     | no       | iOS,Android | yes               |

## Known Issues

- [ ] 暂不支持 KeyboardControllerView 中 onKeyboardMoveStart，onKeyboardMove，onKeyboardMoveInteractive 和 KeyboardEvents 中 keyboardWillShow、keyboardWillHide 键盘事件的回调: [ issue#1 ](https://github.com/react-native-oh-library/react-native-keyboard-controller/issues/1)
- [ ] 暂不支持 KeyboardGestureArea 组件: [issue#2 ](https://github.com/react-native-oh-library/react-native-keyboard-controller/issues/2)
- [ ] 暂不支持 hook 方法 useReanimatedFocusedInput，KeyboardController 中 setFocusTo，KeyboardControllerView 中 onFocusedInputLayoutChanged、onFocusedInputSelectionChanged，FocusedInputEvents 中 focusDidSet，KeyboardToolbar 中 onNextCallback、onPrevCallback 关于输入框聚焦的监听方法回调: [issue#3 ](https://github.com/react-native-oh-library/react-native-keyboard-controller/issues/3)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/kirillzyusko/react-native-keyboard-controller/blob/main/LICENSE).
