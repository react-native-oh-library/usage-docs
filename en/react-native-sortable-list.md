> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-sortable-list</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gitim/react-native-sortable-list">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/gitim/react-native-sortable-list/blob/master/LICENSE"/>
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-sortable-list)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-sortabel-list Releases](https://github.com/react-native-oh-library/react-native-sortable-list/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-sortable-list
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-sortable-list
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 *
 * @format
 */

import React, {
  useCallback,
  useEffect,
  useMemo,
  useRef,
  useState,
} from "react";
import {
  Animated,
  Easing,
  StyleSheet,
  Text,
  Image,
  View,
  Dimensions,
  Platform,
  ScrollView,
  TextInput,
  Button,
} from "react-native";
import SortableList from "react-native-sortable-list";

const window = Dimensions.get("window");

const data = {
  0: {
    text: "Chloe （0）",
  },
  1: {
    text: "Jasper （1）",
  },
  2: {
    text: "Pepper （2）",
  },
  3: {
    text: "Oscar （3）",
  },
};

export default function SortDemo() {
  const renderRow = useCallback(({ data, active }) => {
    return <Row data={data} active={active} />;
  }, []);
  return (
    <View style={{ height: 600 }}>
      <SortableList style={styles.list} data={data} renderRow={renderRow} />
    </View>
  );
}

function Row(props) {
  const { active, data } = props;

  const activeAnim = useRef(new Animated.Value(0));
  const style = useMemo(
    () => ({
      ...Platform.select({
        ios: {
          transform: [
            {
              scale: activeAnim.current.interpolate({
                inputRange: [0, 1],
                outputRange: [1, 1.07],
              }),
            },
          ],
          shadowRadius: activeAnim.current.interpolate({
            inputRange: [0, 1],
            outputRange: [2, 10],
          }),
        },

        android: {
          transform: [
            {
              scale: activeAnim.current.interpolate({
                inputRange: [0, 1],
                outputRange: [1, 1.07],
              }),
            },
          ],
          elevation: activeAnim.current.interpolate({
            inputRange: [0, 1],
            outputRange: [2, 6],
          }),
        },
        harmony: {
          transform: [
            {
              scale: activeAnim.current.interpolate({
                inputRange: [0, 1],
                outputRange: [1, 1.07],
              }),
            },
          ],
          elevation: activeAnim.current.interpolate({
            inputRange: [0, 1],
            outputRange: [2, 6],
          }),
        },
      }),
    }),
    []
  );
  useEffect(() => {
    Animated.timing(activeAnim.current, {
      duration: 300,
      easing: Easing.bounce,
      toValue: Number(active),
      useNativeDriver: true,
    }).start();
  }, [active]);

  return (
    <Animated.View style={[styles.row, style]}>
      <Text style={styles.text}>{data.text}</Text>
    </Animated.View>
  );
}

const styles = StyleSheet.create({
  list: {
    flex: 1,
    backgroundColor: "#AAE",
  },
  contentContainer: {
    width: window.width - 100,
    ...Platform.select({
      ios: {
        paddingHorizontal: 30,
      },
      android: {
        paddingHorizontal: 0,
      },
      harmony: {
        paddingHorizontal: 0,
      },
    }),
  },
  row: {
    flexDirection: "row",
    alignItems: "center",
    backgroundColor: "#fff",
    padding: 16,
    height: 80,
    flex: 1,
    marginTop: 10,
    ...Platform.select({
      ios: {
        width: window.width - 60 * 2,
        shadowColor: "rgba(0,0,0,0.2)",
        shadowOpacity: 1,
        shadowOffset: { height: 2, width: 2 },
        shadowRadius: 2,
      },
      android: {
        width: window.width - 60 * 2,
        elevation: 0,
        marginHorizontal: 30,
      },
      harmony: {
        width: window.width - 60 * 2,
        elevation: 0,
        marginHorizontal: 30,
        shadowColor: "rgba(0,0,0,0.2)",
        shadowOpacity: 1,
        shadowOffset: { height: 2, width: 2 },
        shadowRadius: 2,
      },
    }),
  },
  text: {
    fontSize: 18,
    color: "#222222",
  },
});
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-sortabel-list Releases](https://github.com/react-native-oh-library/react-native-sortable-list/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                           | Description                                                                                                                                                                    | **Type**      | Required | Platform | HarmonyOS Support |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------- | -------- | -------- | ----------------- |
| data                           | data source                                                                                                                                                                    | Object        | yes      | All      | Yes               |
| order                          | an array of keys from data, the order of keys from the array will be used to initial rows order                                                                                | Array         | no       | All      | Yes               |
| style                          | View style                                                                                                                                                                     | Object, Array | no       | All      | Yes               |
| contentContainerStyle          | these styles will be applied to the inner scroll view content container                                                                                                        | Object, Array | no       | All      | Yes               |
| innerContainerStyle            | these styles will be applied to the inner scroll view content container, excluding the header and footer                                                                       | Object, Array | no       | All      | Yes               |
| horizontal                     | when true, the SortableList's children are arranged horizontally in a row instead of vertically in a column. The default value is false.                                       | boolean       | no       | All      | Yes               |
| showsVerticalScrollIndicator   | when false, the vertical scroll indicator will not be visible. The default value is true.                                                                                      | boolean       | no       | All      | Yes               |
| showsHorizontalScrollIndicator | when false, the horizontal scroll indicator will not be visible. The default value is true.                                                                                    | boolean       | no       | All      | Yes               |
| sortingEnabled                 | when false, rows are not sortable. The default value is true.                                                                                                                  | boolean       | no       | All      | Yes               |
| scrollEnabled                  | when false, the content does not scrollable. The default value is true.                                                                                                        | boolean       | no       | All      | Yes               |
| keyboardShouldPersistTaps      | Determines when the keyboard should stay visible after a tap. Default 'never'.                                                                                                 | string        | no       | All      | Yes               |
| manuallyActivateRows           | whether you intend to use the toggleRowActive method to activate a row or use the out of box solution.                                                                         | bool          | no       | All      | Yes               |
| autoscrollAreaSize             | determines the height for vertical list and the width for horizontal list of the area at the begining and the end of the list that will trigger autoscrolling. Defaults to 60. | number        | no       | All      | Yes               |
| rowActivationTime              | determines time delay in ms before pressed row becomes active. Defaults to 200 ms.                                                                                             | number        | no       | All      | Yes               |
| refreshControl                 | A RefreshControl that works the same way as a ScrollView's refreshControl.                                                                                                     | element       | no       | All      | Yes               |
| renderRow                      | Takes a row key, row index, data entry from the data source and its statuses disabled, active and should return a renderable component to be rendered as the row.              | function      | yes      | All      | Yes               |
| renderHeader                   | Renders returned component at the top of the list.                                                                                                                             | function      | no       | All      | Yes               |
| renderFooter                   | Renders returned component at the bottom of the list.                                                                                                                          | function      | no       | All      | Yes               |
| onChangeOrder                  | Called when rows were reordered, takes an array of rows keys of the next rows order.                                                                                           | bool          | no       | All      | Yes               |
| onActivateRow                  | Called when a row was activated (user long tapped).                                                                                                                            | function      | no       | All      | Yes               |
| onReleaseRow                   | Called when the active row was released. Returns the key and the new list order.                                                                                               | function      | no       | All      | Yes               |
| onPressRow                     | Called when a row was pressed.                                                                                                                                                 | function      | no       | All      | Yes               |

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name           | Description                                                                 | **Type**       | Required | Platform | HarmonyOS Support |
| -------------- | --------------------------------------------------------------------------- | -------------- | -------- | -------- | ----------------- |
| scrollBy       | scrolls by a given y offset, either immediately or with a smooth animation. | dy?, animated? | no       | All      | Yes               |
| scrollTo       | scrolls to a given y offset, either immediately or with a smooth animation. | y?, animated?  | no       | All      | Yes               |
| scrollToRowKey | scrolls to a given row key, either immediately or with a smooth animation.  | key, animated? | no       | All      | Yes               |

## Known Issues

## Others

## License

This project is licensed under [MIT License](https://github.com/react-native-oh-library/react-native-sortable-list/blob/sig/LICENSE).
