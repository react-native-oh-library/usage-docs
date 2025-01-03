> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-picker-select)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-picker-select Releases](https://github.com/react-native-oh-library/react-native-picker-select/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-picker-select
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-picker-select
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

The HarmonyOS implementation of this library depends on the native code from@react-native-oh-tpl/@react-native-picker/picker. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in @react-native-oh-tpl/@react-native-picker/picker to add it to your project.


## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-picker-select Releases](https://github.com/react-native-oh-library/react-native-picker-select/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

- [ ] The property useNativeAndroidPickerStyle is currently not supported in HarmonyOS. [issue#3](https://github.com/react-native-oh-library/react-native-picker-select/issues/3)
- [ ] The property fixAndroidTouchableBug is currently not supported in HarmonyOS. [issue#4](https://github.com/react-native-oh-library/react-native-picker-select/issues/4)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/lawnstarter/react-native-picker-select/blob/master/LICENSE).
