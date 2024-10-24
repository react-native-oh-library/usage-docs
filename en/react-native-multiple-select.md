> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-multiple-select</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/toystars/react-native-multiple-select">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/toystars/react-native-multiple-select/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/toystars/react-native-multiple-select)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-multiple-select@0.5.12
```

#### **yarn**

```bash
yarn add react-native-multiple-select@0.5.12
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from 'react';
import { FlatList, Text, View } from 'react-native';
import MultiSelect from 'react-native-multiple-select';

const items = [{
    id: '92iijs7yta',
    name: 'Ondo'
  }, {
    id: 'a0s0a8ssbsd',
    name: 'Ogun'
  }, {
    id: '16hbajsabsd',
    name: 'Calabar'
  }, {
    id: 'nahs75a5sg',
    name: 'Lagos'
  }, {
    id: '667atsas',
    name: 'Maiduguri'
  }, {
    id: 'hsyasajs',
    name: 'Anambra'
  }, {
    id: 'djsjudksjd',
    name: 'Benue'
  }, {
    id: 'sdhyaysdj',
    name: 'Kaduna'
  }, {
    id: 'suudydjsjd',
    name: 'Abuja'
    }
];

export default class MultiSelectExample extends Component {

  state = {
    selectedItems : []
  };

  onSelectedItemsChange = (selectedItems: any) => {
    this.setState({ selectedItems });
  };

  multiSelect!: MultiSelect | any;

  render() {
    const { selectedItems } = this.state;

    return (
      <View style={{ flex: 1 }}>
        <MultiSelect
          hideTags
          items={items}
          uniqueKey="id"
          ref={(component) => { this.multiSelect = component }}
          onSelectedItemsChange={this.onSelectedItemsChange}
          selectedItems={selectedItems}
          selectText="Pick Items"
          searchInputPlaceholderText="Search Items..."
          onChangeInput={ (text)=> console.log(text)}
          altFontFamily="ProximaNova-Light"
          tagRemoveIconColor="#CCC"
          tagBorderColor="#CCC"
          tagTextColor="#CCC"
          selectedItemTextColor="#CCC"
          selectedItemIconColor="#CCC"
          itemTextColor="#000"
          displayKey="name"
          searchInputStyle={{ color: '#CCC' }}
          submitButtonColor="#CCC"
          submitButtonText="Submit"
        />
        <View>
          {this.multiSelect&&this.multiSelect.getSelectedItemsExt(selectedItems)}
        </View>
      </View>
    );
  }
}


export {MultiSelectExample}


```

## Constraints

### 注意事项

本库 HarmonyOS 侧需要引入字体包，如下所示。如已引用，则无需再次引入，可跳过本章节步骤，直接使用。

在 HarmonyOS 工程中的 entry/src/main/ets/pages/index.ets 中添加如下代码：

```diff
  ...
