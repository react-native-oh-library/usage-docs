> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/datetimepicker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-datetimepicker/datetimepicker">
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
       <a href="https://github.com/react-native-datetimepicker/datetimepicker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/datetimepicker)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/datetimepicker Releases](https://github.com/react-native-oh-library/datetimepicker/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/datetimepicker
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/datetimepicker
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react'
import DateTimePicker from '@react-native-community/datetimepicker';
import { SafeAreaView, Button, Text } from 'react-native'

export const MDatetimepicker = () => {
  const [date, setDate] = useState(new Date(new Date()));
  const [mode, setMode] = useState('date');
  const [show, setShow] = useState(false);

  const onChange = (event: any, selectedDate: any) => {
    const currentDate = selectedDate;
    setShow(false);
    setDate(currentDate);
  };

  const showMode = (currentMode: React.SetStateAction<string>) => {
    setShow(true);
    setMode(currentMode);
  };

  const showDatepicker = () => {
    showMode('date');
  };

  const showTimepicker = () => {
    showMode('time');
  };

  return (
    <SafeAreaView>
      <Button onPress={showDatepicker} title="Show date picker!" />
      <Button onPress={showTimepicker} title="Show time picker!" />
      <Text>selected: {date.toLocaleString()}</Text>
      {show && (
        <DateTimePicker
          mode={mode}//partially (仅支持 date/time 模式)
          style={{ width: 180, height: 80, backgroundColor: '#FFFFDD' }}
          display='default' //partially (支持"default"，"spinner"，"compact"，"inline")
          onChange={onChange}//partially (仅支持 type 为 set 类型)
          value={date}
          is24Hour={true} 
          disabled={false} 
          textColor={'#FFFFFF'}
        />
      )}
    </SafeAreaView>
  );
};
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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/datetimepicker": "file:../../node_modules/@react-native-oh-tpl/datetimepicker/harmony/datetimepicker.har"
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

