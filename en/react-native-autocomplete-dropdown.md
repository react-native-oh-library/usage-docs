> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-autoComplete-dropdown</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/onmotion/react-native-autocomplete-dropdown">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/onmotion/react-native-autocomplete-dropdown/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [GitHub address](https://github.com/onmotion/react-native-autocomplete-dropdown)

## Installation and Usage

<!-- tabs:start -->

####  npm

```bash
npm install react-native-autocomplete-dropdown@4.0.0-rc.5
```

#### yarn

```bash
yarn add react-native-autocomplete-dropdown@4.0.0-rc.5
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

1. Wrap your root component in AutocompleteDropdownContextProvider from react-native-autocomplete-dropdown

```jsx
import { AutocompleteDropdownContextProvider } from 'react-native-autocomplete-dropdown';
import { AppRegistry } from 'react-native'

AppRegistry.setWrapperComponentProvider(appParams => {
  return ({ children }) => (
      <AutocompleteDropdownContextProvider >
        {children}
      </AutocompleteDropdownContextProvider>
  );
});


```

2. Example with local Dataset

```jsx
import React, { memo, useState } from 'react'
import { Text, View } from 'react-native'
import type { TAutocompleteDropdownItem } from 'react-native-autocomplete-dropdown'
import { AutocompleteDropdown } from 'react-native-autocomplete-dropdown'

const ItemSeparatorComponent = () => <View style={{ height: 1, width: '100%', backgroundColor: '#d8e1e6' }} />

export const LocalDataSetExample = memo(() => {
  const [selectedItem, setSelectedItem] = useState<TAutocompleteDropdownItem | null>(null)

  return (
    <>
      <AutocompleteDropdown
        clearOnFocus={false}
        closeOnBlur={true}
        showClear={false}
        initialValue={{ id: '2' }} // or just '2'
        onSelectItem={item => setSelectedItem(item)}
        dataSet={[
          { id: '1', title: 'Alpha' },
          { id: '2', title: 'Beta' },
          { id: '3', title: 'Gamma' },
        ]}
        ignoreAccents
      />
      <Text style={{ color: '#668', fontSize: 13 }}>Selected item: {JSON.stringify(selectedItem)}</Text>
    </>
  )
}

```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in @react-native-oh-tpl/react-native-svg to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

   
## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name                          | Description                                                                                                   | Type                | Required | Platform    | HarmonyOS Support |
|-------------------------------|---------------------------------------------------------------------------------------------------------------|---------------------|----------|-------------|-------------------|
| dataSet                       | set of list items                                                                                             | array               | no       | iOS/Android | yes               |
| initialValue                  | string (id) or object that contain id                                                                         | object \| string    | no       | iOS/Android | yes               |
| loading                       | 	loading state                                                                                                | boolean             | no       | iOS/Android | yes               |
| useFilter                     | whether use local filter by dataSet (useful set to false for remote filtering to prevent rerender twice)      | boolean             | no       | iOS/Android | yes               |
| showClear                     | show clear button                                                                                             | boolean             | no       | iOS/Android | yes               |
| showChevron                   | show chevron (open/close) button                                                                              | boolean             | no       | iOS/Android | yes               |
| closeOnSubmit                 | sets the max stroke line width                                                                                | boolean             | no       | iOS/Android | yes               |
| clearOnFocus                  | whether to clear typed text on focus                                                                          | boolean             | no       | iOS/Android | yes               |
| caseSensitive                 | whether to perform case-sensitive search                                                                      | boolean             | no       | iOS/Android | yes               |
| ignoreAccents                 | ignore diacritics                                                                                             | boolean             | no       | iOS/Android | yes               |
| trimSearchText                | trim the searched text                                                                                        | boolean             | no       | iOS/Android | yes               |
| editable                      | is textInput editable                                                                                         | boolean             | no       | iOS/Android | yes               |
| debounce                      | wait ms before call onChangeText                                                                              | number              | no       | iOS/Android | yes               |
| suggestionsListMaxHeight      | max height of dropdown                                                                                        | number              | no       | iOS/Android | yes               |
| direction                     | "up" or "down"                                                                                                | up \| down          | no       | iOS/Android | yes               |
| matchFrom                     | whether match suggestions from start of titles or anywhere in the title. Possible values are "any" or "start" | any \| start        | no       | iOS/Android | yes               |
| onChangeText                  | event textInput onChangeText                                                                                  | function            | no       | iOS/Android | yes               |
| onSelectItem                  | event onSelectItem                                                                                            | function            | no       | iOS/Android | yes               |
| onOpenSuggestionsList         | event onOpenSuggestionsList                                                                                   | function            | no       | iOS/Android | yes               |
| onChevronPress                | event onChevronPress                                                                                          | function            | no       | iOS/Android | yes               |
| onClear                       | event on clear button press                                                                                   | function            | no       | iOS/Android | yes               |
| onSubmit                      | event on submit KB button press                                                                               | function            | no       | iOS/Android | yes               |
| onBlur                        | event fired on text input blur	                                                                               | function            | no       | iOS/Android | yes               |
| onFocus                       | event on focus text input                                                                                     | function            | no       | iOS/Android | yes               |
| renderItem                    | JSX for render item (item, searchText) => JSX                                                                 | function            | no       | iOS/Android | yes               |
| controller                    | return reference to module controller with methods close, open, toggle, clear, setInputText, setItem          | function            | no       | iOS/Android | yes               |
| containerStyle                | containerStyle                                                                                                | ViewStyle           | no       | iOS/Android | yes               |
| inputContainerStyle           | custom input container style                                                                                  | ViewStyle           | no       | iOS/Android | yes               |
| rightButtonsContainerStyle    | rightButtonsContainerStyle                                                                                    | ViewStyle           | no       | iOS/Android | yes               |
| suggestionsListContainerStyle | suggestionsListContainerStyle                                                                                 | ViewStyle           | no       | iOS/Android | yes               |
| suggestionsListTextStyle      | suggestionsListTextStyle                                                                                      | TextStyle           | no       | iOS/Android | yes               |
| rightIconComponent            | custom chevron icon                                                                                           | React.Component     | no       | iOS/Android | yes               |
| ChevronIconComponent          | Chevron Custom Icon                                                                                           | React.Component     | no       | iOS/Android | yes               |
| ClearIconComponent            | Clear Custom Icon                                                                                             | React.Component     | no       | iOS/Android | yes               |
| EmptyResultComponent          | replace the default `` Component on empty result                                                              | React.Component     | no       | iOS/Android | yes               |
| InputComponent                | input element component                                                                                       | React.ComponentType | no       | iOS/Android | yes               |
| emptyResultText               | replace the default "Nothing found" text on empty result                                                      | string              | no       | iOS/Android | yes               |
| textInputProps                | text input props                                                                                              | TextInputProps      | no       | iOS/Android | yes               |
| flatListProps                 | props for \ component                                                                                         | FlatListProps       | no       | iOS/Android | yes               |


## Known Issues

- [ ] When the TextInput is at the bottom of the page, the keyboard popping up can cause the measure method of the View tag to calculate the pageY incorrectly, resulting in an improperly positioned dropdown. This is an issue with the React Native framework.

## Others

- The closeOnBlur and bottomOffset properties are not supported in version 4.0.0-rc5. These properties are not accepted in the props of the component entry in the source code [Source code: index.tsx](https://github.com/onmotion/react-native-autocomplete-dropdown/blob/main/src/index.tsx#L59)

## License

This project is licensed under [The MIT License (MIT)](https://github.com/onmotion/react-native-autocomplete-dropdown/blob/main/LICENSE).
