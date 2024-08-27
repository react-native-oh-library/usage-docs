> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-redash</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wcandillon/react-native-redash">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wcandillon/react-native-redash/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/wcandillon/react-native-redash/)

## 安装与使用

#### **yarn**

```bash
yarn add react-native-redash@^18.1.3
```

#### **npm**

```bash
npm install react-native-redash@^18.1.3
```

<!-- tabs:end -->

> [!TIP] redash库依赖react-native-reanimated动画库， 请参照文档的Link章节进行引进。

下面的代码展示了这个库的基本使用场景：

```js
// findLastIndex 为例
import { mix,
  round,
  bin,
  cubicBezier,
  clamp,
  between,
  avg,
  toRad,
  toDeg} from 'react-native-redash/src/Math';
import {
  canvas2Cartesian,
  cartesian2Canvas,
  cartesian2Polar,
  polar2Cartesian
} from 'react-native-redash/src/Coordinates';
import * as redash from 'react-native-redash';

// 导出组件
export default function RadashDemo() {
  const [text, setText] = useState('');

  const onMix = () => {
      const mixre = mix(0, 10, 20);
      setText(mixre.toString())
  }

  const onRoundre = () => {
      const roundre = round(5.123, 0);
      setText(roundre.toString())
  }

  const onBinre = () => {
      const binre = bin(true);
      setText(binre.toString())
  }

  const onBetweenre = () => {
      const betweenre = between(-1, 0, 100);
      setText(betweenre.toString())
  }

  const onToRadre = () => {
      const toRadre = toRad(180);
      setText(toRadre.toString())
  }

  const onToDegre = () => {
      const toDegre = toDeg(Math.PI);
      setText(toDegre.toString())
  }

  const onClampre = () => {
      const clampre = clamp(-1, 0, 100)
      setText(clampre.toString())
  }

  const avgre = () => {
      const values: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
      const avgs = avg(values)
      setText(avgs.toString())
  }

  const cubicBezires = () => {
      const cubicBezire = cubicBezier(1, 0, 0.1, 0.1, 1)
      setText(cubicBezire.toString())
  }

  const handleCreatePath = () => {
      const vector = {
          x: 10,
          y: 20
      };
      setText(JSON.stringify(redash.createPath(vector)))
  }

  const handleAddCurvePath = () => {
      const vector = {
          x: 200,
          y: 100
      };
      const path = redash.createPath(vector);
      redash.addCurve(path, { c1: { x: 50, y: 50 }, c2: { x: 150, y: 50 }, to: { x: 150, y: 150 } });
      setText(JSON.stringify(path))
  }

  const handleClosePath = () => {
      const vector = {
          x: 200,
          y: 100
      };
      const path = redash.createPath(vector);
      redash.addCurve(path, { c1: { x: 50, y: 50 }, c2: { x: 150, y: 50 }, to: { x: 150, y: 150 } });
      redash.close(path);
      setText(JSON.stringify(path))
  }

  const handleSerializePath = () => {
      const vector = {
          x: 200,
          y: 100
      };
      const path = redash.createPath(vector);
      redash.addCurve(path, { c1: { x: 50, y: 50 }, c2: { x: 150, y: 50 }, to: { x: 150, y: 150 } });
      redash.close(path);
      const serializePath = redash.serialize(path);
      setText(serializePath)
  }

  const handleParsePath = () => {
      const vector = {
          x: 200,
          y: 100
      };
      const path = redash.createPath(vector);
      redash.addCurve(path, { c1: { x: 50, y: 50 }, c2: { x: 150, y: 50 }, to: { x: 150, y: 150 } });
      redash.close(path);
      const serializePath = redash.serialize(path);
      const parsePath = redash.parse(serializePath);
      setText(JSON.stringify(parsePath))
  }

  const handleInterpolatePath = () => {
      const inputRange = [0, 1];
      const outputRange = [
          {
              move: { x: 0, y: 0 },
              curves: [{ c1: { x: 1, y: 1 }, c2: { x: 2, y: 2 }, to: { x: 3, y: 3 } }],
              close: false,
          },
          {
              move: { x: 1, y: 1 },
              curves: [{ c1: { x: 2, y: 2 }, c2: { x: 3, y: 3 }, to: { x: 4, y: 4 } }],
              close: false,
          },
      ];
      const value = 0.5;
      const interpolatePath = redash.interpolatePath(value, inputRange, outputRange);
      setText(JSON.stringify(interpolatePath))
  }

  /** 处理canvas坐标转换为笛卡尔坐标 */
  const handleCanvas2Cartesian = () => {
      const point = canvas2Cartesian({ x: 500, y: 200 }, { x: 500, y: 200 });
      setText(JSON.stringify(point))
  }
  /** 处理笛卡尔坐标转换为canvas坐标 */
  const handleCartesian2Canvas = () => {
      const point = cartesian2Canvas({ x: -500, y: 200 }, { x: 500, y: 200 });
      setText(JSON.stringify(point))
  }
  /** 用于处理笛卡尔坐标转换为极坐标 */
  const handleCartesian2Polar = () => {
      const x = 0;
      const y = 100;
      const center = { x: 100, y: 100 };
      const { theta, radius } = cartesian2Polar(canvas2Cartesian({ x, y }, center));
      setText('theta ==' + theta + "  radius==" + radius);
  }

  /** 处理极坐标转换为笛卡尔坐标 */
  const handlePolar2Cartesian = () => {
      const x = 0;
      const y = 100;
      const center = { x: 100, y: 100 };
      const { theta, radius } = cartesian2Polar(canvas2Cartesian({ x, y }, center));
      const { x: x1, y: y1 } = cartesian2Canvas(
          polar2Cartesian({ theta, radius }),
          center
      );
      setText('x1 ==' + x1 + "  Math.round(y1)==" + Math.round(y1));
  }

  /** 用于处理极坐标转换为canvas坐标 */
  const handlePolar2Canvas = () => {
      const x = 0;
      const y = 100;
      const center = { x: 100, y: 100 };
      const { theta, radius } = cartesian2Polar(canvas2Cartesian({ x, y }, center));
      const point = polar2Canvas({ theta, radius }, center)
      setText(JSON.stringify(point))
  }

  // 用于处理canvas左边转换极坐标
  const handleCanvas2Polar = () => {
      const { theta, radius } = canvas2Polar({ x: -500, y: 200 }, { x: 500, y: 200 });
      setText('theta ==' + theta + "  radius==" + radius);
  }

  return (
    <View style={styles.container}>
      <View style={styles.inputArea}>
          <Text style={styles.baseText}>
              {text}
          </Text>
      </View>
      <ScrollView style={styles.scrollView}>
        <View style={{ flexDirection: 'column' }}>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>mix(0, 10, 20)</Text>
              <Button title='运行' color='#841584' onPress={onMix}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>round(5.123, 0)</Text>
              <Button title='运行' color='#841584' onPress={onRoundre}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>bin(true)</Text>
              <Button title='运行' color='#841584' onPress={onBinre}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>between(-1, 0, 100)</Text>
              <Button title='运行' color='#841584' onPress={onBetweenre}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>toRad(180)</Text>
              <Button title='运行' color='#841584' onPress={onToRadre}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>avg([1,2,3,4,5,6,7,8,9,10])</Text>
              <Button title='运行' color='#841584' onPress={avgre}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>cubicBezier(1, 0, 0.1, 0.1, 1)</Text>
              <Button title='运行' color='#841584' onPress={cubicBezires}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>toDeg(Math.PI)</Text>
              <Button title='运行' color='#841584' onPress={onToDegre}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>clamp(-1, 0, 100)</Text>
              <Button title='运行' color='#841584' onPress={onClampre}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>mix(0, 10, 20)</Text>
              <Button title='运行' color='#841584' onPress={handleCreatePath}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>addCurvePath</Text>
              <Button title='运行' color='#841584' onPress={handleAddCurvePath}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>closePath</Text>
              <Button title='运行' color='#841584' onPress={handleClosePath}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>serializePath</Text>
              <Button title='运行' color='#841584' onPress={handleSerializePath}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>parsePath</Text>
              <Button title='运行' color='#841584' onPress={handleParsePath}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>interpolatePath</Text>
              <Button title='运行' color='#841584' onPress={handleInterpolatePath}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>canvas2Cartesian</Text>
              <Button title='运行' color='#841584' onPress={handleCanvas2Cartesian}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>cartesian2Canvas</Text>
              <Button title='运行' color='#841584' onPress={handleCartesian2Canvas}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>cartesian2Polar</Text>
              <Button title='运行' color='#841584' onPress={handleCartesian2Polar}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>polar2Cartesian</Text>
              <Button title='运行' color='#841584' onPress={handlePolar2Cartesian}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>polar2Canvas</Text>
              <Button title='运行' color='#841584' onPress={handlePolar2Canvas}></Button>
          </View>
          <View style={styles.baseArea}>
              <Text style={{ flex: 1 }}>canvas2Polar</Text>
              <Button title='运行' color='#841584' onPress={handleCanvas2Polar}></Button>
          </View>
        </View>
      </ScrollView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
      width: '100%',
      flexDirection: 'column',
      alignItems: 'center',
      backgroundColor: '#F1F3F5',
  },
  baseText: {
      fontWeight: 'bold',
      textAlign: 'center',
      fontSize: 16
  },

  titleArea: {
      alignItems: 'center',
      flexDirection: 'row',
  },

  title: {
      width: '90%',
      color: '#000000',
      textAlign: 'left',
      fontSize: 30,
  },

  scrollView: {
      width: '90%',
      marginHorizontal: 20,
  },

  inputArea: {
      width: '90%',
      height: 30,
      borderWidth: 2,
      borderColor: '#000000',
      marginTop: 8,
      justifyContent: 'center',
      alignItems: 'center',
  },

  baseArea: {
      width: '100%',
      height: 60,
      borderRadius: 4,
      borderColor: '#000000',
      marginTop: 8,
      backgroundColor: '#FFFFFF',
      flexDirection: 'row',
      alignItems: 'center',
      paddingLeft: 8,
      paddingRight: 8
  }
});
```

