> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-navigation-shared-element</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/IjzerenHein/react-navigation-shared-element">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/IjzerenHein/react-navigation-shared-element/blob/main/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/IjzerenHein/react-navigation-shared-element)


## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-navigation-shared-element@3.1.2 
npm install react-native-shared-element@0.8.9
```

#### **yarn**

```bash
yarn add react-navigation-shared-element@3.1.2 
yarn add react-native-shared-element@0.8.9 
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```js
import  React, { Component } from "react";
import {
  View,
  StyleSheet,
  Animated,
  Dimensions,
  TouchableOpacity,
  Button
} from "react-native";
import {
  SharedElement,
  SharedElementTransition,
  nodeFromRef,
} from "react-native-shared-element";

export class Rativesharedelement extends Component {
  state = {
    progress: new Animated.Value(0),
    isScene2Visible: false,
    isInProgress: false,
    scene1Ancestor: null,
    scene1Node: null,
    scene2Ancestor: null,
    scene2Node: null,
  };

  onPressNavigate = () => {
    this.setState({ isScene2Visible: true, isInProgress: true });
    Animated.timing(this.state.progress, {
      toValue: 1,
      duration: 1000,
      useNativeDriver: true,
    }).start(() => this.setState({ isInProgress: false }));
  };

  onPressBack = () => {
    this.setState({ isInProgress: true });
    Animated.timing(this.state.progress, {
      toValue: 0,
      duration: 1000,
      useNativeDriver: true,
    }).start(() =>
      this.setState({ isScene2Visible: false, isInProgress: false })
    );
  };

  onSetScene1Ref = (ref: View | null) => {
    this.setState({ scene1Ancestor: nodeFromRef(ref) });
  };

  onSetScene2Ref = (ref: View | null) => {
    this.setState({ scene2Ancestor: nodeFromRef(ref) });
  };

  render() {
    const { state } = this;
    const { width } = Dimensions.get("window");
    return (
      <>
        <TouchableOpacity
          style={styles.container}
          activeOpacity={0.5}
          onPress={
            state.isScene2Visible ? this.onPressBack : this.onPressNavigate
          }
        >

          <Animated.View
            style={{
              ...StyleSheet.absoluteFillObject,
              transform: [
                { translateX: Animated.multiply(-200, state.progress) },
              ],
            }}
          >
            <View style={styles.scene} ref={this.onSetScene1Ref}>
              <SharedElement
                onNode={(node) => this.setState({ scene1Node: node })}
              >
                <Button title="page1" color="#39b362" />
              </SharedElement>
            </View>
          </Animated.View>

          {state.isScene2Visible ? (
            <Animated.View
              style={{
                ...StyleSheet.absoluteFillObject,
                transform: [
                  {
                    translateX: Animated.multiply(
                      -width,
                      Animated.add(state.progress, -1)
                    ),
                  },
                ],
              }}
            >
              <View style={styles.scene2} ref={this.onSetScene2Ref}>
                <SharedElement
                  onNode={(node) => this.setState({ scene2Node: node })}
                >
                  <Button title="page2" color="#841584" />
                </SharedElement>
              </View>
            </Animated.View>
          ) : undefined}
        </TouchableOpacity>

        {state.isInProgress ? (
          <View style={styles.sharedElementOverlay} pointerEvents="none">
            <SharedElementTransition
              start={{
                node: state.scene1Node,
                ancestor: state.scene1Ancestor,
              }}
              end={{
                node: state.scene2Node,
                ancestor: state.scene2Ancestor,
              }}
              position={state.progress}
              animation="move"
              resize="auto"
              align="auto"
            />
          </View>
        ) : undefined}
      </>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#ecf0f1",
  },
  scene: {
    ...StyleSheet.absoluteFillObject,
    backgroundColor: "white",
    justifyContent: "center",
    alignItems: "center",
  },
  scene2: {
    ...StyleSheet.absoluteFillObject,
    backgroundColor: "#00d8ff",
    justifyContent: "center",
    alignItems: "center",
  },
  image1: {
    resizeMode: "cover",
    width: 160,
    height: 160,
  },
  image2: {
    resizeMode: "cover",
    width: 300,
    height: 300,
    borderRadius: 0,
  },
  sharedElementOverlay: {
    ...StyleSheet.absoluteFillObject,
  }
});

```
## Constraints

### Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-safe-area-context. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in @react-native-oh-tpl/react-native-safe-area-context to add it to your project.

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.26; SDK：HarmonyOS-NEXT-Developer-Beta1 5.0.0.22；IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.25;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**SharedElement**

| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `children`  |A single child component, which must map to a real view in the native view hierarchy. |  element | no     | All  | yes      |
| `onNode`  | Event handler that sets or unsets the node-handle. | function |  no     | All   | yes      |

**SharedElementTransition**
| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `start`  | Start node- and ancestor. |  node: SharedElementNode, ancestor: SharedElementNode  | no     | All  | yes      |
| `end`  | End node- and ancestor. |node: SharedElementNode, ancestor: SharedElementNode |  no     | All   | yes      |
| `position`  |Interpolated position (0..1), between the start- and end nodes| number or Animated.Value or Reanimated.Value | no     | All | yes      |
| `animation`  | Type of animation, e.g move start element or cross-fade between start- and end elements (default = move).| move or fade or fade-in or fade-out  |  no     | All   | yes      |
| `resize`  | 	Resize behavior (default = auto).| 	auto or stretch or clip or none   |  no     | All   | yes      |
| `align`  | 	Align behavior of the transition (default = auto).| 	auto or top-left    |  no     | All   | yes      |
| `debug`  | 	Renders debug overlays for diagnosing measuring and animations.| 	boolean |  no     | All   | yes      |
| `onMeasure`  | Event handler that is called when nodes have been measured and snapshotted.| function |  no     | All   | yes      |


## Known Issues

## Others

## License
This project is licensed under [The MIT License (MIT)](https://github.com/IjzerenHein/react-navigation-shared-element/blob/main/LICENSE.md).