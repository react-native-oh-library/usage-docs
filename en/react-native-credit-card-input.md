> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-credit-card-input</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/sbycrosz/react-native-credit-card-input">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/sbycrosz/react-native-credit-card-input/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-credit-card-input)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-credit-card-input Releases](https://github.com/react-native-oh-library/react-native-credit-card-input/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-credit-card-input
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-credit-card-input
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React, { Component } from "react";
import { StyleSheet, View, Switch } from "react-native";
import { CreditCardInput, LiteCreditCardInput } from "react-native-credit-card-input";

const s = StyleSheet.create({
  switch: {
    alignSelf: "center",
    marginTop: 20,
    marginBottom: 20,
  },
  container: {
    backgroundColor: "#F5F5F5",
    marginTop: 60,
  },
  label: {
    color: "black",
    fontSize: 12,
  },
  input: {
    fontSize: 16,
    color: "black",
  },
});


export default class Example extends Component {
  state = { useLiteCreditCardInput: false };

  _onChange = (formData) => console.log(JSON.stringify(formData, null, " "));
  _onFocus = (field) => console.log("focusing", field);
  _setUseLiteCreditCardInput = (useLiteCreditCardInput) => this.setState({ useLiteCreditCardInput });

  render() {
    return (
      <View style={s.container}>
        <Switch
          style={s.switch}
          onValueChange={this._setUseLiteCreditCardInput}
          value={this.state.useLiteCreditCardInput} />

        { this.state.useLiteCreditCardInput ?
          (
            <LiteCreditCardInput
              autoFocus
              inputStyle={s.input}

              validColor={"black"}
              invalidColor={"red"}
              placeholderColor={"darkgray"}

              onFocus={this._onFocus}
              onChange={this._onChange} />
          ) : (
            <CreditCardInput
              autoFocus

              requiresName
              requiresCVC
              requiresPostalCode

              labelStyle={s.label}
              inputStyle={s.input}
              validColor={"black"}
              invalidColor={"red"}
              placeholderColor={"darkgray"}

              onFocus={this._onFocus}
              onChange={this._onChange} />
          )
        }
      </View>
    );
  }
}

