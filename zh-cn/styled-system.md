<!-- {% raw %} -->
> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>styled-system</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/styled-system/styled-system/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/styled-system/styled-system)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install styled-system@^5.1.5
```

#### **yarn**

```bash
yarn add styled-system@^5.1.5
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import styled from 'styled-components'
import { space, layout, typography, color } from 'styled-system'

// Add styled-system functions to your component
const Box = styled.div`
  ${space}
  ${layout}
  ${typography}
  ${color}
`
// width: 50%
<Box width={1/2} />

// font-size: 20px (theme.fontSizes[4])
<Box fontSize={4} />

// margin: 16px (theme.space[2])
<Box m={2} />

// padding: 32px (theme.space[3])
<Box p={3} />

// color
<Box color='tomato' />

// color: #333 (theme.colors.gray[0])
<Box color='gray.0' />

// background color
<Box bg='tomato' />
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52(SP22C00E52R1P17log);

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [styled-system 源库地址](https://github.com/styled-system/styled-system)

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
| color | 颜色        | prop | no       | yes               |
| bg    | 背景色      | prop | no       | yes               |

**API typography**

| Name          | Description | Type | Required | HarmonyOS Support | Notes                                   |
| ------------- | ----------- | ---- | -------- | ----------------- | --------------------------------------- |
| fontFamily    | 字体系列    | prop | no       | yes               | 与 Android、iOS效果一致，设置后均无效果 |
| fontSize      | 字号大小    | prop | no       | yes               |
| fontWeight    | 字体权重    | prop | no       | yes               |
| lineHeight    | 行高        | prop | no       | yes               |
| letterSpacing | 字符间距    | prop | no       | yes               |
| textAlign     | 文本对齐    | prop | no       | yes               |
| fontStyle     | 字体样式    | prop | no       | yes               |

**API layout**

| Name          | Description | Type | Required | HarmonyOS Support | Notes                                    |
| ------------- | ----------- | ---- | -------- | ----------------- | ---------------------------------------- |
| width         | 宽度        | prop | no       | yes               |
| height        | 高度        | prop | no       | yes               |
| display       | 显示类型    | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| minWidth      | 最小宽度    | prop | no       | yes               |
| minHeight     | 最小高度    | prop | no       | yes               |
| maxHeight     | 最大高度    | prop | no       | yes               |
| size          | 大小        | prop | no       | yes               |
| verticalAlign | 垂直对齐    | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| overflow      | 溢出        | prop | no       | yes               |
| overflowX     | X 轴溢出    | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| overflowY     | Y 轴溢出    | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |

**API flexbox**

| Name           | Description           | Type | Required | HarmonyOS Support | Notes                                    |
| -------------- | --------------------- | ---- | -------- | ----------------- | ---------------------------------------- |
| alignItems     | 列内轴对齐项          | prop | no       | yes               |                                          |
| alignContent   | 列内轴对齐内容        | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| justifyItems   | 行内轴对齐项          | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| justifyContent | 行内轴对齐内容        | prop | no       | yes               |
| flexWrap       | 换行                  | prop | no       | yes               |
| flexDirection  | 弹性方向              | prop | no       | yes               |
| flex           | 弹性布局              | prop | no       | yes               |
| flexGrow       | 分配剩余空间比例      | prop | no       | yes               |
| flexShrink     | 弹性收缩              | prop | no       | yes               |
| flexBasis      | 弹性初始长度          | prop | no       | yes               |
| justifySelf    | 行内对齐              | prop | no       | yes               |
| alignSelf      | 对齐，覆盖 alignItems | prop | no       | yes               |
| order          | 弹性布局顺序          | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |

**API border**

| Name                    | Description  | Type | Required | HarmonyOS Support | Notes                                    |
| ----------------------- | ------------ | ---- | -------- | ----------------- | ---------------------------------------- |
| border                  | 边框         | prop | no       | yes               |
| borderWidth             | 边框宽度     | prop | no       | yes               |
| borderStyle             | 边框样式     | prop | no       | yes               |
| borderColor             | 边框颜色     | prop | no       | yes               |
| borderRadius            | 边框圆角     | prop | no       | yes               |
| borderTop               | 上边框       | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| borderTopWidth          | 上边框宽度   | prop | no       | yes               |
| borderTopStyle          | 上边框样式   | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| borderTopColor          | 上边框颜色   | prop | no       | yes               |
| borderTopLeftRadius     | 上左边框圆角 | prop | no       | yes               |
| borderTopRightRadius    | 上右边框圆角 | prop | no       | yes               |
| borderRight             | 右边框       | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| borderRightWidth        | 右边框宽度   | prop | no       | yes               |
| borderRightStyle        | 右边框样式   | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| borderRightColor        | 右边框颜色   | prop | no       | yes               |
| borderBottom            | 下边框       | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| borderBottomWidth       | 下边框宽度   | prop | no       | yes               |
| borderBottomStyle       | 下边框样式   | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| borderBottomColor       | 下边框颜色   | prop | no       | yes               |
| borderBottomLeftRadius  | 左下边框圆角 | prop | no       | yes               |
| borderBottomRightRadius | 右下边框圆角 | prop | no       | yes               |
| borderLeft              | 左边框       | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| borderLeftWidth         | 左边框宽度   | prop | no       | yes               |
| borderLeftStyle         | 左边框样式   | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| borderLeftColor         | 左边框颜色   | prop | no       | yes               |
| borderX                 | X 轴边框     | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| borderY                 | Y 轴边框     | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |

**API position**

| Name     | Description  | Type | Required | HarmonyOS Support |
| -------- | ------------ | ---- | -------- | ----------------- |
| position | 定位         | prop | no       | yes               |
| zIndex   | 元素堆叠顺序 | prop | no       | yes               |
| top      | 上偏移量     | prop | no       | yes               |
| right    | 右偏移量     | prop | no       | yes               |
| bottom   | 下偏移量     | prop | no       | yes               |
| left     | 左偏移量     | prop | no       | yes               |

**API shadow**

| Name       | Description | Type | Required | HarmonyOS Support |
| ---------- | ----------- | ---- | -------- | ----------------- |
| textShadow | 文本阴影    | prop | no       | yes               |
| boxShadow  | 盒子阴影    | prop | no       | yes               |

**API background**

| Name               | Description | Type | Required | HarmonyOS Support | Notes                                    |
| ------------------ | ----------- | ---- | -------- | ----------------- | ---------------------------------------- |
| backgroundImage    | 背景图片    | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| backgroundSize     | 背景尺寸    | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| backgroundPosition | 背景定位    | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |
| backgroundRepeat   | 背景图平铺  | prop | no       | yes               | 与 Android、iOS 效果一致，设置后均无效果 |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/styled-system/styled-system/blob/master/LICENSE.md) ，请自由地享受和参与开源。

<!-- {% endraw %} -->