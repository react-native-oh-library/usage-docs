> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>styled-system</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/styled-system/styled-system/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

>[!tip] [Github 地址](https://github.com/styled-system/styled-system)

## 安装与使用

进入到工程目录并输入以下命令：

#### **yarn**

```bash
yarn add styled-system
```
<!-- tabs:start -->

#### **npm**

```bash
npm i styled-system
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

 在下述版本验证通过：

 1. IDE：DevEco Studio 4.1.3.412;SDK：OpenHarmony(api11) 4.1.0.53;测试设备：Mate40 Pro(NOH-AN00);ROM：2.0.0.52(SP22C00E52R1P17log);RNOH：0.72.11

## 属性

详情见 [styled-system源库地址](https://github.com/styled-system/styled-system)

**API space**

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |
| margin | 外边距 | prop | No | / | Yes |
| marginTop | 上外边距 | prop | No | /  | Yes |
| marginRight | 右外边距 | prop | No | /  | Yes |
| marginLeft | 左外边距 | prop | No | /  | Yes |
| marginX | X轴外边距 | prop | No | /  | Yes |
| marginY | Y轴外边距 | prop | No | /  | Yes |
| padding |内边距 |prop  | No | /  | Yes |
| paddingTop |  上内边距| prop | No | / | Yes |
| paddingRight | 右内边距 | prop | No | / | Yes |
| paddingLeft | 左内边距 | prop | No | / | Yes |
| paddingBottom |下内边距 | prop | No | / | Yes |
| paddingX | X轴内边距 | prop | No | / | Yes |
| paddingY | Y轴内边距 | prop | No | / | Yes |

**API color**

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |
| color | 颜色| prop | No | / | Yes |
| bg | 背景色 | prop | No | /  | Yes |

**API typography**

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |
| fontFamily | 字体系列 | prop | No | / | Yes |
| fontSize | 字号大小 | prop | No | /  | Yes |
| fontWeight | 字体权重 | prop | No | / | Yes |
| lineHeight | 行高 | prop | No | /  | Yes |
| letterSpacing | 字符间距 | prop | No | / | Yes |
| textAlign | 文本对齐 | prop | No | /  | Yes |
| fontStyle | 字体样式 | prop | No | / | Yes |

**API layout**

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |备注 |
| ---- | ---- | ---- | -------- | -------- | -------- |-------- |
| width | 宽度 | prop | No | / | Yes |
| height | 高度 | prop | No | /  | Yes |
| display | 显示类型 | prop | No | / |Yes| 与android、ios效果一致，设置后均无效果 |
| minWidth | 最小宽度 | prop | No | /  | Yes |
| minHeight | 最小高度 | prop | No | /  | Yes |
| maxHeight |最大高度 | prop | No | / | Yes |
| size | 大小 | prop | No | /  | Yes |
| verticalAlign | 垂直对齐 | prop | No | / |Yes| 与android、ios效果一致，设置后均无效果 |
| overflow | 溢出 | prop | No | /  | Yes |
| overflowX | X轴溢出 | prop | No | / | Yes |
| overflowY | Y轴溢出 | prop | No | / | Yes |

**API flexbox**

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 | 备注|
| ---- | ---- | ---- | -------- | -------- | -------- |-------- |
| alignItems | 列内轴对齐项 | prop | No | / | Yes | |
| alignContent | 列内轴对齐内容 | prop | No | /  | Yes|与android、ios效果一致，设置后均无效果 |
| justifyItems | 行内轴对齐项 | prop | No | / | Yes|与android、ios效果一致，设置后均无效果 |
| justifyContent | 行内轴对齐内容 | prop | No | /  | Yes |
| flexWrap | 换行 | prop | No | / | Yes |
| flexDirection | 弹性方向 | prop | No | /  | Yes |
| flex | 弹性布局 | prop | No | / | Yes |
| flexGrow | 分配剩余空间比例 | prop | No | /  | Yes |
| flexShrink | 弹性收缩 | prop | No | / | Yes |
| flexBasis | 弹性初始长度 | prop | No | /  | Yes |
| justifySelf | 行内对齐 | prop | No | / | Yes |
| alignSelf | 对齐，覆盖alignItems | prop | No | / | Yes |
| order | 弹性布局顺序 | prop | No | / |Yes| 与android、ios效果一致，设置后均无效果 |

**API border**

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |  备注|
| ---- | ---- | ---- | -------- | -------- | -------- |-------- |
| border | 边框 | prop | No | / | Yes |
| borderWidth | 边框宽度 | prop | No | /  | Yes |
| borderStyle | 边框样式 | prop | No | / | Yes |
| borderColor | 边框颜色 | prop | No | /  | Yes |
| borderRadius | 边框圆角 | prop | No | / | Yes |
| borderTop | 上边框 | prop | No | /  | Yes |与android、ios效果一致，设置后均无效果 |
| borderTopWidth | 上边框宽度 | prop | No | / | Yes |
| borderTopStyle | 上边框样式 | prop | No | /  | Yes |与android、ios效果一致，设置后均无效果 |
| borderTopColor | 上边框颜色 | prop | No | / | Yes |
| borderTopLeftRadius | 上左边框圆角 | prop | No | /  | Yes |
| borderTopRightRadius | 上右边框圆角 | prop | No | / | Yes |
| borderRight | 右边框 | prop | No | / | Yes |与android、ios效果一致，设置后均无效果 |
| borderRightWidth | 右边框宽度 | prop | No | / | Yes |
| borderRightStyle |右边框样式 | prop | No | / |Yes | 与android、ios效果一致，设置后均无效果 |
| borderRightColor | 右边框颜色 | prop | No | /  | Yes |
| borderBottom | 下边框 | prop | No | / | Yes | 与android、ios效果一致，设置后均无效果 |
| borderBottomWidth |下边框宽度 | prop | No | /  | Yes |
| borderBottomStyle |下边框样式 | prop | No | / | Yes |与android、ios效果一致，设置后均无效果 |
| borderBottomColor | 下边框颜色 | prop | No | / | Yes |
| borderBottomLeftRadius | 左下边框圆角 | prop | No | / | Yes |
| borderBottomRightRadius | 右下边框圆角 | prop | No | / | Yes |
| borderLeft | 左边框 | prop | No | /  | Yes |与android、ios效果一致，设置后均无效果 |
| borderLeftWidth | 左边框宽度 | prop | No | / | Yes |
| borderLeftStyle | 左边框样式 | prop | No | /  |Yes | 与android、ios效果一致，设置后均无效果 |
| borderLeftColor | 左边框颜色 | prop | No | / | Yes |
| borderX | X轴边框 | prop | No | / |Yes | 与android、ios效果一致，设置后均无效果 |
| borderY |Y轴边框 | prop | No | / | Yes |与android、ios效果一致，设置后均无效果 |

**API position**

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 | 备注|
| ---- | ---- | ---- | -------- | -------- | -------- |-------- |
| position | 定位 | prop | No | / | Yes |
| zIndex | 元素堆叠顺序 | prop | No | /  |  Yes |与android、ios效果一致，设置后均无效果 |
| top | 上偏移量 | prop | No | / | Yes |
| right | 右偏移量 | prop | No | /  | Yes |
| bottom | 下偏移量 | prop | No | / | Yes |
| left | 左偏移量  | prop | No | /  | Yes |

**API shadow**

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |备注|
| ---- | ---- | ---- | -------- | -------- | -------- |-------- |
| textShadow  | 文本阴影 | prop | No | / | Yes |
| boxShadow | 盒子阴影 | prop | No | /  | Yes |与android、ios效果一致，设置后均无效果 |

**API background**

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |备注|
| ---- | ---- | ---- | -------- | -------- | -------- |-------- |
| backgroundImage  | 背景图片 | prop | No | / |Yes | 与android、ios效果一致，设置后均无效果 |
| backgroundSize | 背景尺寸 | prop | No | /  | Yes |与android、ios效果一致，设置后均无效果 |
| backgroundPosition | 背景定位 | prop | No | /  |Yes | 与android、ios效果一致，设置后均无效果 |
| backgroundRepeat | 背景图平铺 | prop | No | /  | Yes |与android、ios效果一致，设置后均无效果 |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/styled-system/styled-system/blob/master/LICENSE.md) ，请自由地享受和参与开源。
