> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@ptomasroos/react-native-multi-slider</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ptomasroos/react-native-multi-slider">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|web|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ptomasroos/react-native-multi-slider/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-multi-slider)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-multi-slider Releases](https://github.com/react-native-oh-library/react-native-multi-slider/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-multi-slider
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-multi-slider
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";

import {
  StyleSheet,
  View,
  Text,
  ScrollView,
  Alert,
  Animated,
  Image,
} from "react-native";
import MultiSlider from "@ptomasroos/react-native-multi-slider";

const AnimatedView = Animated.createAnimatedComponent(View);

CustomLabel.defaultProps = {
  leftDiff: 0,
};

const width = 50;
const pointerWidth = width * 0.47;

function LabelBase(props: any) {
  const { position, value, leftDiff, pressed } = props;
  const scaleValue = React.useRef(new Animated.Value(0.1)); // Behaves oddly if set to 0
  const cachedPressed = React.useRef(pressed);

  React.useEffect(() => {
    Animated.timing(scaleValue.current, {
      toValue: pressed ? 1 : 0.1,
      duration: 200,
      delay: pressed ? 0 : 2000,
      useNativeDriver: false,
    }).start();
    cachedPressed.current = pressed;
  }, [pressed]);

  return (
    Number.isFinite(position) &&
    Number.isFinite(value) && (
      <AnimatedView
        style={[
          labelStyles.sliderLabel,
          {
            left: position - width / 2,
            transform: [
              { translateY: width },
              { scale: scaleValue.current },
              { translateY: -width },
            ],
          },
        ]}
      >
        <View style={labelStyles.pointer} />
        <Text style={labelStyles.sliderLabelText}>{value}</Text>
      </AnimatedView>
    )
  );
}

function CustomLabel(props: any) {
  const {
    leftDiff,
    oneMarkerValue,
    twoMarkerValue,
    oneMarkerLeftPosition,
    twoMarkerLeftPosition,
    oneMarkerPressed,
    twoMarkerPressed,
  } = props;

  return (
    <View style={labelStyles.parentView}>
      <LabelBase
        position={oneMarkerLeftPosition}
        value={oneMarkerValue}
        leftDiff={leftDiff}
        pressed={oneMarkerPressed}
      />
      <LabelBase
        position={twoMarkerLeftPosition}
        value={twoMarkerValue}
        leftDiff={leftDiff}
        pressed={twoMarkerPressed}
      />
    </View>
  );
}

class CustomMarker extends React.Component<any> {
  render() {
    return (
      <View>
        <Text style={markerStyles.text}>
          {this.props.valuePrefix}
          {this.props.currentValue}
        </Text>
        <Image
          style={markerStyles.image}
          source={
            this.props.pressed
              ? require("./ruby.png")
              : require("./diamond.png")
          }
          resizeMode="contain"
        />
        <Text style={markerStyles.text}>
          {this.props.valuePrefix}
          {this.props.currentValue}
          {this.props.valueSuffix}
        </Text>
      </View>
    );
  }
}

