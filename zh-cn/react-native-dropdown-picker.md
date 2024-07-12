<!-- {% raw %} -->

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

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Props                  | Description               | Type                             | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------------------- | -------------------------------- | -------- | -------- | ----------------- |
| items                  | items                     | Array                            | yes      | all      | yes               |
| open                   | open                      | Boolean                          | yes      | all      | yes               |
| placeholder            | placeholder               | string                           | no       | all      | yes               |
| closeAfterSelecting    | close After Selecting     | boolean                          | no       | all      | yes               |
| disabled               | disabled                  | Boolean                          | no       | all      | yes               |
| disabledStyle          | disabled Style            | Object                           | no       | all      | yes               |
| placeholderStyle       | placeholder style         | Object                           | no       | all      | yes               |
| listMode               | listMode                  | Object                           | no       | all      | yes               |
| searchable             | searchable                | boolean                          | no       | all      | yes               |
| searchPlaceholder      | search Placeholder        | string                           | no       | all      | yes               |
| language               | language                  | string                           | no       | all      | yes               |
| mode                   | Mode Type                 | 'DEFAULT' or 'SIMPLE' or 'BADGE' | no       | all      | yes               |
| maxHeight              | max Height                | number                           | no       | all      | yes               |
| renderBadgeItem        | render Badge Item         | JSX.Element                      | no       | all      | yes               |
| renderListItem         | render List Item          | JSX.Element                      | no       | all      | yes               |
| bottomOffset           | bottom Offset             | number                           | no       | all      | yes               |
| showArrowIcon          | show Arrow Icon           | boolean                          | no       | all      | yes               |
| autoScroll             | auto Scroll               | boolean                          | no       | all      | yes               |
| ArrowUpIconComponent   | Arrow Up Icon Component   | JSX.Element                      | no       | all      | yes               |
| ArrowDownIconComponent | Arrow Down Icon Component | JSX.Element                      | no       | all      | yes               |
| CloseIconComponent     | Close Icon Component      | JSX.Element                      | no       | all      | yes               |
| TickIconComponent      | Tick Icon Component       | JSX.Element                      | no       | all      | yes               |
| ListEmptyComponent     | List Empty Component      | JSX.Element                      | no       | all      | yes               |
| modalTitle             | modal Title               | string                           | no       | all      | yes               |
| modalTitleStyle        | modal Title Style         | object                           | no       | all      | yes               |
| loading                | loading                   | boolean                          | no       | all      | yes               |
| min                    | min                       | number                           | no       | all      | yes               |
| max                    | max                       | number                           | no       | all      | yes               |
| setOpen                | set Open                  | Dispatch                         | yes      | all      | yes               |
| setItems               | set Items                 | Dispatch                         | no       | all      | yes               |
| disableBorderRadius    | disable Border Radius     | object                           | no       | all      | yes               |
| onPress                | onPress                   | Dispatch                         | no       | all      | yes               |
| onOpen                 | onOpen                    | Dispatch                         | no       | all      | yes               |
| onClose                | onClose                   | Dispatch                         | no       | all      | yes               |
| zIndex                 | zIndex                    | number                           | no       | all      | yes               |
| theme                  | theme                     | string                           | no       | all      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/hossein-zare/react-native-dropdown-picker/blob/5.x/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->
