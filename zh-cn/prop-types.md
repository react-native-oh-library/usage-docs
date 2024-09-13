<!-- {% raw %} -->
> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>prop-types</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/facebook/prop-types/blob/v15.8.1/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/facebook/prop-types/tree/v15.8.1)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install prop-types
```

#### **yarn**

```bash
yarn add prop-types
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';
import PropTypes from 'prop-types';

const Greeting = ({ name, age }) => {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Hello, {name}!</Text>
      <Text style={styles.text}>You are {age} years old.</Text>
    </View>
  );
};

// 使用prop-types进行props类型验证
Greeting.propTypes = {
  name: PropTypes.string.isRequired, // name 必须是字符串且是必填项
  age: PropTypes.number,             // age 是可选的且必须是数字
};

// 默认props值
Greeting.defaultProps = {
  age: 0,
};

const App = () => {
  return (
    <View style={styles.appContainer}>
      <Greeting name="John" age={30} />
      <Greeting name="Doe" />
    </View>
  );
};

const styles = StyleSheet.create({
  appContainer: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f5fcff',
  },
  container: {
    marginBottom: 20,
  },
  text: {
    fontSize: 18,
  },
});

export default App;
```

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

#### 属性

| 名称        | 说明                                                 | 类型      | 是否必填 |  HarmonyOS 支持 |
| ----------- | ---------------------------------------------------- | --------- | -------- | -------- |
| any         | 约束属性为任意类型                                   | Attribute | NO       | yes      |
| array       | 约束属性为数组类型                                   | Attribute | NO       | yes      |
| bool        | 约束属性为布尔值类型                                 | Attribute | NO       | yes      |
| func        | 约束属性为函数类型                                   | Attribute | NO       | yes      |
| number      | 约束属性为数字类型                                   | Attribute | NO       | yes      |
| object      | 约束属性为对象类型                                   | Attribute | NO       | yes      |
| string      | 约束属性为字符串类型                                 | Attribute | NO       | yes      |
| symbol      | 约束属性为 symbol 类型                               | Attribute | NO       | yes      |
| element     | 约束属性为 react 元素                                | Attribute | NO       | yes      |
| node        | 约束属性为可以渲染的任何内容数字 字符串 元素 或 数组 | Attribute | NO       | yes      |
| elementType | 约束属性为 react 类型                                | Attribute | NO       | yes      |
| instanceOf  | 约束属性为某个对象的实例                             | function  | NO       | yes      |
| oneOf       | 约束属性为给定值中的任意一个                         | function  | NO       | yes      |
| oneOfType   | 约束属性为给定类型中的任意一个                       | function  | NO       | yes      |
| arrayOf     | 约束属性为指定类型的数组                             | function  | NO       | yes      |
| objectOf    | 约束属性为具有指定类型属性值的对象                   | function  | NO       | yes      |
| shape       | 约束属性为指定构成方式的对象                         | function  | NO       | yes      |
| exact       | 约束属性包含指定属性                                 | function  | NO       | yes      |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/facebook/prop-types/blob/v15.8.1/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->