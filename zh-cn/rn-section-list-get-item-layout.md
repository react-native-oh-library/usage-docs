> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>rn-section-list-get-item-layout</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jsoendermann/rn-section-list-get-item-layout">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jsoendermann/rn-section-list-get-item-layout/blob/master/README.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

>[!tip] [Github 地址](https://github.com/jsoendermann/rn-section-list-get-item-layout)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add react-native-section-list-get-item-layout
```
#### **npm**

```bash
npm install react-native-section-list-get-item-layout
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import sectionListGetItemLayout from 'react-native-section-list-get-item-layout'

class MyComponent extends React.Component {
  constructor(props) {
    super(props)

    this.getItemLayout = sectionListGetItemLayout({
      // The height of the row with rowData at the given sectionIndex and rowIndex
      getItemHeight: (rowData, sectionIndex, rowIndex) => sectionIndex === 0 ? 100 : 50,

      // These four properties are optional
      getSeparatorHeight: () => 1 / PixelRatio.get(), // The height of your separators
      getSectionHeaderHeight: () => 20, // The height of your section headers
      getSectionFooterHeight: () => 10, // The height of your section footers
      listHeaderHeight: 40, // The height of your list header
    })
  }

  render() {
    return (
      <SectionList
        {...otherStuff}
        getItemLayout={this.getItemLayout}
      />
    )
  }
}
```

## 约束与限制

### 兼容性

 在下述版本验证通过：

 1. IDE：DevEco Studio 4.1.3.313;SDK：OpenHarmony(api11) 4.1.0.52;测试设备：Mate40 Pro(NOH-AN00);ROM：2.0.0.52(C00E52R1P17log);RNOH：0.72.11

## API

详情见 [rn-section-list-get-item-layout源库地址](https://github.com/jsoendermann/rn-section-list-get-item-layout)

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |
| sectionListGetItemLayout({getItemHeight, getSeparatorHeight, getSectionHeaderHeight,getSectionFooterHeight,listHeaderHeight}) |This package provides a function that helps you construct the getItemLayout function for your SectionLists. For an explanation of why this exists, see this post. It's meant to be used like this | function | Yes | / | Yes |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/jsoendermann/rn-section-list-get-item-layout/blob/master/LICENSE) ，请自由地享受和参与开源。