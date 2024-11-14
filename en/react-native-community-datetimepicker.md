> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/datetimepicker)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/datetimepicker Releases](https://github.com/react-native-oh-library/datetimepicker/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

    "@react-native-oh-tpl/datetimepicker": "file:../../node_modules/@react-native-oh-tpl/datetimepicker/harmony/datetimepicker.har"
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

### 3. Configuring CMakeLists and Introducing datetimepicker

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

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4.Introducing DateTimePicker Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

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

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ DATETIME_PICKER_VIEW_TYPE
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/datetimepicker Releases](https://github.com/react-native-oh-library/datetimepicker/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

详情请查看[datetimepicker 官方文档](https://github.com/react-native-datetimepicker/datetimepicker)

| Name                    | Description                                                                                                                                                                                                                                                                                                                   | Type     | Required | Platform                 | HarmonyOS Support                                         |
|-------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|----------|--------------------------|-----------------------------------------------------------|
| mode                    | Defines the type of the picker                                                                                                                                                                                                                                                                                                | string   | No       | All                      | partially (仅支持 date/time 模式)                              |
| style                   | Sets style directly on picker component.                                                                                                                                                                                                                                                                                      | object   | No       | IOS only                 | yes                                                       |
| display                 | Defines the visual display of the picker. The default value is "default".                                                                                                                                                                                                                                                     | string   | No       | All                      | partially (支持"default"，<br/>"spinner"，"compact"，"inline") |
| onChange                | Date change handler.                                                                                                                                                                                                                                                                                                          | function | No       | All                      | partially (仅支持 type 为 set 类型)                             |
| value                   | Defines the date or time value used in the component.                                                                                                                                                                                                                                                                         | Date     | Yes      | All                      | partially (仅 mode=date 且 <br/>display=spinner 时支持动态设置)    |
| is24Hour                | Allows changing of the time picker to a 24-hour format.                                                                                                                                                                                                                                                                       | bool     | No       | Windows and Android only | yes                                                       |
| maximumDate             | Defines the maximum date that can be selected                                                                                                                                                                                                                                                                                 | Date     | No       | All                      | partially (仅支持在 mode=date 且 <br/>display=spinner 时设置)     |
| minimumDate             | Defines the minimum date that can be selected.                                                                                                                                                                                                                                                                                | Date     | No       | All                      | partially (仅支持在 mode=date 且 <br/>display=spinner 时设置)     |
| disabled                | If true, the user won't be able to interact with the view.                                                                                                                                                                                                                                                                    | bool     | No       | IOS only                 | yes                                                       |
| textColor               | Allows changing of the textColor of the date picker.                                                                                                                                                                                                                                                                          | string   | No       | IOS only                 | partially (仅支持在 mode=date 且 <br/>display=compact 时设置)     |
| timeZoneName            | Allows changing of the time zone of the date picker. By default, <br/>it uses the device's time zone.<br/> Use the time zone name from the IANA (TZDB) database name in https://en.wikipedia.org/wiki/List_of_tz_database_time_zones.                                                                                         | string   | No       | iOS and Android only     | No                                                        |
| timeZoneOffsetInMinutes | Allows changing of the time zone of the date picker.<br/> By default, it uses the device's time zone.<br/> We strongly recommend using timeZoneName prop instead; <br/>this prop has known issues in the android implementation (eg. #528).                                                                                   | number   | No       | iOS and Android only     | No                                                        |
| timeZoneOffsetInSeconds | Allows changing of the time zone of the date picker. <br/>By default, it uses the device's time zone.                                                                                                                                                                                                                         | number   | No       | Windows only             | No                                                        |
| dayOfWeekFormat         | Sets the display format for the day of the week headers.<br/> Reference: https://docs.microsoft.com/en-us/uwp/api/windows.<br/>ui.xaml.controls.calendarview.dayofweekformat?view=winrt-18362#remarks                                                                                                                         | string   | No       | Windows only             | No                                                        |
| dateFormat              | Sets the display format for the date value in the picker's <br/>text box. Reference: https://docs.microsoft.com/en-us/uwp/api/windows.globalization.datetimeformatting.datetimeformatter?view=winrt-18362#examples                                                                                                            | string   | No       | Windows only             | No                                                        |
| firstDayOfWeek          | Indicates which day is shown as the first day of the week.                                                                                                                                                                                                                                                                    | number   | No       | Android and Windows only | No                                                        |
| accentColor             | Allows changing the accentColor (tintColor) of the date picker. <br/>Has no effect when display is "spinner".                                                                                                                                                                                                                 | string   | No       | iOS only                 | No                                                        |
| themeVariant            | Allows overriding system theme variant (dark or light mode) <br/>used by the date picker. However,<br/> we recommend that you instead control the theme of the whole application using react-native-theme-control.                                                                                                            | string   | No       | iOS only                 | No                                                        |
| locale                  | Allows changing the locale of the component. <br/>This affects the displayed text and the date / time formatting. <br/>By default, the device's locale is used.<br/> Please note using this prop is discouraged due to not working <br/>reliably in all picker modes. Prefer localization as documented in Localization note. | string   | No       | iOS only                 | No                                                        |
| positiveButton          | Set the positive button label and text color.                                                                                                                                                                                                                                                                                 | Object   | No       | Android only             | No                                                        |
| neutralButton           | Allows displaying neutral button on picker dialog. <br/>Pressing button can be observed in onChange handler<br/> as event.type === 'neutralButtonPressed'                                                                                                                                                                     | Object   | No       | Android only             | No                                                        |
| negativeButton          | Set the negative button label and text color.                                                                                                                                                                                                                                                                                 | Object   | No       | Android only             | No                                                        |
| minuteInterval          | The interval at which minutes can be selected. <br/>Possible values are: 1, 2, 3, 4, 5, 6, 10, 12, 15, 20, 30On<br/> Windows, this can be any number between 0-59.                                                                                                                                                            | number   | No       | All                      | No                                                        |
| testID                  | Usually used by app automation frameworks. <br/>Fully supported on iOS.<br/> On Android, only supported for mode="date".                                                                                                                                                                                                      | string   | No       | All                      | Yes                                                       |
| ViewProps               | On iOS, you can pass any View props to the component.<br/> Given that the underlying component is a native view, <br/>not all of them are guaranteed to be supported,<br/> but testID and onLayout are known to work.                                                                                                         | Object   | No       | iOS only                 | No                                                        |
| onError                 | Callback that is called when an error occurs inside <br/>the date picker native code (such as null activity).                                                                                                                                                                                                                 | function | No       | Android only             | No                                                        |


## Known Issues

- [x] 已解决：textColor 属性在 compact 和 inline 模式改变值后使用禁用操作，颜色会变白色[issue#17](https://github.com/react-native-oh-library/datetimepicker/issues/17)
- [ ] 部分接口，未适配: [issue#20](https://github.com/react-native-oh-library/datetimepicker/issues/20#issue-2390348970)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-datetimepicker/datetimepicker/blob/master/LICENSE.md).
