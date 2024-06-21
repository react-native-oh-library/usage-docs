<!-- {% raw %} -->
模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-reanimated-table</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/dohooo/react-native-reanimated-table/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/dohooo/react-native-reanimated-table)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

####  npm

```bash
npm install react-native-reanimated-table@^0.0.2
```

#### yarn

```bash
yarn add react-native-reanimated-table@^0.0.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import React, { Component } from 'react';
import { StyleSheet, View } from 'react-native';
import { Table, Row, Rows } from 'react-native-reanimated-table';

type State = {
  tableHead: string[];
  tableData: Array<string[]>;
}

export default class ExampleOne extends Component<{}, State> {
  constructor(props: {} | Readonly<{}>) {
    super(props);
    this.initData();
  }

  initData(){
    this.state = {
      tableHead: ['Head', 'Head2', 'Head3', 'Head4'],
      tableData: [
        ['1', '2', '3', '4'],
        ['a', 'b', 'c', 'd'],
        ['1', '2', '3', '456\n789'],
        ['a', 'b', 'c', 'd']
      ]
    }
  }

  render() {
    const state = this.state;
    return (
      <View style={styles.container}>
        <Table borderStyle={{borderWidth: 2, borderColor: '#c8e1ff'}}>
          <Row data={state.tableHead} style={styles.head} textStyle={styles.text}/>
          <Rows data={state.tableData} textStyle={styles.text}/>
        </Table>
      </View>
    )
  }
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 16, paddingTop: 30, backgroundColor: '#fff' },
  head: { height: 40, backgroundColor: '#f1f8ff' },
  text: { margin: 6 }
});
```

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-reanimated-table](https://github.com/dohooo/react-native-reanimated-table)

### Properties for all react-native-reanimated-table components:

| Name                      | Description                                                  | **Type** | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| data                      | Table data.                                                  | Array    | All         | Yes               |
| style                     | Container style.                                             | Style   | All         | Yes               |
| borderStyle               | Table border line width and color.                           | Object   | All         | Yes               |
| textStyle                 | Cell font style.                                             | Style   | All         | Yes               |
| flexArr                   | Flex value per column.                                       | Array   | All         | Yes               |
| widthArr                  | Width per column.                                            | Array   | All         | Yes               |
| heightArr                 | Height per line.                                             | Array   | All         | Yes               |
| ...props                  | more props                                                   | any     | All         | Yes               |


## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/dohooo/react-native-reanimated-table/blob/main/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->