动画演示示例

1.位置移动演示动画，通过snapPoint运行指定的位置地点

```js
import { snapPoint } from "react-native-redash/src/Physics";
import {
  useSharedValue,
  withSequence,
  withTiming,
  withRepeat,
} from "@react-native-oh-tpl/react-native-reanimated";

export default function RadashDemo() {
  const offset = useSharedValue(0);

  const translateAnimatedStyles = useAnimatedStyle(() => {
    return {
      transform: [
        {
          translateX: offset.value * 2,
        },
      ],
    };
  });

  const translate = () => {
    offset.value = withSequence(
      withTiming(-snapPoint(96, 600, [0, 125, 393]), { duration: 1000 }),
      withRepeat(
        withTiming(snapPoint(96, 600, [0, 125, 393]), { duration: 1000 }),
        60,
        true,
      ),
      withTiming(0, { duration: 50 }),
    );
  };

  return (
    <View style={styles.container}>
      <View style={styles.baseArea}>
        <View>
            <Animated.View style={[styles.box, translateAnimatedStyles]} />
        </View>
        <View style={{ flexDirection: 'row', alignItems: 'center' }}>
            <View style={{ marginRight: 10 }}>
                <Button color='#841584' onPress={() => handlePress()} title="snapPoint 开始" />
            </View>
            <View>
                <Button color='#841584' onPress={() => cancelAnimation(offset)} title="恢复" />
            </View>
        </View>
      </View>
    </View>
  );
}
```

