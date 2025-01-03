> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-size-matters</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/nirsky/react-native-size-matters">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/nirsky/react-native-size-matters/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/nirsky/react-native-size-matters)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-size-matters@0.4.2
```

#### **yarn**

```bash
yarn add react-native-size-matters@0.4.2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

**Basic usage**:

```js
<!---->
import { Text, View } from 'react-native';
import { scale, verticalScale, moderateScale, moderateVerticalScale } from 'react-native-size-matters';
import { s, vs, ms, mvs } from 'react-native-size-matters';

let scale = () =>{
    return (
        <View style={{
            width: scale(100),
            height: 100,
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{scale(100)}</Text>
        </View>
    )
}

let verticalScale = () =>{
    return (
        <View style={{
            width: 100,
            height: verticalScale(100),
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{verticalScale(100)}</Text>
        </View>
    )
}

let moderateScale = () =>{
    return (
    <View style={{
        width: 100,
        height: 100,
        padding: 5,
        borderWidth:moderateScale(10),
        borderColor: 'red',
        backgroundColor: 'blue'
    }} >
        <Text>borderWidth{moderateScale(10)}</Text>
    </View>
    )
}


let moderateVerticalScale = ()=>{
    return (
        <View style={{
            width: 100,
            height: moderateVerticalScale(100),
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{moderateVerticalScale(100)}</Text>
        </View>
    )
}

let s = () =>{
    return (
        <View style={{
            width: s(100),
            height: 100,
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{s(100)}</Text>
        </View>
    )
}

let vs = () =>{
    return (
        <View style={{
            width: 100,
            height: vs(100),
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{vs(100)}</Text>
        </View>
    )
}

let ms = () =>{
    return (
    <View style={{
        width: 100,
        height: 100,
        padding: 5,
        borderWidth:ms(10),
        borderColor: 'red',
        backgroundColor: 'blue'
    }} >
        <Text>borderWidth{ms(10)}</Text>
    </View>
    )
}


let mvs = ()=>{
    return (
        <View style={{
            width: 100,
            height: mvs(100),
            padding: 5,
            borderWidth: 1,
            borderColor: 'red',
            backgroundColor: 'blue'
        }} >
            <Text>{mvs(100)}</Text>
        </View>
    )
}

export default class sizeMattersDemo {
  render() {
    return (
        <>
            <Scale />
            <VerticalScale />
            <ModerateScale />
            <ModerateVerticalScale />
            <S />
            <Vs />
            <Ms />
            <Mvs />
        </>
    );
  }
}

```

**Annotation usage**:

```javascript
import { Text, View } from "react-native";
import { ScaledSheet } from "react-native-size-matters";

const styles = ScaledSheet.create({
  container: {
    width: "100@s", // = scale(100)
    height: "200@vs", // = verticalScale(200)
    padding: "2@msr", // = Math.round(moderateScale(2))
    margin: 5,
  },
});

export default class sizeMattersDemo {
  render() {
    return (
      <View style={styles.container}>
        <Text>create</Text>
      </View>
    );
  }
}
```

[!TIP] Here is displayed[Custom Default Size](https://github.com/nirsky/react-native-size-matters/blob/master/examples/change-guideline-sizes.md)

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.400; ROM: 3.0.0.25;
2. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71 (API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                                                                                                                                                            | Type     | Required | Platform     | HarmonyOS Support |
| --------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ------------ | ----------------- |
| scale                 | Returns the linear scaling result of the provided size based on the screen width of the device.                                                                                                                                  | Function | No       | Android, iOS| Yes               |
| verticalScale         | Returns the linear scaling result of the provided size based on the screen height of the device.                                                                                                                                  | Function | No       | Android, iOS| Yes               |
| moderateScale         | Scales the content that you do not want to scale in a linear manner. You can control the resize factor, which is 0.5 by default, as required. If normal scaling increases the size by 2X, **moderateScale** will only increase it by X.| Function | No       | Android, iOS| Yes               |
| moderateVerticalScale | Works in the same way as **moderateScale**, but uses **verticalScale** instead of **scale**.                                                                                                                            | Function | No       | Android, iOS| Yes               |
| s                     | Alias of the **scale** API.                                                                                                                                                                      | Function | No       | Android, iOS| Yes               |
| vs                    | Alias of the **verticalScale** API.                                                                                                                                                              | Function | No       | Android, iOS| Yes               |
| ms                    | Alias of the **moderateScale** API.                                                                                                                                                                | Function | No       | Android, iOS| Yes               |
| mvs                   | Alias of the **moderateVerticalScale** API.                                                                                                                                                      | Function | No       | Android, iOS| Yes               |

## Known Issues

## Others

## License

This project is licensed under [MIT License](https://github.com/nirsky/react-native-size-matters/blob/master/LICENSE).