### 3.配置 CMakeLists 和引入 datetimepicker

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/datetimepicker/src/main/cpp" ./datetimepicker)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_datetime_picker)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "DateTimePickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<DateTimePickerPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 DateTimePicker 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RNDateTimePicker, DATETIME_PICKER_VIEW_TYPE } from "@react-native-oh-tpl/datetimepicker"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === DATETIME_PICKER_VIEW_TYPE) {
+   RNDateTimePicker({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
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
+ DATETIME_PICKER_VIEW_TYPE
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/datetimepicker Releases](https://github.com/react-native-oh-library/datetimepicker/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请查看[datetimepicker 官方文档](https://github.com/react-native-datetimepicker/datetimepicker)

| Name        | Description                                              | Type     | Required | Platform                 | HarmonyOS Support                                 |
| ----------- | -------------------------------------------------------- | -------- | -------- | ------------------------ | ------------------------------------------------- |
| mode        | Defines the type of the picker                           | string   | 否       | All                      | partially (仅支持 date/time 模式)                      |
| style       | Sets style directly on picker component.                 | object   | 否       | IOS only                 | yes                                               |
| display     | Defines the visual display of the picker. The default value is "default". | string   | 否       | All                      | partially (支持"default"，<br/>"spinner"，"compact"，"inline") |
| onChange    | Date change handler.                                     | function | 否       | All                      | partially (仅支持 type 为 set 类型)                     |
| value       | Defines the date or time value used in the component.    | Date     | 是       | All                      | partially (仅 mode=date 且 <br/>display=spinner 时支持动态设置) |
| is24Hour    | Allows changing of the time picker to a 24-hour format.  | bool     | 否       | Windows and Android only | yes                                               |
| maximumDate | Defines the maximum date that can be selected            | Date     | 否       | All                      | partially (仅支持在 mode=date 且 <br/>display=spinner 时设置) |
| minimumDate | Defines the minimum date that can be selected.           | Date     | 否       | All                      | partially (仅支持在 mode=date 且 <br/>display=spinner 时设置) |
| disabled    | If true, the user won't be able to interact with the view. | bool     | 否       | IOS only                 | yes                                               |
| textColor   | Allows changing of the textColor of the date picker.     | string   | 否       | IOS only                 | partially (仅支持在 mode=date 且 <br/>display=compact 时设置) |
| timeZoneName   | Allows changing of the time zone of the date picker. By default, <br/>it uses the device's time zone.<br/> Use the time zone name from the IANA (TZDB) database name in https://en.wikipedia.org/wiki/List_of_tz_database_time_zones. | string   | 否       | iOS and Android only                 |  No  |
| timeZoneOffsetInMinutes    | Allows changing of the time zone of the date picker.<br/> By default, it uses the device's time zone.<br/> We strongly recommend using timeZoneName prop instead; <br/>this prop has known issues in the android implementation (eg. #528). | number   | 否       | iOS and Android only                 |  No  |
| timeZoneOffsetInSeconds    | Allows changing of the time zone of the date picker. <br/>By default, it uses the device's time zone. | number  | 否       |  Windows only                |  No  |
| dayOfWeekFormat   | Sets the display format for the day of the week headers.<br/> Reference: https://docs.microsoft.com/en-us/uwp/api/windows.<br/>ui.xaml.controls.calendarview.dayofweekformat?view=winrt-18362#remarks    | string   | 否       | Windows only                 |  No  |
| dateFormat   | Sets the display format for the date value in the picker's <br/>text box. Reference: https://docs.microsoft.com/en-us/uwp/api/windows.globalization.datetimeformatting.datetimeformatter?view=winrt-18362#examples    | string   | 否       | Windows only                 |  No  |
| firstDayOfWeek    | Indicates which day is shown as the first day of the week.    | number   | 否 | Android and Windows only                 |  No  |
| accentColor    | Allows changing the accentColor (tintColor) of the date picker. <br/>Has no effect when display is "spinner".    | string   | 否       | iOS only                 |  No  |
| themeVariant    | Allows overriding system theme variant (dark or light mode) <br/>used by the date picker. However,<br/> we recommend that you instead control the theme of the whole application using react-native-theme-control.   | string   | 否       | iOS only                |  No  |
| locale    | Allows changing the locale of the component. <br/>This affects the displayed text and the date / time formatting. <br/>By default, the device's locale is used.<br/> Please note using this prop is discouraged due to not working <br/>reliably in all picker modes. Prefer localization as documented in Localization note. | string   | 否       | iOS only                 |  No  |
| positiveButton    | Set the positive button label and text color.            | Object   | 否       | Android only                 | No   |
| neutralButton    | Allows displaying neutral button on picker dialog. <br/>Pressing button can be observed in onChange handler<br/> as event.type === 'neutralButtonPressed'    | Object   | 否       | Android only                 |  No  |
| negativeButton     | Set the negative button label and text color.            | Object   | 否       | Android only                 |  No  |
| minuteInterval     | The interval at which minutes can be selected. <br/>Possible values are: 1, 2, 3, 4, 5, 6, 10, 12, 15, 20, 30On<br/> Windows, this can be any number between 0-59.    | number   | 否       | All                 |  No  |
| testID     | Usually used by app automation frameworks. <br/>Fully supported on iOS.<br/> On Android, only supported for mode="date".    | string   | 否       | All                 |  Yes  |
| ViewProps     | On iOS, you can pass any View props to the component.<br/> Given that the underlying component is a native view, <br/>not all of them are guaranteed to be supported,<br/> but testID and onLayout are known to work.   | Object   | 否       | iOS only                 |  No  |
| onError     | Callback that is called when an error occurs inside <br/>the date picker native code (such as null activity). | function   | 否       | Android only                 |  No  |


## 遗留问题

- [x] 已解决：textColor 属性在 compact 和 inline 模式改变值后使用禁用操作，颜色会变白色[issue#17](https://github.com/react-native-oh-library/datetimepicker/issues/17)
- [ ] 部分接口，未适配: [issue#20](https://github.com/react-native-oh-library/datetimepicker/issues/20#issue-2390348970)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-datetimepicker/datetimepicker/blob/master/LICENSE.md) ，请自由地享受和参与开源。
