> Template version: v0.2.2

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


> [!TIP] [GitHub address](https://github.com/jsoendermann/rn-section-list-get-item-layout)

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.26; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.300; ROM: 3.0.0.25;
2. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71(API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## APIs

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [rn-section-list-get-item-layout](https://github.com/jsoendermann/rn-section-list-get-item-layout)

| Name                                                         | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| sectionListGetItemLayout({getItemHeight, getSeparatorHeight, getSectionHeaderHeight,getSectionFooterHeight,listHeaderHeight}) | This package provides a function that helps you construct the getItemLayout function for your SectionLists. For an explanation of why this exists, see this post. It's meant to be used like this | function | Yes      | All      | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/jsoendermann/rn-section-list-get-item-layout/blob/master/LICENSE).
