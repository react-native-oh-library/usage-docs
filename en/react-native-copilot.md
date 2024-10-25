> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-copilot</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mohebifar/react-native-copilot">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mohebifar/react-native-copilot/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/mohebifar/react-native-copilot)

## Installation and Usage

<!-- tabs:start -->

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install --save react-native-copilot@3.3.2
```

#### **yarn**

```bash
yarn add react-native-copilot@3.3.2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React, { useEffect, useState } from "react";
import {
  Image,
  SafeAreaView,
  StyleSheet,
  Switch,
  Text,
  TouchableOpacity,
  View,
} from "react-native";
import {
  CopilotProvider,
  CopilotStep,
  walkthroughable,
  useCopilot,
} from "react-native-copilot";

const WalkthroughableText = walkthroughable(Text);
const WalkthroughableImage = walkthroughable(Image);

function App() {
  const { start, copilotEvents } = useCopilot();
  const [secondStepActive, setSecondStepActive] = useState(true);
  const [lastEvent, setLastEvent] = useState(null);

  useEffect(() => {
    copilotEvents.on("stepChange", (step) => {
      setLastEvent(`stepChange: ${step.name}`);
    });
    copilotEvents.on("start", () => {
      setLastEvent(`start`);
    });
    copilotEvents.on("stop", () => {
      setLastEvent(`stop`);
    });
  }, [copilotEvents]);

  return (
    <SafeAreaView style={styles.container}>
      <CopilotStep
        text="Hey! This is the first step of the tour!"
        order={1}
        name="openApp"
      >
        <WalkthroughableText style={styles.title}>
          {'Welcome to the demo of\n"React Native Copilot"'}
        </WalkthroughableText>
      </CopilotStep>
      <View style={styles.middleView}>
        <CopilotStep
          active={secondStepActive}
          text="Here goes your profile picture!"
          order={2}
          name="secondText"
        >
          <WalkthroughableImage
            source={require("../assets/react-native-copilot-man.jpeg")}
            style={styles.profilePhoto}
          />
        </CopilotStep>
        <View style={styles.activeSwitchContainer}>
          <Text>Profile photo step activated?</Text>
          <View style={{ flexGrow: 1 }} />
          <Switch
            onValueChange={(secondStepActive) =>
              setSecondStepActive(secondStepActive)
            }
            value={secondStepActive}
          />
        </View>
        <TouchableOpacity style={styles.button} onPress={() => start()}>
          <Text style={styles.buttonText}>START THE TUTORIAL!</Text>
        </TouchableOpacity>
        <View style={styles.eventContainer}>
          <Text>{lastEvent && `Last event: ${lastEvent}`}</Text>
        </View>
      </View>
      <View style={styles.row}>
        <CopilotStep
          text="Here is an item in the corner of the screen."
          order={3}
          name="thirdText"
        >
          <WalkthroughableText>
            <View style={styles.imageView}>
              <Image
                source={require("../assets/react-native-copilot-nickname.png")}
              />
            </View>
          </WalkthroughableText>
        </CopilotStep>
        <View style={styles.imageView}>
          <Image
            source={require("../assets/react-native-copilot-earphone.png")}
          />
        </View>
        <View style={styles.imageView}>
          <Image source={require("../assets/react-native-copilot-glass.png")} />
        </View>
        <View style={styles.imageView}>
          <Image source={require("../assets/react-native-copilot-scan.png")} />
        </View>
        <View style={styles.imageView}>
          <Image source={require("../assets/react-native-copilot-todo.png")} />
        </View>
      </View>
    </SafeAreaView>
  );
}

const AppwithProvider = () => (
  <CopilotProvider stopOnOutsideClick androidStatusBarVisible>
    <App />
  </CopilotProvider>
);

export default AppwithProvider;

