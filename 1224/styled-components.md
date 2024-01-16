> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>styled-components</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/styled-components/styled-components/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/styled-components/styled-components)

## 安装与使用

进入到工程目录并输入以下命令：

#### **yarn**

```bash
yarn add styled-components@^6.1.1
```

<!-- tabs:start -->

#### **npm**

```bash
npm install styled-components@^6.1.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React from "react";

import styled from "styled-components";

// Create a <Title> react component that renders an <h1> which is
// centered, palevioletred and sized at 1.5em
const Title = styled.h1`
  font-size: 1.5em;
  text-align: center;
  color: palevioletred;
`;

// Create a <Wrapper> react component that renders a <section> with
// some padding and a papayawhip background
const Wrapper = styled.section`
  padding: 4em;
  background: papayawhip;
`;

function MyUI() {
  return (
    // Use them like any other React component – except they're styled!
    <Wrapper>
      <Title>Hello World, this is my first styled component!</Title>
    </Wrapper>
  );
}
```

## 约束与限制

### 兼容性

在下述版本验证通过：

1. IDE：DevEco Studio 4.1.3.412;SDK：OpenHarmony(api11) 4.1.0.53;测试设备：Mate40 Pro(NOH-AN00);ROM：2.0.0.52(SP22C00E52R1P17log);RNOH：0.72.11

## 属性

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [styled-components 源库地址](https://github.com/styled-components/styled-components)

| Name          | Description       | Type | Required | HarmonyOS Support |
| ------------- | ---------- | ---- | -------- |  -------- |
| ThemeProvider     | A helper component for theming.                                                                                                                                                       | component     | no       | yes      |
| css               | The css prop is a convenient way to iterate on your components without settling on fixed component boundaries yet                                                                     | prop          | no       | yes     |
| toStyleSheet      | convert a style object to a stylesheet object                                                                                                                                         | function      |no       | yes     |
| ThemeContext      | access the theme object and pass the theme object to the style component                                                                                                              | jsx component | no       | yes      |
| isStyledComponent | A utility to help identify styled components.                                                                                                                                         | function      | no       | yes      |
| withTheme         | This is a higher order component factory to get the current theme from a ThemeProvider and pass it to your component as a theme prop.                                                 | function      | no       | yes      |
| useTheme          | This is a custom hook to get the current theme from a ThemeProvider.                                                                                                                  | function      | no       | yes     |
| ThemeConsumer     | It passes the current theme (based on a ThemeProvider higher in your component tree) as an argument to the child function. From this function, you may return further JSX or nothing. | jsx component |no       | yes      |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/styled-components/styled-components/blob/main/LICENSE) ，请自由地享受和参与开源。
