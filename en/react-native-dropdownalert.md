> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-dropdownalert</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-dropdownalert">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-dropdownalert/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-dropdownalert)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-dropdownalert Releases](https://github.com/react-native-oh-library/react-native-dropdownalert/releases).

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-dropdownalert
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-dropdownalert
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useRef, useState } from "react";
import {
  StyleSheet,
  Text,
  View,
  FlatList,
  SafeAreaView,
  TouchableOpacity,
  ImageSourcePropType,
  ColorValue,
} from "react-native";
import DropdownAlert, {
  DropdownAlertData,
  DropdownAlertType,
  DropdownAlertColor,
  DropdownAlertProps,
} from "react-native-dropdownalert";

type ListItem = {
  name: string,
  alertData?: DropdownAlertData,
  alertProps?: DropdownAlertProps,
  color: ColorValue,
};

type ListItemIndex = {
  item: ListItem,
  index: number,
};

function App(): React.JSX.Element {
  const defaultSelected: ListItem = {
    name: "Default",
    color: DropdownAlertColor.Default,
  };
  const [selected, setSelected] = useState(defaultSelected);
  const [processing, setProcessing] = useState(false);
  let alert = useRef(
    (_data?: DropdownAlertData) =>
      new Promise() < DropdownAlertData > ((res) => res)
  );
  let dismiss = useRef(() => {});
  const reactNativeLogoSrc: ImageSourcePropType = {
    uri: "https://reactnative.dev/docs/assets/favicon.png",
  };

  const items: ListItem[] = [
    {
      name: "Warn",
      alertData: {
        type: DropdownAlertType.Warn,
        title: "Warn",
        message:
          "The device battery is low. It will go into low power mode in 5 minutes.",
      },
      color: DropdownAlertColor.Warn,
    },
    {
      name: "Info",
      alertData: {
        type: DropdownAlertType.Info,
        title: "Info",
        message:
          "The system goes offline from midnight to 3 AM for regular maintenance.",
      },
      color: DropdownAlertColor.Info,
    },
    {
      name: "Success",
      alertData: {
        type: DropdownAlertType.Success,
        title: "Success",
        message: "The order is complete and details sent to email.",
      },
      color: DropdownAlertColor.Success,
    },
    {
      name: "Error",
      alertData: {
        type: DropdownAlertType.Error,
        title: "Error",
        message:
          "Something went wrong. Please contact support if error persists.",
      },
      color: DropdownAlertColor.Error,
    },
    {
      name: "Custom",
      alertData: {
        type: "",
        title: "Custom",
        message:
          "This demonstrates the ability to customize image, interval and style.",
        source: reactNativeLogoSrc,
        interval: 5000,
      },
      alertProps: {
        alertViewStyle: styles.alertView,
      },
      color: styles.alertView.backgroundColor,
    },
    {
      name: "Cancel",
      alertData: {
        type: DropdownAlertType.Info,
        title: "Info",
        message:
          "This demonstrates an info alert with a cancel button. Tap cancel button to dismiss.",
      },
      alertProps: {
        dismissInterval: 0,
        showCancel: true,
        onDismissPressDisabled: true,
      },
      color: "teal",
    },
    {
      name: "Bottom",
      alertData: {
        type: DropdownAlertType.Info,
        title: "Info",
        message: "This demonstrates an info alert with bottom alert position.",
      },
      alertProps: {
        alertPosition: "bottom",
        infoColor: "green",
      },
      color: "green",
    },
  ];

  function _renderItem(listItemIndex: ListItemIndex): React.JSX.Element {
    const { item } = listItemIndex;
    return (
      <TouchableOpacity
        style={[styles.item, { backgroundColor: item.color }]}
        onPress={() => _onSelect(item)}
        disabled={processing}
      >
        <Text style={styles.name}>{item.name}</Text>
      </TouchableOpacity>
    );
  }

  function _onSelect(item: ListItem): void {
    setSelected(item);
    setTimeout(async () => {
      setProcessing(true);
      await alert.current(item.alertData);
      setProcessing(false);
    }, 10);
  }

  return (
    <View style={styles.view}>
      <SafeAreaView>
        <FlatList
          keyExtractor={(_item, index) => `${index}`}
          data={items}
          initialNumToRender={items.length}
          renderItem={_renderItem}
        />
      </SafeAreaView>
      <DropdownAlert
        alert={(func) => (alert.current = func)}
        dismiss={(func) => (dismiss.current = func)}
        {...selected.alertProps}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  view: {
    flex: 1,
    justifyContent: "center",
    backgroundColor: "#F4F3E9",
  },
  item: {
    padding: 12,
    margin: 4,
    borderRadius: 8,
    borderColor: "black",
    borderWidth: StyleSheet.hairlineWidth,
  },
  name: {
    fontSize: 18,
    fontWeight: "bold",
    textAlign: "center",
    color: "whitesmoke",
  },
  alertView: {
    padding: 8,
    backgroundColor: "#6441A4",
  },
});