2.颜色渐变动画演示，通过mixColor进行颜色渐变

```js
import { mixColor } from "react-native-redash/src/Colors";
import { useSharedValue } from "@react-native-oh-tpl/react-native-reanimated";

export default function RadashDemo() {
  const progress = useSharedValue(0);

  const colorAnimatedStyle = useAnimatedStyle(() => {
    return {
      backgroundColor: mixColor(progress.value, "#b58df1", "#38ffb3"),
    };
  });

  const handleColorPress = () => {
    progress.value = withRepeat(
      withTiming(1 - progress.value, { duration: 1000 }),
      60,
      true,
    );
  };


  return (
    <View style={styles.container}>
      <View style={styles.baseArea}>
        <View>
            <Animated.View style={[styles.box, translateAnimatedStyles]} />
        </View>
        <View style={{ flexDirection: 'row', alignItems: 'center' }}>
            <View style={{ marginRight: 10 }}>
                <Button color='#841584' onPress={() => handleColorPress()} title="mixColor 开始" />
            </View>
        </View>
      </View>
    </View>
  );
}
```

3.redash目前有两个动画辅助方法：useTiming、useSpring。useTiming可以使用贝塞尔曲线来进行运动,useSpring可以不将持续时间作为参数，而是由sprin物理特性作为运动轨迹。

