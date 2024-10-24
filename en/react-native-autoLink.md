> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-autolink</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/joshswan/react-native-autolink">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/joshswan/react-native-autolink/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/joshswan/react-native-autolink)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-autolink@4.2.0
```

#### **yarn**

```bash
yarn add react-native-autolink@4.2.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { View, Text, StyleSheet } from "react-native";
import Autolink from "react-native-autolink";

const AutolinkDemo = () => {
  return (
    <View style={styles.container}>
      <Text style={styles.text}>Here is a demo of react-native-autolink:</Text>
      <Autolink
        text="This is the string to parse for urls (https://github.com/joshswan/react-native-autolink), phone numbers (415-555-5555), emails (josh@example.com), mentions/handles (@twitter), and hashtags (#exciting)"
        email
        hashtag="instagram"
        mention="twitter"
        phone="sms"
        url
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#f0f0f0",
  },
  text: {
    fontSize: 18,
    marginBottom: 10,
  },
  autolink: {
    fontSize: 16,
    lineHeight: 24,
  },
  link: {
    color: "blue",
    textDecorationLine: "underline",
  },
  customLink: {
    color: "red",
    textDecorationLine: "underline",
  },
  customText: {
    color: "red",
  },
});

export default AutolinkDemo;
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|        Name        |                                                                             Description                                                                              |        Type         | Required |  Platform   | HarmonyOS Support |
| :----------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------: | :------: | :---------: | :---------------: |
|     component      |                                                         Override the component used as the output container.                                                         | React.ComponentType |    No    | Android/IOS |        Yes        |
|       email        |                                                              Whether to link emails (`mailto:{email}`).                                                              |       boolean       |    No    | Android/IOS |        Yes        |
|      hashtag       |                     Whether to link hashtags to supplied service. Possible values: `false` (disabled), `"facebook"`, `"instagram"`, `"twitter"`.                     |  boolean or string  |    No    | Android/IOS |        Yes        |
|     linkProps      |                                                             Attributes applied to link Text components.                                                              |      TextProps      |    No    | Android/IOS |        Yes        |
|     linkStyle      | Styles applied to link Text components. _Note:_ Will be overriden if `style` supplied in [`linkProps`](https://github.com/joshswan/react-native-autolink#linkprops). |      TextStyle      |    No    | Android/IOS |        Yes        |
|      matchers      |                                   Array of custom matcher objects with optional press handlers, styling, and text/url extraction.                                    |   CustomMatcher[]   |    No    | Android/IOS |        Yes        |
|      mention       |                Whether to link mentions/handles to supplied service. Possible values: `false` (disabled), `"instagram"`, `"soundcloud"`, `"twitter"`.                |  boolean or string  |    No    | Android/IOS |        Yes        |
|      onPress       |                                       Override default link press behavior. Signature: `(url: string, match: Match) => void`.                                        |      function       |    No    | Android/IOS |        Yes        |
|    onLongPress     |                                           Handle link long press events. Signature: `(url: string, match: Match) => void`.                                           |      function       |    No    | Android/IOS |        Yes        |
|       phone        |                  Whether to link phone numbers. Possible values: `false` (disabled), `true` (`tel:{number}`), `"sms"` or `"text"` (`sms:{number}`).                  |  boolean or string  |    No    | Android/IOS |        Yes        |
|     renderLink     |                        Override default link rendering behavior. Signature: `(text: string, match: Match, index: number) => React.ReactNode`.                        |      function       |    No    | Android/IOS |        Yes        |
|     renderText     |                               Override default text rendering behavior. Signature: `(text: string, index: number) => React.ReactNode`.                               |      function       |    No    | Android/IOS |        Yes        |
|     showAlert      |                                        Whether to display an alert before leaving the app (for privacy or accidental clicks).                                        |       boolean       |    No    | Android/IOS |        Yes        |
|    stripPrefix     |                                      Whether to strip protocol from URL link text (e.g. `https://github.com` -> `github.com`).                                       |       boolean       |    No    | Android/IOS |        Yes        |
| stripTrailingSlash |                                      Whether to strip trailing slashes from URL link text (e.g. `github.com/` -> `github.com`).                                      |       boolean       |    No    | Android/IOS |        Yes        |
|        text        |                                                                    The string to parse for links.                                                                    |       string        |   Yes    | Android/IOS |        Yes        |
|     textProps      |                                                           Attributes applied to non-link Text components.                                                            |      TextProps      |    No    | Android/IOS |        Yes        |
|      truncate      |                                       Maximum length of URL link text. Possible values: `0` (disabled), `1+` (maximum length).                                       |       number        |    No    | Android/IOS |        Yes        |
|   truncateChars    |                                       Characters to replace truncated URL link text segments with (e.g. `github.com/../repo`)                                        |       string        |    No    | Android/IOS |        Yes        |
|  truncateLocation  |                                            Override truncation location. Possible values: `"smart"`, `"end"`, `"middle"`.                                            |       string        |    No    | Android/IOS |        Yes        |
|        url         |                                     Whether to link URLs. Possible values: `false` (disabled), `true`, `UrlConfig` (see below).                                      |  boolean or object  |    No    | Android/IOS |        Yes        |
|  useNativeSchemes  |                  Whether to use native app schemes (e.g. `twitter://`) rather than web URLs when linking to services for hashtag and mention links.                  |       boolean       |    No    | Android/IOS |        Yes        |

## Known Issues

## Others

## License

This project is licensed under [The MIT License](https://github.com/joshswan/react-native-autolink/blob/master/LICENSE).