export default App;
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-dropdownalert Releases](https://github.com/react-native-oh-library/react-native-dropdownalert/releases)

## DropdownAlert

### DropdownAlertType

**DropdownAlertType**, an enum object exported from the **DropdownAlert** library, enumerates the types of dialog boxes.

#### DropdownAlertType Property

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name    | Description  | Type   | **Required** | Platform | HarmonyOS Support |
| ------- | ------------ | ------ | ------------ | -------- | ----------------- |
| Info    | The value is **info**.   | string | no           | All      | yes               |
| Warn    | The value is **warn**.   | string | no           | All      | yes               |
| Error   | The value is **error**.  | string | no           | All      | yes               |
| Success | The value is **success**.| string | no           | All      | yes               |

### DropdownAlertDismissAction

**DropdownAlertDismissAction**, an enum object exported from the **DropdownAlert** library, enumerates the dismiss action types of dialog boxes.

#### DropdownAlertDismissAction Property

| Name         | Description       | Type   | **Required** | Platform | HarmonyOS Support |
| ------------ | ----------------- | ------ | ------------ | -------- | ----------------- |
| Automatic    | The value is **automatic**.   | string | no           | All      | yes               |
| Cancel       | The value is **cancel**.      | string | no           | All      | yes               |
| Pan          | The value is **pan**.         | string | no           | All      | yes               |
| Programmatic | The value is **programmatic**.| string | no           | All      | yes               |
| Press        | The value is **press**.       | string | no           | All      | yes               |

### DropdownAlertColor

**DropdownAlertColor**, an enum object exported from the **DropdownAlert** library, enumerates the colors of dialog boxes.

#### DropdownAlertColor Property

| Name    | Description    | Type   | **Required** | Platform | HarmonyOS Support |
| ------- | -------------- | ------ | ------------ | -------- | ----------------- |
| Info    | The value is **'#2b73b6'**. | string | no           | All      | yes               |
| Warn    | The value is **'#cd853f'**. | string | no           | All      | yes               |
| Error   | The value is **'#cc3232'**. | string | no           | All      | yes               |
| Success | The value is **'#32a54a'**. | string | no           | All      | yes               |
| Default | The value is **'#000000'**.| string | no           | All      | yes               |

### DropDownAlertImage

**DropDownAlertImage**, an enum object exported from the **DropdownAlert** library, enumerates the image resources of dialog boxes.

#### DropDownAlertImage Property

| Name    | Description                                                              | Type                | **Required** | Platform | HarmonyOS Support |
| ------- | ------------------------------------------------------------------------ | ------------------- | ------------ | -------- | ----------------- |
| Info    | Image resource used in the Info dialog box, which is obtained through **require('./assets/info.png')**.      | ImageSourcePropType | no           | All      | yes               |
| Warn    | Image resource used in the Warn dialog box, which is obtained through **require('./assets/warn.png')**.      | ImageSourcePropType | no           | All      | yes               |
| Error   | Image resource used in the Error dialog box, which is obtained through **require('./assets/error.png')**.    | ImageSourcePropType | no           | All      | yes               |
| Success | Image resource used in the Success dialog box, which is obtained through **require('./assets/success.png')**.| ImageSourcePropType | no           | All      | yes               |
| Cancel  | Image resource used in the Cancel dialog box, which is obtained through **require('./assets/cancel.png')**.  | ImageSourcePropType | no           | All      | yes               |

### DropdownAlertToValue

**DropdownAlertToValue**, an enum object exported from the **DropdownAlert** library, has two members: **Alert** and **Dismiss**.

#### DropdownAlertToValue Property

| Name    | Description | Type   | **Required** | Platform | HarmonyOS Support |
| ------- | ----------- | ------ | ------------ | -------- | ----------------- |
| Alert   | The value is **1**.     | number | no           | All      | yes               |
| Dismiss | The value is **0**.     | number | no           | All      | yes               |

### DropDownAlertTestID

**DropDownAlertTestID**, an enum object exported from the **DropdownAlert** library, enumerates the test IDs of dialog boxes.

#### DropDownAlertTestID Property

| Name         | Description       | Type   | **Required** | Platform | HarmonyOS Support |
| ------------ | ----------------- | ------ | ------------ | -------- | ----------------- |
| AnimatedView | The value is **animatedView**.| string | no           | All      | yes               |
| SafeView     | The value is **safeView**.    | string | no           | All      | yes               |
| TextView     | The value is **textView**.    | string | no           | All      | yes               |
| Alert        | The value is **alert**.       | string | no           | All      | yes               |
| Image        | The value is **image**.       | string | no           | All      | yes               |
| Title        | The value is **title**.       | string | no           | All      | yes               |
| Message      | The value is **message**.     | string | no           | All      | yes               |
| Cancel       | The value is **cancel**.      | string | no           | All      | yes               |
| CancelImage  | The value is **cancelImage**. | string | no           | All      | yes               |

### DropdownAlertData

**DropdownAlertData**, a class object exported from the **DropdownAlert** library, defines the data content of a dialog box, such as the title and prompt information.

#### DropdownAlertData Property

| Name     | Description                             | Type                | **Required** | Platform | HarmonyOS Support |
| -------- | --------------------------------------- | ------------------- | ------------ | -------- | ----------------- |
| type     | Type of the dialog box, which is an enumof **DropdownAlertType**.| DropdownAlertType   | no           | All      | yes               |
| title    | Message title of the dialog box.                         | string              | no           | All      | yes               |
| message  | Message body of the dialog box.                         | string              | no           | All      | yes               |
| source   | Image type of the dialog box.                         | ImageSourcePropType | no           | All      | yes               |
| interval | Interval for the dialog box to disappear automatically, in milliseconds.             | number              | no           | All      | yes               |
| resolve  | Event triggered when a dialog box is processed.                 | function            | no           | All      | yes               |

### DropdownAlertPosition

**DropdownAlertData**, a class object exported from the **DropdownAlert** library, defines the display position of the dialog box, including top and bottom.

#### DropdownAlertPosition Property

| Name   | Description            | Type              | **Required** | Platform | HarmonyOS Support |
| ------ | ---------------------- | ----------------- | ------------ | -------- | ----------------- |
| Top    | The dialog box is displayed on the top. The value is **top**.   | DropdownAlertType | no           | All      | yes               |
| Bottom | The dialog box is displayed at the bottom. The value is **bottom**.| string            | no           | All      | yes               |

### DropdownAlert components

**DropdownAlert**, a core component exported from the **DropdownAlert** library, defines all properties of a dialog box. Its properties are the same as those of **DropdownAlertProps**.

#### DropdownAlert Property

| Name                             | Description                                                                                                                                                        | Type                           | **Required** | Platform | HarmonyOS Support |
| -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------ | ------------ | -------- | ----------------- |
| imageSrc                         | Default custom image used when no image resource is specified for a dialog box.                                                                                                                      | ImageSourcePropType            | no           | All      | yes               |
| infoImageSrc                     | Custom image used when the dialog box type is not set to **Info**.                                                                                                                        | ImageSourcePropType            | no           | All      | yes               |
| warnImageSrc                     | Custom image used when the dialog box type is not set to **Warn**.                                                                                                                        | ImageSourcePropType            | no           | All      | yes               |
| errorImageSrc                    | Custom image used when the dialog box type is not set to **Error**.                                                                                                                       | ImageSourcePropType            | no           | All      | yes               |
| successImageSrc                  | Custom image used when the dialog box type is not set to **Success**.                                                                                                                     | ImageSourcePropType            | no           | All      | yes               |
| cancelImageSrc                   | Custom image used when the dialog box type is not set to **Cancel**.                                                                                                                      | ImageSourcePropType            | no           | All      | yes               |
| infoColor                        | Custom color used when the dialog box type is not set to **Info**.                                                                                                                        | ColorValue                     | no           | All      | yes               |
| warnColor                        | Custom color used when the dialog box type is not set to **Warn**.                                                                                                                        | ColorValue                     | no           | All      | yes               |
| errorColor                       | Custom color used when the dialog box type is not set to **Error**.                                                                                                                       | ColorValue                     | no           | All      | yes               |
| successColor                     | Custom color used when the dialog box type is not set to **Success**.                                                                                                                     | ColorValue                     | no           | All      | yes               |
| activeStatusBarBackgroundColor   | Background color used for the status bar when a dialog box is displayed. This property is valid only when **updateStatusBar** is set to **true**.                                                                                          | ColorValue                     | no           | Android  | yes               |
| inactiveStatusBarBackgroundColor | Background color used for the status bar when a dialog box is dismissed. This property is valid only when **updateStatusBar** is set to **true**.                                                                                          | ColorValue                     | no           | Android  | yes               |
| dismissInterval                  | Interval for the dialog box to disappear automatically, in milliseconds.                                                                                                                                          | number                         | no           | All      | yes               |
| titleNumberOfLines               | Maximum number of lines in the dialog box title.                                                                                                                                              | number                         | no           | All      | yes               |
| messageNumberOfLines             | Maximum number of lines in the message body. If the number of lines exceeds the maximum, the excess lines are omitted.                                                                                                                                    | number                         | no           | All      | yes               |
| elevation                        | Height of the view. This property can be used to add a projection to the view and affects the view cascading sequence. This property applies only to Android 5.0 and later versions.                                                          | number                         | no           | Android  | no                |
| zIndex                           | Index of the z-axis.                                                                                                                                                          | number                         | no           | All      | no                |
| panResponderDismissDistance      | Dismiss distance of the dialog box that can be dismissed by a swipe-down gesture.                                                                                                                                                  | number                         | no           | All      | yes               |
| animatedViewStyle                | Receives a **ViewStyle** object to set the style of **Animated.View**.                                                                                        | ViewStyle                      | no           | All      | no                |
| alertViewStyle                   | Receives a **ViewStyle** object to set the style of the dialog box.                                                                                                             | ViewStyle                      | no           | All      | yes               |
| safeViewStyle                    | Receives a **ViewStyle** object to set the style of **safeView**.                                                                                             | ViewStyle                      | no           | All      | yes               |
| textViewStyle                    | Receives a **ViewStyle** object to set the style of the text.                                                                                                         | ViewStyle                      | no           | All      | yes               |
| cancelViewStyle                  | Receives a **ViewStyle** object to set the style of the cancel button.                                                                                                 | ViewStyle                      | no           | All      | yes               |
| titleTextStyle                   | Receives a **TextStyle** object to set the style of the title.                                                                                                         | TextStyle                      | no           | All      | yes               |
| messageTextStyle                 | Receives a **TextStyle** object to set the style of the message.                                                                                                         | TextStyle                      | no           | All      | yes               |
| imageStyle                       | Receives an **ImageStyle** object to set the style of the image.                                                                                                      | ImageStyle                     | no           | All      | yes               |
| cancelImageStyle                 | Receives an **ImageStyle** object to set the style of the cancel button image.                                                                                          | ImageStyle                     | no           | All      | yes               |
| onDismissAutomatic               | Function triggered when a dialog box is dismissed automatically.                                                                                                                      | function                       | no           | All      | yes               |
| onDismissCancel                  | Function triggered when a dialog box is dismissed by clicking **Cancel**.                                                                                                                   | function                       | no           | All      | yes               |
| onDismissPress                   | Function triggered when a dialog box is dismissed by being pressed.                                                                                                                      | function                       | no           | All      | yes               |
| onDismissPanResponder            | Function triggered when a dialog box is dismissed by a swipe-down gesture. This property is valid only when **alertPosition** is set to **bottom**.                                                                                 | function                       | no           | All      | yes               |
| onDismissProgrammatic            | Function triggered when a dialog box is dismissed programmatically. This function is used by default.                                                      | function                       | no           | All      | no                |
| showCancel                       | Whether to display the **Cancel** module in the dialog box.                                                                                                                                        | boolean                        | no           | All      | yes               |
| onDismissPressDisabled           | Whether to allow a dialog box to be closed by pressing.                                                                                                                                          | boolean                        | no           | All      | yes               |
| panResponderEnabled              | Whether to allow a dialog box to be closed by a swipe-down gesture. This property is valid only when **alertPosition** is set to **bottom**.                                                                                                 | boolean                        | no           | All      | yes               |
| translucent                      | Whether the status bar is translucent. When this property is set to **true**, the application is drawn under the status bar, in other words, partially covered by the status bar. This property is often used with the status bar with a translucent background color, and is supported only by Android.| boolean                        | no           | Android  | no                |
| updateStatusBar                  | Whether to update the status bar.                                                                                                                                                    | boolean                        | no           | All      | yes               |
| activeStatusBarStyle             | Style used for the status bar when a dialog box is displayed. This property is valid only when **updateStatusBar** is set to **true**.                                                                                          | StatusBarStyle                 | no           | Android  | yes               |
| inactiveStatusBarStyle           | Style used for the status bar when a dialog box is dismissed. This property is valid only when **updateStatusBar** is set to **true**.                                                                                          | StatusBarStyle                 | no           | Android  | yes               |
| renderImage                      | Image returned by the function.                                                                                                                                                  | render function                | no           | All      | yes               |
| renderCancel                     | Cancellation returned by the function.                                                                                                                                                  | render function                | no           | All      | yes               |
| renderTitle                      | Message title of the dialog box returned by the function.                                                                                                                                          | render function                | no           | All      | yes               |
| renderMessage                    | Message body of the dialog box returned by the function.                                                                                                                                          | render function                | no           | All      | yes               |
| titleTextProps                   | Text style of the message title.                                                                                                                                                  | TextProps                      | no           | All      | yes               |
| messageTextProps                 | Text style of the message body.                                                                                                                                                  | TextProps                      | no           | All      | yes               |
| animatedViewProps                | Receives a **ViewProps** object to set properties in **Animated.View**.                                                                                    | ViewProps                      | no           | All      | yes               |
| alertTouchableOpacityProps       | Properties of the opacity style of the dialog box.                                                                                                                                                | TouchableOpacityProps          | no           | All      | yes               |
| safeViewProps                    | Receives a **ViewProps** object to set properties in **safeView**.                                                                                         | ViewProps                      | no           | All      | yes               |
| textViewProps                    | Receives a **ViewProps** object to set properties in **textView**.                                                                                       | ViewProps                      | no           | All      | yes               |
| imageProps                       | Receives an **ImageProps** object to set properties in **image**.                                                                                              | ImageProps                     | no           | All      | yes               |
| cancelTouchableOpacityProps      | Receives a **TouchableOpacityProps** object to set the properties of the cancel button.                                                                               | TouchableOpacityProps          | no           | All      | yes               |
| cancelImageProps                 | Receives an **ImageProps** object to set the properties of the cancel button image.                                                                                      | ImageProps                     | no           | All      | yes               |
| alert                            | Event triggered when a dialog box is displayed.                                                                                                                                                  | function                       | no           | All      | yes               |
| dismiss                          | Event triggered when a dialog box is dismissed.                                                                                                                                                  | function                       | no           | All      | yes               |
| springAnimationConfig            | Parameters of the spring animation.                                                                                                                                                      | Animated.SpringAnimationConfig | no           | All      | yes               |
| children                         | Child elements of the dialog box.                                                                                                                                                        | ReactNode                      | no           | All      | yes               |
| alertPosition                    | Position of the dialog box. When this property is set to **top**, the dialog box is displayed from the top of the screen. When this property is set to **bottom**, the dialog box is displayed from the bottom of the screen. The default value is **top**.                                                                          | string                         | no           | All      | yes               |

## Known Issues

## Others

- The **animatedViewStyle** property of the **DropdownAlert** component is invalid. After the property is set, the dialog box turns black, which is the same as that on iOS/Android: [issue#314](https://github.com/testshallpass/react-native-dropdownalert/issues/314).
- The **zindex** property of the **DropdownAlert** component is invalid, and the hierarchical relationship is not displayed, which is the same as that on iOS/Android: [issue#315](https://github.com/testshallpass/react-native-dropdownalert/issues/315).
- The **translucent** property of the **DropdownAlert** component is invalid, and the translucent effect of the status bar is not displayed, which is the same as that on Android: [issue#316](https://github.com/testshallpass/react-native-dropdownalert/issues/316).
- The **onDismissProgrammatic** function bound to the **DropdownAlert** component cannot be triggered, which is the same as that on iOS/Android: [issue#317](https://github.com/testshallpass/react-native-dropdownalert/issues/317).
- The **resolve** property of the **DropdownAlertData** component is invalid. After the dialog box is dismissed, the configured function is not triggered, which is the same as that on iOS/Android: [issue#318](https://github.com/testshallpass/react-native-dropdownalert/issues/318).

## License

This project is licensed under [MIT License](https://github.com/react-native-oh-library/react-native-dropdownalert/blob/master/LICENSE).
