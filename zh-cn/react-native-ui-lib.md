模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-ui-lib</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wix/react-native-ui-lib">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wix/react-native-ui-lib/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-ui-lib)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-ui-lib Releases](https://github.com/react-native-oh-library/react-native-ui-lib/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-reanimated和 @react-native-oh-tpl/react-native-gesture-handler的原生端代码，如已在 HarmonyOS 工程中引入过这些库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参考[@react-native-oh-tpl/react-native-reanimated文档](/zh-cn/react-native-reanimated.md)和[@react-native-oh-tpl/react-native-gesture-handler文档](/zh-cn/react-native-gesture-handler.md)进行引入。

下面是根据使用组件情况按需引入依赖项:

- [@react-native-community/blur](/zh-cn/react-native-community-blur.md) （Card 组件）

- [@react-native-community/datetimepicker](/zh-cn/react-native-community-datetimepicker.md) （DateTimePicker 组件）
- [@react-native-community/netinfo](/zh-cn/react-native-community-netinfo.md) （ConnectionStatusBar 组件）

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-ui-lib
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-ui-lib
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import React, {Component} from 'react';
import {Colors, Typography, Spacings, ThemeManager, View, Text, Card, Button} from 'react-native-ui-lib';

Colors.loadColors({
  primaryColor: '#2364AA',
  secondaryColor: '#81C3D7',
  textColor: '##221D23',
  errorColor: '#E63B2E',
  successColor: '#ADC76F',
  warnColor: '##FF963C'
});

Typography.loadTypographies({
  heading: {fontSize: 36, fontWeight: '600'},
  subheading: {fontSize: 28, fontWeight: '500'},
  body: {fontSize: 18, fontWeight: '400'}
});

Spacings.loadSpacings({
  page: 20,
  card: 12,
  gridGutter: 16
});

// with plain object
ThemeManager.setComponentTheme('Card', {
  borderRadius: 8
});

// with a dynamic function
ThemeManager.setComponentTheme('Button', (props, context) => {
  // 'square' is not an original Button prop, but a custom prop that can
  // be used to create different variations of buttons in your app
  if (props.square) {
    return {
      borderRadius: 0
    };
  }
});

class MyScreen extends Component {
  render() {
    return (
      <View flex padding-page>
        <Text heading marginB-s4>
          My Screen
        </Text>
        <Card height={100} center padding-card marginB-s4>
          <Text body>This is an example card </Text>
        </Card>

        <Button label="Button" body bg-primaryColor square></Button>
      </View>
    );
  }
}
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

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
    "@react-native-oh-tpl/react-native-ui-lib": "file:../../node_modules/@react-native-oh-tpl/react-native-ui-lib/harmony/ui_lib.har"
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

### 3.配置 CMakeLists 和引入 UiLibPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
+ set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-ui-lib/src/main/cpp" ./ui-lib)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_ui_lib)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "UiLibPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<UiLibPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 HighlighterView组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { HighlighterView } from "@react-native-oh-tpl/react-native-ui-lib";

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === HighlighterView.NAME) {
+   HighlighterView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。（如使用混合方案）

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ HighlighterView.NAME
  ];
```

### 5.在 ArkTs 侧引入 UiLibPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { UiLibPackage } from '@react-native-oh-tpl/react-native-ui-lib/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new UiLibPackage(ctx)
  ];
}
```

### 6.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-ui-lib Releases](https://github.com/react-native-oh-library/react-native-ui-lib/releases)



## 组件

