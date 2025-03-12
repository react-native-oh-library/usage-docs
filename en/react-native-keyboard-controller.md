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



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-keyboard-controller
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-keyboard-controller
```

<!-- tabs:end -->

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-reanimated. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [react-native-reanimated docs](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-reanimated.md) to add it to your project.

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

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing RNKeyboardControllerPackage and RNStatusBarManagerCompatPackage

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

### 4. Introducing RNKeyboardControllerPackage and RNStatusBarManagerCompatPackage to ArkTS

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

**Hooks**:Keyboard controller-related hook functions
| Name                           | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------------------------ | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| useKeyboardAnimation           | Hook function for obtaining keyboard animation values        | function | no       | iOS,Android | yes               |
| useReanimatedKeyboardAnimation | Hook function for obtaining keyboard animation values        | function | no       | iOS,Android | yes               |
| useKeyboardHandler             | Sets the hook function of the keyboard callback event.       | function | no       | iOS,Android | yes               |
| useKeyboardController          | Hook function for setting whether to enable keyboard listening events | function | no       | iOS,Android | yes               |
| useFocusedInputHandler         | Sets the hook function for listening to the input box callback event.( Text change listening is supported in HarmonyOS) | function | no       | iOS,Android | partially         |
| useReanimatedFocusedInput      | Hook function for calling back the text change event of the currently focused input control. | function | no       | iOS,Android | no                |

**KeyboardController**: Keyboard controller

| Name                                     | Description                                 | Type     | Required | Platform    | HarmonyOS Support |
| ---------------------------------------- | ------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| setInputMode(mode: number): void         | Setting the Keyboard Display Mode           | function | no       | Android     | no                |
| setDefaultMode(): void                   | Setting the Default Keyboard Display Mode   | function | no       | Android     | no                |
| dismiss(): void                          | Set Keyboard Hide                           | function | no       | iOS,Android | yes               |
| setFocusTo(direction: string): void      | Setting the mode of focus                   | function | no       | iOS,Android | no                |
| addListener: (eventName: string) => void | Adding a Keyboard Listening Event           | function | no       | iOS,Android | yes               |
| removeListeners: (count: number) => void | Delete the listening event of the keyboard. | function | no       | iOS,Android | yes               |

**StatusBarManagerCompat**: Status Bar Controller

| Name                                             | Description                                    | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------------------------ | ---------------------------------------------- | -------- | -------- | -------- | ----------------- |
| setHidden(hidden: boolean): void                 | Set the status bar to be hidden and invisible. | function | no       | Android  | yes               |
| setColor(color: number, animated: boolean): void | Setting the background color of the status bar | function | no       | Android  | no                |
| setTranslucent(translucent: boolean): void       | Sets whether the status bar is transparent.    | function | no       | Android  | no                |
| setStyle(style: string): void                    | Setting the Content Color of the Status Bar    | function | no       | Android  | yes               |

**KeyboardEvents**:Listening for keyboard events

| Name             | Description                             | Type   | Required | Platform    | HarmonyOS Support |
| ---------------- | --------------------------------------- | ------ | -------- | ----------- | ----------------- |
| keyboardWillShow | The keyboard is about to display events | string | no       | iOS,Android | no                |
| keyboardDidShow  | Keyboard has shown events               | string | no       | iOS,Android | yes               |
| keyboardWillHide | Keyboard is about to hide events        | string | no       | iOS,Android | no                |
| keyboardDidHide  | Keyboard has hidden events              | string | no       | iOS,Android | yes               |

**FocusedInputEvents**:Listening to the event of focusing on Input

| Name        | Description                      | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | -------------------------------- | ------ | -------- | ----------- | ----------------- |
| focusDidSet | Focus on the event type of Input | string | no       | iOS,Android | no                |

**WindowDimensionsEvents**:Listening to window layout change events

| Name            | Description                 | Type   | Required | Platform | HarmonyOS Support |
| --------------- | --------------------------- | ------ | -------- | -------- | ----------------- |
| windowDidResize | Listening for window events | string | no       | Android  | no                |

## Component

**KeyboardControllerView**: Keyboard controller View

| Name                                                         | Description                                                  | Type                                                   | Required | Platform    | HarmonyOS Support |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------ | -------- | ----------- | ----------------- |
| enabled                                                      | A boolean prop indicating whether the module is enabled. It indicate only initial state, i. e. if you try to change this prop after component mount it will not have any effect. To change the property in runtime use`useKeyboardController` hook and `setEnabled` method.Defaults to `true`. | boolean                                                | no       | iOS,Android | yes               |
| statusBarTranslucent                                         | Set the value to `true`, if you use translucent status bar on Android,Defaults to `false`.If you already control status bar translucency via `react-native-screens`or `StatusBar` component from `react-native`, you can ignore it | boolean                                                | no       | Android     | no                |
| navigationBarTranslucent                                     | Set the value to `true`, if you use translucent navigation bar on Android,Defaults to `false` | boolean                                                | no       | Android     | no                |
| onKeyboardMoveStart?: DirectEventHandler < KeyboardMoveEvent > | Listening event when the keyboard starts to move             | function                                               | no       | iOS,Android | no                |
| onKeyboardMove?: DirectEventHandler< KeyboardMoveEvent >     | Listening events in keyboard movement                        | function                                               | no       | iOS,Android | no                |
| onKeyboardMoveEnd?: DirectEventHandler< KeyboardMoveEvent >  | Listening event of the end of keyboard movement              | function                                               | no       | iOS,Android | yes               |
| onKeyboardMoveInteractive?: DirectEventHandler< KeyboardMoveEvent > | Listening event of keyboard movement interaction             | function                                               | no       | iOS,Android | no                |
| onFocusedInputLayoutChanged?: DirectEventHandler < FocusedInputLayoutChangedEvent > | Listening event of the coordinate change of the focus text box position | function                                               | no       | iOS,Android | no                |
| onFocusedInputTextChanged?: DirectEventHandler< FocusedInputTextChangedEvent> | Listening event that focuses on text changes in Input        | function                                               | no       | iOS,Android | yes               |
| onFocusedInputSelectionChanged?: DirectEventHandler< FocusedInputSelectionChangedEvent> | Listening event of focusing on text selection in Input       | function                                               | no       | iOS,Android | no                |
| style                                                        | Style of the KeyboardControllerView                          | [ ViewStyle ](https://reactnative.dev/docs/view#props) | no       | iOS,Android | yes               |
| children                                                     | children of the KeyboardControllerView                       | JSX.Element                                            | no       | iOS,Android | yes               |

**KeyboardGestureArea**:Gesture Control Keyboard Assembly

| Name                 | Description                                                  | Type                 | Required | Platform | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | -------------------- | -------- | -------- | ----------------- |
| showOnSwipeUp        | The keyboard slides up with the gesture to display           | boolean              | no       | Android  | no                |
| enableSwipeToDismiss | The keyboard slides down with the gesture to hide            | boolean              | no       | Android  | no                |
| interpolator         | Sets the animation mode for the keyboard to slide with gestures. | linear / ios/ linear | no       | Android  | no                |

**KeyboardAvoidingView**:Container Assembly for Keyboard Controller

| Name                   | Description                                                  | Type                                                   | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------ | -------- | ----------- | ----------------- |
| behavior               | Specify how to react to the presence of the keyboard (HarmonyOS now only surpport position) | "height" / "position" / "padding"                      | no       | iOS,Android | partially         |
| contentContainerStyle  | Style of the content container when `behavior` is 'position' | [ ViewStyle ](https://reactnative.dev/docs/view#props) | no       | Android     | yes               |
| enabled                | Controls whether this `KeyboardAvoidingView` instance should take effect. This is useful when more than one is on the screen. Defaults to true | boolean                                                | no       | Android     | yes               |
| keyboardVerticalOffset | Distance between the top of the user screen and the React Native view. This may be non-zero in some cases. Defaults to 0. | number                                                 | no       | iOS,Android | yes               |
| onLayout               | layout change event                                          | function/undefined                                     | no       | iOS,Android | yes               |
| style                  | Style of the KeyboardAvodingView                             | [ ViewStyle ](https://reactnative.dev/docs/view#props) | no       | iOS,Android | yes               |
| children               | children of the KeyboardAvodingView                          | JSX.Element                                            | no       | iOS,Android | yes               |

**KeyboardAwareScrollView**: Container assembly for scroll keyboard controller

| Name                        | Description                                                  | Type                                                   | Required | Platform    | HarmonyOS Support |
| --------------------------- | ------------------------------------------------------------ | ------------------------------------------------------ | -------- | ----------- | ----------------- |
| bottomOffset                | The distance between keyboard and focused `TextInput` when keyboard is shown | number                                                 | no       | iOS,Android | no                |
| enabled                     | Controls whether this `KeyboardAwareScrollView` instance should take effect. Default is `true` | boolean                                                | no       | Android     | no                |
| disableScrollOnKeyboardHide | Prevents automatic scrolling of the `ScrollView` when the keyboard gets hidden, maintaining the current screen position. Default is `false` | boolean                                                | no       | Android     | no                |
| extraKeyboardSpace          | Adjusting the bottom spacing of KeyboardAwareScrollView. Default is `0` | number                                                 | no       | iOS,Android | no                |
| onLayout                    | Layout change event                                          | function/undefined                                     | no       | iOS,Android | yes               |
| style                       | component style                                              | [ ViewStyle ](https://reactnative.dev/docs/view#props) | no       | iOS,Android | yes               |
| children                    | children element                                             | JSX.Element                                            | no       | iOS,Android | yes               |

**KeyboardStickyView**: Container assembly for scroll keyboard controller

| Name     | Description                                                  | Type                                                   | Required | Platform    | HarmonyOS Support |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------ | -------- | ----------- | ----------------- |
| offset   | Specify additional offset to the view for given keyboard state | {closed?: number;opened?: number;}                     | no       | iOS,Android | yes               |
| style    | component style                                              | [ ViewStyle ](https://reactnative.dev/docs/view#props) | no       | iOS,Android | yes               |
| children | children element                                             | JSX.Element                                            | no       | iOS,Android | yes               |

**KeyboardToolbar**: a component that is shown above the keyboard with `Prev`/`Next` and `Done` buttons.
| Name                        | Description                                                  | Type                         | Required | Platform    | HarmonyOS Support |
| --------------------------- | ------------------------------------------------------------ | ---------------------------- | -------- | ----------- | ----------------- |
| theme                       | A set of dark/light colors consumed by toolbar component     | {light: Theme; dark: Theme;} | no       | iOS,Android | yes               |
| content                     | An element that is shown in the middle of the toolbar        | JSX.Element                  | no       | iOS,Android | yes               |
| doneText                    | Custom text for done button                                  | React.ReactNode              | no       | iOS,Android | yes               |
| button                      | Custom touchable component for toolbar (used for prev/next/done buttons) | React.ReactNode              | no       | iOS,Android | yes               |
| icon                        | Custom icon component used to display next/prev buttons      | React.ReactNode              | no       | iOS,Android | yes               |
| showArrows                  | Whether to show next and previous buttons. Can be useful to set it to `false` if you have only one input and want to show only `Done` button. Default to `true` | boolean                      | no       | iOS,Android | yes               |
| blur                        | A component that applies blur effect to the toolbar          | JSX.Element                  | no       | iOS,Android | yes               |
| opacity                     | A value for container opacity in hexadecimal format (e.g. `ff`). Default value is `ff` | HEX                          | no       | iOS,Android | yes               |
| onNextCallback?: () => void | A callback that is called when the user presses the next button along with the default action | function                     | no       | iOS,Android | no                |
| onPrevCallback?: () => void | A callback that is called when the user presses the previous button along with the default action | function                     | no       | iOS,Android | no                |
| onDoneCallback?: () => void | A callback that is called when the user presses the done button along with the default action | function                     | no       | iOS,Android | yes               |

## Known Issues

- [ ] onKeyboardMoveStart, onKeyboardMove, and onKeyboardMoveInteractive in KeyboardControllerView and keyboardWillShow and keyboardWillHide in KeyboardEvents are not supported: [ issue#1 ](https://github.com/react-native-oh-library/react-native-keyboard-controller/issues/1)
- [ ] KeyboardGestureArea is not supported: [issue#2 ](https://github.com/react-native-oh-library/react-native-keyboard-controller/issues/2)
- [ ] The HarmonyOS SDK does not support the hook method useReanimatedFocusedInput, nor does it support the focus-related methods and callbacks such as setFocusTo in KeyboardController, onFocusedInputLayoutChanged and onFocusedInputSelectionChanged in KeyboardControllerView, focusDidSet in FocusedInputEvents, and onNextCallback and onPrevCallback in KeyboardToolbar for text input box focus event listening: [issue#3 ](https://github.com/react-native-oh-library/react-native-keyboard-controller/issues/3)
- [ ] The bottomOffset, enabled, disableScrollOnKeyboardHide, and extraKeyboardSpace properties of the KeyboardAwareScrollView component cannot be set: [#issue#16](https://github.com/react-native-oh-library/react-native-keyboard-controller/issues/16)
- [ ] The behavior property of KeyboardAvoidingView supports position, but does not support style properties like height or padding: [#issue#13](https://github.com/react-native-oh-library/react-native-harmony-reanimated/issues/13)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/kirillzyusko/react-native-keyboard-controller/blob/main/LICENSE).
