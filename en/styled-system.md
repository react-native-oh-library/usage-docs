> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>styled-system</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/styled-system/styled-system/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [GitHub address](https://github.com/styled-system/styled-system)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install styled-system@5.1.5
```

#### **yarn**

```bash
yarn add styled-system@5.1.5
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React from "react";
import styled from "styled-components/native";
import { space, layout, color } from "styled-system";

const Box = styled.View`
  ${space}
  ${layout}
  ${color}
`;

const App = () => {
  return (
    <Box
      width="100%"
      height={200}
      padding={3}
      margin={4}
      backgroundColor="lightblue"
    >
      <Box
        width={100}
        height={100}
        padding={2}
        margin={2}
        backgroundColor="blue"
      />
    </Box>
  );
};

export default App;
```

## Constraints

## Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52(SP22C00E52R1P17log);
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [styled-system GitHub](https://github.com/styled-system/styled-system)


**API space**

| Name          | Description | Type | Required | HarmonyOS Support |
| ------------- | ----------- | ---- | -------- | ----------------- |
| margin        | 外边距      | prop | no       | yes               |
| marginTop     | 上外边距    | prop | no       | yes               |
| marginRight   | 右外边距    | prop | no       | yes               |
| marginLeft    | 左外边距    | prop | no       | yes               |
| marginX       | X 轴外边距  | prop | no       | yes               |
| marginY       | Y 轴外边距  | prop | no       | yes               |
| padding       | 内边距      | prop | no       | yes               |
| paddingTop    | 上内边距    | prop | no       | yes               |
| paddingRight  | 右内边距    | prop | no       | yes               |
| paddingLeft   | 左内边距    | prop | no       | yes               |
| paddingBottom | 下内边距    | prop | no       | yes               |
| paddingX      | X 轴内边距  | prop | no       | yes               |
| paddingY      | Y 轴内边距  | prop | no       | yes               |

**API color**

| Name  | Description | Type | Required | HarmonyOS Support |
| ----- | ----------- | ---- | -------- | ----------------- |
| color | color        | prop | no       | yes               |
| bg    | background color      | prop | no       | yes               |

**API typography**

| Name          | Description | Type | Required | HarmonyOS Support | Notes |
| ------------- | ----------- | ---- | -------- | ----------------- | ----- |
| fontSize      | fontSize    | prop | no       | yes               |       |
| fontWeight    | fontWeight    | prop | no       | yes               |       |
| lineHeight    | lineHeight        | prop | no       | yes               |       |
| letterSpacing | letterSpacing    | prop | no       | yes               |       |
| textAlign     | textAlign    | prop | no       | yes               |       |
| fontStyle     | fontStyle    | prop | no       | yes               |       |

**API layout**

| Name      | Description | Type | Required | HarmonyOS Support | Notes |
| --------- | ----------- | ---- | -------- | ----------------- | ----- |
| width     | width        | prop | no       | yes               |       |
| height    | height        | prop | no       | yes               |       |
| minHeight | minHeight    | prop | no       | yes               |       |
| maxHeight | maxHeight    | prop | no       | yes               |       |
| size      | size        | prop | no       | yes               |       |

**API flexbox**

| Name           | Description      | Type | Required | HarmonyOS Support | Notes |
| -------------- | ---------------- | ---- | -------- | ----------------- | ----- |
| alignItems     | 列内轴对齐项     | prop | no       | yes               |       |
| justifyContent | 行内轴对齐内容   | prop | no       | yes               |       |
| flexWrap       | 换行             | prop | no       | yes               |       |
| flexDirection  | 弹性方向         | prop | no       | yes               |       |
| flex           | 弹性布局         | prop | no       | yes               |       |
| flexGrow       | 分配剩余空间比例 | prop | no       | yes               |       |
| flexShrink     | 弹性收缩         | prop | no       | yes               |       |
| flexBasis      | 弹性初始长度     | prop | no       | yes               |       |

**API border**

| Name                    | Description  | Type | Required | HarmonyOS Support | Notes |
| ----------------------- | ------------ | ---- | -------- | ----------------- | ----- |
| border                  | 边框         | prop | no       | yes               |       |
| borderWidth             | 边框宽度     | prop | no       | yes               |       |
| borderStyle             | 边框样式     | prop | no       | yes               |       |
| borderColor             | 边框颜色     | prop | no       | yes               |       |
| borderRadius            | 边框圆角     | prop | no       | yes               |       |
| borderTopWidth          | 上边框宽度   | prop | no       | yes               |       |
| borderTopColor          | 上边框颜色   | prop | no       | yes               |       |
| borderTopLeftRadius     | 上左边框圆角 | prop | no       | yes               |       |
| borderTopRightRadius    | 上右边框圆角 | prop | no       | yes               |       |
| borderRightWidth        | 右边框宽度   | prop | no       | yes               |       |
| borderRightColor        | 右边框颜色   | prop | no       | yes               |       |
| borderBottomWidth       | 下边框宽度   | prop | no       | yes               |       |
| borderBottomColor       | 下边框颜色   | prop | no       | yes               |       |
| borderBottomLeftRadius  | 左下边框圆角 | prop | no       | yes               |       |
| borderBottomRightRadius | 右下边框圆角 | prop | no       | yes               |       |
| borderLeftWidth         | 左边框宽度   | prop | no       | yes               |       |
| borderLeftColor         | 左边框颜色   | prop | no       | yes               |       |

**API position**

| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | ----------------- |
| top  | top offset    | prop | no       | yes               |
| left | left offset  | prop | no       | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/styled-system/styled-system/blob/master/LICENSE.md)