```
## Constraints

### Compatibility

This document is verified based on the following versions:

1.RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;

## Properties

>[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

>[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-credit-card-input](https://github.com/sbycrosz/react-native-credit-card-input)

### LiteCreditCardInput

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| autoFocus  | 	Automatically focus Card Number field on render | PropTypes.bool  | no | Android/iOS      | yes |
| onChange  | Receives a formData object every time the form changes | PropTypes.func  | no | Android/iOS | yes |
| onFocus  | 	Receives the name of currently focused field| 	PropTypes.func  | no | Android/iOS | yes |
| placeholders  | Defaults to\{ number: "1234 5678 1234 5678", expiry: "MM/YY", cvc: "CVC" \}  | string | no | Android/iOS | yes |
| inputStyle| Style for credit-card form's textInput | Text.propTypes.style | no | Android/iOS | yes |
| validColor| Color that will be applied for valid text input. Defaults to: "\{inputStyle.color\}" | PropTypes.string | no | Android/iOS | yes |
| invalidColor| Color that will be applied for invalid text input. Defaults to: "red" | PropTypes.string | no | Android/iOS | yes |
| placeholderColor| Color that will be applied for text input placeholder. Defaults to: "gray" | PropTypes.string | no | Android/iOS | yes |
| additionalInputsProps | An object with Each key of the object corresponding to the name of the field. Allows you to change all props documented in RN TextInput. | PropTypes.objectOf(TextInput.propTypes) | no | Android/iOS | yes |

### CreditCardInput

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| autoFocus | Automatically focus Card Number field on render  | 	PropTypes.bool  | no | Android/iOS | yes |
| onChange  | Receives a formData object every time the form changes | PropTypes.func   | no | Android/iOS | yes |
| onFocus | Receives the name of currently focused field   | 	PropTypes.func  | no | Android/iOS  | yes |
| labels |	Defaults to\{ number: "CARD NUMBER", expiry: "EXPIRY", cvc: "CVC/CCV" \}| PropTypes.object  | no | Android/iOS | yes |
| placeholders  | Defaults to\{ number: "1234 5678 1234 5678", expiry: "MM/YY", cvc: "CVC" \} | PropTypes.object   | no | Android/iOS | yes |
| cardScale | 	Scales the credit-card view.Defaults to 1, which translates to \{ width: 300, height: 190 \}   | PropTypes.number  | no | Android/iOS  | yes |
| cardFontFamily | Font family for the CreditCardView, works best with monospace fonts. Defaults to Courier (iOS) or monospace (android)  | PropTypes.string  | no | Android/iOS | yes |
| cardImageFront  | Image for the credit-card view e.g. require("./card.png") | PropTypes.number   | no | Android/iOS | yes |
| cardImageBack | Image for the credit-card view e.g. require("./card.png")   | PropTypes.number  | no | Android/iOS  | yes |
| labelStyle  | Style for credit-card form's labels | Text.propTypes.style   | no | Android/iOS | yes |
| inputStyle | 	Style for credit-card form's textInput   | Text.propTypes.style  | no | Android/iOS  | yes |
| inputContainerStyle  | 	Style for textInput's containerDefaults to: \{ borderBottomWidth: 1, borderBottomColor:"black" \} | ViewPropTypes.style   | no | Android/iOS | yes |
| validColor | Color that will be applied for valid text input. Defaults to: "\{inputStyle.color\}"   | PropTypes.string  | no | Android/iOS  | yes |
| invalidColor | 	Color that will be applied for invalid text input. Defaults to: "red"   | PropTypes.string  | no | Android/iOS  | yes |
| placeholderColor | Color that will be applied for text input placeholder. Defaults to: "gray"  | PropTypes.string  | no | Android/iOS  | yes |
| requiresName | Shows cardholder's name field Default to false  | PropTypes.bool  | no | Android/iOS  | yes |
| requiresCVC | Shows CVC field Default to true  | PropTypes.bool | no | Android/iOS  | yes |
| requiresPostalCode | 	Shows postalCode field Default to false  | PropTypes.string  | no | Android/iOS  | yes |
| validatePostalCode | 	Function to validate postalCode, expects incomplete, valid, or invalid as return values  | PropTypes.func  | no | Android/iOS  | yes |
| allowScroll | enables horizontal scrolling on CreditCardInput Defaults to false  | PropTypes.bool | no | Android/iOS  | yes |
| cardBrandIcons | 		brand icons for CardView. see ./src/Icons.js for details  | PropTypes.object  | no | Android/iOS  | yes |
| additionalInputsProps | An object with Each key of the object corresponding to the name of the field. Allows you to change all props documented in RN TextInput.  | PropTypes.objectOf(TextInput.propTypes)  | no | Android/iOS  | yes |

### CardView

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| focused  | Determines the front face of the card | PropTypes.string  | no | Android/iOS  | yes |
| brand | Brand of the credit card | PropTypes.string  | no | Android/iOS  | yes |
| name  | Cardholder's name (Use empty string if you need to hide the placeholder) | PropTypes.string  | no | Android/iOS  | yes |
| number | Credit card number (you'll need to the formatting yourself) | PropTypes.string  | no | Android/iOS  | yes |
| expiry  | Credit card expiry (should be in MM/YY format) | PropTypes.string  | no | Android/iOS  | yes |
| cvc | Credit card CVC | PropTypes.string  | no | Android/iOS  | yes |
| placeholder  | Placeholder texts | PropTypes.object  | no | Android/iOS  | yes |
| scale | Scales the card | PropTypes.number  | no | Android/iOS  | yes |
| fontFamily  | Defaults to Courier and monospace in iOS and Android respectively | PropTypes.string  | no | Android/iOS  | yes |
| imageFront | Image for the credit-card | PropTypes.number | no | Android/iOS  | yes |
| imageBack  | Image for the credit-card | PropTypes.number  | no | Android/iOS  | yes |
| customIcons | brand icons for CardView. see ./src/Icons.js for details | PropTypes.object  | no | Android/iOS  | yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/sbycrosz/react-native-credit-card-input/blob/master/LICENSE).