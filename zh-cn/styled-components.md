> 模板版本：v0.1.3

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

<!-- tabs:start -->

#### **npm**

```bash
npm install styled-components@6.1.8
```

#### **yarn**

```bash
yarn add styled-components@6.1.8
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

<!-- {% raw %} -->
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
<!-- {% endraw %} -->

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52(SP22C00E52R1P17log);

## 属性

详情见 [styled-components 源库地址](https://github.com/styled-components/styled-components)

| 名称              | 说明                                                                                                                                                                                  | 类型          | 是否必填 | 原库平台 |  HarmonyOS 支持 |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | -------- | -------- | -------- |
| ThemeProvider     | A helper component for theming.                                                                                                                                                       | component     | No       | /        | Yes      |
| css               | The css prop is a convenient way to iterate on your components without settling on fixed component boundaries yet                                                                     | prop          | No       | /        | Yes      |
| toStyleSheet      | convert a style object to a stylesheet object                                                                                                                                         | function      | No       | /        | Yes      |
| ThemeContext      | access the theme object and pass the theme object to the style component                                                                                                              | jsx component | No       | /        | Yes      |
| isStyledComponent | A utility to help identify styled components.                                                                                                                                         | function      | No       | /        | Yes      |
| withTheme         | This is a higher order component factory to get the current theme from a ThemeProvider and pass it to your component as a theme prop.                                                 | function      | No       | /        | Yes      |
| useTheme          | This is a custom hook to get the current theme from a ThemeProvider.                                                                                                                  | function      | No       | /        | Yes      |
| ThemeConsumer     | It passes the current theme (based on a ThemeProvider higher in your component tree) as an argument to the child function. From this function, you may return further JSX or nothing. | jsx component | No       | /        | Yes      |
| createGlobalstyle | A helper function to generate a special StyledComponent that handles global styles                                                                                                    | function      | No       | Web      | No       |
| keyframes         | A helper method to create keyframes for animations.                                                                                                                                   | function      | No       | Web      | No       |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/styled-components/styled-components/blob/main/LICENSE) ，请自由地享受和参与开源。
