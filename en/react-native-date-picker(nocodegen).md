Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-date-picker</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/henninghall/react-native-date-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/henninghall/react-native-date-picker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-date-picker)


## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package:[@react-native-oh-tpl/react-native-date-picker Releases](https://github.com/react-native-oh-library/react-native-date-picker/releases)。

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-date-picker@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-date-picker@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from 'react'
import { Button, View } from 'react-native'
import DatePicker from 'react-native-date-picker'

export default () => {
  const [date, setDate] = useState(new Date())
  const [open, setOpen] = useState(false)

  return (
    <View style={{flex:1, flexDirection:'column', justifyContent:'center'}}>
      <Button title="Open" onPress={() => setOpen(true)} />
      <DatePicker
        mode='date'
        modal
        open={open}
        date={date}
        onConfirm={(date) => {
          setOpen(false)
          setDate(date)
        }}
        onCancel={() => {
          setOpen(false)
        }}
      />
    </View>
  )
}


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

Open `entry/oh-package.json5`， file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-date-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-date-picker/harmony/date_picker.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.


> [!TIP] For details, see[Directly Linking Source Code](/zh-cn/link-source-code.md).


### 3.Configuring CMakeLists and Introducing RNDatePickerPackage

Open `entry/src/main/cpp/CMakeLists.txt`，and add the following code:

```diff
txtproject(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULE "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE}/@react-native-oh-tpl/react-native-date-picker/src/main/cpp" ./date_picker)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_date_picker)
# RNOH_END: link_packages
```

Open `entry/src/main/cpp/PackageProvider.cpp`，and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "DatePickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<DatePickerPackage>(ctx), 
    };
}
```

### 4.Introducing RNDatePicker Component to ArkTS
Find  **function buildCustomRNComponent()**，which is usually located in `entry/src/main/ets/pages/index.ets` or  `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { RNDatePicker } from "@react-native-oh-tpl/react-native-date-picker"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === RNDatePicker.NAME) {
+   RNDatePicker({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+   })
+ }
 ...
}
...
```
> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant arkTsComponentNames in entry/src/main/ets/pages/index.ets or entry/src/main/ets/rn/LoadBundle.ets and add the component name to the array.

```diff
  ...
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ RNDatePicker.NAME, 
  ];
```

### 5.Introducing RNDatePickerPackage Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
import type { RNPackageContext, RNPackage } from 'rnoh/ts';
...
+ import { RNDatePickerPackage} from '@react-native-oh-tpl/react-native-date-picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNDatePickerPackage(ctx)
  ];
}
```


### 6.Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-date-picker Releases](https://github.com/react-native-oh-library/react-native-date-picker/releases)


## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| props  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| date | The currently selected date.   | Date  | no |     all  |       yes|
| onDateChange | Date change handler ( Inline only )   |  (date: Date) => void  | no |     all  |       yes|
| maximumDate | Maximum selectable date.Example: new Date("2021-12-31")   | Date  | no |     all  |       yes|
| minimumDate | Minimum selectable date.Example: new Date("2021-01-01")   | Date  | no |     all  |       yes|
| mode | The date picker mode. "datetime", "date", "time"   | “'date' \|'time' \| 'datetime'”  | yes |     all  |       yes|
| onConfirm | Modal only: Date callback when user presses confirm button   | (date: Date) => void  | no |     all  |       yes|
| onCancel | Modal only: Callback for when user presses cancel button or closing the modal by pressing outside it.   | () => void  | no |     all  |       yes|
| is24hourSource | Change how the 24h mode (am/pm) should be determined, by device settings or by locale. {'locale', 'device'} (android only, default: 'device')   | “'locale' \| 'device'”  | no |     all  |       no|
| modal | Boolean indicating if modal should be used. Default: "false". When enabled, the other modal props needs to be used.   | boolean  | no |     all  |       yes|
| open | Modal only: Boolean indicating if modal should be open.   | boolean  | no |     all  |       yes|
| minuteInterval | The interval at which minutes can be selected.   | 1 \| 2 \| 3 \| 4 \| 5 \| 6 \|  10 \|  12 \| 15 \|  20 \| 30  | no |     all  |       no|
| title | Modal only: Title text. Can be set to null to remove text.   | string  | no |     all  |       no|
| confirmText | Modal only: Confirm button text   | string  | no |     all  |       no|
| cancelText | Modal only: Cancel button text.   | string  | no |     all  |       no|
| theme | Modal only: The theme of the modal. "light", "dark", "auto". Defaults to "auto".   | 'light' \| 'dark' \| 'auto'  | no |     all  |       no|
| buttonColor | Color of the confirm and cancel buttons. (android modal only)   | string  | no |     Android  |       no|
| dividerColor | Color of the divider / separator. (android only)   | string  | no |     Android  |       no|
| onStateChange | Spinner state change handler. Triggered on changes between "idle" and "spinning" state (Android inline only)   | (state: 'spinning' \| 'idle') => void  | no |     Android  |       no|
| locale | The locale for the date picker. Changes language, date order and am/pm preferences. Value needs to be a Locale ID.   | string  | no |     all  |       no|
| timeZoneOffsetInMinutes | imezone offset in minutes (default: device's timezone)   | number  | no |     all  |       no|


## Known Issues
 
- [ ] Property confirmText is not supported。[issue#11](https://github.com/react-native-oh-library/react-native-date-picker/issues/11)
- [ ] Property cancelText is not supported。[issue#12](https://github.com/react-native-oh-library/react-native-date-picker/issues/12)
- [ ] Property theme is not supported。[issue#13](https://github.com/react-native-oh-library/react-native-date-picker/issues/13)
- [ ] Property locale is not supported。[issue#17](https://github.com/react-native-oh-library/react-native-date-picker/issues/17)
- [ ] Property timeZoneOffsetInMinutes is not supported。[issue#18](https://github.com/react-native-oh-library/react-native-date-picker/issues/18)
- [ ] When the modal attribute is false and the mode attribute is datetime, harmonyOS does not support the inline datetime component。[issue#22](https://github.com/react-native-oh-library/react-native-date-picker/issues/22)
- [ ] Property is24hourSource is not supported。[issue#30](https://github.com/react-native-oh-library/react-native-date-picker/issues/30)
- [ ] Property minuteInterval is not supported。[issue#34](https://github.com/react-native-oh-library/react-native-date-picker/issues/34)
## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/henninghall/react-native-date-picker/blob/master/LICENSE) ，请自由地享受和参与开源。
