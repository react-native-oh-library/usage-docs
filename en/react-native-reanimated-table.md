<!-- {% raw %} -->
Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-reanimated-table</code> </h1>
</p>
<p align="center">
  <a href="https://github.com/dohooo/react-native-reanimated-table/blob/main">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/dohooo/react-native-reanimated-table/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [GitHub address](https://github.com/dohooo/react-native-reanimated-table)

## Installation and Usage

Go to the project directory and execute the following instruction：

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

The following code shows the basic use scenario of the repository：

> [!WARNING] The name of the imported repository remains unchanged.

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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


Please check for details [react-native-reanimated-table](https://github.com/dohooo/react-native-reanimated-table)

### Properties for all react-native-reanimated-table components:

| Name                      | Description                                                  | **Type** | Required | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- | ----------------- |
| data                      | Table data.                                                  | Array    | Yes | All         | Yes               |
| style                     | Container style.                                             | Style   | Yes | All         | Yes               |
| borderStyle               | Table border line width and color.                           | Object   | Yes | All         | Yes               |
| textStyle                 | Cell font style.                                             | Style   | Yes | All         | Yes               |
| flexArr                   | Flex value per column.                                       | Array   | Yes | All         | Yes               |
| widthArr                  | Width per column.                                            | Array   | Yes | All         | Yes               |
| heightArr                 | Height per line.                                             | Array   | Yes | All         | Yes               |
| ...props                  | more props                                                   | any     | Yes  | All         | Yes               |


## Others

## Known Issues

## License


This project is licensed under [The MIT License (MIT)](https://github.com/dohooo/react-native-reanimated-table/blob/main/LICENSE).
<!-- {% endraw %} -->