RNApp({
    rnInstanceConfig: {
+    fontResourceByFontFamily: {
+      'Pacifico-Regular': $rawfile("fonts/Pacifico-Regular.ttf"),
+    }
    },
})
```

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.29; SDK: HarmonyOS NEXT Developer Beta6; IDE: DevEco Studio 5.0.3.706; ROM: 3.0.0.61;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Prop                          | Description                                                                                                                                                                                                                                                                                                                                     | Type                               | Required | Platform | HarmonyOS Support |
| ----------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- | -------- | -------- | ----------------- |
| `altFontFamily`               | Font family for searchInputPlaceholderText                                                                                                                                                                                                                                                                                                      | String                             | no       | All      | yes               |
| `canAddItems`                 | Defaults to "false". This allows a user to add items to the list of items provided. You need to handle adding the new items in the onAddItem function prop. Items may be added with the return key on the native keyboard                                                                                                                       | Boolean                            | no       | All      | yes               |
| `displayKey`                  | Defaults to "name". This string will be used to select the key to display the objects in the items array                                                                                                                                                                                                                                        | String                             | no       | All      | yes               |
| `fixedHeight`                 | Defaults to false. Specifies if select dropdown take height of content or a fixed height with a scrollBar (There is an issue with this behavior when component is nested in a ScrollView in which scroll event will only be dispatched to parent ScrollView and select component won't be scrollable). See this issue for more info             | Boolean                            | no       | All      | yes               |
| `filterMethod`                | Defaults to "partial". options: ["partial", "full"] Choose the logic on how the system filters items based on searchTerm. partial: checks all individual words and if at least one word matches will include that item. full: checks to ensure the item contains the full substring of searchterm in order minus any leading or trailing spaces | String                             | no       | All      | yes               |
| `flatListProps`               | Properties for the FlatList. Pass any property that is required on the FlatList of the dropdown menu                                                                                                                                                                                                                                            | Object                             | no       | All      | yes               |
| `fontFamily`                  | Custom font family to be used in component (affects all text except searchInputPlaceholderText described above)                                                                                                                                                                                                                                 | String                             | no       | All      | yes               |
| `fontSize`                    | Font size for selected item name displayed as label for multiselect.                                                                                                                                                                                                                                                                            | Number                             | no       | All      | yes               |
| `hideDropdown`                | Defaults false. Hide dropdown menu with a cancel, and use arrow-back                                                                                                                                                                                                                                                                            | Boolean                            | no       | All      | yes               |
| `hideSubmitButton`            | Defaults to false. Hide submit button from dropdown, and rather use arrow-button in search field                                                                                                                                                                                                                                                | Boolean                            | no       | All      | yes               |
| `hideTags`                    | Defaults to false. Hide tokenized selected items, in case selected items are to be shown somewhere else in view (check below for more info)                                                                                                                                                                                                     | Boolean                            | no       | All      | yes               |
| `searchIcon`                  | Element or functional component to change the Search Icon                                                                                                                                                                                                                                                                                       | Element, Object, boolean, Function | no       | All      | yes               |
| `itemFontFamily`              | Font family for each non-selected item in multi-select drop-down                                                                                                                                                                                                                                                                                | String                             | no       | All      | yes               |
| `itemFontSize`                | Font size used for each item in the multi-select drop-down                                                                                                                                                                                                                                                                                      | Number                             | no       | All      | yes               |
| `itemTextColor`               | Text color for each non-selected item in multi-select drop-down                                                                                                                                                                                                                                                                                 | String                             | no       | All      | yes               |
| `items`                       | List of items to display in the multi-select component. JavaScript Array of objects. Each object must contain a name and unique identifier (Check sample above)                                                                                                                                                                                 | Array, control prop                | yes      | All      | yes               |
| `noItemsText`                 | Text that replace default "no items to display"                                                                                                                                                                                                                                                                                                 | String                             | no       | All      | yes               |
| `onAddItem`                   | JavaScript function passed in as an argument. The function is called everytime a new item is added, and receives the entire list of items. Here you should ensure that the new items are added to your provided list of items in addition to any other consequences of new items being added                                                    | function                           | no       | All      | yes               |
| `onChangeInput`               | JavaScript function passed in as an argument. The function is called everytime TextInput is changed with the value                                                                                                                                                                                                                              | function                           | no       | All      | yes               |
| `onClearSelector`             | JavaScript function passeed in as an argument. The function is called everytime back button is pressed                                                                                                                                                                                                                                          | function                           | no       | All      | yes               |
| `onSelectedItemsChange`       | JavaScript function passed in as an argument. The function is to be defined with an argument (selectedItems). Triggered when Submit button is clicked (for multi select) or item is clicked (for single select). (Check sample above)                                                                                                           | function                           | yes      | All      | yes               |
| `onToggleList`                | JavaScript function passed in as an argument. The function is called everytime the multiselect component is pressed                                                                                                                                                                                                                             | function                           | no       | All      | yes               |
| `searchInputPlaceholderText`  | Placeholder text displayed in multi-select filter input                                                                                                                                                                                                                                                                                         | String                             | no       | All      | yes               |
| `searchInputStyle`            | Style object for multi-select input element                                                                                                                                                                                                                                                                                                     | Object                             | no       | All      | yes               |
| `selectText`                  | Text displayed in main component                                                                                                                                                                                                                                                                                                                | String                             | no       | All      | yes               |
| `selectedText`                | Text displayed when an item is selected can be replaced by any string                                                                                                                                                                                                                                                                           | String                             | no       | All      | yes               |
| `selectedItemFontFamily`      | Font family for each selected item in multi-select drop-down                                                                                                                                                                                                                                                                                    | String                             | no       | All      | yes               |
| `selectedItemIconColor`       | Color for selected check icon for each selected item in multi-select drop-down                                                                                                                                                                                                                                                                  | String                             | no       | All      | yes               |
| `selectedItemTextColor`       | Text color for each selected item in multi-select drop-down                                                                                                                                                                                                                                                                                     | String                             | no       | All      | yes               |
| `single`                      | Toggles select component between single option and multi option                                                                                                                                                                                                                                                                                 | Boolean                            | no       | All      | yes               |
| `styleDropdownMenu`           | Style the view of the dropdown menu                                                                                                                                                                                                                                                                                                             | Style                              | no       | All      | yes               |
| `styleDropdownMenuSubsection` | Style the inner view of the dropdown menu                                                                                                                                                                                                                                                                                                       | Style                              | no       | All      | yes               |
| `styleIndicator`              | Style the Icon for indicator                                                                                                                                                                                                                                                                                                                    | Style                              | no       | All      | yes               |
| `styleInputGroup`             | Style the Container of the Text Input Group                                                                                                                                                                                                                                                                                                     | Style                              | no       | All      | yes               |
| `styleItemsContainer`         | Style the Container of the items that are displayed in a list                                                                                                                                                                                                                                                                                   | Style                              | no       | All      | yes               |
| `styleListContainer`          | Style the Container of main list                                                                                                                                                                                                                                                                                                                | Style                              | no       | All      | yes               |
| `styleMainWrapper`            | Style the Main Container of the MultiSelector                                                                                                                                                                                                                                                                                                   | Style                              | no       | All      | yes               |
| `styleRowList`                | Style the Row that is displayed after you                                                                                                                                                                                                                                                                                                       | Style                              | no       | All      | yes               |
| `styleSelectorContainer`      | Style the Container of the Selector when user clicks on the dropdown                                                                                                                                                                                                                                                                            | Style                              | no       | All      | yes               |
| `styleTextDropdown`           | Style text of the Dropdown                                                                                                                                                                                                                                                                                                                      | Text Style                         | no       | All      | yes               |
| `styleTextDropdownSelected`   | Style text of the Dropdown selected                                                                                                                                                                                                                                                                                                             | Text Style                         | no       | All      | yes               |
| `styleTextTag`                | Style text of the tag                                                                                                                                                                                                                                                                                                                           | Text Style                         | no       | All      | yes               |
| `submitButtonColor`           | Background color for submit button                                                                                                                                                                                                                                                                                                              | String                             | no       | All      | yes               |
| `submitButtonText`            | Text displayed on submit button                                                                                                                                                                                                                                                                                                                 | String                             | no       | All      | yes               |
| `tagBorderColor`              | Border color for each selected item                                                                                                                                                                                                                                                                                                             | String                             | no       | All      | yes               |
| `tagContainerStyle`           | Style the container of the tag view                                                                                                                                                                                                                                                                                                             | Style                              | no       | All      | yes               |
| `tagRemoveIconColor`          | Color to be used for the remove icon in selected items list                                                                                                                                                                                                                                                                                     | String                             | no       | All      | yes               |
| `tagTextColor`                | Text color for selected items list                                                                                                                                                                                                                                                                                                              | String                             | no       | All      | yes               |
| `textColor`                   | Color for selected item name displayed as label for multiselect                                                                                                                                                                                                                                                                                 | String                             | no       | All      | yes               |
| `textInputProps`              | Properties for the Text Input. Pass any property that is required on the text input                                                                                                                                                                                                                                                             | Object                             | no       | All      | yes               |
| `uniqueKey`                   | Unique identifier that is part of each item's properties. Used internally as means of identifying each item (Check sample below)                                                                                                                                                                                                                | String                             | yes      | All      | yes               |
| `selectedItems`               | List of selected items keys . JavaScript Array of strings, that can be instantiated with the component                                                                                                                                                                                                                                          | Array, control prop                | no       | All      | yes               |
| `removeSelected`              | Filter selected items from list to be shown in List                                                                                                                                                                                                                                                                                             | Boolean                            | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/toystars/react-native-multiple-select/blob/master/LICENSE).
