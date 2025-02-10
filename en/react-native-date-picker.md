> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-date-picker)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-date-picker Releases](https://github.com/react-native-oh-library/react-native-date-picker/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-date-picker
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-date-picker
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
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

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-date-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-date-picker/harmony/date_picker"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install 
```

### 3. Introducing RNDatePicker Component to ArkTS

(If the code of the repository is written through CAPI, delete this section.)<br>Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { RNDatePicker } from "@react-native-oh-tpl/react-native-date-picker"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === RNDatePicker.NAME) {
+   RNDatePicker({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
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
+ RNDatePicker.NAME, 
  ];
```
### 4. Introducing RNDatePickerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNDatePickerPackage} from '@react-native-oh-tpl/react-native-date-picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNDatePickerPackage(ctx)
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
- [ ]  不支持属性confirmText。[issue#11](https://github.com/react-native-oh-library/react-native-date-picker/issues/11)
- [ ]  不支持属性cancelText。[issue#12](https://github.com/react-native-oh-library/react-native-date-picker/issues/12)
- [ ]  不支持属性theme。[issue#13](https://github.com/react-native-oh-library/react-native-date-picker/issues/13)
- [ ]  不支持属性locale。[issue#17](https://github.com/react-native-oh-library/react-native-date-picker/issues/17)
- [ ]  不支持属性timeZoneOffsetInMinutes。[issue#18](https://github.com/react-native-oh-library/react-native-date-picker/issues/18)
- [ ]  当属性modal为false，mode属性为datetime时，harmonyOS不支持内联datetime组件。[issue#22](https://github.com/react-native-oh-library/react-native-date-picker/issues/22)
- [ ]  不支持is24hourSource属性。[issue#30](https://github.com/react-native-oh-library/react-native-date-picker/issues/30)
- [ ]  不支持minuteInterval属性。[issue#34](https://github.com/react-native-oh-library/react-native-date-picker/issues/34)

## Others
- The third-party library encapsulates the ArkUI DatePicker component, and there are some anomalies. Please refer to the [Official Description]( https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V13/ts-basic-components-datepicker-V13#datepickeroptions%E5%AF%B9%E8%B1%A1%E8%AF%B4%E6%98%8E)， Dates that slide out of the set range will not bounce back until the trailing animation property ends.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/henninghall/react-native-date-picker/blob/master/LICENSE).