export default function MultiSliderDemo() {
  let testRef = React.useRef < View > null;
  let [currentTestId, setCurrentTestId] = React.useState("");

  const touchDimensionsConfig = {
    height: 60,
    width: 60,
    borderRadius: 10,
    slipDisplacement: 200,
  };

  const onValuesChangeStart = () =>
    Alert.alert("Success", "Callback when the value starts to change");

  const onValuesChange = () =>
    Alert.alert("Success", "Callback when value changes");

  const onValuesChangeFinish = () =>
    Alert.alert("Success", "Callback when the value stops changing");

  const onToggleOne = () =>
    Alert.alert("Success", "The first cursor switch callback");

  const onToggleTwo = () =>
    Alert.alert("Success", "Second cursor switch callback");

  const getCurrentTestId = () => {
    const testId = testRef.current?.props.testID || "";
    setCurrentTestId(testId);
  };

  return (
    <ScrollView>
      <View style={styles.container}>
        <Text style={styles.title}>MultiSlider feature validation</Text>
        <View style={styles.sliders}>
          <Text style={styles.text}>Values (set values, 1 and 6)</Text>
          <MultiSlider values={[1, 6]} />

          <Text style={styles.text}>
            OnValuesChangeStart (triggering callback when value starts to
            change)
          </Text>
          <MultiSlider onValuesChangeStart={onValuesChangeStart} />

          <Text style={styles.text}>
            OnValuesChange (callback triggered when value changes)
          </Text>
          <MultiSlider onValuesChange={onValuesChange} />

          <Text style={styles.text}>
            OnValuesChangeFinish (callback when value stops changing)
          </Text>
          <MultiSlider onValuesChangeFinish={onValuesChangeFinish} />

          <Text style={styles.text}>sliderLength（Slide length{100}）</Text>
          <MultiSlider sliderLength={100} />

          <Text style={styles.text}>
            TouchDimensions (sliding indicator borderRadius 50)
          </Text>
          <MultiSlider touchDimensions={touchDimensionsConfig} />

          <Text style={styles.text}>EnableLabel (enable custom labels)</Text>
          <MultiSlider enableLabel customLabel={() => <CustomLabel />} />

          <Text style={styles.text}>CustomMarker (custom cursor)</Text>
          <MultiSlider customMarker={CustomMarker} />

          <Text style={styles.text}>customMarkerLeft/Right</Text>
          <Text style={styles.text}>
            Custom left and right cursor: not enabled by default
          </Text>
          <MultiSlider
            values={[0, 10]}
            customMarkerLeft={() => <CustomMarker />}
            customMarkerRight={() => <CustomMarker pressed />}
          />

          <Text style={styles.text}>isMarkersSeparated</Text>
          <Text style={styles.text}>
            Customize left and right cursor: Enable
          </Text>
          <MultiSlider
            values={[0, 10]}
            isMarkersSeparated={true}
            customMarkerLeft={() => <CustomMarker />}
            customMarkerRight={() => <CustomMarker pressed />}
          />

          <Text style={styles.text}>
            Min (slider can use a minimum value of 3)
          </Text>
          <MultiSlider enableLabel min={3} />

          <Text style={styles.text}>
            Max (maximum available slider value of 8)
          </Text>
          <MultiSlider enableLabel max={8} />

          <Text style={styles.text}>Step (slider step size 5)</Text>
          <MultiSlider enableLabel step={5} />

          <Text style={styles.text}>OptionsArray (Node Tag)</Text>
          <MultiSlider enableLabel optionsArray={[2, 6, 9]} />

          <Text style={styles.text}>
            ContainerStyle (slider container style)
          </Text>
          <MultiSlider
            containerStyle={{ backgroundColor: "lightblue", padding: 10 }}
          />

          <Text style={styles.text}>TrackStyle (default track style)</Text>
          <MultiSlider trackStyle={{ backgroundColor: "red", height: 5 }} />

          <Text style={styles.text}>
            SelectedStyle (track style: after sliding)
          </Text>
          <MultiSlider
            selectedStyle={{ backgroundColor: "green", height: 5 }}
          />

          <Text style={styles.text}>
            UnselectdStyle (track style: not slid over)
          </Text>
          <MultiSlider
            unselectedStyle={{ backgroundColor: "red", height: 5 }}
          />

          <Text style={styles.text}>
            MarkerContainerStyle (cursor container style)
          </Text>
          <MultiSlider
            markerContainerStyle={{
              backgroundColor: "transparent",
              borderColor: "blue",
              borderWidth: 2,
            }}
          />

          <Text style={styles.text}>MarkerStyle (cursor style)</Text>
          <MultiSlider
            markerStyle={{
              backgroundColor: "red",
              width: 20,
              height: 20,
              borderRadius: 10,
            }}
          />

          <Text style={styles.text}>
            PressedMarkerStyle (the style after touching the cursor)
          </Text>
          <MultiSlider pressedMarkerStyle={{ backgroundColor: "darkblue" }} />

          <Text style={styles.text}>Valueprefix (value prefix b)</Text>
          <MultiSlider
            values={[0, 10]}
            customMarker={CustomMarker}
            valuePrefix="b"
          />

          <Text style={{ ...styles.text, marginTop: 20 }}>
            ValueSuffix (suffix a for values)
          </Text>
          <MultiSlider
            values={[0, 10]}
            customMarker={CustomMarker}
            valueSuffix="a"
          />

          <Text style={styles.text}>EnabledOne (disable the first cursor)</Text>
          <MultiSlider values={[0, 10]} enabledOne={false} />

          <Text style={styles.text}>
            EnabledTwo (disable the second cursor)
          </Text>
          <MultiSlider values={[0, 10]} enabledTwo={false} />

          <Text style={styles.text}>stepsAs</Text>
          <Text style={styles.text}>
            Customize step labels, default display
          </Text>
          <MultiSlider
            values={[0, 10]}
            step={2}
            showSteps
            stepsAs={[
              { index: 1, stepLabel: "t1", prefix: "a1", suffix: "b1" },
              { index: 2, stepLabel: "t2", prefix: "a2", suffix: "b2" },
            ]}
          />

          <Text style={styles.text}>showStepLabels</Text>
          <Text style={styles.text}>Hide/Show Custom Step Tags, Hide Here</Text>
          <MultiSlider
            values={[0, 10]}
            step={2}
            showSteps
            showStepLabels={false}
            stepsAs={[
              { index: 1, stepLabel: "t", prefix: "a", suffix: "b" },
              { index: 2, stepLabel: "t", prefix: "a", suffix: "b" },
            ]}
          />

          <Text style={styles.text}>
            ShowStepMarkers (display the scale points corresponding to the
            steps)
          </Text>
          <MultiSlider values={[0, 10]} step={2} showSteps showStepMarkers />

          <Text style={styles.text}>onToggleOne</Text>
          <Text style={styles.text}>
            Click on the first cursor to call back
          </Text>
          <MultiSlider values={[0, 10]} onToggleOne={onToggleOne} />

          <Text style={styles.text}>onToggleTwo</Text>
          <Text style={styles.text}>
            Click on the second cursor to call back
          </Text>
          <MultiSlider values={[0, 10]} onToggleTwo={onToggleTwo} />

          <Text style={styles.text}>allowOverlap</Text>
          <Text style={styles.text}>
            Allow/prohibit cursor overlap, default prohibited, allowed here
          </Text>
          <MultiSlider values={[0, 10]} enableLabel allowOverlap={true} />

          <Text style={styles.text}>Snapped (Step by Step Moving cursor)</Text>
          <MultiSlider sliderLength={300} step={3} snapped />

          <Text style={styles.text}>SmoothSnapped (jump to nearest node)</Text>
          <MultiSlider smoothSnapped sliderLength={300} step={3} />

          <View style={{ marginTop: 60, marginBottom: 150 }}>
            <Text style={styles.text}>Vertical (vertical direction)</Text>
            <MultiSlider vertical />
          </View>

          <Text style={styles.text}>MarkerOffsetX (lateral offset of 20)</Text>
          <MultiSlider markerOffsetX={20} />

          <Text style={styles.text}>MarkerOffsetY (vertical offset of 20)</Text>
          <MultiSlider markerOffsetY={20} />

          <Text style={styles.text}>
            MarkerSize (distance between cursor and edge)
          </Text>
          <MultiSlider markerSize={50} />

          <Text style={styles.text}>minMarkerOverlapDistance</Text>
          <Text style={styles.text}>
            Avoid large cursor overlap, with an interval of 100
          </Text>
          <MultiSlider values={[0, 10]} minMarkerOverlapDistance={100} />

          <Text style={styles.text}>minMarkerOverlapStepDistance</Text>
          <Text style={styles.text}>
            Avoid overlapping large cursor with an interval of 2 steps
          </Text>
          <MultiSlider
            values={[0, 300]}
            step={3}
            allowOverlap={false}
            smoothSnapped
            minMarkerOverlapStepDistance={2}
          />

          <Text style={styles.text}>ImageContextSource (Background Image)</Text>
          <MultiSlider imageBackgroundSource={require("./logo-og.png")} />

          <Text style={styles.text}>TestID (Set testID)</Text>
          <MultiSlider values={[0, 6]} testID={"666"} ref={testRef} />
          <Text onPress={getCurrentTestId}>
            {currentTestId || "Click to obtain testID"}
          </Text>
        </View>
      </View>
    </ScrollView>
  );
}

