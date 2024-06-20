> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-json-tree
</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Dean177/react-native-json-tree">
        <img src="https://img.shields.io/badge/platforms-ios%20%7C%20android%20%7C%20web%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Dean177/react-native-json-tree/blob/master/LICENSE.md">
        <img src="https://img.shields.io/npm/l/react-native-svg.svg" alt="License" />
    </a>
</p>


> [!tip]
>
>  [Github 地址](https://github.com/Dean177/react-native-json-tree)
>
> `react-native-json-tree` 是一个用于在 React Native 应用中可视化 JSON 数据的组件库。它可以帮助您以树状结构的方式呈现和浏览复杂的 JSON 数据。

## 安装与使用

#### **npm**

```bash
npm install react-native-json-tree@^1.3.0
```

#### **yarn**

```bash
yarn add react-native-json-tree@^1.3.0
```

## 基本用法

```bash
import React from 'react';
import { View } from 'react-native';
import JSONTree from 'react-native-json-tree';

const MyComponent = () => {
  const data = {
    name: 'John Doe',
    age: 30,
    address: {
      city: 'New York',
      country: 'USA',
    },
    hobbies: ['reading', 'gaming', 'hiking'],
  };

  return (
    <View style={{ flex: 1 }}>
      <JSONTree data={data} />
    </View>
  );
};

export default MyComponent;

```

## 配置选项

- **hideRoot**: 是否隐藏根节点，默认为 `false`。
- **theme**: 主题样式对象，可用于自定义 JSON 树的外观。

```
<JSONTree
  data={data}
  hideRoot={true}
  theme={{
    extend: theme,
    valueLabel: {
      textDecoration: 'underline'
    },
    nestedNodeLabel: ({ style }, nodeType, expanded) => ({
      style: {
        ...style,
        textTransform: expanded ? 'uppercase' : style.textTransform
      }
    })
  }}
/>
```


下面是关于 `react-native-json-tree` 高级定制功能的文档：

## 高级定制

### 自定义主题

您可以通过 `theme` 属性来自定义 JSON 树的外观。以下是一些可用的自定义选项：

```
<JSONTree
  data={data}
  theme={{
    extend: theme,
    // 为字面值的键添加下划线
    valueLabel: {
      textDecoration: 'underline'
    },
    // 当对象展开时，将键切换为大写
    nestedNodeLabel: ({ style }, nodeType, expanded) => ({
      style: {
        ...style,
        textTransform: expanded ? 'uppercase' : style.textTransform
      }
    })
  }}
/>
```

### 自定义数组、对象和可迭代节点的标签

您可以使用 `getItemString` 来自定义数组、对象和可迭代节点的显示方式（可选）。

```
<JSONTree getItemString={(type, data, itemType, itemString) =>
  <Text>{itemType} {itemString}</Text>}
/>
```

### 自定义渲染

您可以传递以下属性来自定义渲染的标签和值：

```js
<JSONTree
  labelRenderer={raw => <Text style={{ fontWeight: 'bold' }}>{raw}</Text>}
  valueRenderer={raw => <Text style={{ fontStyle: 'italic' }}>{raw}</Text>}
/>
```

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                                                  | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| `data`          | json tree displays the data                                  | yes      | All      | yes               |
| ``theme``       | can customize the theme                                      | no       | All      | yes               |
| `getItemString` | can use getItemString to customize the display of arrays, objects, and iterable nodes | no       | All      | yes               |
| `labelRenderer` | can pass the following properties to customize the label for rendering | no       | All      | yes               |
| `valueRenderer` | You can pass the following properties to customize the rendered values | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-svg/blob/harmony/LICENSE) ，请自由地享受和参与开源。