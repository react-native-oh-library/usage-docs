> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-material-textfield</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/n4kz/react-native-material-textfield">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/n4kz/react-native-material-textfield/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-BSD-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-material-textfield/tree/sig)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-material-textfield Releases](https://github.com/react-native-oh-library/react-native-material-textfield/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-material-textfield
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-material-textfield
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```tsx

import React, {useState} from 'react';
import {  StyleSheet,SafeAreaView,Platform,ScrollView,View,Button} from 'react-native';
import {
  TextField,
} from 'react-native-material-textfield';


let defaults = {
  firstname: 'Eddard',
  lastname: 'Stark'
};


export default function TextfieldDemo() {
  const [errors, setErrors] = useState({});  
  const [combinedState, setCombinedState] = useState({  
    ...defaults,  
    secureTextEntry:true, 
  }); 
  const firstnameRef  = React.createRef();;
  const lastnameRef  = React.createRef();
  const aboutRef  = React.createRef();
  const emailRef = React.createRef();
  const passwordRef = React.createRef();

  const onSubmit = () => {
    let errors = {};
    ['firstname', 'lastname', 'email', 'password']
    .forEach((name) => {
        const ref = name === 'firstname' ? firstnameRef :  
                    name === 'lastname' ? lastnameRef :
                    name === 'email' ? emailRef : 
                    passwordRef;       
        let value = ref.current ? ref.current.value() : ''; 
        if(!value) {
          errors[name] = 'Should not be empty';
        } else {
          if('password' === name && value.length < 6) {
            errors[name] = 'Too short';
          }
        }
    });
    setErrors(errors)
  }

  const onChangeText= () => {
    ['firstname', 'lastname', 'email', 'password']
    .forEach((name) => {
      const ref = name === 'firstname' ? firstnameRef :  
      name === 'lastname' ? lastnameRef :
      name === 'email' ? emailRef : 
      passwordRef;      
      let value = ref.current ? ref.current.value() : ''; 
      setCombinedState({  
        ...combinedState,  
        [name]: value
      });  
    })
  }
 
  return (
    <SafeAreaView style={styles.safeContainer}>
        <ScrollView
            style={styles.scroll}
            contentContainerStyle={styles.contentContainer}
            keyboardShouldPersistTaps='handled'
          >
          <View style={styles.container}>
              <TextField
                ref={firstnameRef}
                value={defaults.firstname}
                autoCorrect={false}
                enablesReturnKeyAutomatically={true}
                returnKeyType='next'
                label='First Name'
                onChangeText={onChangeText}
                error={errors.firstname}
              />

             <TextField
                ref={lastnameRef}
                value={defaults.lastname}
                autoCorrect={false}
                enablesReturnKeyAutomatically={true}      
                returnKeyType='next'
                label='Last Name'
                onChangeText={onChangeText}
                error={errors.lastname}
              />  

              <TextField
                ref={emailRef}
                keyboardType='email-address'
                autoCapitalize='none'
                autoCorrect={false}
                enablesReturnKeyAutomatically={true}
                returnKeyType='next'
                label='Email Address'
                onChangeText={onChangeText}
                error={errors.email}
              />

              <TextField 
                ref={passwordRef}
                autoCapitalize='none'
                autoCorrect={false}
                enablesReturnKeyAutomatically={true}
                returnKeyType='done'
                label='Password'
                title='Choose wisely'
                maxLength={30}
                onChangeText={onChangeText}
                characterRestriction={20}
                error={errors.password}
              />

             <Button title='running' color='#841584' onPress={onSubmit}></Button>
              
          </View>
        </ScrollView>

    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeContainer: {
    flex: 1,
    backgroundColor: '#FFFFFF',
  },
  scroll: {
    backgroundColor: 'transparent',
  },

  container: {
    margin: 8,
    marginTop: Platform.select({ harmony:8,ios: 8,android: 32 }),
    flex: 1,
  },

  contentContainer: {
    padding: 8,
  },

  buttonContainer: {
    paddingTop: 8,
    margin: 8,
  }
});

```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-material-textfield Releases](https://github.com/react-native-oh-library/react-native-material-textfield/releases)

This document is verified based on the following versions:

RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## Properties

### This component has the following properties:
>[!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

>[!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| **textColor**      |       Text input color         |                         String                           |    No    | iOS/Android |        Yes        |
| **fontSize**        |                   Text input font size                    |                         Number                           |    YES   | iOS/Android |        Yes        |
| **labelFontSize**      |                  Text field label font size               |                         Number                           |    No    | iOS/Android |        Yes        |
| **lineWidth**  |       Text field underline width      |                         Number                           |    No    | iOS/Android |        Yes        |
| **activeLineWidth**  |       Text field active underline width     |                         Number                           |    No    | iOS/Android |        Yes        |
| **disabledLineWidth**  |       Text field disabled underline width     |                         Number                           |    No    | iOS/Android |        Yes        |
| **tintColor**  |       Text field accent color     |                         String                           |    No    | iOS/Android |        Yes        |
| **baseColor**  |      Text field base color     |                         String                           |    No    | iOS/Android |        Yes        |
| **label**  |      Text field label text     |                         String                           |    No    | iOS/Android |        Yes        |
| **title**  |      Text field helper text     |                         String                           |    No    | iOS/Android |        Yes        |
| **prefix**  |     Text field prefix text     |                         String                           |    No    | iOS/Android |        Yes        |
| **suffix**  |     Text field suffix text     |                         String                           |    No    | iOS/Android |        Yes        |
| **error**  |     Text field error text     |                         String                           |    No    | iOS/Android |        Yes        |
| **errorColor**  |     Text field color for errored state     |                         String                           |    No    | iOS/Android |        Yes        |
| **lineType**  |     Text field line type     |                         String                           |    No    | iOS/Android |        Yes        |
| **disabledLineType**  |     Text field line type in disabled state     |                         String                           |    No    | iOS/Android |        Yes        |
| **animationDuration**  |     Text field animation duration in ms     |                         Number                           |    No    | iOS/Android |        Yes        |
| **characterRestriction**  |     Text field soft limit for character counter     |                         Number                           |    No    | iOS/Android |        Yes        |
| **disabled**  |    Text field availability     |                         Boolean                           |    No    | iOS/Android |        Yes        |
| **editable**  |    Text field text can be edited     |                         Boolean                           |    No    | iOS/Android |        Yes        |
| **multiline**  |    Text filed multiline input     |                         Boolean                           |    No    | iOS/Android |        Yes        |
| **contentInset**  |    TLayout configuration object     |                         Object                           |    No    | iOS/Android |        Yes        |
| **labelOffset**  |    Label position adjustment     |                         Object                           |    No    | iOS/Android |        Yes        |
| **inputContainerStyle**  |    Style for input container view     |                         Object                           |    No    | iOS/Android |        Yes        |
| **containerStyle**  |    Style for container view     |                         Object                           |    No    | iOS/Android |        Yes        |
| **labelTextStyle**  |    Style for label inner Text component     |                         Object                           |    No    | iOS/Android |        Yes        |
| **titleTextStyle**  |    Style for title inner Text component     |                         Object                           |    No    | iOS/Android |        Yes        |
| **affixTextStyle**  |    Style for affix inner Text component     |                         Object                           |    No    | iOS/Android |        Yes        |
| **formatText**  |    Input mask callback    |                         Function                           |    No    | iOS/Android |        Yes        |
| **renderLeftAccessory**  |   Render left input accessory view    |                         Function                           |    No    | iOS/Android |        Yes        |
| **renderRightAccessory**  |   Render right input accessory view    |                         Function                           |    No    | iOS/Android |        Yes        |
| **onChangeText**  |   Change text callback    |                         Function                           |    No    | iOS/Android |        Yes        |
| **onFocus**  |   Focus callback    |                         Function                           |    No    | iOS/Android |        Yes        |
| **onBlur**  |  Blur callback    |                         Function                           |    No    | iOS/Android |        Yes        |

## **API（TextField）**
>[!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

>[!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|   **focus()**    |           Acquire focus            |                                                    |    No    | iOS/Android |        Yes        |
|   **blur()**    |   Release focus   |                                                    |    No    | iOS/Android |        Yes        |
|   **clear()**    |   Clear text field   |                                                    |    No    | iOS/Android |        Yes        |
|   **value()**    |   Get current value  |                         String                           |    No    | iOS/Android |        Yes        |
|   **isFocused()**    |   Get current focus state   |                         Boolean                           |    No    | iOS/Android |        Yes        |
|   **isErrored()**    |  Get current error state  |                         Boolean                           |    No    | iOS/Android |        Yes        |
|   **isRestricted()**    |   Get current restriction state	   |                         Boolean                           |    No    | iOS/Android |        Yes        |
|   **isDefaultVisible()**    |   Get default value visibility   |                         Boolean                           |    No    | iOS/Android |        Yes        |
|   **isPlaceholderVisible()**    |   Get placeholder visibility   |                         Boolean                           |    No    | iOS/Android |        Yes        |
|   **setValue()**    |   Set current value   |                                                    |    No    | iOS/Android |        Yes        |

## Known Issues

## Others

## License

This project is licensed under [BSD License](https://github.com/n4kz/react-native-material-textfield/blob/master/license.txt).