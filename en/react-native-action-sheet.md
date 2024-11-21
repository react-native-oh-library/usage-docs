> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-action-sheet</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/expo/react-native-action-sheet">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/expo/react-native-action-sheet/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/expo/react-native-action-sheet)


## Installation and Usage

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @expo/react-native-action-sheet@4.0.1
```

#### **yarn**

```bash
yarn add @expo/react-native-action-sheet@4.0.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```js
import { ActionSheetProvider, connectActionSheet, ActionSheetProps } from '@expo/react-native-action-sheet';
import * as React from 'react';
import { useState } from 'react';
import { StyleSheet, Text, View, ScrollView, SafeAreaView } from 'react-native';
import ShowActionSheetButton from './ShowActionSheetButton';

type Props = ActionSheetProps & {
  useCustomActionSheet: boolean;
  setUseCustomActionSheet: (next: boolean) => void;
};

interface State {
  selectedIndex?: number | null;
  isModalOpen: boolean;
}

class App extends React.Component<Props, State> {
  state: State = {
    selectedIndex: null,
    isModalOpen: false,
  };

  _updateSelectionText = (selectedIndex?: number) => {
    this.setState({
      selectedIndex,
    });
  };

  _renderSelectionText = () => {
    const { selectedIndex } = this.state;
    const text =
      selectedIndex === null || selectedIndex === undefined
        ? 'No Option Selected'
        : `Option #${selectedIndex + 1} Selected`;
    return <Text style={styles.selectionText}>{text}</Text>;
  };

  _renderSectionHeader = (text: string) => {
    return <Text style={styles.sectionHeaderText}>{text}</Text>;
  };

  async _onShare() {
  }

  _renderButtons() {
    const { showActionSheetWithOptions } = this.props;
    return (
      <View
        style={{
          alignItems: 'center',
        }}>
        {this._renderSectionHeader('Android-Only Options')}
        <ShowActionSheetButton
          title="Icons"
          withIcons
          onSelection={this._updateSelectionText}
          showActionSheetWithOptions={showActionSheetWithOptions}
        />
        <ShowActionSheetButton
          title="Title, Message, & Icons"
          withTitle
          withMessage
          withIcons
          onSelection={this._updateSelectionText}
          showActionSheetWithOptions={showActionSheetWithOptions}
        />
        <ShowActionSheetButton
          title="Use Separators"
          withTitle
          withIcons
          withSeparators
          onSelection={this._updateSelectionText}
          showActionSheetWithOptions={showActionSheetWithOptions}
        />
        <ShowActionSheetButton
          title="Custom Styles"
          withTitle
          withMessage
          withIcons
          withCustomStyles
          onSelection={this._updateSelectionText}
          showActionSheetWithOptions={showActionSheetWithOptions}
        />
      </View>
    );
  }

  render() {
    return (
      <SafeAreaView style={styles.flex}>
        <ScrollView style={styles.flex} contentContainerStyle={styles.contentContainer}>
          {this._renderButtons()}
          {this._renderSelectionText()}
        </ScrollView>
      </SafeAreaView>
    );
  }
}

const ConnectedApp = connectActionSheet<any>(App);

export default function WrappedApp() {
  const [useCustomActionSheet, setUseCustomActionSheet] = useState(false);

  return (
    <ActionSheetProvider useCustomActionSheet={useCustomActionSheet}>
      <ConnectedApp
        useCustomActionSheet={useCustomActionSheet}
        setUseCustomActionSheet={setUseCustomActionSheet}
      />
    </ActionSheetProvider>
  );
}

