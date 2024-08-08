> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-section-list-get-item-layout</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jsoendermann/rn-section-list-get-item-layout">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20windows%20%7C%20macos%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jsoendermann/rn-section-list-get-item-layout/blob/master/README.md">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>


> [!tip] [Github 地址](https://github.com/jsoendermann/rn-section-list-get-item-layout)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start --> 

#### **npm**

```bash
npm install react-native-section-list-get-item-layout@2.2.3
```

#### **yarn**

```bash
yarn add react-native-section-list-get-item-layout@2.2.3
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import sectionListGetItemLayout from "react-native-section-list-get-item-layout";

class MyComponent extends React.Component {
  constructor(props) {
    super(props);

    this.getItemLayout = sectionListGetItemLayout({
      // The height of the row with rowData at the given sectionIndex and rowIndex
      getItemHeight: (rowData, sectionIndex, rowIndex) =>
        sectionIndex === 0 ? 100 : 50,

      // These four properties are optional
      getSeparatorHeight: () => 1 / PixelRatio.get(), // The height of your separators
      getSectionHeaderHeight: () => 20, // The height of your section headers
      getSectionFooterHeight: () => 10, // The height of your section footers
      listHeaderHeight: 40, // The height of your list header
    });
  }

  render() {
    return <SectionList {...otherStuff} getItemLayout={this.getItemLayout} />;
  }
}

export default MyComponent
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.25;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [rn-section-list-get-item-layout 源库地址](https://github.com/jsoendermann/rn-section-list-get-item-layout)

| Name                                                         | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| sectionListGetItemLayout({getItemHeight, getSeparatorHeight, getSectionHeaderHeight,getSectionFooterHeight,listHeaderHeight}) | This package provides a function that helps you construct the getItemLayout function for your SectionLists. For an explanation of why this exists, see this post. It's meant to be used like this | function | Yes      | All      | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/jsoendermann/rn-section-list-get-item-layout/blob/master/LICENSE) ，请自由地享受和参与开源。