const styles = StyleSheet.create({
  imageView: {
    width: 50,
    height: 50,
    justifyContent: "space-evenly",
    alignItems: "center",
  },
  container: {
    flex: 1,
    backgroundColor: "#fff",
    alignItems: "center",
    paddingTop: 25,
  },
  title: {
    fontSize: 24,
    textAlign: "center",
  },
  profilePhoto: {
    width: 140,
    height: 140,
    borderRadius: 70,
    marginVertical: 20,
  },
  middleView: {
    flex: 1,
    alignItems: "center",
  },
  button: {
    backgroundColor: "#2980b9",
    paddingVertical: 10,
    paddingHorizontal: 15,
  },
  buttonText: {
    color: "white",
    fontSize: 16,
  },
  row: {
    flexDirection: "row",
    alignItems: "center",
    justifyContent: "space-between",
  },
  tabItem: {
    flex: 1,
    textAlign: "center",
  },
  activeSwitchContainer: {
    flexDirection: "row",
    justifyContent: "space-between",
    marginBottom: 20,
    alignItems: "center",
    paddingHorizontal: 25,
  },
  eventContainer: {
    marginTop: 20,
  },
});
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-svg](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-svg-capi.md#link) to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

For details, see [react-native-copilot](https://github.com/mohebifar/react-native-copilot/blob/master/README.md) 的文档介绍

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name            | Description                       | Type         | Required | Platform    | HarmonyOS Support |
| --------------- | --------------------------------- | ------------ | -------- | ----------- | ----------------- |
| CopilotProps    | Prompt Style Properties           | CopilotProps | no       | Android/iOS | partially         |
| TooltipProps    | Prompt Tool Properties            | TooltipProps | no       | Android/iOS | yes               |
| CopilotProvider | Custom Tooltip Styles             | function     | no       | Android/iOS | yes               |
| CopilotStep     | Customizing Component Step Styles | function     | no       | Android/iOS | yes               |
| DefaultUI       | Default UI Attributes             | object       | no       | Android/iOS | yes               |
| useCopilot      | Use Prompt Style                  | function     | no       | Android/iOS | yes               |
| walkthroughable | Wrappable Components              | function     | no       | Android/iOS | yes               |

### CopilotProps

| Name                    | Description                   | Type                                                                    | Required | Platform    | HarmonyOS Support |
| ----------------------- | ----------------------------- | ----------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| easing                  | The animation display will be smoother            | ((value: number) => number) \| undefined                                | no       | Android/iOS | yes               |
| overlay                 | Use SVG or View to execute animations | "svg" \| "view"                                                         | no       | Android/iOS | yes               |
| animationDuration       | Animation execution time                  | number                                                                  | no       | Android/iOS | yes               |
| tooltipComponent        | 可自定义 tooltip 组件         | React.ComponentType\<TooltipProps\>                                     | no       | Android/iOS | yes               |
| tooltipStyle            | Customizable tooltip components                | ViewStyle                                                               | no       | Android/iOS | yes               |
| stepNumberComponent     | Customizable step component            | React.ComponentType\<any\>                                              | no       | Android/iOS | yes               |
| animated                | Do you want to enable animation                  | boolean                                                                 | no       | Android/iOS | yes               |
| labels                  | Text of step button                | Partial\<Record\<"skip" \| "previous" \| "next" \| "finish", string\>\> | no       | Android/iOS | yes               |
| androidStatusBarVisible | Show or hide the StatusBar          | boolean                                                                 | no       | Android     | no                |
| svgMaskPath             | Custom Modal Box                  | Function                                                                | no       | Android/iOS | yes               |
| verticalOffset          | The offset of the modal box distance element        | number                                                                  | no       | Android/iOS | yes               |
| arrowColor              | The color of the arrow                    | string                                                                  | no       | Android/iOS | yes               |
| arrowSize               | The position of the arrow                    | number                                                                  | no       | Android/iOS | yes               |
| margin                  | The distance between two modal boxes            | number                                                                  | no       | Android/iOS | yes               |
| stopOnOutsideClick      | Call stop when clicking on the mask           | boolean                                                                 | no       | Android/iOS | yes               |
| backdropColor           | The color of the external background                    | string                                                                  | no       | Android/iOS | yes               |

### TooltipProps

| Name         | Description    | Type                                                                    | Required | Platform    | HarmonyOS Support |
| ------------ | -------------- | ----------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| TooltipProps | Text of step button | Partial\<Record\<"skip" \| "previous" \| "next" \| "finish", string\>\> | no       | Android/iOS | yes               |

## Known Issues

## Others
- The androidStatusBarVisible property is invalid on HarmonyOS. This property is used to calculate the position of the modal box even after hiding the Status Bar on Android. However, when HarmonyOS hides the Status Bar, its height is 0, so this property is invalid on HarmonyOS.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mohebifar/react-native-copilot/blob/master/LICENSE).
