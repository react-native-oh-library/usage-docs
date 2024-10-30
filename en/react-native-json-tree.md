> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-json-tree</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Dean177/react-native-json-tree">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Dean177/react-native-json-tree/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/Dean177/react-native-json-tree)

## Installation and Usage

#### **npm**

```bash
npm install react-native-json-tree@^1.3.0
```

#### **yarn**

```bash
yarn add react-native-json-tree@^1.3.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { View, ScrollView, Text } from "react-native";
import JSONTree from "react-native-json-tree";

export default () => {
  const data = {
    name: "John Doe",
    age: 30,
    address: {
      city: "New York",
      country: "USA",
    },
    hobbies: ["reading", "gaming", "hiking"],
  };

  const data1 = {
    name: "Charlie",
    age: 22,
  };

  const data2 = {
    name: "Bob",
    age: 35,
    info: {
      height: 180,
      weight: 120,
    },
    address: {
      street: "123 Elm St",
      city: "Springfield",
    },
  };

  const theme = {
    scheme: "monokai",
    author: "wimer hazenberg (http://www.monokai.nl)",
    base00: "#272822",
    base01: "#383830",
    base02: "#49483e",
    base03: "#75715e",
    base04: "#a59f85",
    base05: "#f8f8f2",
    base06: "#f5f4f1",
    base07: "#f9f8f5",
    base08: "#f92672",
    base09: "#fd971f",
    base0A: "#f4bf75",
    base0B: "#a6e22e",
    base0C: "#a1efe4",
    base0D: "#66d9ef",
    base0E: "#ae81ff",
    base0F: "#cc6633",
  };

  const shouldExpandNode = (key: any) => {
    const shouldExpandNodeKey = key.some((item: any) => {
      return item === "address";
    });
    return shouldExpandNodeKey;
  };

  const data3 = {
    name: "Fiona",
    age: 29,
  };

  const data4 = {
    name: "Wx",
    task: {
      weekday: "ro to work",
      weekend: "play",
    },
    beliked: "xiao mei",
    age: 18,
  };

  const data5 = {
    user: {
      name: "Alice",
      age: 25,
      address: {
        street: "123 Main St",
        city: "Somewhere",
        country: "Wonderland",
      },
    },
  };

  const data6 = {
    users: Array.from({ length: 100 }, (_, i) => ({
      id: i,
      name: `User ${i}`,
    })),
  };

  const data7 = {
    date: new Date(),
    number: 123456.789,
    name: "moon",
  };

  const formatDate = (date: any) => {
    if (!(date instanceof Date)) return "";
    const year = date.getFullYear();
    const month = String(date.getMonth() + 1).padStart(2, "0");
    const day = String(date.getDate()).padStart(2, "0");
    return `${year}-${month}-${day}`;
  };

  const postprocessValue = (value: any) => {
    if (value instanceof Date) {
      return formatDate(value);
    }
    if (typeof value === "number") {
      return value.toFixed(2);
    }
    return value;
  };

  const data8 = {
    name: "John Doe",
    age: 30,
    job: "Developer",
    salary: 100000,
  };

  const isCustomNode = (value: any) => {
    return typeof value === "number";
  };

  return (
    <ScrollView
      style={{ height: "100%", marginBottom: 20, backgroundColor: "pink" }}
    >
      <View style={{ marginBottom: 20 }}>
        <Text>要展示的 JSON 数据对象</Text>
        <JSONTree data={data} />
      </View>
      <View style={{ marginBottom: 20 }}>
        <Text>定制树状视图的主题样式</Text>
        <JSONTree data={data1} theme={theme} />
      </View>
      <View style={{ marginBottom: 20 }}>
        <Text>控制节点是否展开的函数</Text>
        <JSONTree data={data2} shouldExpandNode={shouldExpandNode} />
      </View>
      <View style={{ marginBottom: 20 }}>
        <Text>是否隐藏树的根节点</Text>
        <JSONTree data={data2} hideRoot={true} />
        <JSONTree data={data2} hideRoot={false} />
      </View>
      <View style={{ marginBottom: 20 }}>
        <Text>是否反转主题颜色</Text>
        <JSONTree data={data2} theme={theme} invertTheme={true} />
        <JSONTree data={data2} theme={theme} invertTheme={false} />
      </View>
      <View style={{ marginBottom: 20 }}>
        <Text>自定义节点的显示文本</Text>
        <JSONTree
          data={data3}
          getItemString={(type, data, itemType, itemString) => {
            return (
              <Text>
                {itemType}&&{itemString}{" "}
              </Text>
            );
          }}
        />
      </View>
      <View style={{ marginBottom: 20 }}>
        <Text>自定义节点标签的渲染函数</Text>
        <JSONTree
          data={data3}
          labelRenderer={(raw: any) => (
            <Text style={{ fontWeight: "bold" }}>{raw}</Text>
          )}
        />
      </View>
      <View style={{ marginBottom: 20 }}>
        <Text>自定义节点值的渲染函数</Text>
        <JSONTree
          data={data3}
          valueRenderer={(raw: any) => (
            <Text style={{ fontStyle: "italic" }}>{raw}</Text>
          )}
        />
      </View>
      <View style={{ marginBottom: 20 }}>
        <Text>对 JSON 对象的键进行排序</Text>
        <JSONTree
          data={data4}
          sortObjectKeys={(a: any, b: any) => {
            return a.localeCompare(b);
          }}
        />
      </View>
      <View style={{ marginBottom: 20 }}>
        <Text>用于在 JSON 树中标识和定制特定路径的数据节点</Text>
        <JSONTree data={data5} keyPath={["information"]} />
      </View>
      <View style={{ marginBottom: 20 }}>
        <Text>用于控制在 JSON 树中显示的集合的元素最大数量</Text>
        <JSONTree data={data6} collectionLimit={5} />
      </View>
      <View style={{ marginBottom: 20 }}>
        <Text>用于在值渲染之前对其进行自定义处理</Text>
        <JSONTree data={data7} postprocessValue={postprocessValue} />
      </View>
      <View>
        <Text>指定哪些节点应使用自定义渲染的属性</Text>
        <JSONTree data={data8} theme={theme} isCustomNode={isCustomNode} />
      </View>
    </ScrollView>
  );
};
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

This document is verified based on the following versions:

1. RNOH: 0.72.29; SDK: HarmonyOS NEXT Developer Beta6; IDE: DevEco Studio 5.0.3.706; ROM: NEXT.0.0.36;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

For details, see [react-native-json-tree docs](https://github.com/Dean177/react-native-json-tree)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                                                                               | Type         | Required | Platform | HarmonyOS Support |
| ------------------ | ----------------------------------------------------------------------------------------- | ------------ | -------- | -------- | ----------------- |
| `data`             | `JSON data object to be displayed`.                                                       | `Object`     | Yes      | All      | Yes               |
| `theme`            | `Theme style of the tree view.`                                                           | `Object`     | No       | All      | Yes               |
| `shouldExpandNode` | `Function that controls whether a node is expanded`.                                      | `() => bool` | No       | All      | Yes               |
| `hideRoot`         | `Whether to hide the root node of the tree`.                                              | `bool`       | No       | All      | Yes               |
| `invertTheme`      | `Indicates whether to reverse the theme color.`                                           | `bool`       | No       | All      | Yes               |
| `getItemString`    | `Customize the display of arrays, objects, and iterable nodes.`                           | `()=>void`   | No       | All      | Yes               |
| `labelRenderer`    | `Rendering function for custom node labels`.                                              | `()=>void`   | No       | All      | Yes               |
| `valueRenderer`    | `Rendering function for custom node values`.                                              | `()=>void`   | No       | All      | Yes               |
| `sortObjectKeys`   | `Sort the keys of JSON objects`.                                                          | `()=>void`   | No       | All      | Yes               |
| `keyPath`          | `A data node used to identify and customize a specific path in a JSON tree`.              | `['']`       | No       | All      | Yes               |
| `collectionLimit`  | `Use to control the maximum number of elements of a collection displayed in a JSON tree`. | `number`     | No       | All      | Yes               |
| `postprocessValue` | `For customizing values before they are rendered`.                                        | `()=>void`   | No       | All      | Yes               |
| `isCustomNode`     | `Specify which nodes should use custom rendered properties.`                              | `()=>bool`   | No       | All      | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/Dean177/react-native-json-tree/blob/master/LICENSE.md).