详细请查看 [react-native-ui-lib的文档介绍](https://wix.github.io/react-native-ui-lib/docs/getting-started/setup)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Text**：文本组件，该组件扩展了[Text](https://reactnative.dev/docs/text)属性。

| Name            | Description                                                  | Type                                | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ----------------------------------- | -------- | ----------- | ----------------- |
| animated        | Use Animated.Text as a container                             | boolean                             | no       | iOS/Android | yes               |
| center          | Whether to center the text (using textAlign)                 | boolean                             | no       | iOS/Android | yes               |
| color           | Color of the text                                            | string                              | no       | iOS/Android | yes               |
| highlightString | Substring to highlight. Can be a simple string or a HighlightStringProps object, or an array of the above | HighlightString \|HighlightString[] | no       | iOS/Android | yes               |
| highlightStyle  | Custom highlight style for highlight string                  | TextStyle                           | no       | iOS/Android | yes               |
| recorderTag     | Recorder Tag                                                 | 'mask' \|'unmask'                   | no       | iOS/Android | yes               |
| underline       | Whether to add an underline                                  | boolean                             | no       | iOS/Android | yes               |
| uppercase       | Whether to change the text to uppercase                      | boolean                             | no       | iOS/Android | yes               |

**TouchableOpacity**：触摸反馈透明度组件，该组件扩展了[TouchableOpacity](https://reactnative.dev/docs/touchableopacity)属性。

| Name                  | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| activeBackgroundColor | Apply background color on TouchableOpacity when active (press is on) | string                                                       | no       | iOS/Android | yes               |
| backgroundColor       | Background color for TouchableOpacity                        | string                                                       | no       | iOS/Android | yes               |
| customValue           | Custom value of any type to pass on to TouchableOpacity and receive back in onPress callback | any                                                          | no       | iOS/Android | yes               |
| onPress               | On press callback                                            | (props?: TouchableOpacityProps & {event: GestureResponderEvent} \|any) => void | no       | iOS/Android | yes               |
| recorderTag           | Recorder Tag                                                 | 'mask'\|'unmask'                                             | no       | iOS/Android | yes               |
| style                 | Custom style                                                 | ViewStyle                                                    | no       | iOS/Android | yes               |
| throttleOptions       | Throttle options                                             | ThrottleOptions                                              | no       | iOS/Android | yes               |
| throttleTime          | Throttle time in MS for onPress callback                     | number                                                       | no       | iOS/Android | yes               |
| useNative             | Should use an enhanced native implementation with extra features | boolean                                                      | no       | iOS/Android | yes               |

**View**：容器组件，该组件扩展了[View](https://reactnative.dev/docs/view)属性。

| Name            | Description                                                  | Type             | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ---------------- | -------- | ----------- | ----------------- |
| animated        | Use Animate.View as a container                              | boolean          | no       | iOS/Android | yes               |
| backgroundColor | Set background color                                         | string           | no       | iOS/Android | yes               |
| inaccessible    | Turn off accessibility for this view and its nested children | boolean          | no       | iOS/Android | yes               |
| reanimated      | Use Animate.View (from react-native-reanimated) as a container | boolean          | no       | iOS/Android | yes               |
| recorderTag     | Recorder Tag                                                 | 'mask'\|'unmask' | no       | iOS/Android | yes               |
| renderDelay     | Experimental: Pass time in ms to delay render                | number           | no       | iOS/Android | yes               |
| style           | Custom style                                                 | ViewStyle        | no       | iOS/Android | yes               |
| useSafeArea     | If true, will render as SafeAreaView                         | boolean          | no       | iOS/Android | yes               |

**ActionBar**：快速操作栏，每个操作都支持按钮组件道具，该组件扩展了[View](https://wix.github.io/react-native-ui-lib/docs/components/basic/View)属性。

| Name            | Description                                                  | Type          | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ------------- | -------- | ----------- | ----------------- |
| actions         | The actions for the action bar                               | ButtonProps[] | no       | iOS/Android | yes               |
| backgroundColor | Background color                                             | string        | no       | iOS/Android | yes               |
| centered        | Should action be equally centered                            | boolean       | no       | iOS/Android | yes               |
| height          | Height                                                       | number        | no       | iOS/Android | yes               |
| keepRelative    | Keep the action bar position relative instead of it absolute position | boolean       | no       | iOS/Android | yes               |
| style           | Component's style                                            | ViewStyle     | no       | iOS/Android | yes               |
| useSafeArea     | In iOS, use safe area, in case component attached to the bottom | boolean       | no       | iOS/Android | yes               |

**Button**：按钮组件，该组件扩展了[TouchableOpacity](https://wix.github.io/react-native-ui-lib/docs/components/basic/TouchableOpacity)属性。

| Name                     | Description                                                  | Type                                            | Required | Platform    | HarmonyOS Support |
| :----------------------- | ------------------------------------------------------------ | ----------------------------------------------- | -------- | ----------- | ----------------- |
| animateLayout            | should animate layout change. Note: For Android you must set ' setLayoutAnimationEnabledExperimental (true) ' via RN's 'UIManager' | boolean                                         | no       | iOS/Android | yes               |
| animateTo                | the direction of the animation ('left' and 'right' will effect the button's own alignment) | ButtonAnimationDirection                        | no       | iOS/Android | yes               |
| avoidInnerPadding        | avoid inner button padding                                   | boolean                                         | no       | iOS/Android | yes               |
| avoidMinWidth            | avoid minimum width constraints                              | boolean                                         | no       | iOS/Android | yes               |
| backgroundColor          | Color of the button background                               | string                                          | no       | iOS/Android | yes               |
| borderRadius             | Custom border radius.                                        | number                                          | no       | iOS/Android | yes               |
| color                    | The Button text color (inherited from Text component)        | string                                          | no       | iOS/Android | yes               |
| disabled                 | Disable interactions for the component                       | boolean                                         | no       | iOS/Android | yes               |
| disabledBackgroundColor  | Color of the disabled button background                      | string                                          | no       | iOS/Android | yes               |
| enableShadow             | Control shadow visibility (iOS-only)                         | boolean                                         | no       | iOS         | no                |
| fullWidth                | should the button act as a coast to coast button (no border radius) | boolean                                         | no       | iOS/Android | yes               |
| getActiveBackgroundColor | callback for getting activeBackgroundColor (e.g. (calculatedBackgroundColor, prop) => {...}). Better set using ThemeManager | (backgroundColor: string, props: any) => string | no       | iOS/Android | yes               |
| hyperlink                | Button will look like a hyperlink                            | boolean                                         | no       | iOS/Android | yes               |
| iconOnRight              | Should the icon be right to the label                        | boolean                                         | no       | iOS/Android | yes               |
| iconProps                | Icon image props                                             | Partial<ImageProps>                             | no       | iOS/Android | yes               |
| iconSource               | Icon image source or a callback function that returns a source | ImageProps['source']\|Function                  | no       | iOS/Android | yes               |
| iconStyle                | Icon image style                                             | ImageStyle                                      | no       | iOS/Android | yes               |
| label                    | Text to show inside the button                               | string                                          | no       | iOS/Android | yes               |
| labelProps               | Props that will be passed to the button's Text label.        | TextProps                                       | no       | iOS/Android | yes               |
| labelStyle               | Additional styles for label text                             | TextStyle                                       | no       | iOS/Android | yes               |
| link                     | Button will look like a link                                 | boolean                                         | no       | iOS/Android | yes               |
| linkColor                | label color for when it's displayed as link or hyperlink     | string                                          | no       | iOS/Android | yes               |
| onPress                  | Actions handler                                              | (props: any) => void                            | no       | iOS/Android | yes               |
| outline                  | Button will have outline style                               | boolean                                         | no       | iOS/Android | yes               |
| outlineColor             | The outline color                                            | string                                          | no       | iOS/Android | yes               |
| outlineWidth             | The outline width                                            | number                                          | no       | iOS/Android | yes               |
| round                    | should the button be a round button                          | boolean                                         | no       | iOS/Android | yes               |
| size                     | Size of the button [large, medium, small, xSmall]            | ButtonSize                                      | no       | iOS/Android | yes               |
| supportRTL               | whether the icon should flip horizontally on RTL locals      | boolean                                         | no       | iOS/Android | yes               |

**Checkbox**：复选框组件，该组件扩展了[TouchableOpacity](https://wix.github.io/react-native-ui-lib/docs/components/basic/TouchableOpacity)属性。

| Name             | Description                                                  | Type                       | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------------------------- | -------- | ----------- | ----------------- |
| borderRadius     | The Checkbox border radius                                   | number                     | no       | iOS/Android | yes               |
| color            | The Checkbox color                                           | string                     | no       | iOS/Android | yes               |
| containerStyle   | Custom styling for the checkbox and label container          | ViewStyle                  | no       | iOS/Android | yes               |
| disabled         | Whether the checkbox should be disabled                      | boolean                    | no       | iOS/Android | yes               |
| iconColor        | The selected icon color                                      | string                     | no       | iOS/Android | yes               |
| label            | Add a label to the Checkbox                                  | string                     | no       | iOS/Android | yes               |
| labelProps       | Props to pass on to the label component                      | TextProps                  | no       | iOS/Android | yes               |
| labelStyle       | Pass to style the label                                      | TextStyle                  | no       | iOS/Android | yes               |
| onChangeValidity | Callback for when field validity has changed                 | (isValid: boolean) => void | no       | iOS/Android | yes               |
| onValueChange    | Callback function for value change event                     | (value) => void            | no       | iOS/Android | yes               |
| outline          | Alternative Checkbox outline style                           | boolean                    | no       | iOS/Android | yes               |
| required         | Whether the checkbox is required                             | boolean                    | no       | iOS/Android | yes               |
| selectedIcon     | The icon asset to use for the selected indication            | ImageRequireSource         | no       | iOS/Android | yes               |
| size             | The Checkbox size, affect both width and height              | number                     | no       | iOS/Android | yes               |
| style            | Custom styling for the Checkbox                              | ViewStyle                  | no       | iOS/Android | yes               |
| value            | The Checkbox value. If true the switch will be turned on. Default value is false | boolean                    | no       | iOS/Android | yes               |

**Chip**：芯片组件，该组件扩展了[TouchableOpacity](https://wix.github.io/react-native-ui-lib/docs/components/basic/TouchableOpacity)，[View](https://wix.github.io/react-native-ui-lib/docs/components/basic/View)属性。

| Name                  | Description                                                  | Type                                      | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ----------------------------------------- | -------- | ----------- | ----------------- |
| avatarProps           | Avatar props object                                          | AvatarProps                               | no       | iOS/Android | yes               |
| backgroundColor       | Background color                                             | string                                    | no       | iOS/Android | yes               |
| badgeProps            | Badge props object                                           | BadgeProps                                | no       | iOS/Android | yes               |
| borderRadius          | Border radius                                                | number                                    | no       | iOS/Android | yes               |
| containerStyle        | Component's container style                                  | ViewStyle                                 | no       | iOS/Android | yes               |
| dismissColor          | Dismiss color                                                | string                                    | no       | iOS/Android | yes               |
| dismissContainerStyle | Dismiss container style                                      | ImageStyle                                | no       | iOS/Android | yes               |
| dismissIcon           | Dismiss asset                                                | ImageSourcePropType                       | no       | iOS/Android | yes               |
| dismissIconStyle      | Dismiss style                                                | ImageStyle                                | no       | iOS/Android | yes               |
| iconProps             | Additional icon props                                        | Omit<ImageProps, 'source'>                | no       | iOS/Android | yes               |
| iconSource            | Left icon's source                                           | ImageSourcePropType                       | no       | iOS/Android | yes               |
| iconStyle             | Icon style                                                   | ImageStyle                                | no       | iOS/Android | yes               |
| label                 | Main Chip text                                               | string                                    | no       | iOS/Android | yes               |
| labelStyle            | Label's style                                                | TextStyle                                 | no       | iOS/Android | yes               |
| leftElement           | Left custom element                                          | JSX.Element                               | no       | iOS/Android | yes               |
| onDismiss             | Adds a dismiss button and serves as its callback             | (props: any) => void                      | no       | iOS/Android | yes               |
| onPress               | On Chip press callback                                       | (props: any) => void                      | no       | iOS/Android | yes               |
| resetSpacings         | Disables all internal elements default spacings. Helps reach a custom design | boolean                                   | no       | iOS/Android | yes               |
| rightElement          | Right custom element                                         | JSX.Element                               | no       | iOS/Android | yes               |
| rightIconSource       | Right icon's source                                          | ImageSourcePropType                       | no       | iOS/Android | yes               |
| size                  | Chip's size. Number or a width and height object             | number\|{{width: number, height: number}} | no       | iOS/Android | yes               |
| testID                | The test id for e2e tests                                    | string                                    | no       | iOS/Android | yes               |
| useCounter            | Display badge as counter (no background)                     | boolean                                   | no       | iOS/Android | yes               |
| useSizeAsMinimum      | Uses size as minWidth and minHeight                          | boolean                                   | no       | iOS/Android | yes               |

**RadioButton**：单选按钮组件。

| Name           | Description                                                  | Type                        | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | --------------------------- | -------- | ----------- | ----------------- |
| borderRadius   | The radio button border radius                               | number                      | no       | iOS/Android | yes               |
| color          | The color of the radio button                                | string                      | no       | iOS/Android | yes               |
| containerStyle | Additional styling for the container                         | ViewStyle                   | no       | iOS/Android | yes               |
| contentOnLeft  | Should the content be rendered left to the button            | boolean                     | no       | iOS/Android | yes               |
| disabled       | Whether the radio button should be disabled                  | boolean                     | no       | iOS/Android | yes               |
| iconOnRight    | Should the icon be on the right side of the label            | boolean                     | no       | iOS/Android | yes               |
| iconSource     | Icon image source                                            | ImageSource                 | no       | iOS/Android | yes               |
| iconStyle      | Icon image style                                             | ImageStyle                  | no       | iOS/Android | yes               |
| label          | A label for the radio button description                     | string                      | no       | iOS/Android | yes               |
| labelStyle     | Label style                                                  | TextStyle                   | no       | iOS/Android | yes               |
| onPress        | Invoked when pressing the button                             | (selected: boolean) => void | no       | iOS/Android | yes               |
| selected       | When using RadioButton without a RadioGroup, use this prop to toggle selection | boolean                     | no       | iOS/Android | yes               |
| size           | The size of the radio button, affect both width & height     | number                      | no       | iOS/Android | yes               |
| value          | The identifier value of the radio button. must be different than other RadioButtons in the same group | string \| number \| boolean | no       | iOS/Android | yes               |

**RadioGroup**：包裹单选按钮组件，和RadioButton配合使用。

| Name          | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| initialValue  | The initial value of the selected radio button               | string \| number \| boolean                                  | no       | iOS/Android | yes               |
| onValueChange | Invoked once when value changes, by selecting one of the radio buttons in the group | ((value?: string) => void)\|((value?: number) => void)\|((value?: boolean) => void)\|((value?: any) => void) | no       | iOS/Android | yes               |

**Slider**：滑块组件。

| Name                  | Description                                                  | Type                                 | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ------------------------------------ | -------- | ----------- | ----------------- |
| accessible            | If true the component will have accessibility features enabled | boolean                              | no       | iOS/Android | yes               |
| activeThumbStyle      | The active (during press) thumb style                        | ViewStyle                            | no       | iOS/Android | yes               |
| containerStyle        | The container style                                          | ViewStyle                            | no       | iOS/Android | yes               |
| disableActiveStyling  | If true the Slider will not change it's style on press       | boolean                              | no       | iOS/Android | yes               |
| disableRTL            | If true the Slider will stay in LTR mode even if the app is on RTL mode | boolean                              | no       | iOS/Android | yes               |
| disabled              | If true the Slider will be disabled and will appear in disabled color | boolean                              | no       | iOS/Android | yes               |
| initialMaximumValue   | Only when `useRange` is true, Initial maximum value          | number                               | no       | iOS/Android | yes               |
| initialMinimumValue   | Only when `useRange` is true, Initial minimum value          | number                               | no       | iOS/Android | yes               |
| maximumTrackTintColor | The track color                                              | string                               | no       | iOS/Android | yes               |
| maximumValue          | Track maximum value                                          | number                               | no       | iOS/Android | yes               |
| migrate               | Temporary prop required for migration to the Slider's new implementation | boolean                              | no       | iOS/Android | yes               |
| minimumTrackTintColor | The color used for the track from minimum value to current value | string                               | no       | iOS/Android | yes               |
| minimumValue          | Track minimum value                                          | number                               | no       | iOS/Android | yes               |
| onRangeChange         | Callback for onRangeChange. Returns values object with the min and max values | SliderOnRangeChange                  | no       | iOS/Android | yes               |
| onReset               | Callback that notifies when the reset function was invoked   | () => void                           | no       | iOS/Android | yes               |
| onSeekEnd             | Callback that notifies about slider seeking is finished      | () => void                           | no       | iOS/Android | yes               |
| onSeekStart           | Callback that notifies about slider seeking is started       | () => void                           | no       | iOS/Android | yes               |
| onValueChange         | Callback for onValueChange                                   | SliderOnValueChange                  | no       | iOS/Android | yes               |
| renderTrack           | Custom render instead of rendering the track                 | () => ReactElement \| ReactElement[] | no       | iOS/Android | yes               |
| step                  | Step value of the slider. The value should be between 0 and (maximumValue - minimumValue) | number                               | no       | iOS/Android | yes               |
| testID                | The component test id                                        | string                               | no       | iOS/Android | yes               |
| thumbStyle            | The thumb style                                              | ViewStyle                            | no       | iOS/Android | yes               |
| thumbTintColor        | Thumb color                                                  | string                               | no       | iOS/Android | yes               |
| trackStyle            | The track style                                              | ViewStyle                            | no       | iOS/Android | yes               |
| useGap                | If true the min and max thumbs will not overlap              | boolean                              | no       | iOS/Android | yes               |
| useRange              | If true the Slider will display a second thumb for the min value | boolean                              | no       | iOS/Android | yes               |
| value                 | Initial value                                                | number                               | no       | iOS/Android | yes               |

**Switch**：开关切换组件。

| Name          | Description                                                  | Type                     | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | ------------------------ | -------- | ----------- | ----------------- |
| disabled      | Whether the switch should be disabled                        | boolean                  | no       | iOS/Android | yes               |
| disabledColor | The Switch background color when it's disabled               | string                   | no       | iOS/Android | yes               |
| height        | The Switch height                                            | number                   | no       | iOS/Android | yes               |
| id            | Component id                                                 | string                   | no       | iOS/Android | yes               |
| offColor      | The Switch background color when it's turned off             | string                   | no       | iOS/Android | yes               |
| onColor       | The Switch background color when it's turned on              | string                   | no       | iOS/Android | yes               |
| onValueChange | Invoked with the new value when the value changes            | (value: boolean) => void | no       | iOS/Android | yes               |
| style         | Custom style                                                 | ViewStyle                | no       | iOS/Android | yes               |
| testID        | Component test id                                            | string                   | no       | iOS/Android | yes               |
| thumbColor    | The Switch's thumb color                                     | string                   | no       | iOS/Android | yes               |
| thumbSize     | The Switch's thumb size (width & height)                     | number                   | no       | iOS/Android | yes               |
| thumbStyle    | The Switch's thumb style                                     | ViewStyle                | no       | iOS/Android | yes               |
| value         | The value of the switch. If true the switch will be turned on. Default value is false | boolean                  | no       | iOS/Android | yes               |
| width         | The Switch width                                             | number                   | no       | iOS/Android | yes               |

**ChipsInput**：芯片输入组件，该组件扩展了[TextField](https://wix.github.io/react-native-ui-lib/docs/components/form/TextField)属性。

| Name             | Description                                          | Type                                          | Required | Platform    | HarmonyOS Support |
| ---------------- | ---------------------------------------------------- | --------------------------------------------- | -------- | ----------- | ----------------- |
| chips            | List of chips to render                              | ChipProps[]                                   | no       | iOS/Android | yes               |
| defaultChipProps | Default set of props to pass by default to all chips | ChipProps                                     | no       | iOS/Android | yes               |
| maxChips         | The maximum chips to allow adding                    | number                                        | no       | iOS/Android | yes               |
| onChange         | Callback for chips change (adding or removing chip)  | (newChips, changeReason, updatedChip) => void | no       | iOS/Android | yes               |

**ColorPalette**：调色板组件。

| Name            | Description                                                  | Type                                          | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | --------------------------------------------- | -------- | ----------- | ----------------- |
| animatedIndex   | Default is last，The index of the item to animate at first render | number                                        | no       | iOS/Android | yes               |
| backgroundColor | The ColorPalette's background color                          | string                                        | no       | iOS/Android | yes               |
| colors          | Array of colors to render in the palette                     | string[]                                      | no       | iOS/Android | yes               |
| containerStyle  | Component's container style                                  | ViewStyle                                     | no       | iOS/Android | yes               |
| containerWidth  | The container margins                                        | number                                        | no       | iOS/Android | yes               |
| loop            | Whether the colors pagination scrolls in a loop              | boolean                                       | no       | iOS/Android | yes               |
| numberOfRows    | The number of color rows from 2 to 5                         | number                                        | no       | iOS/Android | yes               |
| onValueChange   | Invoked once when value changes by selecting one of the swatches in the palette | (value: string, colorInfo: ColorInfo) => void | no       | iOS/Android | yes               |
| style           | Component's style                                            | ViewStyle                                     | no       | iOS/Android | yes               |
| swatchStyle     | Style to pass all the ColorSwatches in the palette           | ViewStyle                                     | no       | iOS/Android | yes               |
| testID          | The test id for e2e tests                                    | string                                        | no       | iOS/Android | yes               |
| usePagination   | Whether to use pagination when number of colors exceeds the number of rows | boolean                                       | no       | iOS/Android | yes               |
| value           | The value of the selected swatch                             | string                                        | no       | iOS/Android | yes               |

**ColorPicker**：选色器组件。

| Name                | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| accessibilityLabels | Accessibility labels as an object of strings                 | { addButton: string, dismissButton: string, doneButton: string, input: string} | no       | iOS/Android | yes               |
| animatedIndex       | Default is last，The index of the item to animate at first render | number                                                       | no       | iOS/Android | yes               |
| backgroundColor     | The ColorPicker's background color                           | string                                                       | no       | iOS/Android | yes               |
| colors              | Array of colors for the picker's color palette (hex values)  | string[]                                                     | no       | iOS/Android | yes               |
| onValueChange       | Callback for the picker's color palette change               | (value: string, colorInfo: ColorInfo) => void                | no       | iOS/Android | yes               |
| testID              | The test id for e2e tests                                    | string                                                       | no       | iOS/Android | yes               |
| value               | The value of the selected swatch                             | string                                                       | no       | iOS/Android | yes               |

**ColorSwatch**：颜色样板组件。

| Name        | Description                                                  | Type                                          | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | --------------------------------------------- | -------- | ----------- | ----------------- |
| animated    | Is first render should be animated                           | boolean                                       | no       | iOS/Android | yes               |
| color       | The color of the ColorSwatch                                 | string                                        | no       | iOS/Android | yes               |
| index       | The index of the Swatch if in array                          | number                                        | no       | iOS/Android | yes               |
| onPress     | Callback from press event                                    | (value: string, colorInfo: ColorInfo) => void | no       | iOS/Android | yes               |
| selected    | Is the initial state is selected                             | boolean                                       | no       | iOS/Android | yes               |
| size        | Color Swatch size                                            | number                                        | no       | iOS/Android | yes               |
| style       | Component's style                                            | ViewStyle                                     | no       | iOS/Android | yes               |
| testID      | The test id for e2e tests                                    | string                                        | no       | iOS/Android | yes               |
| unavailable | Is the initial state is unavailable                          | boolean                                       | no       | iOS/Android | yes               |
| value       | Must be different than other ColorSwatches in the same group，The identifier value of the ColorSwatch in a ColorSwatch palette | string                                        | no       | iOS/Android | yes               |

**DateTimePicker**：时间选择组件，该组件扩展了[TextField](https://wix.github.io/react-native-ui-lib/docs/components/form/TextField)属性，依赖[@react-native-community/datetimepicker](/zh-cn/react-native-community-datetimepicker)库。

| Name                    | Description                                                  | Type                                              | Required | Platform    | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | ------------------------------------------------- | -------- | ----------- | ----------------- |
| dateTimeFormatter       | A callback function to format the time or date               | (value: Date, mode: DateTimePickerMode) => string | no       | iOS/Android | yes               |
| dialogProps             | Props to pass the Dialog component                           | DialogProps                                       | no       | iOS/Android | yes               |
| display                 | Defines the visual display of the picker. The default value is 'spinner' on iOS and 'default' on Android. The list of all possible values are default, spinner, calendar or clock on Android and default, spinner, compact or inline for iOS. Full list can be found here:[react-native-datetimepicker](https://github.com/react-native-datetimepicker/datetimepicker#display-optional) | string                                            | no       | iOS/Android | yes               |
| editable                | Should this input be editable or disabled                    | boolean                                           | no       | iOS/Android | yes               |
| headerStyle             | Style to apply to the iOS dialog header                      | ViewStyle                                         | no       | iOS/Android | yes               |
| is24Hour                | Android only, Allows changing of the time picker to a 24 hour format | boolean                                           | no       | Android     | no                |
| locale                  | iOS only, Allows changing of the locale of the component     | string                                            | no       | iOS         | yes               |
| maximumDate             | The maximum date or time value to use                        | Date                                              | no       | iOS/Android | yes               |
| minimumDate             | The minimum date or time value to use                        | Date                                              | no       | iOS/Android | yes               |
| minuteInterval          | iOS only, The interval at which minutes can be selected. Possible values are: 1, 2, 3, 4, 5, 6, 10, 12, 15, 20, 30 | number                                            | no       | iOS         | yes               |
| mode                    | The type of picker to display ('date' or 'time')             | DATE \|TIME                                       | no       | iOS/Android | yes               |
| onChange                | Called when the date/time change                             | () => Date                                        | no       | iOS/Android | yes               |
| renderInput             | Render custom input                                          | JSX.Element                                       | no       | iOS/Android | yes               |
| themeVariant            | Override system theme variant (dark or light mode) used by the date picker | LIGHT \|DARK                                      | no       | iOS/Android | yes               |
| timeZoneOffsetInMinutes | iOS only, Allows changing of the timeZone of the date picker. By default it uses the device's time zone | number                                            | no       | iOS         | yes               |
| value                   | Defaults to device's date and time, The initial value to set the picker to | Date                                              | no       | iOS/Android | yes               |

**MaskedInput**：掩码输入组件，该组件扩展了[TextInput](https://reactnative.dev/docs/textinput)属性。

| Name             | Description                                                  | Type               | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | ------------------ | -------- | ----------- | ----------------- |
| containerStyle   | container style for the masked input container               | ViewStyle          | no       | iOS/Android | yes               |
| renderMaskedText | callback for rendering the custom input out of the value returns from the actual input | React.ReactElement | no       | iOS/Android | yes               |

**NumberInput**：数字输入框组件。

| Name              | Description                                                  | Type                            | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | ------------------------------- | -------- | ----------- | ----------------- |
| containerStyle    | Container style of the whole component                       | ViewStyle                       | no       | iOS/Android | yes               |
| contextMenuHidden | Requires @react-native-community/clipboard to be installed. If true, context menu is hidden. | boolean                         | no       | iOS/Android | yes               |
| fractionDigits    | Number of digits after the decimal point. Must be in the range 0 - 20, inclusive. | number                          | no       | iOS/Android | yes               |
| initialNumber     | A valid number (in en locale, i.e. only digits and a decimal point). | number                          | no       | iOS/Android | yes               |
| leadingText       | A leading text                                               | string                          | no       | iOS/Android | yes               |
| leadingTextStyle  | The style of the leading text                                | TextStyle                       | no       | iOS/Android | yes               |
| onChangeNumber    | Callback that is called when the number value has changed.   | (data: NumberInputData) => void | no       | iOS/Android | yes               |
| textFieldProps    | Most of TextField's props can be applied, except for ones that are passed directly via named props. | TextFieldProps                  | no       | iOS/Android | yes               |
| trailingText      | A trailing text                                              | string                          | no       | iOS/Android | yes               |
| trailingTextStyle | The style of the trailing text                               | ViewStyle                       | no       | iOS/Android | yes               |

**Picker**：弹窗选择组件。

| Name               | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| customPickerProps  | Custom picker props (when using renderPicker, will apply on the button wrapper) | object                                                       | no       | iOS/Android | yes               |
| enableModalBlur    | iOS only，Adds blur effect to picker modal                   | boolean                                                      | no       | iOS         | yes               |
| fieldType          | Pass for different field type UI (form, filter or settings)  | PickerFieldTypes                                             | no       | iOS/Android | yes               |
| getLabel           | A function that returns the label to show for the selected Picker value | (value: string \| number) => void                            | no       | iOS/Android | yes               |
| items              | Data source for Picker                                       | {label: string, value: string \| number}[]                   | no       | iOS/Android | yes               |
| listProps          | Pass props to the list component that wraps the picker options (allows to control FlatList behavior) | FlatListProps                                                | no       | iOS/Android | yes               |
| migrate            | Temporary prop required for migration to Picker's new API    | boolean                                                      | no       | iOS/Android | yes               |
| mode               | SINGLE mode or MULTI mode                                    | SINGLE \| MULTI                                              | no       | iOS/Android | yes               |
| onChange           | Callback for when picker value change                        | (value: string \| number) => void                            | no       | iOS/Android | yes               |
| onPress            | Add onPress callback for when pressing the picker            | () => void                                                   | no       | iOS/Android | yes               |
| onSearchChange     | Callback for picker modal search input text change (only when passing showSearch) | (searchValue: string) => void                                | no       | iOS/Android | yes               |
| pickerModalProps   | Pass props to the picker modal                               | ModalProps                                                   | no       | iOS/Android | yes               |
| renderCustomModal  | Render custom picker modal                                   | ({visible, children, toggleModal}) => void)                  | no       | iOS/Android | yes               |
| renderCustomSearch | Render custom search input (only when passing showSearch)    | (props) => void                                              | no       | iOS/Android | yes               |
| renderItem         | Render custom picker item                                    | (value, {{...props, isSelected}}, itemLabel) => void         | no       | iOS/Android | yes               |
| renderPicker       | Render custom picker - input will be value (see above)\Example:\renderPicker = (selectedItem) => {...} | (selectedItem, itemLabel) => void                            | no       | iOS/Android | yes               |
| searchPlaceholder  | Placeholder text for the search input (only when passing showSearch) | string                                                       | no       | iOS/Android | yes               |
| searchStyle        | Style object for the search input (only when passing showSearch) | {color: string, placeholderTextColor: string, selectionColor: string} | no       | iOS/Android | yes               |
| selectionLimit     | Limit the number of selected items                           | number                                                       | no       | iOS/Android | yes               |
| showSearch         | Show search input to filter picker items by label            | boolean                                                      | no       | iOS/Android | yes               |
| topBarProps        | The picker modal top bar props                               | Modal's TopBarProps                                          | no       | iOS/Android | yes               |
| useSafeArea        | Add safe area in the Picker modal view                       | boolean                                                      | no       | iOS/Android | yes               |
| useWheelPicker     | Use wheel picker instead of a list picker                    | boolean                                                      | no       | iOS/Android | yes               |
| value              | Picker current value                                         | string \| number                                             | no       | iOS/Android | yes               |

**Picker.Item**：弹窗选择Item组件，配合Picker组件使用。

| Name              | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| disabled          | Is the item disabled                                         | boolean                                                      | no       | iOS/Android | yes               |
| getItemLabel      | Custom function for the item label                           | (value: string \| number) => string                          | no       | iOS/Android | yes               |
| isSelected        | Is the item selected                                         | boolean                                                      | no       | iOS/Android | yes               |
| label             | Item's label                                                 | string                                                       | no       | iOS/Android | yes               |
| labelStyle        | Item's label style                                           | ViewStyle                                                    | no       | iOS/Android | yes               |
| onPress           | Callback for onPress action, will stop selection if false is returned | (selected: boolean \| undefined, props: any) => void \| Promise<boolean>; | no       | iOS/Android | yes               |
| onSelectedLayout  | Callback for onLayout event                                  | (event: LayoutChangeEvent) => void                           | no       | iOS/Android | yes               |
| selectedIcon      | Pass to change the selected icon                             | string                                                       | no       | iOS/Android | yes               |
| selectedIconColor | Pass to change the selected icon color                       | ImageSource                                                  | no       | iOS/Android | yes               |
| value             | Item's value                                                 | string \| number                                             | no       | iOS/Android | yes               |

**SectionsWheelPicker**：滚动选择组件。

| Name                | Description                                         | Type             | Required | Platform    | HarmonyOS Support |
| ------------------- | --------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| activeTextColor     | Text color for the focused row                      | string           | no       | iOS/Android | yes               |
| faderProps          | Custom props for fader.                             | FaderProps       | no       | iOS/Android | yes               |
| inactiveTextColor   | Text color for other, non-focused rows              | string           | no       | iOS/Android | yes               |
| itemHeight          | Describe the height of each item in the WheelPicker | number           | no       | iOS/Android | yes               |
| numberOfVisibleRows | Describe the number of rows visible                 | number           | no       | iOS/Android | yes               |
| sections            | Array of sections                                   | WheelPickerProps | no       | iOS/Android | yes               |
| testID              | The component test id                               | string           | no       | iOS/Android | yes               |
| textStyle           | Row text style                                      | TextStyle        | no       | iOS/Android | yes               |

**SegmentedControl**：切换值组件。

| Name                  | Description                                     | Type                      | Required | Platform    | HarmonyOS Support |
| --------------------- | ----------------------------------------------- | ------------------------- | -------- | ----------- | ----------------- |
| activeBackgroundColor | The background color of the active segment      | string                    | no       | iOS/Android | yes               |
| activeColor           | The color of the active segment label           | string                    | no       | iOS/Android | yes               |
| backgroundColor       | The background color of the inactive segments   | string                    | no       | iOS/Android | yes               |
| borderRadius          | The segmentedControl borderRadius               | number                    | no       | iOS/Android | yes               |
| containerStyle        | Additional spacing styles for the container     | ViewStyle                 | no       | iOS/Android | yes               |
| iconOnRight           | Should the icon be on right of the label        | boolean                   | no       | iOS/Android | yes               |
| initialIndex          | Initial index to be active                      | number                    | no       | iOS/Android | yes               |
| onChangeIndex         | Callback for when index has change.             | (index: number) => void   | no       | iOS/Android | yes               |
| outlineColor          | The color of the active segment outline         | string                    | no       | iOS/Android | yes               |
| outlineWidth          | The width of the active segment outline         | number                    | no       | iOS/Android | yes               |
| segmentLabelStyle     | Segment label style                             | TextStyle                 | no       | iOS/Android | yes               |
| segments              | Array on segments                               | SegmentedControlItemProps | no       | iOS/Android | yes               |
| segmentsStyle         | Additional style for the segments               | ViewStyle                 | no       | iOS/Android | yes               |
| style                 | Custom style to inner container                 | ViewStyle                 | no       | iOS/Android | yes               |
| testID                | Component test id                               | string                    | no       | iOS/Android | yes               |
| throttleTime          | Trailing throttle time of changing index in ms. | number                    | no       | iOS/Android | yes               |

**Stepper**：步进器组件。

| Name               | Description                                         | Type                                     | Required | Platform    | HarmonyOS Support |
| ------------------ | --------------------------------------------------- | ---------------------------------------- | -------- | ----------- | ----------------- |
| accessibilityLabel | Component accessibility label                       | string                                   | no       | iOS/Android | yes               |
| disabled           | Disables interaction with the stepper               | boolean                                  | no       | iOS/Android | yes               |
| maxValue           | Maximum value                                       | number                                   | no       | iOS/Android | yes               |
| minValue           | Minimum value                                       | number                                   | no       | iOS/Android | yes               |
| onValueChange      | Value change callback function                      | (value: number, testID?: string) => void | no       | iOS/Android | yes               |
| small              | Renders a small sized Stepper                       | boolean                                  | no       | iOS/Android | yes               |
| step               | The step to increase and decrease by (default is 1) | number                                   | no       | iOS/Android | yes               |
| testID             | Test id for component                               | string                                   | no       | iOS/Android | yes               |
| value              | Stepper value                                       | number                                   | no       | iOS/Android | yes               |

**TextField**：文本域组件，扩展了[TextInput](https://reactnative.dev/docs/textinput)属性。

| Name                      | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| centered                  | Whether to center the TextField - container and label        | boolean                                                      | no       | iOS/Android | yes               |
| charCounterStyle          | Pass custom style to character counter text                  | TextStyle                                                    | no       | iOS/Android | yes               |
| color                     | Input color                                                  | ColorType                                                    | no       | iOS/Android | yes               |
| containerProps            | Container props of the whole component                       | Omit<ViewProps, 'style'>                                     | no       | iOS/Android | yes               |
| containerStyle            | Container style of the whole component                       | ViewStyle                                                    | no       | iOS/Android | yes               |
| enableErrors              | Should support showing validation error message              | boolean                                                      | no       | iOS/Android | yes               |
| fieldStyle                | Internal style for the field container to style the field underline, outline and fill color | ViewStyle \| (context: FieldContextType, props) => ViewStyle | no       | iOS/Android | yes               |
| floatOnFocus              | Should placeholder float on focus or when start typing       | boolean                                                      | no       | iOS/Android | yes               |
| floatingPlaceholder       | Pass to add floating placeholder support                     | boolean                                                      | no       | iOS/Android | yes               |
| floatingPlaceholderColor  | The floating placeholder color                               | ColorType                                                    | no       | iOS/Android | yes               |
| floatingPlaceholderStyle  | Custom style for the floating placeholder                    | TextStyle                                                    | no       | iOS/Android | yes               |
| formatter                 | Custom formatter for the input value (used only when input if not focused) | (value) => string \| undefined                               | no       | iOS/Android | yes               |
| hint                      | A hint text to display when focusing the field               | string                                                       | no       | iOS/Android | yes               |
| label                     | Field label                                                  | string                                                       | no       | iOS/Android | yes               |
| labelColor                | Field label color. Either a string or color by state map ({default, focus, error, disabled, readonly}) | ColorType                                                    | no       | iOS/Android | yes               |
| labelProps                | Pass extra props to the label Text element                   | TextProps                                                    | no       | iOS/Android | yes               |
| labelStyle                | Custom style for the field label                             | TextStyle                                                    | no       | iOS/Android | yes               |
| leadingAccessory          | Pass to render a leading element                             | ReactElement                                                 | no       | iOS/Android | yes               |
| onChangeValidity          | Callback for when field validity has changed                 | (isValid: boolean) => void                                   | no       | iOS/Android | yes               |
| onValidationFailed        | Callback for when field validated and failed                 | (failedValidatorIndex: number) => void                       | no       | iOS/Android | yes               |
| placeholder               | The placeholder for the field                                | string                                                       | no       | iOS/Android | yes               |
| placeholderTextColor      | Placeholder text color                                       | ColorType                                                    | no       | iOS/Android | yes               |
| preset                    | Predefined preset to use for styling the field               | 'default' \| null \|string                                   | no       | iOS/Android | yes               |
| readonly                  | A UI preset for read only state                              | boolean                                                      | no       | iOS/Android | yes               |
| recorderTag               | Recorder Tag                                                 | 'mask' \| 'unmask'                                           | no       | iOS/Android | yes               |
| retainValidationSpace     | Keep the validation space even if there is no validation message | boolean                                                      | no       | iOS/Android | yes               |
| showCharCounter           | Should show a character counter (works only with maxLength)  | boolean                                                      | no       | iOS/Android | yes               |
| showMandatoryIndication   | Whether to show a mandatory field indication                 | boolean                                                      | no       | iOS/Android | yes               |
| trailingAccessory         | Pass to render a trailing element                            | ReactElement                                                 | no       | iOS/Android | yes               |
| useGestureHandlerInput    | Use react-native-gesture-handler instead of react-native for the base TextInput | boolean                                                      | no       | iOS/Android | yes               |
| validate                  | A single or multiple validator. Can be a string (required, email) or custom function. | Validator \| Validator []                                    | no       | iOS/Android | yes               |
| validateOnBlur            | Should validate when losing focus of TextField               | boolean                                                      | no       | iOS/Android | yes               |
| validateOnChange          | Should validate when the TextField value changes             | boolean                                                      | no       | iOS/Android | yes               |
| validateOnStart           | Should validate when the TextField mounts                    | boolean                                                      | no       | iOS/Android | yes               |
| validationMessage         | The validation message to display when field is invalid (depends on validate) | string \| string[]                                           | no       | iOS/Android | yes               |
| validationMessagePosition | The position of the validation message (top/bottom)          | ValidationMessagePosition                                    | no       | iOS/Android | yes               |
| validationMessageStyle    | Custom style for the validation message                      | TextStyle                                                    | no       | iOS/Android | yes               |

**WheelPicker**：轮式拾取器组件。

| Name                | Description                                                  | Type                                            | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | ----------------------------------------------- | -------- | ----------- | ----------------- |
| activeTextColor     | Text color for the focused row                               | string                                          | no       | iOS/Android | yes               |
| align               | Align the content to center, right ot left                   | WheelPickerAlign                                | no       | iOS/Android | yes               |
| flatListProps       | Props to be sent to the FlatList.                            | FlatListProps                                   | no       | iOS/Android | yes               |
| inactiveTextColor   | Text color for other, non-focused rows                       | string                                          | no       | iOS/Android | yes               |
| initialValue        | Initial value (uncontrolled)                                 | number \| string                                | no       | iOS/Android | yes               |
| itemHeight          | Height of each item in the WheelPicker                       | number                                          | no       | iOS/Android | yes               |
| items               | Data source for WheelPicker                                  | WheelPickerItemProps[]                          | no       | iOS/Android | yes               |
| label               | Additional label to render next to the items text            | string                                          | no       | iOS/Android | yes               |
| labelProps          | Additional label's props                                     | TextProps                                       | no       | iOS/Android | yes               |
| labelStyle          | Additional label's style                                     | TextStyle                                       | no       | iOS/Android | yes               |
| numberOfVisibleRows | Number of rows visible                                       | number                                          | no       | iOS/Android | yes               |
| onChange            | Change item event callback                                   | (item: string \| number, index: number) => void | no       | iOS/Android | yes               |
| separatorsStyle     | Extra style for the separators                               | ViewStyle                                       | no       | iOS/Android | yes               |
| style               | height is computed according to itemHeight * numberOfVisibleRows. Container's custom style | ViewStyle                                       | no       | iOS/Android | yes               |
| testID              | test identifier                                              | string                                          | no       | iOS/Android | yes               |
| textStyle           | Row text custom style                                        | TextStyle                                       | no       | iOS/Android | yes               |

**Incubator.Dialog**：弹出对话框组件。

| Name                  | Description                                                  | Type                          | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ----------------------------- | -------- | ----------- | ----------------- |
| containerProps        | Extra props for the container                                | ViewProps                     | no       | iOS/Android | yes               |
| containerStyle        | The Dialog`s container style (it is set to {position: 'absolute'}) `ViewStyle ` | ViewStyle                     | no       | iOS/Android | yes               |
| direction             | The direction from which and to which the dialog is animating \ panning (default down). | up \|down \|left \|right      | no       | iOS/Android | yes               |
| headerProps           | The Dialog's header (title, subtitle etc)                    | DialogHeaderProps             | no       | iOS/Android | yes               |
| ignoreBackgroundPress | Whether or not to ignore background press.                   | boolean                       | no       | iOS/Android | yes               |
| modalProps            | Pass props to the dialog modal                               | ModalProps                    | no       | iOS/Android | yes               |
| onDismiss             | Callback that is called after the dialog's dismiss (after the animation has ended). | (props?: DialogProps) => void | no       | iOS/Android | yes               |
| testID                | Used to locate this view in end-to-end tests.The container has the original id.Supported inner elements IDs:`${TestID}.modal` - the Modal's id.`${TestID}. overlayFadingBackground` - the fading background id. | string                        | no       | iOS/Android | yes               |
| visible               | The visibility of the dialog                                 | boolean                       | no       | iOS/Android | yes               |

**Dialog.Header**：弹窗头部组件。

| Name                  | Description                                                  | Type                 | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | -------------------- | -------- | ----------- | ----------------- |
| bottomAccessory       | Pass to render a bottom element below the subtitle           | ReactElement         | no       | iOS/Android | yes               |
| contentContainerStyle | Style for the leading + content + trailing components (without the bottomAccessory) | ViewProps['style']   | no       | iOS/Android | yes               |
| leadingAccessory      | Pass to render a leading element                             | ReactElement         | no       | iOS/Android | yes               |
| onPress               | onPress callback for the inner content                       | () => void           | no       | iOS/Android | yes               |
| showDivider           | Show the header's divider                                    | boolean              | no       | iOS/Android | yes               |
| showKnob              | Show the header's knob                                       | boolean              | no       | iOS/Android | yes               |
| subtitle              | Subtitle                                                     | string               | no       | iOS/Android | yes               |
| subtitleProps         | Subtitle extra props                                         | TextProps            | no       | iOS/Android | yes               |
| subtitleStyle         | Subtitle text style                                          | StyleProp<TextStyle> | no       | iOS/Android | yes               |
| title                 | Title                                                        | string               | no       | iOS/Android | yes               |
| titleProps            | Title extra props                                            | TextProps            | no       | iOS/Android | yes               |
| titleStyle            | Title text style                                             | StyleProp<TextStyle> | no       | iOS/Android | yes               |
| topAccessory          | Pass to render a top element above the title                 | ReactElement         | no       | iOS/Android | yes               |
| trailingAccessory     | Pass to render a trailing element                            | ReactElement         | no       | iOS/Android | yes               |

**Incubator.Slider**：滑块组件。

| Name                   | Description                                                  | Type                                  | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------- | -------- | ----------- | ----------------- |
| accessible             | If true the component will have accessibility features enabled | boolean                               | no       | iOS/Android | yes               |
| activeThumbStyle       | The active (during press) thumb style                        | ViewStyle                             | no       | iOS/Android | yes               |
| containerStyle         | The container style                                          | ViewStyle                             | no       | iOS/Android | yes               |
| disableActiveStyling   | If true the Slider will not change it's style on press       | boolean                               | no       | iOS/Android | yes               |
| disableRTL             | If true the Slider will stay in LTR mode even if the app is on RTL mode | boolean                               | no       | iOS/Android | yes               |
| disabled               | If true the Slider will be disabled and will appear in disabled color | boolean                               | no       | iOS/Android | yes               |
| disabledThumbTintColor | Disabled thumb color                                         | string                                | no       | iOS/Android | yes               |
| enableThumbShadow      | Whether the thumb will have a shadow (with 'migrate' true only) | boolean                               | no       | iOS/Android | yes               |
| initialMaximumValue    | Only when `useRange` is true. Initial maximum value          | number                                | no       | iOS/Android | yes               |
| initialMinimumValue    | Only when `useRange` is true. Initial minimum value          | number                                | no       | iOS/Android | yes               |
| maximumTrackTintColor  | The track color                                              | string                                | no       | iOS/Android | yes               |
| maximumValue           | Track maximum value                                          | number                                | no       | iOS/Android | yes               |
| minimumTrackTintColor  | The color used for the track from minimum value to current value | string                                | no       | iOS/Android | yes               |
| minimumValue           | Track minimum value                                          | number                                | no       | iOS/Android | yes               |
| onRangeChange          | Callback for onRangeChange. Returns values object with the min and max values | SliderOnRangeChange                   | no       | iOS/Android | yes               |
| onReset                | Callback that notifies when the reset function was invoked   | () => void                            | no       | iOS/Android | yes               |
| onSeekEnd              | Callback that notifies about slider seeking is finished      | () => void                            | no       | iOS/Android | yes               |
| onSeekStart            | Callback that notifies about slider seeking is started       | () => void                            | no       | iOS/Android | yes               |
| onValueChange          | Callback for onValueChange                                   | SliderOnValueChange                   | no       | iOS/Android | yes               |
| renderTrack            | Custom render instead of rendering the track                 | () => ReactElement  \| ReactElement[] | no       | iOS/Android | yes               |
| step                   | Step value of the slider. The value should be between 0 and (maximumValue - minimumValue) | number                                | no       | iOS/Android | yes               |
| testID                 | The component test id                                        | string                                | no       | iOS/Android | yes               |
| throttleTime           | Control the throttle time of the onValueChange and onRangeChange callbacks | number                                | no       | iOS/Android | yes               |
| thumbHitSlop           | Defines how far a touch event can start away from the thumb  | number                                | no       | iOS/Android | yes               |
| thumbStyle             | The thumb style                                              | ViewStyle                             | no       | iOS/Android | yes               |
| thumbTintColor         | Thumb color                                                  | string                                | no       | iOS/Android | yes               |
| trackStyle             | The track style                                              | ViewStyle                             | no       | iOS/Android | yes               |
| useGap                 | If true the min and max thumbs will not overlap              | boolean                               | no       | iOS/Android | yes               |
| useRange               | If true the Slider will display a second thumb for the min value | boolean                               | no       | iOS/Android | yes               |
| value                  | Initial value                                                | number                                | no       | iOS/Android | yes               |

**Incubator.Toast**：非中断式弹窗组件。

| Name                 | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| action               | A single action for the user (showLoader will override this) | ButtonProps                                                  | no       | iOS/Android | yes               |
| autoDismiss          | Time of milliseconds to automatically invoke the onDismiss callback | number                                                       | no       | iOS/Android | yes               |
| backgroundColor      | The toast background color                                   | string                                                       | no       | iOS/Android | yes               |
| centerMessage        | Should message be centered in the toast                      | boolean                                                      | no       | iOS/Android | yes               |
| containerStyle       | Toast container style                                        | ViewStyle                                                    | no       | iOS/Android | yes               |
| elevation            | Android only. Custom elevation                               | number                                                       | no       | Android     | no                |
| enableHapticFeedback | Whether to trigger an haptic feedback once the toast is shown (requires react-native-haptic-feedback dependency) | boolean                                                      | no       | iOS/Android | yes               |
| icon                 | A custom icon to render on the left side of the toast        | ImageSourcePropType                                          | no       | iOS/Android | yes               |
| iconColor            | The icon color                                               | string                                                       | no       | iOS/Android | yes               |
| message              | Toast message                                                | string                                                       | no       | iOS/Android | yes               |
| messageProps         | Toast message props                                          | TextProps                                                    | no       | iOS/Android | yes               |
| messageStyle         | Toast message style                                          | StyleProp <TextStyle>                                        | no       | iOS/Android | yes               |
| onAnimationEnd       | Callback for end of toast animation                          | (visible?: boolean) => void                                  | no       | iOS/Android | yes               |
| onDismiss            | Callback for the toast dismissal                             | () => void                                                   | no       | iOS/Android | yes               |
| position             | The position of the toast. 'top' or 'bottom'.                | 'top' \| 'bottom'                                            | no       | iOS/Android | yes               |
| preset               | Pass to have preset UI                                       | ToastPreset ('success' \| 'failure' \| 'general' \| 'offline') | no       | iOS/Android | yes               |
| renderAttachment     | Render a custom view that will appear permanently above or below a Toast, depends on the Toast's position and animate with it when the Toast is made visible or dismissed | () => JSX.Element \| undefined                               | no       | iOS/Android | yes               |
| showLoader           | Whether to show a loader                                     | boolean                                                      | no       | iOS/Android | yes               |
| style                | Toast style                                                  | ViewStyle                                                    | no       | iOS/Android | yes               |
| swipeable            | Whether to support dismissing the toast with a swipe gesture. Requires to pass onDismiss method to control visibility | boolean                                                      | no       | iOS/Android | yes               |
| testID               | The component test id                                        | string                                                       | no       | iOS/Android | yes               |
| visible              | Whether to show or hide the toast                            | boolean                                                      | no       | iOS/Android | yes               |
| zIndex               | Custom zIndex for toast                                      | number                                                       | no       | iOS/Android | yes               |

**Dash**：阔折现组件。

| Name           | Description                           | Type      | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------- | --------- | -------- | ----------- | ----------------- |
| color          | The color of the dashes               | string    | no       | iOS/Android | yes               |
| containerStyle | The container style                   | ViewStyle | no       | iOS/Android | yes               |
| gap            | The gap between the dashes            | number    | no       | iOS/Android | yes               |
| length         | The length of the dashes              | number    | no       | iOS/Android | yes               |
| style          | Additional style to the dashes        | ViewStyle | no       | iOS/Android | yes               |
| thickness      | The thickness of the dashes           | number    | no       | iOS/Android | yes               |
| vertical       | Is the dashed line should be vertical | boolean   | no       | iOS/Android | yes               |

**ExpandableSection**：展开收起组件。

| Name          | Description                                              | Type            | Required | Platform    | HarmonyOS Support |
| ------------- | -------------------------------------------------------- | --------------- | -------- | ----------- | ----------------- |
| children      | The expandable's children                                | React.ReactNode | no       | iOS/Android | yes               |
| expanded      | Should the ExpandableSection be expanded                 | boolean         | no       | iOS/Android | yes               |
| onPress       | Called when pressing the header of the ExpandableSection | () => void      | no       | iOS/Android | yes               |
| sectionHeader | Header element                                           | JSX.Element     | no       | iOS/Android | yes               |
| testID        | testing identifier                                       | string          | no       | iOS/Android | yes               |
| top           | Should it open above the 'sectionHeader'                 | boolean         | no       | iOS/Android | yes               |

**Fader**：渐变淡入淡出组件。

| Name      | Description                                        | Type                           | Required | Platform    | HarmonyOS Support |
| --------- | -------------------------------------------------- | ------------------------------ | -------- | ----------- | ----------------- |
| position  | The position of the fader (the image is different) | START  \|END \| TOP  \| BOTTOM | no       | iOS/Android | yes               |
| size      | change the size of the fade view                   | number                         | no       | iOS/Android | yes               |
| tintColor | Change the tint color of the fade view             | string                         | no       | iOS/Android | yes               |
| visible   | Whether the fader is visible (default is true)     | boolean                        | no       | iOS/Android | yes               |

**Gradient**：渐变色组件。

| Name          | Description                       | Type          | Required | Platform    | HarmonyOS Support |
| ------------- | --------------------------------- | ------------- | -------- | ----------- | ----------------- |
| color         | The color of the gradient         | string        | no       | iOS/Android | yes               |
| numberOfSteps | The number of steps               | number        | no       | iOS/Android | yes               |
| style         | Additional style to the component | ViewStyle     | no       | iOS/Android | yes               |
| type          | hue \| lightness \| saturation    | GradientTypes | no       | iOS/Android | yes               |

**KeyboardAccessoryView**：键盘附件视图。

| Name                  | Description                                                  | Type                     | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ------------------------ | -------- | ----------- | ----------------- |
| kbComponent           | The keyboard ID (the componentID sent to KeyboardRegistry)   | string                   | no       | iOS/Android | no                |
| kbInitialProps        | The props that will be sent to the KeyboardComponent         | any                      | no       | iOS/Android | no                |
| kbInputRef            | iOS only. The reference to the actual text input (or the keyboard may not reset when instructed to, etc.). | any                      | no       | iOS         | no                |
| onHeightChanged       | A callback for when the height is changed                    | (height: number) => void | no       | iOS/Android | no                |
| onItemSelected        | Callback that will be called when an item on the keyboard has been pressed. | () => void               | no       | iOS/Android | no                |
| onKeyboardResigned    | Callback that will be called once the keyboard has been closed | () => void               | no       | iOS/Android | no                |
| onRequestShowKeyboard | Callback that will be called if KeyboardRegistry.requestShowKeyboard is called. | () => void               | no       | iOS/Android | no                |
| renderContent         | Content to be rendered above the keyboard                    | () => React.ReactElement | no       | iOS/Android | yes               |

**KeyboardAwareInsetsView**：用于在使用键盘时添加插入，可能会隐藏部分屏幕，该组件扩展了[KeyboardTrackingView](https://wix.github.io/react-native-ui-lib/docs/components/infra/KeyboardTrackingView)属性，此组件仅适用与iOS。

| Name                    | Description                                                  | Type      | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | --------- | -------- | -------- | ----------------- |
| KeyboardAwareInsetsView | Used to add an inset when a keyboard is used and might hide part of the screen. | Component | no       | iOS      | no                |

**KeyboardRegistry**：用于注册键盘并在键盘上执行某些操作。

| Name                | Description                                                  | Type            | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | --------------- | -------- | ----------- | ----------------- |
| addListener         | Add a listener for a callback. globalID (string) - ID that includes the componentID and the event name (i.e. if componentID='kb1' globalID='kb1.onItemSelected') callback (function) - the callback to be called when the said event happens | static function | no       | iOS/Android | yes               |
| getAllKeyboards     | Get all keyboards                                            | static function | no       | iOS/Android | yes               |
| getKeyboard         | Get a specific keyboard componentID (string) - the ID of the keyboard. | static function | no       | iOS/Android | yes               |
| getKeyboards        | Get keyboards by IDs componentIDs (string[]) - the ID of the keyboard. | static function | no       | iOS/Android | yes               |
| notifyListeners     | Notify that an event has occurred. globalID (string) - ID that includes the componentID and the event name (i.e. if componentID='kb1' globalID='kb1.onItemSelected') args (object) - data to be sent to the listener. | static function | no       | iOS/Android | yes               |
| onItemSelected      | Default event to be used for when an item on the keyboard has been pressed. componentID (string) - the ID of the keyboard. args (object) - data to be sent to the listener. | static function | no       | iOS/Android | yes               |
| registerKeyboard    | Register a new keyboard. componentID (string) - the ID of the keyboard. generator (function) - a function for the creation of the keyboard. params (object) - to be returned when using other methods (i.e. getKeyboards and getAllKeyboards). | static function | no       | iOS/Android | yes               |
| removeListeners     | Remove a listener for a callback. globalID (string) - ID that includes the componentID and the event name (i.e. if componentID='kb1' globalID='kb1.onItemSelected') | static function | no       | iOS/Android | yes               |
| requestShowKeyboard | Request to show the keyboard componentID (string) - the ID of the keyboard. | static function | no       | iOS/Android | yes               |

**KeyboardTrackingView**：为该视图及其子视图启用“键盘跟踪”的 UI 组件。通常用于该视图内有 TextField 或 TextInput 的情况，该组件仅适用于iOS。

| Name                                 | Description                                                  | Type      | Required | Platform | HarmonyOS Support |
| ------------------------------------ | ------------------------------------------------------------ | --------- | -------- | -------- | ----------------- |
| addBottomView                        | Add a view beneath the KeyboardAccessoryView.                | boolean   | no       | iOS      | no                |
| allowHitsOutsideBounds               | Allow hitting sub-views that are placed beyond the view bounds. | boolean   | no       | iOS      | no                |
| bottomViewColor                      | The bottom view's color.                                     | string    | no       | iOS      | no                |
| manageScrollView                     | Set to false to turn off inset management and manage it yourself. | boolean   | no       | iOS      | no                |
| ref                                  | Ref                                                          | any       | no       | iOS      | no                |
| requiresSameParentToManageScrollView | Set to true manageScrollView is set to true and still does not work, it means that the ScrollView found is the wrong one and you'll have to have the KeyboardAccessoryView and the ScrollView as siblings and set this to true. | boolean   | no       | iOS      | no                |
| revealKeyboardInteractive            | Show the keyboard on a negative scroll.                      | boolean   | no       | iOS      | no                |
| scrollBehavior                       | The scrolling behavior (use KeyboardTrackingView. scrollBehaviors.NONE \|SCROLL_TO_BOTTOM_INVERTED_ONLY \| FIXED_OFFSET) | number    | no       | iOS      | no                |
| scrollToFocusedInput                 | Should the scrollView scroll to the focused input            | boolean   | no       | iOS      | no                |
| style                                | Style                                                        | ViewStyle | no       | iOS      | no                |
| trackInteractive                     | Enables tracking of the keyboard when it's dismissed interactively (false by default). Why? When using an external keyboard (BT), you still get the keyboard events and the view just hovers when you focus the input. Also, if you're not using interactive style of dismissing the keyboard (or if you don't have an input inside this view) it doesn't make sense to track it anyway. (This is caused because of the usage of inputAccessory to be able to track the keyboard interactive change and it introduces this bug) | boolean   | no       | iOS      | no                |
| useSafeArea                          | Whether or not to handle SafeArea.                           | boolean   | no       | iOS      | no                |
| usesBottomTabs                       | Whether or not to include bottom tab bar inset.              | boolean   | no       | iOS      | no                |

**Overlay**：带类型覆盖视图，为Image组件属性，扩展了[image](https://reactnative.dev/docs/image)组件。

| Name          | Description                                               | Type                                                  | Required | Platform    | HarmonyOS Support |
| ------------- | --------------------------------------------------------- | ----------------------------------------------------- | -------- | ----------- | ----------------- |
| color         | The overlay color                                         | string                                                | no       | iOS/Android | yes               |
| customContent | Custom overlay content to be rendered on top of the image | JSX.Element                                           | no       | iOS/Android | yes               |
| intensity     | The intensity of the gradient.                            | low \|medium \|high                                   | no       | iOS/Android | yes               |
| type          | The type of overlay to set on top of the image            | vertical \| top  \| bottom \| solid (OverlayTypeType) | no       | iOS/Android | yes               |

**Card**：卡片组件，扩展了[TouchableOpacity](https://wix.github.io/react-native-ui-lib/docs/components/basic/TouchableOpacity)组件，依赖[@react-native-community/blur](/zh-cn/react-native-community-blur.md)。

| Name             | Description                                                  | Type                 | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------------------- | -------- | ----------- | ----------------- |
| blurOptions      | Blur options for blur effect according to @react-native-community/blur lib (make sure enableBlur is on) | object               | no       | iOS/Android | yes               |
| borderRadius     | Card border radius (will be passed to inner Card.Image component) | number               | no       | iOS/Android | yes               |
| containerStyle   | Additional styles for the card container                     | ViewStyle            | no       | iOS/Android | yes               |
| elevation        | Android only. Elevation value                                | number               | no       | Android     | no                |
| enableBlur       | iOS only. Enable blur effect                                 | boolean              | no       | iOS         | no                |
| enableShadow     | Whether the card should have shadow or not                   | boolean              | no       | iOS/Android | yes               |
| height           | Card custom height                                           | number \| string     | no       | iOS/Android | yes               |
| onPress          | Callback function for card press event                       | function             | no       | iOS/Android | yes               |
| row              | Should inner card flow direction be horizontal               | boolean              | no       | iOS/Android | yes               |
| selected         | Adds visual indication that the card is selected             | boolean              | no       | iOS/Android | yes               |
| selectionOptions | Custom options for styling the selection indication          | CardSelectionOptions | no       | iOS/Android | yes               |
| width            | Card custom width                                            | number  \| string    | no       | iOS/Android | yes               |

**Card.Image**：Card 组件的内部组件（最好是直接子组件），扩展了[Image](https://wix.github.io/react-native-ui-lib/docs/components/media/Image)组件。

| Name     | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| -------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| height   | Height                                                       | number   | no       | iOS/Android | yes               |
| position | The Image position which determines the appropriate flex-ness of the image and border radius (for Android) this prop derived automatically from Card parent component if it rendered as a direct child of the Card component | string[] | no       | iOS/Android | yes               |
| width    | Width                                                        | number   | no       | iOS/Android | yes               |

**Card.Section**：用于在 Card 组件内轻松渲染内容的内部组件，扩展了[View](https://wix.github.io/react-native-ui-lib/docs/components/basic/View)组件。

| Name            | Description                                                  | Type                | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ------------------- | -------- | ----------- | ----------------- |
| backgroundColor | Background color                                             | string              | no       | iOS/Android | yes               |
| content         | Text content. Example: content={[{text: 'You’re Invited!', text70: true, grey10: true}]} | ContentType[]       | no       | iOS/Android | yes               |
| contentStyle    | Component's container style                                  | ViewStyle           | no       | iOS/Android | yes               |
| imageProps      | Other image props that will be passed to the image           | ImageProps          | no       | iOS/Android | yes               |
| imageSource     | Will be used for the background when provided                | ImageSourcePropType | no       | iOS/Android | yes               |
| imageStyle      | The style for the background image                           | ImageStyle          | no       | iOS/Android | yes               |
| leadingIcon     | Image props for a leading icon to render before the text     | ImageProps          | no       | iOS/Android | yes               |
| trailingIcon    | Image props for a trailing icon to render after the text     | ImageProps          | no       | iOS/Android | yes               |

**Carousel**：轮播组件，扩展了[ScrollView](https://reactnative.dev/docs/scrollview)组件。

| Name                      | Description                                                  | Type                                    | Required | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | --------------------------------------- | -------- | ----------- | ----------------- |
| allowAccessibleLayout     | Whether to layout Carousel for accessibility                 | boolean                                 | no       | iOS/Android | yes               |
| animated                  | Should the container be animated (send the animation style via containerStyle) | boolean                                 | no       | iOS/Android | yes               |
| animatedScrollOffset      | Pass to attach to ScrollView's Animated.event in order to animated elements base on Carousel scroll offset (pass new Animated.ValueXY()) | Animated.ValueXY                        | no       | iOS/Android | yes               |
| autoplay                  | Enable to switch automatically between the pages             | boolean                                 | no       | iOS/Android | yes               |
| autoplayInterval          | Time is ms to wait before switching to the next page (requires 'autoplay' to be enabled) | number                                  | no       | iOS/Android | yes               |
| containerMarginHorizontal | Horizontal margin for the carousel container                 | number                                  | no       | iOS/Android | yes               |
| containerPaddingVertical  | Vertical padding for the carousel container (Sometimes needed when there are overflows that are cut in Android). | number                                  | no       | iOS/Android | yes               |
| containerStyle            | The carousel container style                                 | ViewStyle                               | no       | iOS/Android | yes               |
| counterTextStyle          | The counter's text style                                     | ViewStyle                               | no       | iOS/Android | yes               |
| horizontal                | Whether pages will be rendered horizontally or vertically    | boolean                                 | no       | iOS/Android | yes               |
| initialPage               | The initial page to start at                                 | number                                  | no       | iOS/Android | yes               |
| itemSpacings              | The spacing between the pages                                | number                                  | no       | iOS/Android | yes               |
| loop                      | If true, will have infinite scroll (works only for horizontal carousel) | boolean                                 | no       | iOS/Android | yes               |
| onChangePage              | Callback for page change event                               | (pageIndex, oldPageIndex, info) => void | no       | iOS/Android | yes               |
| onScroll                  | Attach a callback for onScroll event of the internal ScrollView | function                                | no       | iOS/Android | yes               |
| pageControlPosition       | The position of the PageControl component ['over', 'under'], otherwise it won't display | PageControlPosition                     | no       | iOS/Android | yes               |
| pageControlProps          | PageControl component props                                  | PageControlProps                        | no       | iOS/Android | yes               |
| pageHeight                | The page height (all pages should have the same height).     | number                                  | no       | iOS/Android | yes               |
| pageWidth                 | The page width (all pages should have the same width). Does not work if passing 'loop' prop | number                                  | no       | iOS/Android | yes               |
| pagingEnabled             | Will block multiple pages scroll (will not work with 'pageWidth' prop) | boolean                                 | no       | iOS/Android | yes               |
| showCounter               | Whether to show a page counter (will not work with 'pageWidth' prop) | boolean                                 | no       | iOS/Android | yes               |

**LoaderScreen**：全屏显示组件，通常用于页面加载loading，扩展了[Activityindicator](https://reactnative.dev/docs/activityindicator)组件。

| Name            | Description                                                  | Type             | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ---------------- | -------- | ----------- | ----------------- |
| backgroundColor | Color of the loader background (only when passing 'overlay') | string           | no       | iOS/Android | yes               |
| containerStyle  | Custom container style                                       | ViewStyle        | no       | iOS/Android | yes               |
| customLoader    | Custom loader                                                | React.ReactChild | no       | iOS/Android | yes               |
| loaderColor     | Color of the loading indicator                               | string           | no       | iOS/Android | yes               |
| message         | loader message                                               | string           | no       | iOS/Android | yes               |
| messageStyle    | message style                                                | TextStyle        | no       | iOS/Android | yes               |
| overlay         | Show the screen as an absolute overlay                       | boolean          | no       | iOS/Android | yes               |

**StackAggregator**：堆栈聚合器组件。

| Name                  | Description                                                  | Type                         | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ---------------------------- | -------- | ----------- | ----------------- |
| buttonProps           | Props passed to the 'show less' button                       | ButtonProps                  | no       | iOS/Android | yes               |
| children              | Component Children                                           | JSX.Element \| JSX.Element[] | no       | iOS/Android | yes               |
| collapsed             | The initial state of the stack                               | boolean                      | no       | iOS/Android | yes               |
| containerStyle        | The container style                                          | ViewStyle                    | no       | iOS/Android | yes               |
| contentContainerStyle | The content container style                                  | ViewStyle                    | no       | iOS/Android | yes               |
| disablePresses        | A setting that disables pressability on cards                | boolean                      | no       | iOS/Android | yes               |
| itemBorderRadius      | The items border radius                                      | number                       | no       | iOS/Android | yes               |
| onCollapseChanged     | A callback for collapse state change (value is collapsed state) | (changed: boolean) => void   | no       | iOS/Android | yes               |
| onCollapseWillChange  | A callback for collapse state will change (value is future collapsed state) | (changed: boolean) => void   | no       | iOS/Android | yes               |
| onItemPress           | A callback for item press                                    | (index: number) => void      | no       | iOS/Android | yes               |

**StateScreen**：显示全屏组件。

| Name        | Description                                                  | Type           | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | -------------- | -------- | ----------- | ----------------- |
| ctaLabel    | Text to to show in the CTA button                            | string         | no       | iOS/Android | yes               |
| imageSource | The image source that's showing at the top. use an image that was required locally | ImageURISource | no       | iOS/Android | yes               |
| onCtaPress  | Action handler for CTA button                                | () => void     | no       | iOS/Android | yes               |
| testID      | Use to identify the container in tests                       | string         | no       | iOS/Android | yes               |
| title       | To to show as the title                                      | string         | no       | iOS/Android | yes               |

**Drawer**：抽屉组件，如果您的应用程序与 RNN 配合使用，则您的屏幕必须使用“react-native-gesture-handler”中的gestureHandlerRootHOC 进行包装。请参阅[这里](https://kmagiera.github.io/react-native-gesture-handler/docs/getting-started.html#with-wix-react-native-navigation-https-githubcom-wix-react-native-navigation)。

| Name                 | Description                                                  | Type                                                  | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ----------------------------------------------------- | -------- | ----------- | ----------------- |
| bounciness           | The drawer animation bounciness                              | number                                                | no       | iOS/Android | yes               |
| customValue          | Custom value of any type to pass on to the component and receive back in the action callbacks | any                                                   | no       | iOS/Android | yes               |
| disableHaptic        | Whether to disable the haptic                                | boolean                                               | no       | iOS/Android | yes               |
| fullLeftThreshold    | Threshold for a left full swipe (0-1)                        | number                                                | no       | iOS/Android | yes               |
| fullRightThreshold   | Threshold for a right full swipe (0-1)                       | number                                                | no       | iOS/Android | yes               |
| fullSwipeLeft        | Whether to allow a full left swipe                           | boolean                                               | no       | iOS/Android | yes               |
| fullSwipeRight       | Whether to allow a full right swipe                          | boolean                                               | no       | iOS/Android | yes               |
| itemsIconSize        | The items' icon size                                         | number                                                | no       | iOS/Android | yes               |
| itemsMinWidth        | Set a different minimum width                                | number                                                | no       | iOS/Android | yes               |
| itemsTextStyle       | The items' text style                                        | TextStyle                                             | no       | iOS/Android | yes               |
| itemsTintColor       | The color for the text and icon tint of the items            | string                                                | no       | iOS/Android | yes               |
| leftItem             | The bottom layer's item to appear when opened from the left (a single item) | ItemProps                                             | no       | iOS/Android | yes               |
| onDragStart          | Called when drag gesture starts                              | () => any                                             | no       | iOS/Android | yes               |
| onFullSwipeLeft      | Callback for left item full swipe                            | () => void                                            | no       | iOS/Android | yes               |
| onFullSwipeRight     | Callback for right item full swipe                           | () => void                                            | no       | iOS/Android | yes               |
| onSwipeableWillClose | Callback for close action                                    | () => void                                            | no       | iOS/Android | yes               |
| onSwipeableWillOpen  | Callback for open action                                     | () => void                                            | no       | iOS/Android | yes               |
| onToggleSwipeLeft    | Callback for left item toggle swipe                          | () => {rowWidth, leftWidth, dragX, resetItemPosition} | no       | iOS/Android | yes               |
| onWillFullSwipeLeft  | Callback for just before left item full swipe                | () => void                                            | no       | iOS/Android | yes               |
| onWillFullSwipeRight | Callback for just before right item full swipe               | () => void                                            | no       | iOS/Android | yes               |
| rightItems           | The bottom layer's items to appear when opened from the right | ItemProps[]                                           | no       | iOS/Android | yes               |
| style                | Component's style                                            | ViewStyle                                             | no       | iOS/Android | yes               |
| testID               | The test id for e2e tests                                    | string                                                | no       | iOS/Android | yes               |
| useNativeAnimations  | Perform the animation in natively                            | boolean                                               | no       | iOS/Android | yes               |

**GridList**：网格列表组件，扩展了[FlatList](https://reactnative.dev/docs/flatlist)组件。

| Name                  | Description                                                  | Type                                | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ----------------------------------- | -------- | ----------- | ----------------- |
| containerWidth        | Pass when you want to use a custom container width for calculation | number                              | no       | iOS/Android | yes               |
| contentContainerStyle | Custom content container style                               | ScrollView[ contentContainerStyle ] | no       | iOS/Android | yes               |
| itemSpacing           | Spacing between each item                                    | number                              | no       | iOS/Android | yes               |
| keepItemSize          | whether to keep the items initial size when orientation changes, in which case the apt number of columns will be calculated automatically. | boolean                             | no       | iOS/Android | yes               |
| listPadding           | List padding (used for item size calculation)                | number                              | no       | iOS/Android | yes               |
| maxItemWidth          | Allow a responsive item width to the maximum item width      | number                              | no       | iOS/Android | yes               |
| numColumns            | Number of items to show in a row (ignored when passing maxItemWidth) | number                              | no       | iOS/Android | yes               |

**GridListItem**：单个网格视图/列表项组件。

| Name                      | Description                                                 | Type                               | Required | Platform    | HarmonyOS Support |
| ------------------------- | ----------------------------------------------------------- | ---------------------------------- | -------- | ----------- | ----------------- |
| alignToStart              | Should content be align to start                            | boolean                            | no       | iOS/Android | yes               |
| containerProps            | Props to pass on to the touchable container                 | TouchableOpacityProps \| ViewProps | no       | iOS/Android | yes               |
| containerStyle            | Custom container style                                      | ViewStyle                          | no       | iOS/Android | yes               |
| description               | Description content text                                    | string \| React.ReactElement       | no       | iOS/Android | yes               |
| descriptionColor          | Description content color                                   | string                             | no       | iOS/Android | yes               |
| descriptionLines          | Description content number of lines                         | number                             | no       | iOS/Android | yes               |
| descriptionTypography     | Description content typography                              | string                             | no       | iOS/Android | yes               |
| horizontalAlignment       | Content horizontal alignment                                | HorizontalAlignment                | no       | iOS/Android | yes               |
| imageProps                | Image props object for rendering an image item              | ImageProps                         | no       | iOS/Android | yes               |
| itemSize                  | The item size                                               | number \| ImageSize                | no       | iOS/Android | yes               |
| onPress                   | The item's action handler                                   | TouchableOpacityProps ['onPress']  | no       | iOS/Android | yes               |
| overlayText               | Renders the title, subtitle and description inside the item | boolean                            | no       | iOS/Android | yes               |
| overlayTextContainerStyle | Custom container styling for inline text                    | ViewStyle                          | no       | iOS/Android | yes               |
| renderCustomItem          | Custom GridListItem to be rendered in the GridView          | () => React.ReactElement           | no       | iOS/Android | yes               |
| renderOverlay             | Renders an overlay on top of the image                      | () => React.ReactElement           | no       | iOS/Android | yes               |
| subtitle                  | Subtitle content text                                       | string \| React.ReactElement       | no       | iOS/Android | yes               |
| subtitleColor             | Subtitle content color                                      | string                             | no       | iOS/Android | yes               |
| subtitleLines             | Subtitle content number of lines                            | number                             | no       | iOS/Android | yes               |
| subtitleTypography        | Subtitle content typography                                 | string                             | no       | iOS/Android | yes               |
| testID                    | Test ID for component                                       | string                             | no       | iOS/Android | yes               |
| title                     | Title content text                                          | string \| React.ReactElement       | no       | iOS/Android | yes               |
| titleColor                | Title content color                                         | string                             | no       | iOS/Android | yes               |
| titleLines                | Title content number of lines                               | number                             | no       | iOS/Android | yes               |
| titleTypography           | Title content typography                                    | string                             | no       | iOS/Android | yes               |

**GridView**：网格视图组件。

| Name                 | Description                                                  | Type                                            | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ----------------------------------------------- | -------- | ----------- | ----------------- |
| itemSpacing          | Spacing between each item                                    | number                                          | no       | iOS/Android | yes               |
| items                | The list of items based on GridListItem props                | GridListItemProps[]                             | no       | iOS/Android | yes               |
| keepItemSize         | whether to keep the items initial size when orientation changes, in which case the apt number of columns will be calculated automatically. | boolean                                         | no       | iOS/Android | yes               |
| lastItemLabel        | overlay label for the last item                              | string \| number                                | no       | iOS/Android | yes               |
| lastItemOverlayColor | color of overlay label for the last item                     | string                                          | no       | iOS/Android | yes               |
| numColumns           | Number of items to show in a row                             | number                                          | no       | iOS/Android | yes               |
| renderCustomItem     | Pass to render a custom item                                 | (item: GridListItemProps) => React.ReactElement | no       | iOS/Android | yes               |
| viewWidth            | pass the desired grid view width (will improve loading time) | number                                          | no       | iOS/Android | yes               |

**ListItem**：列表中列表项组件，该组件扩展了[TouchableOpacity](https://reactnative.dev/docs/touchableopacity)属性。

| Name             | Description                                | Type                                                         | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| containerElement | The container element to wrap the ListItem | React.ComponentType <ListItemProps \| TouchableOpacityProps> | no       | iOS/Android | yes               |
| containerStyle   | Additional styles for the top container    | ViewStyle                                                    | no       | iOS/Android | yes               |
| height           | the list item height                       | ViewStyle['height']                                          | no       | iOS/Android | yes               |
| onLongPress      | action for when long pressing the item     | () => void                                                   | no       | iOS/Android | yes               |
| onPress          | action for when pressing the item          | () => void                                                   | no       | iOS/Android | yes               |
| style            | The inner element style                    | ViewStyle                                                    | no       | iOS/Android | yes               |
| testID           | The test id for e2e tests                  | string                                                       | no       | iOS/Android | yes               |
| underlayColor    | The inner element pressed backgroundColor  | string                                                       | no       | iOS/Android | yes               |

**ListItem.Part**：用于在 ListItem 内进行布局的子 ListItem 组件。

| Name           | Description                                   | Type      | Required | Platform    | HarmonyOS Support |
| -------------- | --------------------------------------------- | --------- | -------- | ----------- | ----------------- |
| column         | this part content direction will be column    | boolean   | no       | iOS/Android | yes               |
| containerStyle | container style                               | ViewStyle | no       | iOS/Android | yes               |
| left           | this part content will be aligned to left     | boolean   | no       | iOS/Android | yes               |
| middle         | this part content will be aligned to spreaded | boolean   | no       | iOS/Android | yes               |
| right          | this part content will be aligned to right    | boolean   | no       | iOS/Android | yes               |
| row            | this part content direction will be row       | boolean   | no       | iOS/Android | yes               |

**SortableGridList**：可排序网格列表组件，该组件扩展了[GridList](https://wix.github.io/react-native-ui-lib/docs/components/lists/GridList)组件属性。

| Name          | Description                                                  | Type                                         | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | -------------------------------------------- | -------- | ----------- | ----------------- |
| data          | Do not update 'data' in 'onOrderChange' (i.e. for each order change); only update it when you change the items (i.g. adding and removing an item). Data of items with an id prop as unique identifier | any[] & {id: string}                         | no       | iOS/Android | yes               |
| extraData     | Pass any extra data that should trigger a re-render          | any                                          | no       | iOS/Android | yes               |
| onOrderChange | Order change callback                                        | (newData: T[], newOrder: ItemsOrder) => void | no       | iOS/Android | yes               |
| renderItem    | Custom render item callback                                  | FlatListProps ['renderItem']                 | no       | iOS/Android | yes               |

**SortableList**：可排序列表组件，该组件扩展了[FlatList](https://reactnative.dev/docs/flatlist)组件属性。

| Name          | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| data          | Do not update 'data' in 'onOrderChange' (i.e. for each order change); only update it when you change the items (i.g. adding and removing an item).The data of the list, with an id prop as unique identifier. | ItemT[] (ItemT extends {id: string})                         | no       | iOS/Android | yes               |
| enableHaptic  | Whether to enable the haptic feedback. (please note that react-native-haptic-feedback does not support the specific haptic type on Android starting on an unknown version, you can use 1.8.2 for it to work properly) | boolean                                                      | no       | iOS/Android | yes               |
| itemProps     | Extra props for the item.                                    | {margins?: {marginTop?: number; marginBottom?: number; marginLeft?: number; marginRight?: number}} | no       | iOS/Android | yes               |
| onOrderChange | A callback to get the new order (or swapped items).          | (data: ItemT[]) => void                                      | no       | iOS/Android | yes               |
| scale         | Scale the item once dragged.                                 | number                                                       | no       | iOS/Android | yes               |

**Timeline**：时间线组件，该组件扩展了[View](https://reactnative.dev/docs/view)组件属性。

| Name            | Description                                                  | Type                               | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ---------------------------------- | -------- | ----------- | ----------------- |
| backgroundColor | Background color for the item                                | string                             | no       | iOS/Android | yes               |
| bottomLine      | The bottom line props                                        | LineProps                          | no       | iOS/Android | yes               |
| point           | The point props                                              | PointProps                         | no       | iOS/Android | yes               |
| renderContent   | Custom content to render right to the timeline indicator     | any                                | no       | iOS/Android | yes               |
| state           | The state of the timeline. Will affect the color of the indication (use static 'states') | current \| next \| error \|success | no       | iOS/Android | yes               |
| testID          | The test id for e2e tests                                    | string                             | no       | iOS/Android | yes               |
| topLine         | The top line props                                           | LineProps                          | no       | iOS/Android | yes               |

**AnimatedImage**：图像加载后以动画淡入的图像组件，该组件扩展了[Image](https://wix.github.io/react-native-ui-lib/docs/components/media/Image)组件属性。

| Name              | Description                                              | Type        | Required | Platform    | HarmonyOS Support |
| ----------------- | -------------------------------------------------------- | ----------- | -------- | ----------- | ----------------- |
| animationDuration | Duration for the fade animation when the image is loaded | number      | no       | iOS/Android | yes               |
| containerStyle    | Additional spacing styles for the container              | ViewStyle   | no       | iOS/Android | yes               |
| loader            | A component to render while the image is loading         | JSX.element | no       | iOS/Android | yes               |

**AnimatedScanner**：该组件扩展了[Animated.View](https://reactnative.dev/docs/animated)组件属性。

| Name            | Description                                              | Type                         | Required | Platform    | HarmonyOS Support |
| --------------- | -------------------------------------------------------- | ---------------------------- | -------- | ----------- | ----------------- |
| backgroundColor | Background color                                         | string                       | no       | iOS/Android | yes               |
| containerStyle  | Component's container style                              | ViewStyle                    | no       | iOS/Android | yes               |
| duration        | Duration of current break (can be change between breaks) | number                       | no       | iOS/Android | yes               |
| hideScannerLine | Whether to hide the scanner line                         | boolean                      | no       | iOS/Android | yes               |
| onBreakpoint    | Breakpoint callback                                      | ({progress, isDone}) => void | no       | iOS/Android | yes               |
| opacity         | Opacity                                                  | number                       | no       | iOS/Android | yes               |
| progress        | Animated value between 0 and 100                         | number                       | no       | iOS/Android | yes               |
| testID          | Used as a testing identifier                             | string                       | no       | iOS/Android | yes               |

**Avatar**：头像组件，该组件扩展了[TouchableOpacity](https://wix.github.io/react-native-ui-lib/docs/components/basic/TouchableOpacity)，[Image](https://wix.github.io/react-native-ui-lib/docs/components/media/Image)组件属性。

| Name             | Description                                                  | Type                                              | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------- | -------- | ----------- | ----------------- |
| animate          | Adds fade in animation when Avatar image loads               | boolean                                           | no       | iOS/Android | yes               |
| autoColorsConfig | Send this to use the name to infer a backgroundColor         | AutoColorsProps                                   | no       | iOS/Android | yes               |
| backgroundColor  | Background color for Avatar                                  | string                                            | no       | iOS/Android | yes               |
| badgePosition    | Badge location on Avatar                                     | TOP_RIGHT \|TOP_LEFT \|BOTTOM_RIGHT \|BOTTOM_LEFT | no       | iOS/Android | yes               |
| badgeProps       | Badge props passed down to Badge component                   | BadgeProps                                        | no       | iOS/Android | yes               |
| containerStyle   | Additional spacing styles for the container                  | ViewStyle                                         | no       | iOS/Android | yes               |
| customRibbon     | Custom ribbon                                                | JSX.Element                                       | no       | iOS/Android | yes               |
| imageProps       | Image props object                                           | ImageProps                                        | no       | iOS/Android | yes               |
| imageStyle       | Image style object used to pass additional style props by components which render image | ImageStyle                                        | no       | iOS/Android | yes               |
| isOnline         | Determine if to show online badge                            | boolean                                           | no       | iOS/Android | yes               |
| label            | Label that can represent initials                            | string                                            | no       | iOS/Android | yes               |
| labelColor       | The label color                                              | string                                            | no       | iOS/Android | yes               |
| name             | The name of the avatar user. If no label is provided, the initials will be generated from the name. autoColorsConfig will use the name to create the background color of the Avatar. | string                                            | no       | iOS/Android | yes               |
| onImageLoadEnd   | Listener-callback for when an image's (uri) loading either succeeds or fails (equiv. to Image.onLoadEnd()). | ImagePropsBase ['onLoadEnd']                      | no       | iOS/Android | yes               |
| onImageLoadError | Listener-callback for when an image's (uri) loading fails (equiv. to Image.onError()). | ImagePropsBase ['onError']                        | no       | iOS/Android | yes               |
| onImageLoadStart | Listener-callback for when an image's (uri) loading starts (equiv. to Image.onLoadStart()). | ImagePropsBase ['onLoadStart']                    | no       | iOS/Android | yes               |
| onPress          | Press handler                                                | (props: any) => void                              | no       | iOS/Android | yes               |
| ribbonLabel      | Ribbon label to display on the avatar                        | string                                            | no       | iOS/Android | yes               |
| ribbonLabelStyle | Ribbon label custom style                                    | TextStyle                                         | no       | iOS/Android | yes               |
| ribbonStyle      | Ribbon custom style                                          | ViewStyle                                         | no       | iOS/Android | yes               |
| size             | Custom size for the Avatar                                   | number                                            | no       | iOS/Android | yes               |
| source           | The image source (external or from assets)                   | ImageSourcePropType                               | no       | iOS/Android | yes               |
| status           | AWAY, ONLINE, OFFLINE or NONE mode (if set to a value other then 'NONE' will override isOnline prop) | StatusModes                                       | no       | iOS/Android | yes               |
| testID           | Test identifier                                              | string                                            | no       | iOS/Android | yes               |
| useAutoColors    | Hash the name (or label) to get a color, so each name will have a specific color. Default is false. | boolean                                           | no       | iOS/Android | yes               |

**Icon**：图标组件，该组件扩展了[Image](https://reactnative.dev/docs/image)组件属性。

| Name        | Description                                              | Type              | Required | Platform    | HarmonyOS Support |
| ----------- | -------------------------------------------------------- | ----------------- | -------- | ----------- | ----------------- |
| assetGroup  | the asset group, default is icons                        | string            | no       | iOS/Android | yes               |
| assetName   | if provided icon source will be driven from asset name   | string            | no       | iOS/Android | yes               |
| recorderTag | Recorder Tag                                             | 'mask' \|'unmask' | no       | iOS/Android | yes               |
| size        | The icon size                                            | number            | no       | iOS/Android | yes               |
| supportRTL  | whether the image should flip horizontally on RTL locals | boolean           | no       | iOS/Android | yes               |
| tintColor   | The icon tint                                            | string            | no       | iOS/Android | yes               |

**Image**：图片组件，该组件扩展了[Image](https://reactnative.dev/docs/image)组件属性。

| Name                   | Description                                                  | Type                                | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | ----------------------------------- | -------- | ----------- | ----------------- |
| aspectRatio            | The aspect ratio for the image                               | number                              | no       | iOS/Android | yes               |
| assetGroup             | the asset group, default is icons                            | string                              | no       | iOS/Android | yes               |
| assetName              | if provided image source will be driven from asset name      | string                              | no       | iOS/Android | yes               |
| cover                  | Show image as a cover, full width, image (according to aspect ratio, default: 16:8) | boolean                             | no       | iOS/Android | yes               |
| customOverlayContent   | Render an overlay with custom content                        | JSX.Element                         | no       | iOS/Android | yes               |
| errorSource            | Default image source in case of an error                     | ImageSourcePropType                 | no       | iOS/Android | yes               |
| imageId                | An imageId that can be used in sourceTransformer logic       | string                              | no       | iOS/Android | yes               |
| overlayColor           | Pass a custom color for the overlay                          | string                              | no       | iOS/Android | yes               |
| overlayIntensity       | OverlayIntensityType                                         | LOW \|MEDIUM \|HIGH                 | no       | iOS/Android | yes               |
| overlayType            | the image MUST have proper size, The type of overlay to place on top of the image. | VERTICAL \|TOP \|BOTTOM \|SOLID     | no       | iOS/Android | yes               |
| recorderTag            | Recorder Tag                                                 | 'mask' \| 'unmask'                  | no       | iOS/Android | yes               |
| sourceTransformer      | custom source transform handler for manipulating the image source (great for size control) | (props: any) => ImageSourcePropType | no       | iOS/Android | yes               |
| supportRTL             | whether the image should flip horizontally on RTL locals     | boolean                             | no       | iOS/Android | yes               |
| tintColor              | the asset tint                                               | string                              | no       | iOS/Android | yes               |
| useBackgroundContainer | Use a container for the Image, this can solve issues on Android when animation needs to be performed on the same view; i.e. animation related crashes on Android. | boolean                             | no       | iOS/Android | yes               |

**Marquee**：滑动文本组件。

| Name           | Description                             | Type               | Required | Platform    | HarmonyOS Support |
| -------------- | --------------------------------------- | ------------------ | -------- | ----------- | ----------------- |
| containerStyle | Custom container style                  | ViewProps['style'] | no       | iOS/Android | yes               |
| direction      | Marquee direction                       | MarqueeDirections  | no       | iOS/Android | yes               |
| duration       | Marquee animation duration              | number             | no       | iOS/Android | yes               |
| label          | Marquee label                           | string             | no       | iOS/Android | yes               |
| labelStyle     | Marquee label style                     | TextProps['style'] | no       | iOS/Android | yes               |
| numberOfReps   | Marquee animation number of repetitions | number             | no       | iOS/Android | yes               |

**ProgressiveImage**：带动画的图像组件，该组件扩展了[AnimatedImage](https://wix.github.io/react-native-ui-lib/docs/components/media/AnimatedImage)组件属性。

| Name            | Description                                                  | Type        | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ----------- | -------- | ----------- | ----------------- |
| thumbnailSource | Small thumbnail source to display while the full-size image is loading | ImageSource | no       | iOS/Android | yes               |

**PageControl**：页面指示器组件。

| Name            | Description                                                  | Type                               | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ---------------------------------- | -------- | ----------- | ----------------- |
| color           | Color of the selected page dot and, if inactiveColor not passed, the border of the not selected pages | string                             | no       | iOS/Android | yes               |
| containerStyle  | Additional styles for the top container                      | ViewStyle                          | no       | iOS/Android | yes               |
| currentPage     | Zero-based index of the current page                         | number                             | no       | iOS/Android | yes               |
| enlargeActive   | Whether to enlarge the active page indicator. Irrelevant when limitShownPages is in effect. | boolean                            | no       | iOS/Android | yes               |
| inactiveColor   | Color of the unselected page dots and the border of the not selected pages | string                             | no       | iOS/Android | yes               |
| limitShownPages | Limit the number of page indicators shown.\enlargeActive prop is disabled in this state, when set to true there will be maximum of 7 shown.\Only relevant when numOfPages > 5. | boolean                            | no       | iOS/Android | yes               |
| numOfPages      | Total number of pages                                        | number                             | no       | iOS/Android | yes               |
| onPagePress     | Action handler for clicking on a page indicator              | (index: number) => void            | no       | iOS/Android | yes               |
| size            | The size of the page indicator.\When setting limitShownPages the medium sized will be 2/3 of size and the small will be 1/3 of size.\An alternative is to send an array [smallSize, mediumSize, largeSize]. | number \| [number, number, number] | no       | iOS/Android | yes               |
| spacing         | The space between the siblings page indicators               | number                             | no       | iOS/Android | yes               |
| testID          | Used to identify the pageControl in tests                    | string                             | no       | iOS/Android | yes               |

**TabController**：具有延迟加载机制的选项卡控制器组件，该组件基于react-native-gesture-handler，使用react-native-navigation时，请确保使用gestureHandlerRootHOC包裹屏幕。

| Name              | Description                                                  | Type                                               | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | -------------------------------------------------- | -------- | ----------- | ----------------- |
| asCarousel        | When using TabController.PageCarousel this should be turned on | boolean                                            | no       | iOS/Android | yes               |
| carouselPageWidth | Pass for custom carousel page width                          | number                                             | no       | iOS/Android | yes               |
| initialIndex      | Initial selected index                                       | number                                             | no       | iOS/Android | yes               |
| items             | The list of tab bar items                                    | TabControllerItemProps []                          | no       | iOS/Android | yes               |
| onChangeIndex     | Callback for when index has change (will not be called on ignored items) | (index: number, prevIndex: number \| null) => void | no       | iOS/Android | yes               |

**TabController.PageCarousel**：TabController 的 PageCarousel 组件，该组件扩展了[ScrollView](https://reactnative.dev/docs/scrollview)组件属性。

| Name                       | Description                                                  | Type      | Required | Platform    | HarmonyOS Support |
| -------------------------- | ------------------------------------------------------------ | --------- | -------- | ----------- | ----------------- |
| TabController.PageCarousel | TabController's PageCarousel component，You must pass asCarousel flag to TabController and render your TabPages inside a PageCarousel | Component | no       | iOS/Android | yes               |

**TabController.TabBar**：TabController的TabBar组件。

| Name                  | Description                                  | Type      | Required | Platform    | HarmonyOS Support |
| --------------------- | -------------------------------------------- | --------- | -------- | ----------- | ----------------- |
| activeBackgroundColor | Apply background color on press for tab item | string    | no       | iOS/Android | yes               |
| backgroundColor       | The TabBar background Color                  | string    | no       | iOS/Android | yes               |
| centerSelected        | Pass to center selected item                 | boolean   | no       | iOS/Android | yes               |
| containerStyle        | Additional styles for the container          | ViewStyle | no       | iOS/Android | yes               |
| containerWidth        | The TabBar container width                   | number    | no       | iOS/Android | yes               |
| enableShadow          | Show Tab Bar bottom shadow                   | boolean   | no       | iOS/Android | yes               |
| height                | Tab Bar height                               | number    | no       | iOS/Android | yes               |
| iconColor             | Icon tint color                              | string    | no       | iOS/Android | yes               |
| indicatorInsets       | The indicator insets                         | number    | no       | iOS/Android | yes               |
| indicatorStyle        | Custom style for the selected indicator      | ViewStyle | no       | iOS/Android | yes               |
| labelColor            | The default label color                      | string    | no       | iOS/Android | yes               |
| labelStyle            | Custom label style                           | TextStyle | no       | iOS/Android | yes               |
| selectedIconColor     | Icon selected tint color                     | string    | no       | iOS/Android | yes               |
| selectedLabelColor    | The selected label color                     | string    | no       | iOS/Android | yes               |
| selectedLabelStyle    | Custom selected label style                  | TextStyle | no       | iOS/Android | yes               |
| shadowStyle           | Custom shadow style                          | ViewStyle | no       | iOS/Android | yes               |
| spreadItems           | Whether the tabBar should be spread          | boolean   | no       | iOS/Android | yes               |
| testID                | The component test id                        | string    | no       | iOS/Android | yes               |
| uppercase             | Whether to change the text to uppercase      | boolean   | no       | iOS/Android | yes               |

**TabController.TabBarItem**：TabController的TabBarItem组件。

| Name                  | Description                                          | Type                    | Required | Platform    | HarmonyOS Support |
| --------------------- | ---------------------------------------------------- | ----------------------- | -------- | ----------- | ----------------- |
| activeBackgroundColor | Apply background color on press for TouchableOpacity | string                  | no       | iOS/Android | yes               |
| activeOpacity         | The active opacity when pressing a tab               | number                  | no       | iOS/Android | yes               |
| backgroundColor       | Apply background color for the tab bar item          | string                  | no       | iOS/Android | yes               |
| badge                 | Badge component props to display next the item label | BadgeProps              | no       | iOS/Android | yes               |
| icon                  | Icon of the tab                                      | number                  | no       | iOS/Android | yes               |
| iconColor             | Icon tint color                                      | string                  | no       | iOS/Android | yes               |
| ignore                | Ignore tab presses                                   | boolean                 | no       | iOS/Android | yes               |
| label                 | Label of the tab                                     | string                  | no       | iOS/Android | yes               |
| labelColor            | The default label color                              | string                  | no       | iOS/Android | yes               |
| labelProps            | Extra label props to pass to label Text element      | TextProps               | no       | iOS/Android | yes               |
| labelStyle            | Custom label style                                   | TextStyle               | no       | iOS/Android | yes               |
| leadingAccessory      | Pass to render a leading element                     | ReactElement            | no       | iOS/Android | yes               |
| onPress               | Callback for when pressing a tab                     | (index: number) => void | no       | iOS/Android | yes               |
| selectedIconColor     | Icon selected tint color                             | string                  | no       | iOS/Android | yes               |
| selectedLabelColor    | The selected label color                             | string                  | no       | iOS/Android | yes               |
| selectedLabelStyle    | Custom selected label style                          | TextStyle               | no       | iOS/Android | yes               |
| style                 | Pass custom style                                    | ViewStyle               | no       | iOS/Android | yes               |
| testID                | Used as a testing identifier                         | string                  | no       | iOS/Android | yes               |
| trailingAccessory     | Pass to render a trailing element                    | ReactElement            | no       | iOS/Android | yes               |
| uppercase             | Whether to change the text to uppercase              | boolean                 | no       | iOS/Android | yes               |
| width                 | A fixed width for the item                           | number                  | no       | iOS/Android | yes               |

**TabController.TabPage**：TabController的TabPage 组件。

| Name          | Description                                                  | Type              | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | ----------------- | -------- | ----------- | ----------------- |
| index         | The index of the the TabPage                                 | number            | no       | iOS/Android | yes               |
| lazy          | Whether this page should be loaded lazily                    | boolean           | no       | iOS/Android | yes               |
| lazyLoadTime  | How long to wait till lazy load complete (good for showing loader screens) | number            | no       | iOS/Android | yes               |
| renderLoading | Render a custom loading page when lazy loading               | () => JSX.Element | no       | iOS/Android | yes               |
| testID        | The component test id                                        | string            | no       | iOS/Android | yes               |

**Wizard**：向导组件。

| Name                 | Description                                                  | Type                    | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ----------------------- | -------- | ----------- | ----------------- |
| activeConfig         | The configuration of the active step (see Wizard.Step.propTypes) | WizardStepProps         | no       | iOS/Android | yes               |
| activeIndex          | The active step's index                                      | number                  | no       | iOS/Android | yes               |
| containerStyle       | Add or override style of the container                       | ViewStyle               | no       | iOS/Android | yes               |
| onActiveIndexChanged | Callback that is called when the active step is changed (i.e. a step was clicked on). The new activeIndex will be the input of the callback | (index: number) => void | no       | iOS/Android | yes               |
| testID               | The component test id                                        | string                  | no       | iOS/Android | yes               |

**Wizard.Step**：向导组件中Step组件。

| Name                  | Description                                                  | Type             | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ---------------- | -------- | ----------- | ----------------- |
| accessibilityInfo     | Extra text to be read in accessibility mode                  | string           | no       | iOS/Android | yes               |
| circleBackgroundColor | Circle's background color                                    | string           | no       | iOS/Android | yes               |
| circleColor           | Color of the circle                                          | string           | no       | iOS/Android | yes               |
| circleSize            | The step's circle size (diameter)                            | number           | no       | iOS/Android | yes               |
| color                 | Color of the step index (or of the icon, when provided)      | string           | no       | iOS/Android | yes               |
| connectorStyle        | Additional styles for the connector                          | ViewStyle        | no       | iOS/Android | yes               |
| enabled               | Whether the step should be enabled                           | boolean          | no       | iOS/Android | yes               |
| icon                  | Icon to replace the (default) index                          | ImageProps       | no       | iOS/Android | yes               |
| indexLabelStyle       | Additional styles for the index's label (when icon is not provided) | TextStyle        | no       | iOS/Android | yes               |
| label                 | The label of the item                                        | string           | no       | iOS/Android | yes               |
| labelStyle            | Additional styles for the label                              | TextStyle        | no       | iOS/Android | yes               |
| state                 | The state of the step (Wizard.States.X)                      | WizardStepStates | no       | iOS/Android | yes               |

**ActionSheet**：弹窗选择组件。

| Name                   | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| cancelButtonIndex      | Index of the option represents the cancel action (to be displayed as the separated bottom bold button) | number                                                       | no       | iOS/Android | yes               |
| containerStyle         | Add or override style of the action sheet (wraps the title and actions) | ViewStyle                                                    | no       | iOS/Android | yes               |
| destructiveButtonIndex | Index of the option represents the destructive action (will display red text. Usually used for delete or abort actions) | number                                                       | no       | iOS/Android | yes               |
| dialogStyle            | Add or override style of the dialog wrapping the action sheet | ViewStyle                                                    | no       | iOS/Android | yes               |
| message                | Message of the action sheet                                  | string                                                       | no       | iOS/Android | yes               |
| onDismiss              | Called when dismissing the action sheet (usually used for setting 'visible' prop to false) | DialogProps['onDismiss']                                     | no       | iOS/Android | yes               |
| onModalDismissed       | iOS only, modal only. Called once the modal has been dismissed | DialogProps ['onDialogDismissed']                            | no       | iOS         | no                |
| options                | List of options for the action sheet, follows the Button prop types (supply 'label' string and 'onPress' function) | Array<ButtonProps>                                           | no       | iOS/Android | yes               |
| optionsStyle           | Add or override style of the options list                    | ViewStyle                                                    | no       | iOS/Android | yes               |
| renderAction           | You will need to call 'onOptionPress' so the option's 'onPress' will be called. Render custom action | ( option: ButtonProps, index: number, onOptionPress: ActionSheetOnOptionPress ) => JSX.Element | no       | iOS/Android | yes               |
| renderTitle            | Render custom title                                          | () => JSX.Element                                            | no       | iOS/Android | yes               |
| showCancelButton       | When passed (only with useNativeIOS), will display a cancel button at the bottom (overrides cancelButtonIndex) | boolean                                                      | no       | iOS/Android | yes               |
| testID                 | The test id for e2e tests                                    | string                                                       | no       | iOS/Android | yes               |
| title                  | If both 'title' and 'message' are not passed will not render the title view at all. Title of the action sheet | string                                                       | no       | iOS/Android | yes               |
| useNativeIOS           | Should use the native action sheet for iOS                   | boolean                                                      | no       | iOS/Android | yes               |
| useSafeArea            | In iOS, use safe area, in case component attached to the bottom | boolean                                                      | no       | iOS/Android | yes               |
| visible                | Whether to show the action sheet or not                      | boolean                                                      | no       | iOS/Android | yes               |

**Dialog**：弹窗组件。

| Name                   | Description                                                  | Type                        | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | --------------------------- | -------- | ----------- | ----------------- |
| containerStyle         | Component's container style                                  | ViewStyle                   | no       | iOS/Android | yes               |
| height                 | Height                                                       | string \|number             | no       | iOS/Android | yes               |
| ignoreBackgroundPress  | Whether or not to ignore background press                    | boolean                     | no       | iOS/Android | yes               |
| onDialogDismissed      | Called once the dialog has been dismissed completely         | (props: any) => void        | no       | iOS/Android | yes               |
| onDismiss              | Called when clicking on the background                       | (props?: any) => void       | no       | iOS/Android | yes               |
| overlayBackgroundColor | The color of the overlay background                          | string                      | no       | iOS/Android | yes               |
| panDirection           | The direction of the allowed pan                             | UP \|DOWN \|LEFT \|RIGHT    | no       | iOS/Android | yes               |
| pannableHeaderProps    | The props that will be passed to the pannable header         | any                         | no       | iOS/Android | yes               |
| renderPannableHeader   | If this is added only the header will be pannable. Props are transferred to the 'renderPannableHeader'. For scrollable content (the children of the dialog) | (props: any) => JSX.Element | no       | iOS/Android | yes               |
| testID                 | The test id for e2e tests                                    | string                      | no       | iOS/Android | yes               |
| useSafeArea            | In iOS, use safe area, in case component attached to the bottom | boolean                     | no       | iOS/Android | yes               |
| visible                | Control visibility of the component                          | boolean                     | no       | iOS/Android | yes               |
| width                  | Width                                                        | string \| number            | no       | iOS/Android | yes               |

**FeatureHighlight**：功能发现组件，FeatureHighlight 组件必须是 render() 返回的根视图的直接子级，如果要突出显示的元素没有样式属性，请添加 'style={{opacity: 1}}' 以便 Android 操作系统可以检测到它，FeatureHighlight 使用native库，你需要引入它。

| Name                 | Description                                                  | Type                                      | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ----------------------------------------- | -------- | ----------- | ----------------- |
| borderColor          | Color of the border around the highlighted element           | string                                    | no       | iOS/Android | yes               |
| borderRadius         | Border radius for the border corners around the highlighted element | number                                    | no       | iOS/Android | yes               |
| borderWidth          | Width of the border around the highlighted element           | number                                    | no       | iOS/Android | yes               |
| confirmButtonProps   | Props that will be passed to the dismiss button              | ButtonProps                               | no       | iOS/Android | yes               |
| getTarget            | Callback that extract the ref of the element to be highlighted | () => any                                 | no       | iOS/Android | yes               |
| highlightFrame       | Frame of the area to highlight {x, y, width, height}         | HighlightFrame                            | no       | iOS/Android | yes               |
| innerPadding         | The padding of the highlight frame around the highlighted element's frame (only when passing ref in 'getTarget') | number                                    | no       | iOS/Android | yes               |
| message              | Message to be displayed                                      | string                                    | no       | iOS/Android | yes               |
| messageNumberOfLines | Message's max number of lines                                | number                                    | no       | iOS/Android | yes               |
| messageStyle         | Message text style                                           | TextStyle                                 | no       | iOS/Android | yes               |
| minimumRectSize      | Android API 21+, and only when passing a ref in 'getTarget'. The minimum size of the highlighted component | RectSize                                  | no       | iOS/Android | yes               |
| onBackgroundPress    | Called the background pressed                                | TouchableWithoutFeedbackProps ['onPress'] | no       | iOS/Android | yes               |
| overlayColor         | Color of the content's background (usually includes alpha for transparency) | string                                    | no       | iOS/Android | yes               |
| pageControlProps     | PageControl component's props                                | PageControlProps                          | no       | iOS/Android | yes               |
| testID               | The test id for e2e tests                                    | string                                    | no       | iOS/Android | yes               |
| textColor            | Color of the content's text                                  | string                                    | no       | iOS/Android | yes               |
| title                | Title of the content to be displayed                         | string                                    | no       | iOS/Android | yes               |
| titleNumberOfLines   | Title's max number of lines                                  | number                                    | no       | iOS/Android | yes               |
| titleStyle           | Title text style                                             | TextStyle                                 | no       | iOS/Android | yes               |
| visible              | Determines if to present the feature highlight component     | boolean                                   | no       | iOS/Android | yes               |

**FloatingButton**：具有渐变的悬浮按钮。

| Name                  | Description                                                  | Type                  | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | --------------------- | -------- | ----------- | ----------------- |
| bottomMargin          | The bottom margin of the button, or secondary button if passed | number                | no       | iOS/Android | yes               |
| button                | Props for the Button component                               | ButtonProps           | no       | iOS/Android | yes               |
| buttonLayout          | Button layout direction: vertical or horizontal              | FloatingButtonLayouts | no       | iOS/Android | yes               |
| duration              | The duration of the button's animations (show/hide)          | number                | no       | iOS/Android | yes               |
| fullWidth             | Relevant to vertical layout only. Whether the buttons get the container's full with | boolean               | no       | iOS/Android | yes               |
| hideBackgroundOverlay | Whether to show background overlay                           | boolean               | no       | iOS/Android | yes               |
| secondaryButton       | Props for the secondary Button component                     | ButtonProps           | no       | iOS/Android | yes               |
| testID                | Use `testID.button` for the main button or `testID.secondaryButton` for the secondary. The test id for e2e tests | string                | no       | iOS/Android | yes               |
| visible               | Whether the component is visible                             | boolean               | no       | iOS/Android | yes               |
| withoutAnimation      | Whether to show/hide the button without animation            | boolean               | no       | iOS/Android | yes               |

**Modal**：模态框组件，该组件扩展了[Modal](https://reactnative.dev/docs/modal)组件属性。

| Name                      | Description                                                  | Type                                   | Required | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | -------------------------------------- | -------- | ----------- | ----------------- |
| accessibilityLabel        | Overrides the text that's read by the screen reader when the user interacts with the element.\By default, the label is constructed by traversing all the children and accumulating all the Text nodes separated by space. | string                                 | no       | iOS/Android | yes               |
| blurView                  | A custom view to use as a BlurView instead of the default one | JSX.Element                            | no       | iOS/Android | yes               |
| enableModalBlur           | iOS only. Blurs the modal background when transparent        | boolean                                | no       | iOS         | no                |
| onBackgroundPress         | allow dismissing a modal when clicking on its background     | (event: GestureResponderEvent) => void | no       | iOS/Android | yes               |
| overlayBackgroundColor    | The background color of the overlay                          | string                                 | no       | iOS/Android | yes               |
| testID                    | The modal's end-to-end test identifier                       | string                                 | no       | iOS/Android | yes               |
| useGestureHandlerRootView | Android only. Should add a GestureHandlerRootView            | boolean                                | no       | Android     | no                |

**Modal.TopBar**：模态框的TopBar组件。

| Name              | Description                                                | Type                                   | Required | Platform    | HarmonyOS Support |
| ----------------- | ---------------------------------------------------------- | -------------------------------------- | -------- | ----------- | ----------------- |
| cancelButtonProps | Cancel action props                                        | ButtonProps                            | no       | iOS/Android | yes               |
| cancelIcon        | Cancel action icon                                         | ImageSource                            | no       | iOS/Android | yes               |
| cancelLabel       | Cancel action label                                        | string                                 | no       | iOS/Android | yes               |
| containerStyle    | Style for the TopBar container                             | ViewStyle                              | no       | iOS/Android | yes               |
| doneButtonProps   | Done action props                                          | ButtonProps                            | no       | iOS/Android | yes               |
| doneIcon          | Done action icon                                           | ImageSource                            | no       | iOS/Android | yes               |
| doneLabel         | Done action label                                          | string                                 | no       | iOS/Android | yes               |
| includeStatusBar  | Whether to include status bar or not (height calculations) | boolean                                | no       | iOS/Android | yes               |
| leftButtons       | Buttons to render on the left side of the top bar          | topBarButtonProp\| topBarButtonProp[]  | no       | iOS/Android | yes               |
| onCancel          | Cancel action callback                                     | (props?: any) => void                  | no       | iOS/Android | yes               |
| onDone            | Done action callback                                       | (props?: any) => void                  | no       | iOS/Android | yes               |
| rightButtons      | Buttons to render on the right side of the top bar         | topBarButtonProp \| topBarButtonProp[] | no       | iOS/Android | yes               |
| subtitle          | Subtitle to display below the top bar title                | string                                 | no       | iOS/Android | yes               |
| subtitleStyle     | Subtitle custom style                                      | TextStyle                              | no       | iOS/Android | yes               |
| title             | Title to display in the center of the top bar              | string                                 | no       | iOS/Android | yes               |
| titleStyle        | Title custom style                                         | TextStyle                              | no       | iOS/Android | yes               |

**Toast**：非中断式弹窗组件， 请考虑转向我们新的 Toast 实现并使用 Incubator.Toast 代替。

| Name  | Description                    | Type      | Required | Platform    | HarmonyOS Support |
| ----- | ------------------------------ | --------- | -------- | ----------- | ----------------- |
| Toast | A customizable Toast component | Component | no       | iOS/Android | yes               |

**Badge**：圆形彩色徽章组件。

| Name                | Description                                                  | Type                       | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | -------------------------- | -------- | ----------- | ----------------- |
| backgroundColor     | Background color                                             | string                     | no       | iOS/Android | yes               |
| borderColor         | Color of border around the badge                             | ImageStyle ['borderColor'] | no       | iOS/Android | yes               |
| borderRadius        | Radius of border around the badge                            | number                     | no       | iOS/Android | yes               |
| borderWidth         | Width of border around the badge                             | number                     | no       | iOS/Android | yes               |
| containerStyle      | Additional styles for the top container                      | ViewStyle                  | no       | iOS/Android | yes               |
| customElement       | Custom element to render instead of an icon                  | JSX.Element                | no       | iOS/Android | yes               |
| hitSlop             | Defines how far a touch event can start away from the badge  | ViewProps['hitSlop']       | no       | iOS/Android | yes               |
| icon                | Renders an icon badge                                        | ImageSourcePropType        | no       | iOS/Android | yes               |
| iconProps           | Additional props passed to icon                              | ImageProps                 | no       | iOS/Android | yes               |
| iconStyle           | Additional styling to badge icon                             | ImageStyle                 | no       | iOS/Android | yes               |
| label               | Passing a label (undefined) will present a pimple badge. Text to show inside the badge | string                     | no       | iOS/Android | yes               |
| labelFormatterLimit | Beyond the max number for that digit length, a '+' will show at the end. If set to a value not included in LABEL_FORMATTER_VALUES, no formatting will occur. Example: labelLengthFormatter={2}, label={124}, label will present '99+' Receives a number from 1 to 4, representing the label's max digit length | LabelFormatterValues       | no       | iOS/Android | yes               |
| labelStyle          | Additional styles for the badge label                        | TextStyle                  | no       | iOS/Android | yes               |
| onPress             | Called when the badge is pressed                             | (props: any) => void       | no       | iOS/Android | yes               |
| size                | Badge's size                                                 | number                     | no       | iOS/Android | yes               |

**ConnectionStatusBar**：顶部栏显示无网络连接状态，该组件依赖[@react-native-community/netinfo](/zh-cn/react-native-community-netinfo.md) 库。

| Name                | Description                                         | Type                                               | Required | Platform    | HarmonyOS Support |
| ------------------- | --------------------------------------------------- | -------------------------------------------------- | -------- | ----------- | ----------------- |
| allowDismiss        | Whethere to allow the user to dismiss               | boolean                                            | no       | iOS/Android | yes               |
| label               | Text to show as the status                          | string                                             | no       | iOS/Android | yes               |
| onConnectionChange  | Handler to get connection change events propagation | (isConnected: boolean, isInitial: boolean) => void | no       | iOS/Android | yes               |
| useAbsolutePosition | Use absolute position for the component             | boolean                                            | no       | iOS/Android | yes               |

**ProgressBar**：进度条组件。

| Name          | Description                                              | Type        | Required | Platform    | HarmonyOS Support |
| ------------- | -------------------------------------------------------- | ----------- | -------- | ----------- | ----------------- |
| customElement | Custom element to render on top of the animated progress | JSX.Element | no       | iOS/Android | yes               |
| fullWidth     | FullWidth Ui preset                                      | boolean     | no       | iOS/Android | yes               |
| progress      | The progress of the bar from 0 to 100                    | number      | no       | iOS/Android | yes               |
| progressColor | Progress color                                           | string      | no       | iOS/Android | yes               |
| style         | Override container style                                 | ViewStyle   | no       | iOS/Android | yes               |

**SkeletonView**：骨架视图组件，用于内容还未加载临时显示骨架，该组件需要安装[react-native-shimmer-placeholder](/zh-cn/react-native-shimmer-placeholder.md)和[react-native-linear-gradient](/zh-cn/react-native-linear-gradient.md)库。

| Name          | Description                                                  | Type                                   | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | -------------------------------------- | -------- | ----------- | ----------------- |
| borderRadius  | The border radius of the skeleton view                       | number                                 | no       | iOS/Android | yes               |
| circle        | Whether the skeleton is a circle (will override the borderRadius) | boolean                                | no       | iOS/Android | yes               |
| colors        | The colors of the skeleton view, the array length has to be >=2 | string[]                               | no       | iOS/Android | yes               |
| customValue   | Custom value of any type to pass on to SkeletonView and receive back in the renderContent callback. | any                                    | no       | iOS/Android | yes               |
| height        | The height of the skeleton view                              | number                                 | no       | iOS/Android | yes               |
| listProps     | Props that are available when using template={SkeletonView.templates.LIST_ITEM} | SkeletonListProps                      | no       | iOS/Android | yes               |
| renderContent | A function that will render the content once the content is ready (i.e. showContent is true). The method will be called with the Skeleton's customValue (i.e. renderContent(props?.customValue)) | (customValue?: any) => React.ReactNode | no       | iOS/Android | yes               |
| shimmerStyle  | Additional style to the skeleton view                        | ViewStyle                              | no       | iOS/Android | yes               |
| showContent   | The content has been loaded, start fading out the skeleton and fading in the content | boolean                                | no       | iOS/Android | yes               |
| style         | Override container styles                                    | ViewStyle                              | no       | iOS/Android | yes               |
| template      | Accessible through SkeletonView.templates.xxx. The type of the skeleton view. | listItem \|content                     | no       | iOS/Android | yes               |
| testID        | The component test id                                        | string                                 | no       | iOS/Android | yes               |
| times         | Generates duplicate skeletons                                | number                                 | no       | iOS/Android | yes               |
| timesKey      | A key prefix for the duplicated SkeletonViews                | string                                 | no       | iOS/Android | yes               |
| width         | The width of the skeleton view                               | number                                 | no       | iOS/Android | yes               |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Color**: 可以进行全局样式预设，通过Color获取预设样式。

| Name         | Description                                                  | Type                                             | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------ | -------- | ----------- | ----------------- |
| loadColors   | Load a set of colors to be used in the app.                  | ({[key: string]: string}) => void                | no       | iOS/Android | yes               |
| loadSchemes  | Load a set of scheme colors to support dark/light mode.      | ({[name: string]: {[key: string]: any}}) => void | no       | iOS/Android | yes               |
| rgba         | Return rgba string with color and transparency               | (color: string, num: number) => string           | no       | iOS/Android | yes               |
| getColorTint | Get color tint                                               | (color: string, num: number) => string           | no       | iOS/Android | yes               |
| isDark       | returns `true` if a color is considered dark (bright colors will return `false`) | (color: string) => boolean                       | no       | iOS/Android | yes               |

**ThemeManager**: 使用 ThemeManager 为您的应用程序设置默认的全局行为。

| Name              | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| setComponentTheme | Set default props for a component by passing an object or a callback | (componentName, defaultPropsObject) => void \| (componentName, componentProps => newDefaultPropsObject) => void | no       | iOS/Android | yes               |

**Typography**: 设置样式属性，可直接通过“属性”的方式给组件设置样式。

| Name             | Description                   | Type                                             | Required | Platform    | HarmonyOS Support |
| ---------------- | ----------------------------- | ------------------------------------------------ | -------- | ----------- | ----------------- |
| loadTypographies | Set style attribute variables | ({[name: string]: {[key: string]: any}}) => void | no       | iOS/Android | yes               |

**Spacings**: 设置空间大小变量，可通过 “属性-变量名” 的方式设置样式。

| Name             | Description             | Type                                | Required | Platform    | HarmonyOS Support |
| ---------------- | ----------------------- | ----------------------------------- | -------- | ----------- | ----------------- |
| loadTypographies | Set space size variable | ({ [key: string]: number }) => void | no       | iOS/Android | yes               |

## 遗留问题

- [ ] KeyboardTrackingView组件，将输入框子节点保持在键盘上方后点击事件位置异常: [issue#4](https://github.com/react-native-oh-library/react-native-ui-lib/issues/4)
- [ ]  原生组件KeyboardAccessoryView切换自定义键盘未实现: [issue#3](https://github.com/react-native-oh-library/react-native-ui-lib/issues/3)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wix/react-native-ui-lib/blob/master/LICENSE) ，请自由地享受和参与开源。
