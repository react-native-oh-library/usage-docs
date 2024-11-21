> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-flip-card</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/moschan/react-native-flip-card">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/moschan/react-native-flip-card/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/moschan/react-native-flip-card)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm i react-native-flip-card@3.5.7
```

#### **yarn**

```bash
yarn add react-native-flip-card@3.5.7
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import FlipCard from "react-native-flip-card";
import {
  Text,
  View,
  StyleSheet,
  ScrollView,
  TouchableOpacity,
} from "react-native";

export const FlipCardExample = () => {
  const styles = StyleSheet.create({
    container: {
      flex: 1,
      justifyContent: "center",
      alignItems: "center",
      backgroundColor: "#F5FCFF",
    },
    welcome: {
      fontSize: 20,
      textAlign: "center",
      margin: 10,
      marginTop: 20,
    },
    instructions: {
      textAlign: "center",
      color: "#333333",
      marginBottom: 5,
    },
    card: {
      width: 200,
      marginTop: 20,
    },
    face: {
      flex: 1,
      backgroundColor: "#2ecc71",
      justifyContent: "center",
      alignItems: "center",
    },
    back: {
      flex: 1,
      backgroundColor: "#f1c40f",
      justifyContent: "center",
      alignItems: "center",
    },
    button: {
      width: 100,
      height: 30,
      marginTop: 30,
      paddingTop: 6,
      paddingBottom: 6,
      borderRadius: 3,
      borderWidth: 1,
      backgroundColor: "#007AFF",
      borderColor: "transparent",
    },
    buttonText: {
      color: "#fff",
      textAlign: "center",
    },
    img: {
      flex: 1,
      height: 64,
    },
  });
  const [flip, setFlip] = useState(false);
  var CARDS = [1, 2, 3, 4, 5, 6, 7, 8, 9];
  const MyFlipCard = ({ val }) => {
    return (
      <View style={{ margin: 3 }}>
        <FlipCard style={styles.card}>
          <View style={styles.face}>
            <Text>Card {val}</Text>
          </View>
          <View style={styles.back}>
            <Text>The back side</Text>
          </View>
        </FlipCard>
      </View>
    );
  };
  const createCard = (val, i) => <MyFlipCard key={i} val={val} />;

  return (
    <View style={styles.container}>
      <ScrollView>
        <Text style={styles.welcome}>Flip Card Example</Text>
        <View>
          <Text style={styles.welcome}>Minimal</Text>
          <FlipCard style={{ marginBottom: 5 }}>
            <View style={styles.face}>
              <Text>The Face</Text>
            </View>
            <View style={styles.back}>
              <Text>The Back</Text>
            </View>
          </FlipCard>

          <Text style={styles.welcome}>Customized</Text>
          <FlipCard
            flip={flip}
            friction={3}
            perspective={500}
            flipHorizontal={true}
            flipVertical={false}
            clickable={true}
            style={styles.card}
            alignHeight={true}
            onFlipStart={(isFlipStart) => {
              console.log("isFlipStart", isFlipStart);
            }}
            useNativeDriver={true}
          >
            <View style={styles.face}>
              <Text>The Face</Text>
            </View>
            <View style={styles.back}>
              <Text style={{ fontSize: 50 }}> The Back </Text>
            </View>
          </FlipCard>
          <FlipCard
            flip={flip}
            friction={10}
            perspective={4000}
            flipHorizontal={false}
            flipVertical={true}
            clickable={true}
            style={styles.card}
            alignHeight={true}
            onFlipEnd={(isFlipEnd) => {
              console.log("isFlipEnd", isFlipEnd);
            }}
          >
            <View style={styles.face}>
              <Text>The Face</Text>
            </View>
            <View style={styles.back}>
              <Text>T</Text>
              <Text>h</Text>
              <Text>e</Text>
              <Text></Text>
              <Text>B</Text>
              <Text>a</Text>
              <Text>c</Text>
              <Text>k</Text>
            </View>
          </FlipCard>
        </View>
        <View>
          <TouchableOpacity
            style={styles.button}
            onPress={() => {
              setFlip({ flip: !flip });
            }}
          >
            <Text style={styles.buttonText}>Flip</Text>
          </TouchableOpacity>
        </View>
        <View>{CARDS.map(createCard)}</View>
      </ScrollView>
    </View>
  );
};
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.26; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.300SP2; ROM:3.0.0.24;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

### FlipCard

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.
>
> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

This library is a UI component library that achieves corresponding functionalities by configuring attribute tags.

| Name            | Type     | Description                                                                                                                     | Default | Required | Platform    | HarmonyOS Support |
| --------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| flip            | boolean  | If you change default display side, you can set true to this param. If you change side, you can pass bool variable dynamically. | false   | no       | iOS/Android | yes               |
| clickable       | boolean  | If you want to disable click a card, you can set false to this paramicon.                                                       | true    | no       | iOS/Android | yes               |
| friction        | number   | The friction of card animation                                                                                                  | 6       | no       | iOS/Android | yes               |
| perspective     | number   | The amount of perspective applied to the flip transformation                                                                    | 1000    | no       | iOS/Android | yes               |
| flipHorizontal  | boolean  | If you set true, a card flip to horizontal.                                                                                     | false   | no       | iOS/Android | yes               |
| flipVertical    | boolean  | If you set false, a card not flip to vertical. If you set true both flipHoriszontal and flipVertical , a card flip to diagonal. | true    | no       | iOS/Android | yes               |
| onFlipStart     | function | When a card starts a flip animation, call onFlipEnd function with param.                                                        | NA      | no       | iOS/Android | yes               |
| onFlipEnd       | function | When a card finishes a flip animation, call onFlipEnd function with param.                                                      | NA      | no       | iOS/Android | yes               |
| alignHeight     | boolean  | If you pass true to alignHeight param, the card keep height of bigger side.                                                     | false   | no       | iOS/Android | yes               |
| alignWidth      | boolean  | If you pass true to alignWidth param, the card keep width of bigger side.                                                       | false   | no       | iOS/Android | yes               |
| useNativeDriver | boolean  | If you pass true to useNativeDriver param, the card animation will utilize the native driver.                                   | true    | no       | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/moschan/react-native-flip-card/blob/master/LICENSE).
