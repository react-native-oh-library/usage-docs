> Template version: v0.2.2



<p align="center">
  <h1 align="center"> <code>@freakycoder/react-native-bounceable</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/WrathChaos/react-native-bounceable">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://opensource.org/license/MIT">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [GitHub address](https://github.com/WrathChaos/react-native-bounceable)

## Installation and Usage

Go to the project directory and execute the following instruction:

###  npm

```bash
npm i @freakycoder/react-native-bounceable@1.0.3
```

### yarn

```
yarn add @freakycoder/react-native-bounceable@1.0.3
```

The following code shows the basic use scenario of the repository:

1、引入库文件

```jsx
import RNBounceable from "@freakycoder/react-native-bounceable";
```

2、使用场景：

您可以将**任何子组件**放入 **RNBounceable** 组件中，当它被按下时，它会使其反弹

```jsx
<RNBounceable onPress={() => {}}>
  <View style={styles.bounceButtonStyle}>
    <Text style={styles.bounceButtonTextStyle}>Bounce</Text>
  </View>
</RNBounceable>
```

详细使用场景

```javascript
import React from 'react';
import type { PropsWithChildren } from 'react';
import { StyleSheet, View, Text }from 'react-native';
import RNBounceable from "@freakycoder/react-native-bounceable";

let flag:boolean = true;
export function BounceableExample () {
    const customStyle = {
        backgroundColor: 'red',
        padding: 10,
        borderRadius: 100,
        alignItems: 'center',
        justifyContent: 'center',
      };
    
    <RNBounceable
    style={[customStyle, styles.bounceStyle]}
    onPress = {onPress}
    bounceEffectIn={0.1}
    bounceEffectOut={1.5}
    bounceVelocityIn={60}
    bounceVelocityOut={70}
    bouncinessIn={50}
    bouncinessOut={50}
    >
    	<Text style={styles.textStyle}>Press Me</Text>
    </RNBounceable>
}

const styles = StyleSheet.create({
    container: {
      width: '100%',
      height: '100%',
    },
    bounceStyle: {
      backgroundColor: 'lightblue'
    },
    textStyle: {
      fontSize: 20,
      color: 'red',
    },
  });
```



## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.28; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.500; ROM：5.0.0.31;

## Properties And Static Methods (If Any)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Property          | Description                                                  |   Type   | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | :------: | :------: | ----------- | ----------------- |
| bounceEffectIn    | change the bounce effect's value（reduce）                   |  number  |    no    | iOS/Android | yes               |
| bounceEffectOut   | change the bounce effect's value（amplification）            |  number  |    no    | iOS/Android | yes               |
| bounceVelocityIn  | The speed of the press                                       |  number  |    no    | iOS/Android | yes               |
| bounceVelocityOut | The speed at which it is released                            |  number  |    no    | iOS/Android | yes               |
| bouncinessIn      | Elastic coefficient when pressed (set value 0-50 has obvious effect display) |  number  |    no    | iOS/Android | yes               |
| bouncinessOut     | Elastic coefficient when released (set value 0-50 has obvious effect display) |  number  |    no    | iOS/Android | yes               |
| onPress           | set your own logic for the onPress functionality             | function |    no    | iOS/Android | yes               |
| style             | set the style like any other View container                  |  style   |    no    | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://opensource.org/license/MIT).
