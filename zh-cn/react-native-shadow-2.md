<!-- {% raw %} -->
> 模板版本：v0.2.0

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

> [!TIP] [Github 地址](https://github.com/SrBrahma/react-native-shadow-2)

## 安装与使用

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import { Text, ScrollView, View, StyleSheet } from "react-native";
import { Shadow } from "react-native-shadow-2";

function Shadow2Demo() {
  return (
    <ScrollView>
      <View style={styles.container}>
        <Text style={styles.title}>shadow2测试</Text>
        <View style={styles.sliders}>
          <Text style={styles.title}>base</Text>
          <Shadow>
            <Text style={styles.box}>base</Text>
          </Shadow>

          <Text style={styles.title}>startColor</Text>
          <Shadow startColor={"#eb9066d8"}>
            <Text style={styles.box}>startColor</Text>
          </Shadow>

          <Text style={styles.title}>endColor</Text>
          <Shadow endColor={"#ff00ff10"}>
            <Text style={styles.box}>endColor</Text>
          </Shadow>

          <Text style={styles.title}>distance</Text>
          <Shadow distance={50}>
            <Text style={styles.box}>distance</Text>
          </Shadow>

          {/* <Text style={styles.title}>offset</Text>
                    <Shadow offset={[10, 4]}>
                        <Text style={styles.box}>offset</Text>
                    </Shadow>

                    <Text style={styles.title}>paintInside</Text>
                    <Shadow style={styles.shadow} paintInside startColor={'#eb9066d8'} >
                        <Text style={styles.box}>paintInside</Text>
                    </Shadow>  */}

          <Text style={styles.title}>sides</Text>
          <Shadow
            style={styles.shadow}
            sides={{ start: false, end: true, top: false, bottom: false }}
            startColor={"#eb9066d8"}
          >
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
            startColor={"red"}
          >
            <Text style={styles.box}>corners</Text>
          </Shadow>

          <Text style={styles.title}>style</Text>
          <Shadow style={{ marginTop: 10 }}>
            <Text style={styles.box}>style</Text>
          </Shadow>

          <Text style={styles.title}>containerStyle</Text>
          <Shadow containerStyle={{ backgroundColor: "red" }}>
            <Text style={styles.box}>containerStyle</Text>
          </Shadow>

          <Text style={styles.title}>stretch</Text>
          <Shadow stretch>
            <Text style={styles.box}>stretch</Text>
          </Shadow>

          <View style={{ width: 200, height: 200 }}>
            <Text style={styles.title}>safeRender</Text>
            <Shadow distance={10} safeRender={true}>
              <Text
                style={{ width: "100%", height: "80%", backgroundColor: "red" }}
              >
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
    flexDirection: "column",
    justifyContent: "center",
    alignItems: "center",
  },
  sliders: {
    margin: 20,
    width: 280,
  },
  shadow: {
    marginBottom: 20,
  },
  text: {
    alignSelf: "center",
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
    flexDirection: "row",
    justifyContent: "space-around",
  },
});

export default Shadow2Demo;
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](/zh-cn/react-native-svg.md#link)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name           | Description                                                                                                                                                                                                                                        | Type                                                                    | Required | Platform | HarmonyOS Support |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | -------- | -------- | ----------------- |
| startColor     | The initial gradient color of the shadow.                                                                                                                                                                                                          | string                                                                  | No       | All      | yes               |
| endColor       | The final gradient color of the shadow.                                                                                                                                                                                                            | string                                                                  | No       | All      | yes               |
| distance       | How far the shadow goes.                                                                                                                                                                                                                           | number                                                                  | No       | All      | yes               |
| offset         | Moves the shadow. Negative x moves it left/start, negative y moves it up. Accepts 'x%' values. Defining this will default paintInside to true, as it's the usual desired behaviour.                                                                | [x: string \| number, y: string \| number]                              | No       | All      | no                |
| paintInside    | Apply the shadow below/inside the content. startColor is used as fill color, without a gradient. Useful when using offset or if your child has some transparency.                                                                                  | boolean                                                                 | No       | All      | no                |
| sides          | The sides that will have their shadows drawn. Doesn't include corners. Undefined sides fallbacks to true.                                                                                                                                          | Record<'start' \| 'end' \| 'top' \| 'bottom', boolean>                  | No       | All      | yes               |
| corners        | The corners that will have their shadows drawn. Undefined corners fallbacks to true.                                                                                                                                                               | Record<'topStart' \| 'topEnd' \| 'bottomStart' \| 'bottomEnd', boolean> | No       | android  | no                |
| style          | The style of the View that wraps your children.                                                                                                                                                                                                    | StyleProp<ViewStyle>                                                    | No       | All      | yes               |
| containerStyle | The style of the View that wraps the Shadow and your children. Useful for margins.                                                                                                                                                                 | StyleProp<ViewStyle>                                                    | No       | All      | yes               |
| stretch        | Make your children ocuppy all available horizontal space.                                                                                                                                                                                          | boolean                                                                 | No       | All      | yes               |
| safeRender     | Won't use the relative sizing and positioning on the 1st render but on the following renders with the exact onLayout sizes. Useful if dealing with radii greater than the sides sizes (like a circle) to avoid visual artifacts on the 1st render. | boolean                                                                 | No       | All      | yes               |
| disabled       | Disables the Shadow. Useful for easily reusing components as sometimes shadows are not desired. containerStyle and style are still applied.                                                                                                        | boolean                                                                 | No       | All      | yes               |

## 遗留问题

目前可使用的属性，具体见上面已列出。

- [ ] 由于react-native-shadow-2强依赖[`react-native-svg`](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg.md)库，但react-native-svg目前仅实现少部分属性，其余还未实现 HarmonyOS 化， 导致属性offset、paintInside、corners不可用问题: [issue#5](https://github.com/react-native-oh-library/react-native-svg/issues/5)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/SrBrahma/react-native-shadow-2/blob/main/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->