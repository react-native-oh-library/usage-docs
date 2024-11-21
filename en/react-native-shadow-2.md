> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-shadow-2</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/SrBrahma/react-native-shadow-2">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/SrBrahma/react-native-shadow-2/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/SrBrahma/react-native-shadow-2)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-shadow-2@7.0.8
```

#### **yarn**

```bash
yarn add react-native-shadow-2@7.0.8
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import {Text, ScrollView, View, StyleSheet} from 'react-native';
import {Shadow} from 'react-native-shadow-2';

export function Shadow2Demo() {
  return (
    <ScrollView>
      <View style={styles.container}>
        <Text style={styles.title}>shadow2</Text>
        <View style={styles.sliders}>
          <Text style={styles.title}>base</Text>
          <Shadow>
            <Text style={styles.box}>base</Text>
          </Shadow>

          <Text style={styles.title}>startColor</Text>
          <Shadow startColor={'#eb9066d8'}>
            <Text style={styles.box}>startColor</Text>
          </Shadow>

          <Text style={styles.title}>endColor</Text>
          <Shadow endColor={'#ff00ff10'}>
            <Text style={styles.box}>endColor</Text>
          </Shadow>

          <Text style={styles.title}>distance</Text>
          <Shadow distance={50}>
            <Text style={styles.box}>distance</Text>
          </Shadow>

          <Text style={styles.title}>offset</Text>
          <Shadow offset={[50, 4]}>
            <Text style={styles.box}>offset</Text>
          </Shadow>

          <Text style={styles.title}>paintInside</Text>
          <Shadow style={styles.shadow} paintInside startColor={'#eb9066d8'}>
            <Text style={styles.box}>paintInside</Text>
          </Shadow>

          <Text style={styles.title}>sides</Text>
          <Shadow
            style={styles.shadow}
            sides={{start: false, end: true, top: false, bottom: false}}
            startColor={'#eb9066d8'}>
            <Text style={styles.box}>sides</Text>
          </Shadow>

          <Text style={styles.title}>corners</Text>
          <Shadow
            style={styles.shadow}
            distance={20}
            corners={{
              topStart: false,
              topEnd: false,
              bottomStart: true,
              bottomEnd: false,
            }}
            startColor={'red'}>
            <Text style={styles.box}>corners</Text>
          </Shadow>

          <Text style={styles.title}>style</Text>
          <Shadow style={{backgroundColor: 'red'}}>
            <Text style={styles.box}>style</Text>
          </Shadow>

          <Text style={styles.title}>containerStyle</Text>
          <Shadow containerStyle={{backgroundColor: 'red'}}>
            <Text style={styles.box}>containerStyle</Text>
          </Shadow>

          <Text style={styles.title}>stretch</Text>
          <Shadow stretch>
            <Text style={styles.box}>stretch</Text>
          </Shadow>

          <View style={{width: 200, height: 200}}>
            <Text style={styles.title}>safeRender</Text>
            <Shadow distance={10} safeRender={true}>
              <Text
                style={{width: '100%', height: '80%', backgroundColor: 'red'}}>
                shadow
              </Text>
            </Shadow>
          </View>

          <Text style={styles.title}>disabled</Text>
          <Shadow disabled>
            <Text style={styles.box}>disabled</Text>
          </Shadow>
        </View>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'column',
    justifyContent: 'center',
    alignItems: 'center',
  },
  sliders: {
    margin: 20,
    width: 280,
  },
  shadow: {
    marginBottom: 20,
  },
  text: {
    alignSelf: 'center',
    paddingVertical: 20,
  },
  title: {
    fontSize: 30,
    marginTop: 20,
  },
  box: {
    margin: 20,
    fontSize: 16,
  },
  sliderOne: {
    flexDirection: 'row',
    justifyContent: 'space-around',
  },
});

```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in @react-native-oh-tpl/react-native-svg to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.27; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25 (API Version 12 Canary4); IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name           | Description                                                  | Type                                                         | Required | Platform | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| startColor     | The initial gradient color of the shadow.                    | string                                                       | no       | All      | yes               |
| endColor       | The final gradient color of the shadow.                      | string                                                       | no       | All      | yes               |
| distance       | How far the shadow goes.                                     | number                                                       | no       | All      | yes               |
| offset         | Moves the shadow. Negative x moves it left/start, negative y moves it up. Accepts 'x%' values. Defining this will default paintInside to true, as it's the usual desired behaviour. | [x: string \| number, y: string \| number]                   | no       | All      | yes               |
| paintInside    | Apply the shadow below/inside the content. startColor is used as fill color, without a gradient. Useful when using offset or if your child has some transparency. | boolean                                                      | no       | All      | yes               |
| sides          | The sides that will have their shadows drawn. Doesn't include corners. Undefined sides fallbacks to true. | Record<'start' \| 'end' \| 'top' \| 'bottom', boolean>       | no       | All      | yes               |
| corners        | The corners that will have their shadows drawn. Undefined corners fallbacks to true. | Record<'topStart' \| 'topEnd' \| 'bottomStart' \| 'bottomEnd', boolean> | no       | Android  | yes               |
| style          | The style of the View that wraps your children.              | StyleProp<ViewStyle>                                         | no       | All      | yes               |
| containerStyle | The style of the View that wraps the Shadow and your children. Useful for margins. | StyleProp<ViewStyle>                                         | no       | All      | yes               |
| stretch        | Make your children ocuppy all available horizontal space.    | boolean                                                      | no       | All      | yes               |
| safeRender     | Won't use the relative sizing and positioning on the 1st render but on the following renders with the exact onLayout sizes. Useful if dealing with radii greater than the sides sizes (like a circle) to avoid visual artifacts on the 1st render. | boolean                                                      | no       | All      | yes               |
| disabled       | Disables the Shadow. Useful for easily reusing components as sometimes shadows are not desired. containerStyle and style are still applied. | boolean                                                      | no       | All      | yes               |

## Known Issues

The currently available properties are specifically listed above.

- [x] Due to the strong dependency of react-native-shadow-2 on the [`react-native-svg`](https://react-native-oh-library.gitee.io/usage-docs/#/zh-cn/react-native-svg)library，and the current limited implementation of react-native-svg on HarmonyOS, only a small number of properties are available， Consequently, properties such as offset, paintInside, and corners are not yet supported, leading to issues as documented in: [issue#5](https://github.com/react-native-oh-library/react-native-svg/issues/5)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/SrBrahma/react-native-shadow-2/blob/main/LICENSE).