const labelStyles = StyleSheet.create({
  parentView: {
    position: "relative",
  },
  sliderLabel: {
    position: "absolute",
    justifyContent: "center",
    bottom: "100%",
    width: width,
    height: width,
  },
  sliderLabelText: {
    textAlign: "center",
    lineHeight: width,
    borderRadius: width / 2,
    borderWidth: 2,
    borderColor: "#999",
    backgroundColor: "#fff",
    flex: 1,
    fontSize: 18,
    color: "#aaa",
  },
  pointer: {
    position: "absolute",
    bottom: -pointerWidth / 4,
    left: (width - pointerWidth) / 2,
    transform: [{ rotate: "45deg" }],
    width: pointerWidth,
    height: pointerWidth,
    backgroundColor: "#999",
  },
});

const markerStyles = StyleSheet.create({
  image: {
    height: 40,
    width: 40,
  },
  text: {
    alignSelf: "center",
    paddingVertical: 20,
  },
  title: {
    fontSize: 30,
  },
});

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: "column",
    justifyContent: "center",
    alignItems: "center",
  },
  sliders: {
    margin: 20,
    // width: 280,
  },
  text: {
    alignSelf: "center",
    paddingVertical: 20,
  },
  title: {
    fontSize: 30,
  },
  sliderOne: {
    flexDirection: "row",
    justifyContent: "space-around",
  },
});
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-multi-slider Releases](https://github.com/react-native-oh-library/react-native-multi-slider/releases)

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.Known Issues

| Name                         | Description                                                                                                                                                                                                                                                                                                                                                                            | Type              | Required | Platform | HarmonyOS Support |
| ---------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | -------- | -------- | ----------------- |
| values                       | Prefixed values of the slider.                                                                                                                                                                                                                                                                                                                                                         | array of numbers  | NO       | All      | YES               |
| onValuesChangeStart          | Callback when the value starts changing                                                                                                                                                                                                                                                                                                                                                | function          | NO       | All      | YES               |
| onValuesChange               | Callback when the value changes                                                                                                                                                                                                                                                                                                                                                        | function          | NO       | All      | YES               |
| onValuesChangeFinish         | Callback when the value stops changing                                                                                                                                                                                                                                                                                                                                                 | function          | NO       | All      | YES               |
| sliderLength                 | Length of the slider                                                                                                                                                                                                                                                                                                                                                                   | number            | NO       | All      | YES               |
| touchDimensions              | Defines the size of the touch area of the slider                                                                                                                                                                                                                                                                                                                                       | object            | NO       | All      | YES               |
| enableLabel                  | Enable the label rendering                                                                                                                                                                                                                                                                                                                                                             | function          | NO       | All      | YES               |
| customLabel                  | Component used for rendering a label above the cursors.                                                                                                                                                                                                                                                                                                                                | function          | NO       | All      | YES               |
| customMarker                 | Component used for the cursor.                                                                                                                                                                                                                                                                                                                                                         | function          | NO       | All      | YES               |
| customMarkerLeft             | Component used for the left cursor.                                                                                                                                                                                                                                                                                                                                                    | function          | NO       | All      | YES               |
| customMarkerRight            | Component used for the right cursor.                                                                                                                                                                                                                                                                                                                                                   | function          | NO       | All      | YES               |
| isMarkersSeparated           | Enable custom left and right cursors                                                                                                                                                                                                                                                                                                                                                   | boolean           | NO       | All      | YES               |
| min                          | Minimum value available in the slider.                                                                                                                                                                                                                                                                                                                                                 | number            | NO       | All      | YES               |
| max                          | Maximum value available in the slider.                                                                                                                                                                                                                                                                                                                                                 | number            | NO       | All      | YES               |
| step                         | Step value of the slider.                                                                                                                                                                                                                                                                                                                                                              | number            | NO       | All      | YES               |
| optionsArray                 | Possible values of the slider. Ignores min and max.                                                                                                                                                                                                                                                                                                                                    | array of numbers  | NO       | All      | YES               |
| containerStyle               | The style of the slider container                                                                                                                                                                                                                                                                                                                                                      | style object      | NO       | All      | YES               |
| trackStyle                   | track Default Style                                                                                                                                                                                                                                                                                                                                                                    | style object      | NO       | All      | YES               |
| selectedStyle                | Style after track sliding                                                                                                                                                                                                                                                                                                                                                              | style object      | NO       | All      | YES               |
| unselectedStyle              | Style when the track is not sliding                                                                                                                                                                                                                                                                                                                                                    | style object      | NO       | All      | YES               |
| markerContainerStyle         | Marker container style                                                                                                                                                                                                                                                                                                                                                                 | style object      | NO       | All      | YES               |
| markerStyle                  | Marker style                                                                                                                                                                                                                                                                                                                                                                           | style object      | NO       | All      | YES               |
| pressedMarkerStyle           | Marker style after touch                                                                                                                                                                                                                                                                                                                                                               | style object      | NO       | All      | YES               |
| stepStyle                    | Step style                                                                                                                                                                                                                                                                                                                                                                             | style object      | NO       | -        | YES               |
| stepLabelStyle               | Step lable style                                                                                                                                                                                                                                                                                                                                                                       | style object      | NO       | -        | YES               |
| stepMarkerStyle              | Step marker style                                                                                                                                                                                                                                                                                                                                                                      | style object      | NO       | -        | YES               |
| valuePrefix                  | Prefix added to the value.                                                                                                                                                                                                                                                                                                                                                             | string            | NO       | All      | YES               |
| valueSuffix                  | Suffix added to the value.                                                                                                                                                                                                                                                                                                                                                             | string            | NO       | All      | YES               |
| enabledOne                   | Enables the first cursor                                                                                                                                                                                                                                                                                                                                                               | boolean           | NO       | All      | YES               |
| enabledTwo                   | Enables the second cursor                                                                                                                                                                                                                                                                                                                                                              | boolean           | NO       | All      | YES               |
| stepsAs                      | Use stepsAs when you want to customize the steps-labels. stepsAs expects an array of objects [{index: number, stepLabel: string, prefix: string, suffix: string}]. Where index is for which step you want to customize, and all the other steps will show its index as its stepLabel. Both showSteps and showStepsLabels has to be enabled for stepsAs to be used.                     | array of objects  | NO       | All      | YES               |
| showSteps                    | Show steps                                                                                                                                                                                                                                                                                                                                                                             | boolean           | NO       | All      | YES               |
| showStepMarkers              | Show steps-markers on the track, showSteps has to be enabled as well                                                                                                                                                                                                                                                                                                                   | boolean           | NO       | All      | YES               |
| showStepLabels               | Show steps-labels underneath the track, showSteps has to be enabled as well                                                                                                                                                                                                                                                                                                            | boolean           | NO       | All      | YES               |
| onToggleOne                  | Listener when first cursor toggles.                                                                                                                                                                                                                                                                                                                                                    | function callback | NO       | All      | YES               |
| onToggleTwo                  | Listener when second cursor toggles.                                                                                                                                                                                                                                                                                                                                                   | function callback | NO       | All      | YES               |
| allowOverlap                 | Allow the overlap within the cursors.                                                                                                                                                                                                                                                                                                                                                  | boolean           | NO       | All      | YES               |
| snapped                      | Use this when you want a fixed position for your markers, this will split the slider in N specific positions                                                                                                                                                                                                                                                                           | boolean           | NO       | All      | YES               |
| smoothSnapped                | Same as snapped but you can move the slider as usual. When released it will go to the nearest marker                                                                                                                                                                                                                                                                                   | boolean           | NO       | All      | YES               |
| vertical                     | Use vertical orientation instead of horizontal.                                                                                                                                                                                                                                                                                                                                        | boolean           | NO       | All      | YES               |
| markerOffsetX                | Offset first cursor.                                                                                                                                                                                                                                                                                                                                                                   | number            | NO       | All      | YES               |
| markerOffsetY                | Offset second cursor.                                                                                                                                                                                                                                                                                                                                                                  | number            | NO       | All      | YES               |
| markerSize                   | It determines the marker margin from the edges of the track, useful to avoid the markers to overflow out of the track.                                                                                                                                                                                                                                                                 | number            | NO       | All      | YES               |
| minMarkerOverlapDistance     | if this is > 0 and allowOverlap is false, this value will determine the closest two markers can come to each other. This can be used for cases where you have two markers large cursors and you don't want them to overlap. Note that markers will still overlap at the start if starting values are too near.                                                                         | number            | NO       | All      | YES               |
| minMarkerOverlapStepDistance | if this is > 0 and allowOverlap is false, this value will determine the closest two markers can come to each other (in steps, not pixels). This can be used for cases where you have two markers large cursors and you don't want them to overlap. Note that markers will still overlap at the start if starting values are too near. CANNOT be combined with minMarkerOverlapDistance | number            | NO       | All      | YES               |
| imageBackgroundSource        | Specifies the source required for the ImageBackground                                                                                                                                                                                                                                                                                                                                  | string            | NO       | All      | YES               |
| testID                       | Used to locate this view in end-to-end tests                                                                                                                                                                                                                                                                                                                                           | string            | NO       | All      | YES               |

## Known Issues

## Others

## License

This project is licensed under[The MIT License (MIT)](https://github.com/ptomasroos/react-native-multi-slider/blob/master/LICENSE)，请自由地享受和参与开源。
