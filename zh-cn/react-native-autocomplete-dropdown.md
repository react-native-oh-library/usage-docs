> 模板版本：v0.2.2

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



> [!TIP] [Github 地址](https://github.com/onmotion/react-native-autocomplete-dropdown)

## 安装与使用

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

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

1. Wrap your root component in AutocompleteDropdownContextProvider from react-native-autocomplete-dropdown

```tsx
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

```tsx
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

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档](/zh-cn/react-native-svg-capi.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

   
## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name                          | Description                                                                                                   | Type                | Required | Platform    | HarmonyOS Support |
|-------------------------------|---------------------------------------------------------------------------------------------------------------|---------------------|----------|-------------|-------------------|
| dataSet                       | set of list items                                                                                             | array               | no       | iOS/Android | yes               |
| initialValue                  | string (id) or object that contain id                                                                         | object \| string    | no       | iOS/Android | yes               |
| loading                       | 	loading state                                                                                                | boolean             | no       | iOS/Android | yes               |
| useFilter                     | whether use local filter by dataSet (useful set to false for remote filtering to prevent rerender twice)      | boolean             | no       | iOS/Android | yes               |
| showClear                     | show clear button                                                                                             | boolean             | no       | iOS/Android | yes               |
| showChevron                   | show chevron (open/close) button                                                                              | boolean             | no       | iOS/Android | yes               |
| closeOnBlur                   | whether to close dropdown on blur                                                                             | boolean             | no       | iOS/Android | yes               |
| closeOnSubmit                 | sets the max stroke line width                                                                                | boolean             | no       | iOS/Android | yes               |
| clearOnFocus                  | whether to clear typed text on focus                                                                          | boolean             | no       | iOS/Android | yes               |
| caseSensitive                 | whether to perform case-sensitive search                                                                      | boolean             | no       | iOS/Android | yes               |
| ignoreAccents                 | ignore diacritics                                                                                             | boolean             | no       | iOS/Android | yes               |
| trimSearchText                | trim the searched text                                                                                        | boolean             | no       | iOS/Android | yes               |
| editable                      | is textInput editable                                                                                        | boolean             | no       | iOS/Android | yes               |
| debounce                      | wait ms before call onChangeText                                                                              | number              | no       | iOS/Android | yes               |
| suggestionsListMaxHeight      | max height of dropdown                                                                                        | number              | no       | iOS/Android | yes               |
| direction                     | "up" or "down"                                                                                                | up \| down          | no       | iOS/Android | yes               |
| matchFrom                     | whether match suggestions from start of titles or anywhere in the title. Possible values are "any" or "start" | any \| start        | no       | iOS/Android | yes               |
| bottomOffset                  | for calculate dropdown direction (e.g. tabbar)                                                                | number              | no       | iOS/Android | yes               |
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
| rightButtonsContainerStyle    | rightButtonsContainerStyle                                                                                    | ViewStyle           | no       | iOS/Android | yes               |
| suggestionsListContainerStyle | suggestionsListContainerStyle                                                                                 | ViewStyle           | no       | iOS/Android | yes               |
| suggestionsListTextStyle      | suggestionsListTextStyle                                                                                      | TextStyle           | no       | iOS/Android | yes               |
| ChevronIconComponent          | Chevron Custom Icon                                                                                           | React.Component     | no       | iOS/Android | yes               |
| ClearIconComponent            | Clear Custom Icon                                                                                             | React.Component     | no       | iOS/Android | yes               |
| EmptyResultComponent          | replace the default `` Component on empty result                                                              | React.Component     | no       | iOS/Android | yes               |
| InputComponent                | input element component                                                                                       | React.ComponentType | no       | iOS/Android | yes               |
| emptyResultText               | replace the default "Nothing found" text on empty result                                                      | string              | no       | iOS/Android | yes               |
| textInputProps                | text input props                                                                                              | TextInputProps      | no       | iOS/Android | yes               |
| flatListProps                 | props for \ component                                                                                         | FlatListProps       | no       | iOS/Android | yes               |


## 遗留问题

- [ ] TextInput在页面底部时，键盘弹起会导致View标签measure方法计算pageY错误,导致dropdown位置不正确,RN框架问题。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/onmotion/react-native-autocomplete-dropdown/blob/main/LICENSE) ，请自由地享受和参与开源。
