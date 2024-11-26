Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-localization</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/stefalda/ReactNativeLocalization">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/stefalda/ReactNativeLocalization/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/ReactNativeLocalization)


## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-localization Releases](https://github.com/react-native-oh-library/ReactNativeLocalization/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-localization
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-localization
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';
import Localize from 'react-native-localization';

const strings = new Localize({
  en: {
    welcome: 'Welcome',
    question: 'I\'d like some {0} and {1}, or just {0}',
    bread: 'bread',
    butter: 'butter',
    greeting: 'Hello, {0}!   ',
    currentlanguage: 'Current Language',
    availableLanguages: 'Available Languages',
    interfaceLanguage: 'The System Language'
  },
  fr: {
    welcome: 'Bienvenue',
    question: 'Je voudrais un peu de {0} et {1}, ou juste {0}',
    bread: 'pain',
    butter: 'beurre',
    greeting: 'Bonjour, {0}!',
    currentlanguage: 'Langue actuelle',
    availableLanguages: 'Langues disponibles',
    interfaceLanguage: 'Langue du système'
  },
  bo: {
    welcome: 'བསྐུལ་མཁན།',
    question: 'ང་ལུས་འདི་ལས། {0} དང། {1} ཡང་ཡིན། གང་ཡིན་ནི། {0}',
    bread: 'བཀྲུངས',
    butter: 'བརྡེན',
    greeting: 'བཀའ་བདག་ {0}!',
    currentlanguage: 'ད་དུས་ལག་འཁྱེར།',
    availableLanguages: 'ད་དུས་ལག་འཁྱེར་སྒྲིགས།',
    interfaceLanguage: 'རྩམ་གཞི་སྒྲིག་ལེན་དེ་རྒྱལ་སྤོད་'
  },
  zh: {
    welcome: '欢迎',
    question: '我想要一些{0}和{1}，或者只要{0}',
    bread: '面包',
    butter: '黄油',
    greeting: '你好, {0}!',
    currentlanguage: '当前语言',
    availableLanguages: '当前可用语言列表',
    interfaceLanguage: '当前系统语言'
  },
});

export function LocalizationDemo() {
  // getLanguage API
  const [language, setLanguage] = useState(strings.getLanguage());
  const changeLanguage = (lang: string) => {
    // setLanguage API
    strings.setLanguage(lang);
    setLanguage(strings.getLanguage());
  };

  return (
    <View style={styles.screen}>
      <View style={{ height: 180, justifyContent: 'space-between', marginBottom: 30 }}>
        <Button
          color="#144400"
          title="Switch to Chinese"
          onPress={() => changeLanguage('zh')}
        />
        <Button
          color="#841584"
          title="Switch to French"
          onPress={() => changeLanguage('fr')}
        />
        <Button
          color="#645555"
          title="Switch to English"
          onPress={() => changeLanguage('en')}
        />
        <Button
          color="#241595"
          title="Switch to Tibetan"
          onPress={() => changeLanguage('bo')}
        />
      </View>

      <Text style={styles.text}>
        {strings.welcome}
      </Text>
      <Text style={styles.text}>
        {/* formatString API */}
        {strings.formatString(strings.question, strings.bread, strings.butter)}
      </Text>
      <Text style={styles.text}>
        {strings.currentlanguage}: {language}
      </Text>
      {/* getAvailableLanguages API */}
      <Text style={styles.text}>
        {strings.availableLanguages}: {strings.getAvailableLanguages().join(', ')}
      </Text>
      {/* getInterfaceLanguage API */}
      <Text style={styles.text}>
        {strings.interfaceLanguage}: {strings.getInterfaceLanguage()}
      </Text>
    </View>
  );
}

const styles = StyleSheet.create({
  text: {
    fontSize: 18,
    marginBottom: 10,
    color: 'white'
  },

  screen: {
    flex: 1,
    padding: 4,
    paddingTop: 10,
    backgroundColor: 'black',
    marginHorizontal: 4,
    marginVertical: 8,
    paddingHorizontal: 8,
  },
});
```
## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

 

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-localization": "file:../../node_modules/@react-native-oh-tpl/react-native-localization/harmony/react_localization.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```
Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).


### 3. Introducing RNReactLocalizationPackage to ArkTS

 Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNReactLocalizationPackage } from '@react-native-oh-tpl/react-native-localization';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNReactLocalizationPackage(ctx),
  ];
}
```

### 4.Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-localization Releases](https://github.com/react-native-oh-library/ReactNativeLocalization/releases)



## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | :---------- | ---- | :------: | :------: | :----------------: |
| setLanguage(languageCode)                 | force manually a particular language                         | void     |   yes    | iOS/Android |        yes        |
| getLanguage()                             | get the current displayed language                           | string   |   yes    | iOS/Android |        yes        |
| getInterfaceLanguage()                    | get the current device interface language                    | string   |   yes    | iOS/Android |        yes        |
| formatString()                            | format the passed string replacing its placeholders with the other arguments strings | string   |   yes    | iOS/Android |        yes        |
| getAvailableLanguages()                   | get an array of the languages passed in the constructor      | string[] |   yes    | iOS/Android |        yes        |
| getString(key: string, language?: string) | character information based on the key value | string | yes | iOS/Android | yes |
| setContent(props: any) | replace the NamedLocalization object without reinstantiating the object | void | yes | iOS/Android | yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/stefalda/ReactNativeLocalization/blob/master/LICENSE).