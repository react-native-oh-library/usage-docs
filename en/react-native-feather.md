> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-feather</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/yigithanyucedag/react-native-feather">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/yigithanyucedag/react-native-feather)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-feather@1.1.2
```

#### **yarn**

```bash
yarn add react-native-feather@1.1.2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

This library can use the [icon list](https://feathericons.com/).

> [!WARNING] The name of the imported repository remains unchanged. In addition, this library strongly depends on [@react-native-oh-tpl/react-native-svg](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-svg.md), therefore, install the svg library first.

```js
import React from "react";
import { Text, ScrollView } from "react-native";
import * as Icon from "react-native-feather";
import { Check } from "react-native-feather";

const FeatherExample = () => {
  return (
    <ScrollView>
      <Text style={{ color: "blue" }}>
        The react-native-feather library is only used to process SVG images. The following demos contain only images and are not bound to click events.
      </Text>
      <Text style={{ color: "blue" }}>
        Battery icon. The stroke is red, the filling color is green, and the width and height are 150.
      </Text>
      <Icon.Battery stroke="red" width={150} height={150} fill="green" />
      <Text style={{ color: "blue" }}> Menu bar. The stroke is green, and the default width and height are 25.</Text>
      <Icon.Menu stroke="green" />
      <Text style={{ color: "blue" }}>
        Playback icon. The default stroke color is the current color, the filling color is blue, and the width and height are 50.
      </Text>
      <Icon.Video fill="blue" width={50} height={50} />

      <Text style={{ color: "blue" }}>
        Check icon. The stroke color is red and the width and height are 32.
      </Text>
      <Check stroke="red" width={32} height={32} />
    </ScrollView>
  );
};

export default FeatherExample;
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-svg](/zh-cn/react-native-svg.md#link) to add it to your project.

## Constraints

### Compatibility

1. RNOH: 0.72.13; SDK: HarmonyOS NEXT Developer Preview1; IDE: DevEco Studio 4.1.3.500; ROM: 204.1.0.59;
2. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1 B.0.18, HarmonyOS NEXT Developer Preview0 B.0.60, HarmonyOS NEXT Developer Preview2 B.0.73; IDE: DevEco Studio 5.0.3.200; ROM: 2.0.0.18;

## Properties

This library receives all [SVG properties](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-svg.md).

### feather

This library is a UI component library. You can configure properties to implement corresponding functionalities.

| Prop        | Description                                                          | Default      | HarmonyOS Support |
| ----------- | -------------------------------------------------------------------- | ------------ | ----------------- |
| width       | Width of the icon.                                                   | 24           | yes               |
| height      | Height of the icon.                                                  | 24           | yes               |
| stroke      | The stroke prop refers to the color outline the icon.                | currentColor | yes               |
| strokeWidth | The strokeWidth prop specifies the width of the outline on the icon. | 2            | yes               |
| fill        | The fill prop refers to the color inside the icon.                   | none         | yes               |

## Known Issues

## Others

The following items must be consistent with those in the original library:

1. Before using this library, ensure that [`react-native-svg`](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-svg.md) has been installed.
2. This component contains all Feather icons that are compatible with [`react-native-svg`](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-svg.md).
3. This library is based on Feather V4.28.0.

## License

This project is licensed under [MIT License](https://www.mit-license.org).
