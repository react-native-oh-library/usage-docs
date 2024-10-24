<!-- {% raw %} -->

> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-switch</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/shahen94/react-native-switch">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/shahen94/react-native-switch/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/shahen94/react-native-switch)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install --save react-native-switch@1.5.1
```

#### **yarn**

```bash
yarn add react-native-switch@1.5.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import { Switch } from "react-native-switch";
import {
  SafeAreaView,
  StyleSheet,
  Button,
  Text,
  View,
  Alert,
} from "react-native";

export function SwitchDemo() {
  const [isEnabled, setIsEnabled] = useState(false);
  const toggleSwitch = (val: boolean) => {
    setIsEnabled(val);
  };

  return (
    <View style={styles.container}>
      <Text style={{ fontSize: 32 }}>Welcome to React Native !</Text>
      <Switch
        value={isEnabled}
        onValueChange={(val) => toggleSwitch(val)}
        disabled={false}
        activeText={"On"}
        inActiveText={"Off"}
        circleSize={30}
        barHeight={30}
        circleBorderWidth={3}
        backgroundActive={"green"}
        backgroundInactive={"gray"}
        circleActiveColor={"#30a566"}
        circleInActiveColor={"#fff"}
        renderInsideCircle={() => ""} // custom component to render inside the Switch circle (Text, Image, etc.)
        changeValueImmediately={true} // if rendering inside circle, change state immediately or wait for animation to complete
        innerCircleStyle={{ alignItems: "center", justifyContent: "center" }} // style for inner animated circle for what you (may) be rendering inside the circle
        outerCircleStyle={{}} // style for outer animated circle
        renderActiveText={true}
        renderInActiveText={true}
        switchLeftPx={2} // denominator for logic when sliding to TRUE position. Higher number = more space from RIGHT of the circle to END of the slider
        switchRightPx={2} // denominator for logic when sliding to FALSE position. Higher number = more space from LEFT of the circle to BEGINNING of the slider
        switchWidthMultiplier={3} // multiplied by the `circleSize` prop to calculate total width of the Switch
        switchBorderRadius={50} // Sets the border Radius of the switch slider. If unset, it remains the circleSize.
      />
      <Text style={{ color: "gray", fontSize: 20, marginBottom: 10 }}>
        To get started,edit index.harmony.js
      </Text>
      <Text style={{ color: "gray", fontSize: 20 }}>
        Press Cmd +R to reload,
      </Text>
      <Text style={{ color: "gray", fontSize: 20 }}>
        Cmd+D or shake for dev menu
      </Text>
    </View>
  );
}
const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
    backgroundColor: "#fff",
  },
});
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|           Name            |                                                             Description                                                             |          Type           | Required |  Platform   | HarmonyOS Support |
| :-----------------------: | :---------------------------------------------------------------------------------------------------------------------------------: | :---------------------: | :------: | :---------: | :---------------: |
|       onValueChange       |                                               when to change value(value: `boolean`)                                                |        function         |    No    | Android/IOS |        Yes        |
|         disabled          |                                                           Display or not                                                            |         boolean         |    No    | Android/IOS |        Yes        |
|        activeText         |                                                             active text                                                             |         string          |    No    | Android/IOS |        Yes        |
|       inActiveText        |                                                           in Active Text                                                            |         string          |    No    | Android/IOS |        Yes        |
|     backgroundActive      |                                                          background active                                                          |         string          |    No    | Android/IOS |        Yes        |
|    backgroundInactive     |                                                        background in active                                                         |         string          |    No    | Android/IOS |        Yes        |
|           value           |                                                            swtich value                                                             |         boolean         |    No    | Android/IOS |        Yes        |
|     circleActiveColor     |                                                         circle active color                                                         |         string          |    No    | Android/IOS |        Yes        |
|    circleInActiveColor    |                                                       circle in active color                                                        |         string          |    No    | Android/IOS |        Yes        |
|        circleSize         |                                                             circle Size                                                             |         number          |    No    | Android/IOS |        Yes        |
|     circleBorderWidth     |                                                         circle Border Width                                                         |        function         |    No    | Android/IOS |        Yes        |
|  circleBorderactiveColor  |                                                     circle Border Active Color                                                      |        function         |    No    | Android/IOS |        Yes        |
| circleBorderInactiveColor |                                                    circle Border Inactive Color                                                     |         boolean         |    No    | Android/IOS |        Yes        |
|      activeTextStyle      |                                                          active Text Style                                                          | StyleProp`<TextStyle> ` |    No    | Android/IOS |        Yes        |
|     inactiveTextStyle     |                                                        in Active Text Style.                                                        | StyleProp`<TextStyle> ` |    No    | Android/IOS |        Yes        |
|      containerStyle       |                                                           container Style                                                           | StyleProp`<TextStyle> ` |    No    | Android/IOS |        Yes        |
|         barHeight         |                                                             Bar Height                                                              |         number          |    No    | Android/IOS |        Yes        |
|     circleBorderWidth     |                                                         circle Border Width                                                         |         number          |    No    | Android/IOS |        Yes        |
|    renderInsideCircle     |                               custom component to render inside the Switch circle (Text, Image, etc.)                               |        function         |    No    | Android/IOS |        Yes        |
|  changeValueImmediately   |                       if rendering inside circle, change state immediately or wait for animation to complete                        |         boolean         |    No    | Android/IOS |        Yes        |
|     innerCircleStyle      |                          style for inner animated circle for what you (may) be rendering inside the circle                          | StyleProp`<TextStyle> ` |    No    | Android/IOS |        Yes        |
|     outerCircleStyle      |                                                   style for outer animated circle                                                   | StyleProp`<TextStyle> ` |    No    | Android/IOS |        Yes        |
|     renderActiveText      |                                                         render Active Text                                                          |         boolean         |    No    | Android/IOS |        Yes        |
|    renderInActiveText     |                                                        render In Active Text                                                        |         boolean         |    No    | Android/IOS |        Yes        |
|       switchLeftPx        |    denominator for logic when sliding to TRUE position. Higher number = more space from RIGHT of the circle to END of the slider    |         number          |    No    | Android/IOS |        Yes        |
|       switchRightPx       | denominator for logic when sliding to FALSE position. Higher number = more space from LEFT of the circle to BEGINNING of the slider |         number          |    No    | Android/IOS |        Yes        |
|   switchWidthMultiplier   |                             multiplied by the `circleSize` prop to calculate total width of the Switch                              |         number          |    No    | Android/IOS |        Yes        |
|    switchBorderRadius     |                          Sets the border Radius of the switch slider. If unset, it remains the circleSize.                          |         number          |    No    | Android/IOS |        Yes        |
|          testID           |                                                           swtich test ID                                                            |         string          |    No    | Android/IOS |        Yes        |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/shahen94/react-native-switch/blob/master/LICENSE).

<!-- {% endraw %} -->
