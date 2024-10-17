<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-element-dropdown</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/hoaphantn7604/react-native-element-dropdown">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/hoaphantn7604/react-native-element-dropdown/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/hoaphantn7604/react-native-element-dropdown)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-element-dropdown@2.12.1
```

#### **yarn**

```bash
yarn add react-native-element-dropdown@2.12.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。
### Dropdown example
```js
 import React, { useState } from 'react';
  import { StyleSheet, Text, View } from 'react-native';
  import { Dropdown } from 'react-native-element-dropdown';

  const data = [
    { label: 'Item 1', value: '1' },
    { label: 'Item 2', value: '2' },
    { label: 'Item 3', value: '3' },
    { label: 'Item 4', value: '4' },
    { label: 'Item 5', value: '5' },
    { label: 'Item 6', value: '6' },
    { label: 'Item 7', value: '7' },
    { label: 'Item 8', value: '8' },
  ];

  const DropdownComponent = () => {
    const [value, setValue] = useState(null);
    const [isFocus, setIsFocus] = useState(false);

    const renderLabel = () => {
      if (value || isFocus) {
        return (
          <Text style={[styles.label, isFocus && { color: 'blue' }]}>
            Dropdown label
          </Text>
        );
      }
      return null;
    };

    return (
      <View style={styles.container}>
        {renderLabel()}
        <Dropdown
          style={[styles.dropdown, isFocus && { borderColor: 'blue' }]}
          placeholderStyle={styles.placeholderStyle}
          selectedTextStyle={styles.selectedTextStyle}
          inputSearchStyle={styles.inputSearchStyle}
          iconStyle={styles.iconStyle}
          data={data}
          search
          maxHeight={300}
          labelField="label"
          valueField="value"
          placeholder={!isFocus ? 'Select item' : '...'}
          searchPlaceholder="Search..."
          value={value}
          onFocus={() => setIsFocus(true)}
          onBlur={() => setIsFocus(false)}
          onChange={item => {
            setValue(item.value);
            setIsFocus(false);
          }}
        />
      </View>
    );
  };

  export default DropdownComponent;

  const styles = StyleSheet.create({
    container: {
      backgroundColor: 'white',
      padding: 16,
    },
    dropdown: {
      height: 50,
      borderColor: 'gray',
      borderWidth: 0.5,
      borderRadius: 8,
      paddingHorizontal: 8,
    },
    icon: {
      marginRight: 5,
    },
    label: {
      position: 'absolute',
      backgroundColor: 'white',
      left: 22,
      top: 8,
      zIndex: 999,
      paddingHorizontal: 8,
      fontSize: 14,
    },
    placeholderStyle: {
      fontSize: 16,
    },
    selectedTextStyle: {
      fontSize: 16,
    },
    iconStyle: {
      width: 20,
      height: 20,
    },
    inputSearchStyle: {
      height: 40,
      fontSize: 16,
    },
  });
```
### MultiSelect example
```js
  import React, { useState } from 'react';
  import { StyleSheet, View } from 'react-native';
  import { MultiSelect } from 'react-native-element-dropdown';

  const data = [
    { label: 'Item 1', value: '1' },
    { label: 'Item 2', value: '2' },
    { label: 'Item 3', value: '3' },
    { label: 'Item 4', value: '4' },
    { label: 'Item 5', value: '5' },
    { label: 'Item 6', value: '6' },
    { label: 'Item 7', value: '7' },
    { label: 'Item 8', value: '8' },
  ];

  const MultiSelectComponent = () => {
    const [selected, setSelected] = useState([]);

    return (
      <View style={styles.container}>
        <MultiSelect
          style={styles.dropdown}
          placeholderStyle={styles.placeholderStyle}
          selectedTextStyle={styles.selectedTextStyle}
          inputSearchStyle={styles.inputSearchStyle}
          iconStyle={styles.iconStyle}
          search
          data={data}
          labelField="label"
          valueField="value"
          placeholder="Select item"
          searchPlaceholder="Search..."
          value={selected}
          onChange={item => {
            setSelected(item);
          }}
          selectedStyle={styles.selectedStyle}
        />
      </View>
    );
  };

  export default MultiSelectComponent;

  const styles = StyleSheet.create({
    container: { padding: 16 },
    dropdown: {
      height: 50,
      backgroundColor: 'transparent',
      borderBottomColor: 'gray',
      borderBottomWidth: 0.5,
    },
    placeholderStyle: {
      fontSize: 16,
    },
    selectedTextStyle: {
      fontSize: 14,
    },
    iconStyle: {
      width: 20,
      height: 20,
    },
    inputSearchStyle: {
      height: 40,
      fontSize: 16,
    },
    icon: {
      marginRight: 5,
    },
    selectedStyle: {
      borderRadius: 12,
    },
  });
```
### SelectCountry example
```js
  import React, { useState } from 'react';
  import { StyleSheet } from 'react-native';
  import { SelectCountry } from 'react-native-element-dropdown';

  const local_data = [
    {
      value: '1',
      lable: 'Country 1',
      image: {
        uri: 'https://www.vigcenter.com/public/all/images/default-image.jpg',
      },
    },
    {
      value: '2',
      lable: 'Country 2',
      image: {
        uri: 'https://www.vigcenter.com/public/all/images/default-image.jpg',
      },
    },
    {
      value: '3',
      lable: 'Country 3',
      image: {
        uri: 'https://www.vigcenter.com/public/all/images/default-image.jpg',
      },
    },
    {
      value: '4',
      lable: 'Country 4',
      image: {
        uri: 'https://www.vigcenter.com/public/all/images/default-image.jpg',
      },
    },
    {
      value: '5',
      lable: 'Country 5',
      image: {
        uri: 'https://www.vigcenter.com/public/all/images/default-image.jpg',
      },
    },
  ];

  const SelectCountryScreen = _props => {
    const [country, setCountry] = useState('1');

    return (
      <SelectCountry
        style={styles.dropdown}
        selectedTextStyle={styles.selectedTextStyle}
        placeholderStyle={styles.placeholderStyle}
        imageStyle={styles.imageStyle}
        inputSearchStyle={styles.inputSearchStyle}
        iconStyle={styles.iconStyle}
        search
        maxHeight={200}
        value={country}
        data={local_data}
        valueField="value"
        labelField="lable"
        imageField="image"
        placeholder="Select country"
        searchPlaceholder="Search..."
        onChange={e => {
          setCountry(e.value);
        }}
      />
    );
  };

  export default SelectCountryScreen;

  const styles = StyleSheet.create({
    dropdown: {
      margin: 16,
      height: 50,
      borderBottomColor: 'gray',
      borderBottomWidth: 0.5,
    },
    imageStyle: {
      width: 24,
      height: 24,
    },
    placeholderStyle: {
      fontSize: 16,
    },
    selectedTextStyle: {
      fontSize: 16,
      marginLeft: 8,
    },
    iconStyle: {
      width: 20,
      height: 20,
    },
    inputSearchStyle: {
      height: 40,
      fontSize: 16,
    },
  });
```


## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71

## 属性

详细请查看 [react-native-element-dropdown的文档介绍](https://github.com/hoaphantn7604/react-native-element-dropdown)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Dropdown**：单选组件

| Name          | Description | Type                                 | Required | Platform                                                 | HarmonyOS Support                                        |
| ------------------ | ----------------------------------------------- | --------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| mode               | Mode 'modal' is show the dropdown in the middle of the screen. | 'default' or 'modal' of 'auto'                  | No        | All | Yes |
| data               | Data is a plain array | Array                                           | Yes       | All | Yes                                            |
| labelField         | Extract the label from the data item | String                                          | Yes       | All | Yes                             |
| valueField         | Extract the primary key from the data item | String                                          | Yes       | All | Yes |
| searchField        | Specify the field of data list you want to search | String                                          | No       | All | Yes |
| onChange           | Selection callback | (item: object) => void                          | Yes       | All | Yes |
| onChangeText       | Callback that is called when the text input's text changes | (search: string) => void                        | No       | All | Yes |
| value              | Set default value | Item                                            | No        | All | Yes |
| placeholder        | The string that will be rendered before dropdown has been selected | String                                          | No        | All | Yes |
| placeholderStyle   | Styling for text placeholder | TextStyle                                       | No        | All | Yes |
| selectedTextStyle  | Styling for selected text | TextStyle                                       | No        | All | Yes |
| selectedTextProps  | Text Props for selected text. Ex: numberOfLines={1} | TextProps                                       | No        | All | Yes |
| style              | Styling for view container | ViewStyle                                       | No        | All | Yes |
| containerStyle     | Styling for list container | ViewStyle                                       | No        | All | Yes |
| maxHeight          | Customize max height for list container | Number                                          | No        | All | Yes |
| minHeight          | Customize min height for list container | Number                                          | No        | All | Yes |
| fontFamily         | Customize font style | String                                          | No        | All | Yes |
| iconStyle          | Styling for icon | ImageStyle                                      | No        | All | Yes |
| iconColor          | Color of icons | String                                          | No        | All | Yes |
| itemContainerStyle | Styling for item container in list | TextStyle                                       | No        | All | Yes |
| itemTextStyle      | Styling for text item in list | TextStyle                                       | No        | All | Yes |
| activeColor        | Background color for item selected in list container | String                                          | No        | All | Yes |
| search             | Show or hide input search | Boolean                                         | No        | All | Yes |
| searchQuery        | Callback used to filter the list of items | (keyword: string, labelValue: string) => Boolean| No        | All | Yes |
| inputSearchStyle   | Styling for input search | ViewStyle                                       | No        | All | Yes |
| searchPlaceholder  | The string that will be rendered before text input has been entered | String                                          | No        | All | Yes |
| renderInputSearch  | Customize TextInput search | (onSearch: (text:string) => void) => JSX.Element| No        | All | Yes |
| disable            | Specifies the disabled state of the Dropdown | Boolean                                         | No        | All | Yes |
| dropdownPosition   | Dropdown list position. Default is 'auto' | 'auto' or 'top' or 'bottom'                     | No        | All | Yes |
| autoScroll         | Auto scroll to index item selected, default is true | Boolean                                         | No        | All | Yes |
| showsVerticalScrollIndicator | When true, shows a vertical scroll indicator, default is true | Boolean                               | No        | All | Yes |
| renderLeftIcon     | Customize left icon for dropdown | (visible?: boolean) => JSX.Element              | No        | All | Yes |
| renderRightIcon    | Customize right icon for dropdown | (visible?: boolean) => JSX.Element              | No        | All | Yes |
| renderItem         | Takes an item from data and renders it into the list | (item: object, selected: Boolean) => JSX.Element| No        | All | Yes |
| flatListProps      | Customize FlatList element | FlatListProps                                   | No        | All | Yes |
| inverted           | Reverses the direction of scroll on top position mode. Default is true | Boolean                                         | No        | All | Yes |
| onFocus            | Callback that is called when the dropdown is focused | () => void                                      | No        | All | Yes |
| onBlur             | Callback that is called when the dropdown is blurred | () => void                                      | No        | All | Yes |
| keyboardAvoiding   | keyboardAvoiding default is true | Boolean                                         | No        | All | Yes |
| backgroundColor    | Set background color | String                                          | No        | All | Yes |
| confirmSelectItem  | Turn On confirm select item. Refer example/src/dropdown/example3 | Boolean                                         | No        | All | Yes |
| onConfirmSelectItem | Selection callback. Refer example/src/dropdown/example3 | (item: object) => void                         | No        | All | Yes |
| testID             | Used to locate this view in end-to-end tests | String                                          | No        | All | Yes |
| itemTestIDField    | Add this field to the input data. Ex: DATA = [{itemTestIDField: '', label: '', value:: ''}] | String                                          | No        | All | Yes |
| accessibilityLabel | Set an accessibilityLabel on the view, so that people who use VoiceOver know what element they have selected | String     | No    | All | Yes |
| itemAccessibilityLabelField | Add this field to the input data. Ex: DATA = [{itemAccessibilityLabelField: '', label: '', value:: ''}] | String                                 | No        | All | Yes |
| closeModalWhenSelectedItem | By default, closeModalWhenSelectedItem is set to true. When closeModalWhenSelectedItem is set to false, the Modal won't close when an item is selected. | Boolean                                 | No        | All | Yes |
| excludeItems       | The array containing the items to be excluded. | Item[]                                          | No        | All | Yes |
| excludeSearchItems | The array containing the items to be excluded. | Item[]                                          | No        | All | Yes |

**MultiSelect**：多选组件
| Name          | Description   | Type                                         | Required | Platform                                                 | HarmonyOS Support                                        |
| ------------------ | -----------------------------------------------------| --------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| mode               | Mode 'modal' is show the dropdown in the middle of the screen. | 'default' or 'modal' of 'auto'                       | No        | All   | Yes |
| data               | Data is a plain array | Array                                                | Yes       | All                                            | Yes |
| labelField         | Extract the label from the data item | String                                               | Yes       | All                             | Yes |
| valueField         | Extract the primary key from the data item | String                                               | Yes       | All                       | Yes |
| searchField        | Specify the field of data list you want to search | String                                               | No       | All                | Yes |
| onChange           | Selection callback. A array containing the "valueField". | (value[]) => void                                    | Yes       | All         | Yes |
| onChangeText       | Callback that is called when the text input's text changes | (search: string) => void                             | No       | All       | Yes |
| value              | Set default value. A array containing the "valueField". | Item[]                                               | No        | All          | Yes |
| placeholder        | The string that will be rendered before dropdown has been selected | String                                               | No        | All | Yes |
| placeholderStyle   | Styling for text placeholder | TextStyle                                            | No        | All                                     | Yes |
| style              | Styling for view container | ViewStyle                                            | No        | All                                       | Yes |
| containerStyle     | Styling for list container | ViewStyle                                            | No        | All                                       | Yes |
| maxHeight          | Customize max height for list container | Number                                               | No        | All                          | Yes |
| minHeight          | Customize min height for list container | Number                                               | No        | All                          | Yes |
| maxSelect          | maximum number of items that can be selected | Number                                               | No        | All                     | Yes |
| fontFamily         | Customize font style | String                                               | No        | All                                             | Yes |
| iconStyle          | Styling for icon | ImageStyle                                           | No        | All                                                 | Yes |
| iconColor          | Color of icons | String                                               | No        | All                                                   | Yes |
| activeColor        | Background color for item selected in list container | String                                               | No        | All             | Yes |
| itemContainerStyle | Styling for item container in list | TextStyle                                            | No        | All                               | Yes |
| itemTextStyle      | Styling for text item in list | TextStyle                                            | No        | All                                    | Yes |
| selectedStyle      | Styling for selected view | ViewStyle                                            | No        | All                                        | Yes |
| selectedTextStyle  | Styling for selected text | TextStyle                                            | No        | All                                        | Yes |
| selectedTextProps  | Text Props for selected text. Ex: numberOfLines={1} | TextProps                                            | No        | All              | Yes |
| renderSelectedItem | Takes an item from data and renders it into the list selected | (item: object, unSelect?: () => void) => JSX.Element | No        | All    | Yes |
| alwaysRenderSelectedItem | Always show the list of selected items | Boolean                                        | No        | All                           | Yes |
| visibleSelectedItem | Option to hide selected item list, Ẽx: visibleSelectedItem={false} | Boolean                                             | No        | All | Yes |
| search             | Show or hide input search | Boolean                                              | No        | All                                        | Yes |
| searchQuery        | Callback used to filter the list of items | (keyword: string, labelValue: string) => Boolean     | No        | All                        | Yes |
| inputSearchStyle   | Styling for input search | ViewStyle                                            | No        | All                                         | Yes |
| searchPlaceholder  | The string that will be rendered before text input has been entered | String                                               | No        | All | Yes |
| renderInputSearch  | Customize TextInput search | (onSearch: (text:string) => void) => JSX.Element     | No        | All                                       | Yes |
| disable            | Specifies the disabled state of the Dropdown | Boolean                                              | No        | All                     | Yes |
| dropdownPosition   | Dropdown list position. Default is 'auto' | 'auto' or 'top' or 'bottom'                          | No        | All                        | Yes |
| showsVerticalScrollIndicator | When true, shows a vertical scroll indicator, default is true | Boolean                                    | No        | All    | Yes |
| renderLeftIcon     | Customize left icon for dropdown | (visible?: boolean) => JSX.Element                   | No        | All                                 | Yes |
| renderRightIcon    | Customize right icon for dropdown | (visible?: boolean) => JSX.Element                   | No        | All                                | Yes |
| renderItem         | Takes an item from data and renders it into the list | (item: object, selected: Boolean) => JSX.Element     | No        | All             | Yes |
| flatListProps      | Customize FlatList element | FlatListProps                                        | No        | All                                       | Yes |
| inverted           | Reverses the direction of scroll on top position mode. Default is true | Boolean                                              | No        | All | Yes |
| onFocus            | Callback that is called when the dropdown is focused | () => void                                           | No        | All             | Yes |
| onBlur             | Callback that is called when the dropdown is blurred | () => void                                           | No        | All             | Yes |
| keyboardAvoiding   | keyboardAvoiding default is true | Boolean                                              | No        | All                                 | Yes |
| inside             | inside default is false | Boolean                                              | No        | All                                          | Yes |
| backgroundColor    | Set background color | String                                               | No        | All                                             | Yes |
| confirmSelectItem  | Turn On confirm select item. Refer example/src/dropdown/example7 | Boolean                                              | No        | All | Yes |
| confirmUnSelectItem | Turn On confirm un-select item. Refer example/src/dropdown/example7 | Boolean                                             | No        | All | Yes |
| onConfirmSelectItem | Selection callback. Refer example/src/dropdown/example7 | (item: any) => void                                 | No        | All          | Yes |
| testID             | Used to locate this view in end-to-end tests | String                                               | No        | All                     | Yes |
| itemTestIDField    | Add this field to the input data. Ex: DATA = [{itemTestIDField: '', label: '', value:: ''}] | String                                               | No        | All | Yes |
| accessibilityLabel | Set an accessibilityLabel on the view, so that people who use VoiceOver know what element they have selected | String          | No    | All | Yes |
| itemAccessibilityLabelField | Add this field to the input data. Ex: DATA = [{itemAccessibilityLabelField: '', label: '', value:: ''}] | String                                      | No        | All | Yes |
| excludeItems       | The array containing the items to be excluded. | Item[]                                               | No        | All                   |                       |
| excludeSearchItems | The array containing the items to be excluded. | Item[]                                               | No        | All                   | Yes |

**SelectCountry**：选择国家/地区组件，接收所有Dropdown的props并新增了以下props

| Name       | Description                          | Type       | Required | Platform | HarmonyOS Support |
| ---------- | ------------------------------------ | ---------- | -------- | -------- | ----------------- |
| imageField | Extract the image from the data item | String     | Yes      | All      | Yes               |
| imageStyle | Styling for image                    | ImageStyle | No       | All      | Yes               |

## **Method**：静态方法

| Name  | Description         | Type       | Required | Platform | HarmonyOS Support |
| ----- | ------------------- | ---------- | -------- | -------- | ----------------- |
| open  | Open dropdown list  | () => void | No       | All      | Yes               |
| close | Close dropdown list | () => void | No       | All      | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/hoaphantn7604/react-native-element-dropdown/blob/master/LICENSE)，请自由地享受和参与开源。
<!-- {% endraw %} -->