const styles = StyleSheet.create({
  flex: {
    flex: 1,
  },
  contentContainer: {
    padding: 16,
    paddingVertical: 20,
  },
  headerText: {
    textAlign: 'center',
    fontSize: 16,
    marginBottom: 10,
  },
  notes: {
    marginTop: 32,
  },
  sectionHeaderText: {
    color: 'orange',
    textAlign: 'center',
    fontWeight: 'bold',
    fontSize: 20,
    marginTop: 20,
    marginBottom: 10,
  },
  selectionText: {
    textAlign: 'center',
    color: 'blue',
    fontSize: 16,
    marginTop: 20,
  },
});
```
## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**showActionSheetWithOptions**

| Name   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `icons`  | Show icons to go along with each option. If image source paths are provided via `require`, images will be rendered for you. Alternatively, you can provide an array of elements such as vector icons, pre-rendered Images, etc.  | array of required images or icons  | no     | Android/Web  | yes      |
| `tintIcons`  | Icons by default will be tinted to match the text color. When set to false, the icons will be the color of the source image. This is useful if you want to use multicolor icons. If you provide your own nodes/pre-rendered icons rather than required images in the `icons` array, you will need to tint them appropriately before providing them in the array of `icons`; `tintColor` will not be applied to icons unless they are images from a required source.  | boolean            |  no     | Android/Web  | yes      |
| `textStyle`  | Apply any text style props to the options. If the tintColor option is provided, it takes precedence over a color text style prop. | TextStyle    | no     | Android/Web    | yes      |
| `titleTextStyle`  | Apply any text style props to the title if present. | TextStyle      |  no     | Android/Web   | yes      |
| `messageTextStyle`  | Apply any text style props to the message if present.    | TextStyle      |  no     | Android/Web   | yes      |
| `autoFocus`  | If `true`, this will give the first option screen reader focus automatically when the action sheet becomes visible. On iOS, this is the default behavior of the native action sheet.       | boolean    |  no     | Android/Web   | yes      |
| `showSeparators`              | Show separators between items. On iOS, separators always show so this prop has no effect.    | boolean    |no     | Android/Web/ios   | yes      |
| `containerStyle`   | Apply any view style props to the container rather than use the default look (e.g. dark mode) | ViewStyle | no     | Android/Web | yes      |
| `separatorStyle`   | Modify the look of the separators rather than use the default look.  |ViewStyle  |no     | Android/Web | yes      |
| `useModal`         |  Defaults to `false` (`true` if autoFocus is also `true`) Wraps the ActionSheet with a Modal, in order to show in front of other Modals that were already opened ([issue reference](https://github.com/expo/react-native-action-sheet/issues/164)). |boolean   | no     | Android/Web | yes      |
| `destructiveColor` |  Modify color for text of destructive option. Defaults to `#d32f2f`. |string    | no     | Android/Web  | yes      |
| `options` | A list of button titles (required)|array of strings   | no     | All  | yes      |
| `cancelButtonIndex` |	Index of cancel button in options|number | no     | All  | yes      |
| `cancelButtonTintColor` |		Color used for the change the text color of the cancel button |string | no     | All  | yes      |
| `destructiveButtonIndex` |			Indices of destructive buttons in options|	number or array of numbers | no     | All  | yes      |
| `title` |		Title to show above the action sheet|		string| no     | All  | yes      |
| `message` |	Message to show below the title|		string| no     | All  | yes      |
| `tintColor` |	Color used for non-destructive button titles|		string| no     | All  | yes      |
| `disabledButtonIndices` |Indices of disabled buttons in options|			array of numbers| no     | All  | yes      |

**ActionSheetProvider**

| Name               | Description                                     | Type            | Required | Platform | HarmonyOS Support |
| ------------------ | ----------------------------------------------- | --------------- | -------- | -------- | ----------------- |
| `useCustomActionSheet` | iOS only prop that uses the custom pure JS action sheet (Android/Web version) instead of the native ActionSheetIOS component. Defaults to false. |boolean   | no     | ios  | yes      |
| `useNativeDriver` | Windows only option that provides the option to disable the native animation driver for React Native Windows projects targeting Windows 10 Version-1809 ; Build-10.0.17763.0 and earlier. useNativeDriver is supported in Version-1903 and later so if your project is targeting that, you don't need to set this prop. |boolean   | no     | Web  | yes      |
## Known Issues

## Others

## License
This project is licensed under [The MIT License (MIT)](https://github.com/expo/react-native-action-sheet/blob/master/LICENSE).