```js
import { useTiming, useSpring } from "react-native-redash/src/Transitions";
import Animated from "@react-native-oh-tpl/react-native-reanimated";

export default function RadashDemo() {
  const timing = useSpring(255, { duration: 1000 });
  const spring = useTiming(255, { duration: 1000 });

  const customSpringStyles = useAnimatedStyle(() => {
    return {
      transform: [
        {
          translateX: spring.value,
        },
      ],
    };
  });

  const customTimingStyles = useAnimatedStyle(() => {
    return {
      transform: [
        {
          translateX: timing.value,
        },
      ],
    };
  });

  return (
    <View>
      <Animated.View style={[styles.box, defaultSpringStyles]} />
      <Animated.View style={[styles.box, defaultTimingStyles]} />
    </View>
  );
}
```

4.redash提供能接受字符串动画节点属性的文本组件

```js
import { ReText } from "react-native-redash";
import { useSharedValue } from "@react-native-oh-tpl/react-native-reanimated";

export default function RadashDemo() {
  const price = useSharedValue(42);
  const formattedPrice = useDerivedValue(() => `${price.value}`.toLocaleString());

  return (
    <View>
      <ReText
        text={formattedPrice}
        style={{
          color: "black",
          backgroundColor: "#38ffb3",
        }}
      />
    </View>
  );
}
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-reanimated 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-reanimated 文档的 Link 章节](/zh-cn/react-native-reanimated.md#link)进行引入

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.28; SDK：OpenHarmony(api12) 5.0.0.60; IDE：DevEco Studio 5.0.3.655; ROM：3.0.0.36;

## 静态方法
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

如下是已验证接口展示:

### **Animations**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| defineAnimation()             | This utility function enables you to declare custom animations that can be invoked on both the JS and UI thread.                                              | function | No       | iOS/Android               | yes               |
| animationParameter(animation) | Access animations passed as parameters safely on both the UI and JS thread with the proper static types. Animations can receive other animations as parameter | function | No       | iOS/Android               | yes               |
| withPause()                   | Make an animation pausable. The state of the animation (paused or not) is controlled by a boolean shared value.                                               | function | No       | iOS/Android               | yes               |
| withBouncing()                | Add a bouncing behavior to a physics-based animation. An animation is defined as being physics-based if it contains a velocity in its state.                  | function | No       | iOS/Android               | yes               |
### **Coordinates**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| canvas2Cartesian() | Convert plane coordinate system to Cadir coordinate system         | function | No       | iOS/Android               | yes               |
| cartesian2Canvas() | Convert Kadir coordinate system to plane coordinate system         | function | No       | iOS/Android               | yes               |
| cartesian2Polar()  | Conversion from Kadir coordinate system to polar coordinate system | function | No       | iOS/Android               | yes               |
| polar2Cartesian()  | Convert polar coordinate system to Cadir coordinate system         | function | No       | iOS/Android               | yes               |
| polar2Canvas()     | Convert polar coordinate system to Cadir coordinate system         | function | No       | iOS/Android               | yes               |
| canvas2Polar()     | Convert plane coordinate system to polar coordinate system         | function | No       | iOS/Android               | yes               |
### **Strings**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| ReText | This component is like <Text> but accepts a string animation node as property. Behind the scene, <ReText> is using <TextInput> with some default styling. Therefore there might be some slight inconsistencies with <Text>. | function | No       | iOS/Android               | yes               |
### **Math**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| mix()              | mix performs a linear interpolation between x and y using a to weight between them. The return value is computed as x _ (1 - value) + y _ value   | function       | No       | iOS/Android               | yes               |
| bin()              | Convert a boolean value into a number. This can be useful in reanimated since 0 and 1 are used for conditional statements.  | function | No       | iOS/Android               | yes               |
| toRad()            | Transforms an angle from degrees to radians| function | No       | iOS/Android               | yes               |
| toDeg()            | Transforms an angle from radians to degrees| function | No       | iOS/Android               | yes               |
| clamp()            | Clamps a node with a lower and upper bound  | function | No       | iOS/Android               | yes               |
| avg()              | Returns the average value of an array        | function | No       | iOS/Android               | yes               |
| between()          | Returns true if node is within lowerBound and upperBound| function | No       | iOS/Android               | yes               |
| round()            | Computes animation node rounded to precision  | function | No       | iOS/Android               | yes               |
| cubicBezier()      | Returns the coordinate of a cubic bezier curve. t is the length of the curve from 0 to 1. cubicBezier(0, p0, p1, p2, p3) equals p0 and cubicBezier(1, p0, p1, p2, p3) equals p3. p0 and p3 are respectively the starting and ending point of the curve. p1 and p2 are the control points. | function | No       | iOS/Android               | yes               |
| cubicBezierYForX() | Given a cubic Bèzier curve, return the y value for x  | function | No       | iOS/Android               | yes               |
### **Transitions**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| useTiming() | Transitions can attach an animation value to a change of React state. | function | No       | iOS/Android               | yes               |
| useSpring() | Transitions can attach an animation value to a change of React state. | function | No       | iOS/Android               | yes               |
### **Vectors**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| useVector() | Returns a vector of shared values. | function | No       | iOS/Android               | yes               |
### **Paths**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| createPath(path, {x, y})                             | Create a new path  | function | No       | iOS/Android               | yes               |
| addCurve(path, {c1: {x, y}, c2: {x, y}, to: {x, y}}) | Add a Bèzier curve command to a path | function | No       | iOS/Android               | yes               |
| close(path)                                          | Add a close command to a path | function | No       | iOS/Android               | yes               |
| parse(path)                                          | Parse an SVG path into a sequence of Bèzier curves. The SVG is normalized to have absolute values and to be approximated to a sequence of Bèzier curves. | function | No       | iOS/Android               | yes               |
| serialize(path)                                      | Serialize a path into an SVG path string | function | No       | iOS/Android               | yes               |
| interpolatePath()                                    | Interpolate between paths | function | No       | iOS/Android               | yes               |
### **Physics**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| snapPoint() | Select a point where the animation should snap to given the value of the gesture and it's velocity. | function | No       | iOS/Android               | yes               |
### **Colors**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| mixColor() | Identical to interpolateColor() but with an animation value that goes from 0 to 1. | function | No       | iOS/Android               | yes               |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wcandillon/react-native-redash/blob/master/LICENSE) ，请自由地享受和参与开源。
