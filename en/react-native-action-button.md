> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-action-button</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mastermoo/react-native-action-button">
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
     <a href="https://github.com/mastermoo/react-native-action-button/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/mastermoo/react-native-action-button)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-action-button@2.8.5
```

#### **yarn**

```bash
yarn add react-native-action-button@2.8.5
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React, { Component } from "react";
import { StyleSheet, View,Text } from "react-native";
import ActionButton from "react-native-action-button";

export class App extends Component {
  render() {
    return (
      <View style={{ flex: 1, backgroundColor: "#f3f3f3" }}>
        <ActionButton buttonColor="rgba(231,76,60,1)">
          <ActionButton.Item
            buttonColor="#9b59b6"
            title="New Task"
            onPress={() => console.log("notes tapped!")}
          >
            <Text>1</Text>
          </ActionButton.Item>
          <ActionButton.Item
            buttonColor="#3498db"
            title="Notifications"
            onPress={() => {}}
          >
             <Text>2</Text>
          </ActionButton.Item>
          <ActionButton.Item
            buttonColor="#1abc9c"
            title="All Tasks"
            onPress={() => {}}
          >
             <Text>3</Text>
          </ActionButton.Item>
        </ActionButton>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  actionButtonIcon: {
    fontSize: 20,
    height: 22,
    color: "#000",
  },
});
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.11; SDK: OpenHarmony(api11) 4.1.0.53; IDE: DevEco Studio 4.1.3.412; ROM: 2.0.0.52;
2. RNOH: 0.72.13; SDK: HarmonyOS NEXT Developer Preview1; IDE: DevEco Studio 4.1.3.500; ROM: 2.0.0.58;
3. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.400; ROM: 3.0.0.25;
4. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71(API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                      |  Description                                                                                                                                                                                                                                             | Type     | Required | Platform |  HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- |----------| -------- |
| resetToken                | use this to reset the internal component state (expand/collapse) in a re-render cycle. Synchronize the component state.                                                                                                                           | any      | No       | All      | Yes      |
| size                      | use this to change the size of the Button                                                                                                                                                                                                         | number   | No       | All        | Yes      |
| active                    | action buttons visible or not                                                                                                                                                                                                                     | boolean  | No       | All        | Yes      |
| position                  | one of: left center and right                                                                                                                                                                                                                     | string   | No       | All        | Yes      |
| autoInactive              | Auto hide ActionButtons when ActionButton.Item is pressed.                                                                                                                                                                                        | boolean  | No       | All        | Yes      |
| hideShadow                | use this to hide the default elevation and boxShadow                                                                                                                                                                                              | boolean  | No       | All        | Yes      |
| spacing                   | spacing between the ActionButton.Items                                                                                                                                                                                                            | number   | No       | All        | Yes      |
| offsetX                   | offset from the left/right side of the screen                                                                                                                                                                                                     | number   | No       | All        | Yes      |
| offsetY                   | offset from the bottom/top of the screen                                                                                                                                                                                                          | number   | No       | All        | Yes      |
| buttonText                | use this to set a different text on the button                                                                                                                                                                                                    | string   | No       | All        | Yes      |
| degrees                   | degrees to rotate icon                                                                                                                                                                                                                            | number   | No       | All        | Yes      |
| shadowStyle               | The custom shadow style you want to pass in the action button                                                                                                                                                                                     | style    | No       | All        | Yes      |
| bgColor                   | background color when ActionButtons are visible                                                                                                                                                                                                   | string   | No       | All        | Yes      |
| bgOpacity                 | set the transparency of the background color                                                                                                                                                                                                      | number   | No       | All        | Yes      |
| buttonTextStyle           | use this to set the textstyle of the button's text                                                                                                                                                                                                | style    | No       | All        | Yes      |
| verticalOrientation       | direction action buttons should expand. One of: up or down                                                                                                                                                                                        | string   | No       | All        | Yes      |
| backgroundTappable        | make background tappable in active state of ActionButton                                                                                                                                                                                          | boolean  | No       | All        | Yes      |
| activeOpacity             | activeOpacity props of TouchableOpacity                                                                                                                                                                                                           | number   | No       | All        | Yes      |
| renderIcon                | Function to render the component for ActionButton Icon. It is passed a boolean, active, which is true if the FAB has been expanded, and false if it is collapsed, allowing you to show a different icon when the ActionButton Items are expanded. | function | No       | All        | Yes      |
| onPress                   | fires, when ActionButton is tapped                                                                                                                                                                                                                | function | No       | All        | Yes      |
| useNativeFeedback         | Android: Whether to use a TouchableNativeFeedback                                                                                                                                                                                                 | boolean  | No       | Android  | No       |
| fixNativeFeedbackRadius   | Android: Activate this to fix TouchableNativeFeedback Ripple UI problems                                                                                                                                                                          | boolean  | No       | Android  | No       |
| nativeFeedbackRippleColor | Android: Pass a color to the Ripple Effect of a TouchableNativeFeedback                                                                                                                                                                           | string   | No       | Android  | No       |

### ActionButton.Item:

| Name                      |  Description                                                                                                                                                                                                                                             | Type     | Required | Platform |  HarmonyOS Support |
| ------------------------- | -------------------------------------------------------------------------- | -------- | -------- |----------| -------- |
| size                      | use this to change the size of the Button                                  | number   | No       | All      | Yes      |
| buttonColor               | background color of the Button                                             | string   | No       | All      | Yes      |
| title                     | the title shown next to the button. When undefined the title is not hidden | string   | No       | All      | Yes      |
| textStyle                 | use this to set the textstyle of the button's item text                    | style    | No       | All      | Yes      |
| shadowStyle               | The custom shadow style you want to pass in the action button item         | style    | No       | All      | Yes      |
| textContainerStyle        | use this to set the textstyle of the button's item text container          | style    | No       | All      | Yes      |
| spaceBetween              | use this to set the space between the Button and the text container        | number   | No       | All      | Yes      |
| hideLabelShadow           | use this to hide the button's label default elevation and boxShadow        | boolean  | No       | All      | Yes      |
| activeOpacity             | activeOpacity props of TouchableOpacity                                    | number   | No       | All      | Yes      |
| onPress                   | required function, triggers when a button is tapped                        | function | No       | All      | Yes      |
| useNativeFeedback         | Android: Whether to use a TouchableNativeFeedback                          | boolean  | No       | Android  | No       |
| fixNativeFeedbackRadius   | Android: Activate this to fix TouchableNativeFeedback Ripple UI problems   | boolean  | No       | Android  | No       |
| nativeFeedbackRippleColor | Android: Pass a color to the Ripple Effect of a TouchableNativeFeedback    | string   | No       | Android  | No       |

## Known Issues

## Others

## License

This project is licensed under [MIT License](https://github.com/mastermoo/react-native-action-button/blob/master/LICENSE).
