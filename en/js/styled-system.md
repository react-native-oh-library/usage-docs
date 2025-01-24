> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>styled-system</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/styled-system/styled-system/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/styled-system/styled-system)

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

1. RNOH: 0.72.11; SDK: OpenHarmony (api11) 4.1.0.53; IDE: DevEco Studio 4.1.3.412; ROM: 2.0.0.52 (SP22C00E52R1P17log);
2. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71 (API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [styled-system GitHub](https://github.com/styled-system/styled-system)


**API space**

| Name          | Description    | Type | Required | HarmonyOS Support |
| ------------- | -------------- | ---- | -------- | ----------------- |
| margin        | Margin         | prop | no       | yes               |
| marginTop     | Top margin     | prop | no       | yes               |
| marginRight   | Right margin   | prop | no       | yes               |
| marginLeft    | Left margin    | prop | no       | yes               |
| marginX       | X-axis margin  | prop | no       | yes               |
| marginY       | Y-axis margin  | prop | no       | yes               |
| padding       | Padding        | prop | no       | yes               |
| paddingTop    | Top padding    | prop | no       | yes               |
| paddingRight  | Right padding  | prop | no       | yes               |
| paddingLeft   | Left padding   | prop | no       | yes               |
| paddingBottom | Bottom padding | prop | no       | yes               |
| paddingX      | X-axis padding | prop | no       | yes               |
| paddingY      | Y-axis padding | prop | no       | yes               |

**API color**

| Name  | Description      | Type | Required | HarmonyOS Support |
| ----- | ---------------- | ---- | -------- | ----------------- |
| color | color            | prop | no       | yes               |
| bg    | background color | prop | no       | yes               |

**API typography**

| Name          | Description   | Type | Required | HarmonyOS Support | Notes |
| ------------- | ------------- | ---- | -------- | ----------------- | ----- |
| fontSize      | fontSize      | prop | no       | yes               |       |
| fontWeight    | fontWeight    | prop | no       | yes               |       |
| lineHeight    | lineHeight    | prop | no       | yes               |       |
| letterSpacing | letterSpacing | prop | no       | yes               |       |
| textAlign     | textAlign     | prop | no       | yes               |       |
| fontStyle     | fontStyle     | prop | no       | yes               |       |

**API layout**

| Name      | Description | Type | Required | HarmonyOS Support | Notes |
| --------- | ----------- | ---- | -------- | ----------------- | ----- |
| width     | width       | prop | no       | yes               |       |
| height    | height      | prop | no       | yes               |       |
| minHeight | minHeight   | prop | no       | yes               |       |
| maxHeight | maxHeight   | prop | no       | yes               |       |
| size      | size        | prop | no       | yes               |       |

**API flexbox**

| Name           | Description     | Type | Required | HarmonyOS Support | Notes |
| -------------- | --------------- | ---- | -------- | ----------------- | ----- |
| alignItems     | Align items     | prop | no       | yes               |       |
| justifyContent | Justify content | prop | no       | yes               |       |
| flexWrap       | Flex wrap       | prop | no       | yes               |       |
| flexDirection  | Flex direction  | prop | no       | yes               |       |
| flex           | Flex layout     | prop | no       | yes               |       |
| flexGrow       | Flex grow       | prop | no       | yes               |       |
| flexShrink     | Flex shrink     | prop | no       | yes               |       |
| flexBasis      | Flex basis      | prop | no       | yes               |       |

**API border**

| Name                    | Description                       | Type | Required | HarmonyOS Support | Notes |
| ----------------------- | --------------------------------- | ---- | -------- | ----------------- | ----- |
| border                  | Border                            | prop | no       | yes               |       |
| borderWidth             | Border width                      | prop | no       | yes               |       |
| borderStyle             | Border style                      | prop | no       | yes               |       |
| borderColor             | Border color                      | prop | no       | yes               |       |
| borderRadius            | Border radius                     | prop | no       | yes               |       |
| borderTopWidth          | Top border width                  | prop | no       | yes               |       |
| borderTopColor          | Top border color                  | prop | no       | yes               |       |
| borderTopLeftRadius     | Top border radius on the left     | prop | no       | yes               |       |
| borderTopRightRadius    | Top border radius on the right    | prop | no       | yes               |       |
| borderRightWidth        | Right border width                | prop | no       | yes               |       |
| borderRightColor        | Right border color                | prop | no       | yes               |       |
| borderBottomWidth       | Bottom border width               | prop | no       | yes               |       |
| borderBottomColor       | Bottom border color               | prop | no       | yes               |       |
| borderBottomLeftRadius  | Bottom border radius on the left  | prop | no       | yes               |       |
| borderBottomRightRadius | Bottom border radius on the right | prop | no       | yes               |       |
| borderLeftWidth         | Left border width                 | prop | no       | yes               |       |
| borderLeftColor         | Left border color                 | prop | no       | yes               |       |

**API position**

| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | ----------------- |
| top  | top offset  | prop | no       | yes               |
| left | left offset | prop | no       | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/styled-system/styled-system/blob/master/LICENSE.md)