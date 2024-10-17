模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-dropdown-picker</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/hossein-zare/react-native-dropdown-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/hossein-zare/react-native-dropdown-picker/blob/5.x/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/hossein-zare/react-native-dropdown-picker)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-dropdown-picker@5.4.6
```

#### **yarn**

```bash
yarn add react-native-dropdown-picker@5.4.6
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, Text } from "react-native";
import DropDownPicker from "react-native-dropdown-picker";

export default function App() {
  const [open, setOpen] = useState(false);
  const [value, setValue] = useState(null);
  const [items, setItems] = useState([
    { label: "Apple", value: "apple" },
    { label: "Banana", value: "banana" },
    { label: "Pear", value: "pear" },
  ]);

  return (
    <View style={{ flex: 1 }}>
      <View
        style={{
          flex: 1,
          alignItems: "center",
          justifyContent: "center",
          paddingHorizontal: 15,
        }}
      >
        <DropDownPicker
          open={open}
          value={value}
          items={items}
          setOpen={setOpen}
          setValue={setValue}
          setItems={setItems}
          placeholder={"Choose a fruit."}
        />
      </View>

      <View
        style={{
          flex: 1,
          alignItems: "center",
          justifyContent: "center",
        }}
      >
        <Text>Chosen fruit: {value === null ? "none" : value}</Text>
      </View>
    </View>
  );
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25 (API Version 12 Canary4); IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                       | Description                                                                                                      | Type                                                               | Required | Platform | HarmonyOS Support |
|----------------------------|------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|----------|----------|-------------------|
| items                      | State variable that holds the items.                                                                             | array                                                              | yes      | All      | yes               |
| value                      | State variable that specifies the value of the selected item. It's an array of values for multiple item pickers. | string\|string[]                                                   | yes      | All      | yes               |
| open                       | State variable that specifies whether the picker is open.                                                        | boolean                                                            | yes      | All      | yes               |
| props                      | Adds native props for the container TouchableOpacity.                                                            | object                                                             | no       | All      | yes               |
| itemProps                  | Adds native props for the TouchableOpacity of each item.                                                         | object                                                             | no       | All      | yes               |
| containerProps             | Adds native props for the container.                                                                             | object                                                             | no       | All      | yes               |
| labelProps                 | Adds native props for the Text element of the selected item.                                                     | object                                                             | no       | All      | yes               |
| multiple                   | You can select multiple items                                                                                    | boolean                                                            | no       | All      | yes               |
| min                        | Specifies the minimum number of items.                                                                           | number                                                             | no       | All      | yes               |
| max                        | Specifies the maximum number of items.                                                                           | number                                                             | no       | All      | yes               |
| disabled                   | Disables the picker.                                                                                             | boolean                                                            | no       | All      | yes               |
| maxHeight                  | Max height of the drop-down box.                                                                                 | number                                                             | no       | All      | yes               |
| disableBorderRadius        | Disables changing the border radius when opening.                                                                | boolean                                                            | no       | All      | yes               |
| stickyHeader               | Makes categories stick to the top of the screen until the next one pushes it off.                                | boolean                                                            | no       | All      | yes               |
| autoScroll                 | Automatically scrolls to the first selected item.                                                                | boolean                                                            | no       | All      | yes               |
| testID                     | Used to locate the picker in end-to-end tests.                                                                   | string                                                             | no       | All      | yes               |
| zIndex                     | Specifies the stack order.                                                                                       | number                                                             | no       | All      | yes               |
| zIndexInverse              | Specifies the inverse stack order.                                                                               | number                                                             | no       | All      | yes               |
| setOpen                    | State callback that is called when the user presses the picker.                                                  | (open: boolean) => void                                            | yes      | All      | yes               |
| setItems                   | State callback that is called to modify or add new items.                                                        | (callback: SetStateAction[]) => void                               | no       | All      | yes               |
| setValue                   | State callback that is called when the value changes.                                                            | (callback: SetStateAction) => void                                 | yes      | All      | yes               |
| onChangeValue              | Callback that returns the current value.                                                                         | (value: ValueType) => void \| (value: ValueType[]) => void \| null | no       | All      | yes               |
| onSelectItem               | Callback that returns the selected item / items.                                                                 | (item: ItemType) => void \| (items: ItemType[]) => void \| null    | no       | All      | yes               |
| onPress                    | Callback that is called as soon as the user presses the picker.                                                  | (open: boolean) => void                                            | no       | All      | yes               |
| onOpen                     | Callback that is called when the user opens the picker.                                                          | () => void                                                         | no       | All      | yes               |
| onClose                    | Callback that is called when the user closes the picker.                                                         | () => void                                                         | no       | All      | yes               |
| style                      | Set style                                                                                                        | object                                                             | no       | All      | yes               |
| containerStyle             | Set containerStyle                                                                                               | object                                                             | no       | All      | yes               |
| disabledStyle              | Set disabledStyle                                                                                                | object                                                             | no       | All      | yes               |
| textStyle                  | Set textStyle                                                                                                    | object                                                             | no       | All      | yes               |
| labelStyle                 | Set labelStyle                                                                                                   | object                                                             | no       | All      | yes               |
| placeholder                | Placeholder text.                                                                                                | string                                                             | no       | All      | yes               |
| placeholderStyle           | placeholderStyle                                                                                                 | object                                                             | no       | All      | yes               |
| showArrowIcon              | Specifies if the arrow icons should be visible.                                                                  | boolean                                                            | no       | All      | yes               |
| showTickIcon               | Specifies if the tick icon should be visible.                                                                    | boolean                                                            | no       | All      | yes               |
| hideSelectedItemIcon       | Hides the icon of the selected item.                                                                             | boolean                                                            | no       | All      | yes               |
| ArrowUpIconComponent       | Changes the arrow-up icon.                                                                                       | function                                                           | no       | All      | yes               |
| ArrowDownIconComponent     | Changes the arrow-down icon.                                                                                     | function                                                           | no       | All      | yes               |
| TickIconComponent          | Changes the tick icon.                                                                                           | function                                                           | no       | All      | yes               |
| CloseIconComponent         | Changes the close icon.                                                                                          | function                                                           | no       | All      | yes               |
| arrowIconStyle             | Set arrowIconStyle                                                                                               | object                                                             | no       | All      | yes               |
| tickIconStyle              | Set tickIconStyle                                                                                                | object                                                             | no       | All      | yes               |
| closeIconStyle             | Set closeIconStyle                                                                                               | object                                                             | no       | All      | yes               |
| iconContainerStyle         | Set iconContainerStyle                                                                                           | object                                                             | no       | All      | yes               |
| arrowIconContainerStyle    | Set arrowIconContainerStyle                                                                                      | object                                                             | no       | All      | yes               |
| tickIconContainerStyle     | Set tickIconContainerStyle                                                                                       | object                                                             | no       | All      | yes               |
| closeIconContainerStyle    | Set closeIconContainerStyle                                                                                      | object                                                             | no       | All      | yes               |
| loading                    | Displays an ActivityIndicator when the items aren't loaded yet.                                                  | boolean                                                            | no       | All      | yes               |
| ActivityIndicatorComponent | Customizes the ActivityIndicator.                                                                                | function                                                           | no       | All      | yes               |
| activityIndicatorColor     | Changes the default color of the ActivityIndicator.                                                              | string                                                             | no       | All      | yes               |
| activityIndicatorSize      | Changes the default size of the ActivityIndicator.                                                               | number                                                             | no       | All      | yes               |
| searchable                 | Enables the search feature in the drop-down menu / modal.                                                        | boolean                                                            | no       | All      | yes               |
| searchTextInputProps       | Adds native props for the text input.                                                                            | object                                                             | no       | All      | yes               |
| searchWithRegionalAccents  | Allows searching without typing local accents.                                                                   | boolean                                                            | no       | All      | no               |
| disableLocalSearch         | Disables search between local items. This comes in handy for remote search.                                      | boolean                                                            | no       | All      | yes               |
| addCustomItem              | Shows the searched text as an item when there's nothing to show.                                                 | boolean                                                            | no       | All      | yes               |
| searchPlaceholder          | Changes the placeholder text of the text input. Both of the following properties are available.                  | string                                                             | no       | All      | yes               |
| onChangeSearchText         | Callback that is called when the text changes in the text input.                                                 | function                                                           | no       | All      | yes               |
| searchContainerStyle       | Set searchContainerStyle                                                                                         | object                                                             | no       | All      | yes               |
| searchTextInputStyle       | Set searchTextInputStyle                                                                                         | object                                                             | no       | All      | yes               |
| searchPlaceholderTextColor | Set searchPlaceholderTextColor                                                                                   | string                                                             | no       | All      | yes               |
| customItemContainerStyle   | Set customItemContainerStyle                                                                                     | object                                                             | no       | All      | yes               |
| customItemLabelStyle       | Set customItemLabelStyle                                                                                         | object                                                             | no       | All      | yes               |
| categorySelectable         | Specifies if the categories can be selected.                                                                     | boolean                                                            | no       | All      | yes               |
| listParentContainerStyle   | Set listParentContainerStyle                                                                                     | object                                                             | no       | All      | yes               |
| listParentLabelStyle       | Set listParentLabelStyle                                                                                         | object                                                             | no       | All      | yes               |
| listChildContainerStyle    | Set listChildContainerStyle                                                                                      | object                                                             | no       | All      | yes               |
| listChildLabelStyle        | Set listChildLabelStyle                                                                                          | object                                                             | no       | All      | yes               |
| mode                       | Modes display selected items.                                                                                    | 'DEFAULT'\|'SIMPLE'\|'BADGE'                                       | no       | All      | yes               |
| showBadgeDot               | Shows dots in the badges.                                                                                        | boolean                                                            | no       | All      | yes               |
| badgeProps                 | Adds native props for the badge container TouchableOpacity.                                                      | object                                                             | no       | All      | yes               |
| extendableBadgeContainer   | Allows the badges to expand in multiple rows.                                                                    | boolean                                                            | no       | All      | yes               |
| renderBadgeItem            | Renders the selected items.                                                                                      | function                                                           | no       | All      | yes               |
| badgeStyle                 | Set badgeStyle                                                                                                   | object                                                             | no       | All      | yes               |
| badgeTextStyle             | Set badgeTextStyle                                                                                               | object                                                             | no       | All      | yes               |
| badgeDotStyle              | Set badgeDotStyle                                                                                                | object                                                             | no       | All      | yes               |
| badgeSeparatorStyle        | Set badgeSeparatorStyle                                                                                          | object                                                             | no       | All      | yes               |
| badgeColors                | Gives background colors to badges based on the value.                                                            | object, string                                                     | no       | All      | yes               |
| badgeDotColors             | Gives background colors to badge dots based on the value.                                                        | object, string                                                     | no       | All      | yes               |
| dropDownDirection          | Specifies which direction the drop-down menu should open.                                                        | 'DEFAULT'\|'TOP'\|'BOTTOM'\|'AUTO'                                 | no       | All      | yes               |
| bottomOffset               | Specifies the maximum bottom offset. To use this prop you need dropDownDirection="AUTO".                         | number                                                             | no       | All      | yes               |
| onDirectionChanged         | Callback that is called when the direction changes.                                                              | function                                                           | no       | All      | yes               |
| dropDownContainerStyle     | Set dropDownContainerStyle                                                                                       | object                                                             | no       | All      | yes               |
| itemKey                    | Specifies which item key should be used as a key.                                                                | string                                                             | no       | All      | yes               |
| closeAfterSelecting        | Closes the picker after selecting an item.                                                                       | boolean                                                            | no       | All      | yes               |
| closeOnBackPressed         | Closes the picker after pressing the back button.                                                                | boolean                                                            | no       | All      | yes               |
| itemSeparator              | Specifies if the item separater should be visible.                                                               | boolean                                                            | no       | All      | yes               |
| renderListItem             | Customizes the renderListItem.                                                                                   | function                                                           | no       | All      | yes               |
| ListEmptyComponent         | Changes the default ListEmptyComponent.                                                                          | function                                                           | no       | All      | yes               |
| listItemContainerStyle     | Set listItemContainerStyle                                                                                       | object                                                             | no       | All      | yes               |
| listItemLabelStyle         | Set listItemLabelStyle                                                                                           | object                                                             | no       | All      | yes               |
| selectedItemContainerStyle | Set selectedItemContainerStyle                                                                                   | object                                                             | no       | All      | yes               |
| selectedItemLabelStyle     | Set selectedItemLabelStyle                                                                                       | object                                                             | no       | All      | yes               |
| disabledItemContainerStyle | Set disabledItemContainerStyle                                                                                   | object                                                             | no       | All      | yes               |
| disabledItemLabelStyle     | Set disabledItemLabelStyle                                                                                       | object                                                             | no       | All      | yes               |
| listMessageContainerStyle  | Set listMessageContainerStyle                                                                                    | object                                                             | no       | All      | yes               |
| listMessageTextStyle       | Set listMessageTextStyle                                                                                         | object                                                             | no       | All      | yes               |
| itemSeparatorStyle         | Set itemSeparatorStyle                                                                                           | object                                                             | no       | All      | yes               |
| listMode                   | You have 3 options when choosing the list mode.                                                                  | 'DEFAULT'\|'FLATLIST'\|'SCROLLVIEW'\|'MODAL'                       | no       | All      | yes               |
| flatListProps              | Adds native props for the FlatList.                                                                              | object                                                             | no       | All      | yes               |
| scrollViewProps            | Adds native props for the ScrollView.                                                                            | object                                                             | no       | All      | yes               |
| modalProps                 | Adds native props for the Modal.                                                                                 | object                                                             | no       | All      | yes               |
| modalTitle                 | Sets modal title.listMode="MODAL" and searchable={false} are required.                                           | string                                                             | no       | All      | yes               |
| modalAnimationType         | This prop controls how the modal animates.                                                                       | 'slide'\|'fade'\|'none'                                            | no       | All      | yes               |
| modalContentContainerStyle | Set modalContentContainerStyle                                                                                   | object                                                             | no       | All      | yes               |
| modalTitleStyle            | Set modalTitleStyle                                                                                              | object                                                             | no       | All      | yes               |
| rtl                        | Makes the component right to left.                                                                               | boolean                                                            | no       | All      | yes               |


## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                                           | Type     | Required | Platform | HarmonyOS Support |
|-------------------|-------------------------------------------------------|----------|----------|----------|-------------------|
| setLanguage       | You can also change the default language globally.    | function | no       | All      | yes               |
| addTranslation    | You are able to add a new translation to the package. | function | no       | All      | yes               |
| modifyTranslation | Modify an existing translation                        | function | no       | All      | yes               |
| addTheme          | Add a theme                                           | function | no       | All      | yes               |
| setTheme          | Change the default theme​                             | function | no       | All      | yes               |
## 遗留问题

- [ ] 方法String.prototype.normalize('NFD')在RN框架下有问题，导致属性searchWithRegionalAccents不生效。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/hossein-zare/react-native-dropdown-picker/blob/5.x/LICENSE) ，请自由地享受和参与开源。
