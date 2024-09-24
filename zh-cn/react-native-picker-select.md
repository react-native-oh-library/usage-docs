> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-picker-select</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lawnstarter/react-native-picker-select?tab=readme-ov-file">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lawnstarter/react-native-picker-select/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-picker-select)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-picker-select Releases](https://github.com/react-native-oh-library/react-native-picker-select/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-picker-select@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-picker-select@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useRef, useState } from 'react';
import { StyleSheet, Text, View, TextInput, ScrollView } from 'react-native';
import RNPickerSelect from 'react-native-picker-select';

const sports = [
  {
    label: 'Football',
    value: 'football',
    key: 'football'
  },
  {
    label: 'Baseball',
    value: 'baseball',
    key: 'baseball'
  },
  {
    label: 'Hockey',
    value: 'hockey',
    key: 'hockey'
  },
];
const placeholder = {
  label: 'Select a sport...',
  value: null,
  color: '#9EA0A4',
};

export function PickerSelectExample() {
  const firstTextInputRef = useRef<TextInput | null>(null);
  const favSport0Ref = useRef<RNPickerSelect | null>(null);
  const favSport1Ref = useRef<RNPickerSelect | null>(null);

  const [stateval, setStateval] = useState({
    favSport0: undefined,
    favSport1: undefined,
    favSport2: undefined
  });

  return (
    <ScrollView style={{ flex: 1, backgroundColor: "#fff", }}>
      <Text>Standard TextInput</Text>
      <TextInput
        ref={firstTextInputRef}
        returnKeyType="next"
        enablesReturnKeyAutomatically
        onSubmitEditing={() => {
          favSport0Ref.current!.togglePicker(true, () => {
            console.log('togglePicker');
          });
        }}
        style={styles.inputAndroid}
        blurOnSubmit={false}
      />

      <View style={styles.paddingView} />

      <Text>useNativeAndroidPickerStyle (default)</Text>
      <RNPickerSelect
        ref={favSport0Ref}
        style={styles}
        placeholder={placeholder}
        items={sports}
        onValueChange={value => {
          setStateval({ ...stateval, favSport0: value });
        }}
        onUpArrow={() => {
          firstTextInputRef.current!.focus();
        }}
        onDownArrow={() => {
          favSport1Ref.current!.togglePicker();
        }}
        value={stateval.favSport0}
      />

      <View style={styles.paddingView} />

      <Text>set useNativeAndroidPickerStyle to false</Text>
      <RNPickerSelect
        ref={favSport1Ref}
        style={styles}
        placeholder={placeholder}
        items={sports}
        onValueChange={value => {
          setStateval({ ...stateval, favSport1: value });
        }}
        value={stateval.favSport1}
        useNativeAndroidPickerStyle={false}
      />

      <Text>example</Text>
      <RNPickerSelect
        style={styles}
        placeholder={placeholder}
        onValueChange={(value) => console.log(value)}
        items={[
          { label: 'Football', value: 'football' },
          { label: 'Baseball', value: 'baseball' },
          { label: 'Hockey', value: 'hockey' },
        ]}
      />
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#f8f9fa",
    alignItems: "center",
    justifyContent: "center"
  },
  paddingView: {
    margin: 10,
  },
  inputIOS: {
    fontSize: 16,
    paddingVertical: 12,
    paddingHorizontal: 10,
    borderWidth: 1,
    borderColor: 'gray',
    borderRadius: 4,
    color: 'black',
    paddingRight: 30, // to ensure the text is never behind the icon
  },
  inputAndroid: {
    width: 200,
    fontSize: 16,
    paddingHorizontal: 10,
    paddingVertical: 8,
    borderWidth: 0.5,
    borderColor: 'purple',
    borderRadius: 8,
    color: 'black',
    paddingRight: 30, // to ensure the text is never behind the icon
  },
});
```

## Link

本库依赖@react-native-oh-tpl/@react-native-picker/picker，如已在鸿蒙工程中引入过该库，则无需再次引入。

如未引入请参照[@react-native-oh-tpl/@react-native-picker/picker 文档](<https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-picker-picker(nocodegen).md>)进行引入。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-picker-select Releases](https://github.com/react-native-oh-library/react-native-picker-select/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Default | Required | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- | --- |
| onValueChange | Callback which returns `value, index`. | function | null | yes | All | yes |
| items | The items for the component to render.<br> - Each item should be in the following format:<br>`{label: 'Orange', value: 'orange', key: 'orange', color: 'orange', inputLabel: 'Orange!', testID: 'e2e-orange'}`<br>- `label` and `value` are required<br>- `key`, `color`, `testID`, and `inputLabel` are optional<br>- `key` will be set to equal `label` if not included<br>- `value` can be any data type<br>- If `inputLabel` exists, the TextInput will display that value instead of the `label` | array | null | yes | All | yes |
| placeholder | - An override for the default placeholder object with a label of `Select an item...` and a value of `null`.<br>- An empty object can be used if you'd like to disable the placeholder entirely. | object | null | no | All | yes |
| disabled | Disables interaction with the component. | boolean | false | no | All | yes |
| value | Will attempt to locate a matching item from the `items` array by checking each item's `value` property. If found, it will update the component to show that item as selected. If the value is not found, it will default to the first item. **WARNING:** do not use this attribute on iOS if you plan to allow the user to modify the value from within the `Picker`, use `itemKey` instead. | any | null | no | All | yes |
| itemKey | Will attempt to locate a matching item from the `items` array by checking each item's `key` property. If found, it will update the component to show that item as selected. If the key is not found, it will attempt to find a matching item by `value` as above. | string, number | undefined | no | All | yes |
| style | Style overrides for most parts of the component.<br>_More details in [styling](https://github.com/lawnstarter/react-native-picker-select?tab=readme-ov-file#styling)_. | object | {} | no | All | yes |
| darkTheme | Use the dark theme for the Picker. | boolean | false | no | iOS | yes |
| pickerProps | Additional props to pass to the Picker (some props are used in core functionality so use this carefully). | object | {} | no | All | yes |
| Icon | Custom icon component to be rendered.<br>_More details in [styling](https://github.com/lawnstarter/react-native-picker-select?tab=readme-ov-file#styling)_. | Component | null | no | All | yes |
| textInputProps | Additional props to pass to the TextInput (some props are used in core functionality so use this carefully). This is iOS only unless `useNativeAndroidPickerStyle={false}`. | object | {} | no | All | yes |
| touchableWrapperProps | Additional props to pass to the touchable wrapping the TextInput (some props are used in core functionality so use this carefully). | object | {} | no | All | yes |
| onOpen() | Callback triggered right before the opening of the picker.<br>_Not supported when `useNativeAndroidPickerStyle={true}`_. | function | null | no | All | yes |
| useNativeAndroidPickerStyle | The component defaults to using the native Android Picker in its un-selected state. Setting this flag to `false` will mimic the default iOS presentation where a tappable TextInput is displayed.<br>_More details in [styling](https://github.com/lawnstarter/react-native-picker-select?tab=readme-ov-file#styling)_. | boolean | true | no | Android | no |
| fixAndroidTouchableBug | Experimental flag to fix issue [#354](https://github.com/lawnstarter/react-native-picker-select/issues/354). | boolean | false | no | Android | no |
| InputAccessoryView | Replace the InputAcessoryView section (bar with tabbing arrown and Done button) of the opened picker with your own custom component. Can also return `null` here to hide completely. While this bar is typical on `select` elements on the web, the [interface guidelines](https://developer.apple.com/ios/human-interface-guidelines/controls/pickers/) does not include it. View the [snack](https://snack.expo.io/@lfkwtz/react-native-picker-select) to see examples on how this can be customized. | Component | null | no | iOS | yes |
| doneText | "Done" default text on the modal. Can be overwritten here. | string | "Done" | no | iOS | yes |
| onUpArrow() \/ onDownArrow() | Presence enables the corresponding arrow.<br>- Closes the picker.<br>- Calls the callback provided. | function | null | no | iOS | yes |
| onDonePress() | Callback when the 'Done' button is pressed. | function | null | no | iOS | yes |
| onClose(Bool) | Callback triggered right before the closing of the picker. It has one boolean parameter indicating if the done button was pressed or not. | function | null | no | iOS | yes |
| modalProps | Additional props to pass to the Modal (some props are used in core functionality so use this carefully). | function | null | no | iOS | yes |
| touchableDoneProps | Additional props to pass to the Done touchable (some props are used in core functionality so use this carefully). | function | null | no | iOS | yes |

## 遗留问题

- [ ] 属性useNativeAndroidPickerStyle在HarmonyOS中暂不支持 [issue#3](https://github.com/react-native-oh-library/react-native-picker-select/issues/3)
- [ ] 属性fixAndroidTouchableBug在HarmonyOS中暂不支持 [issue#4](https://github.com/react-native-oh-library/react-native-picker-select/issues/4)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/lawnstarter/react-native-picker-select/blob/master/LICENSE) ，请自由地享受和参与开源。
