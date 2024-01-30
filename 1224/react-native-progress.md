> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>react-native-progress</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-progress/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```
yarn add  @react-native-oh-tpl/react-native-progress
```

#### **npm**

```bash
npm install  @react-native-oh-tpl/react-native-progress
```
<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useEffect } from 'react';
import { StyleSheet, View, Text } from 'react-native';
import * as Progress from 'react-native-progress';

const ProgressExample = () => {
  const [progress, setProgress] = React.useState(0);
  const [indeterminate, setIndeterminate] = React.useState(true);

  useEffect(() => {
    let interval: ReturnType<typeof setInterval>;
    const timer = setTimeout(() => {
      setIndeterminate(false);
      interval = setInterval(() => {
        setProgress((prevProgress) => {
          if (prevProgress >= 1) {
            return 0
          }
          return Math.min(1, prevProgress + Math.random() / 5)
        });
      }, 500);
    }, 1500);
    return () => {
      clearTimeout(timer);
      clearInterval(interval);
    };
  }, []);

  return (
    <View >
      <Text style={styles.welcome}>Progress Example</Text>
      <Progress.Bar
        style={styles.progress}
        progress={progress}
        indeterminate={indeterminate}
      />
      <View style={styles.circles}>
        <Progress.Circle
          style={styles.progress}
          progress={progress}
          indeterminate={indeterminate}
        />
        <Progress.Pie
          style={styles.progress}
          progress={progress}
          indeterminate={indeterminate}
        />
        <Progress.Circle
          style={styles.progress}
          progress={progress}
          indeterminate={indeterminate}
          direction="counter-clockwise"
        />
      </View>
      <View style={styles.circles}>
        <Progress.CircleSnail style={styles.progress} />
        <Progress.CircleSnail
          style={styles.progress}
          color={['#F44336', '#2196F3', '#009688']}
        />
      </View>
    </View >
  );
}
export default ProgressExample;

const styles = StyleSheet.create({
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  bar: {
    flexDirection: 'row',
    justifyContent: 'center',
  },
  circles: {
    flexDirection: 'row',
    justifyContent: 'center',
  },
  progress: {
    margin: 10,
  },
});
```

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/1224/react-native-svg.md#link)进行引入

## 兼容性

在以下版本验证通过
  1. IDE:4.1.3.500;
     SDK:4.1.0.57;
     测试设备：Mate60 (BAR-AL00);
     Rom:2.0.0.59(SP2DEVC00E59R4P1);
     RNOH:0.72.13。

## 属性
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-progress](https://github.com/oblador/react-native-progress)

### Properties for all progress components:

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- | -------- |
| animated |Whether or not to animate changes to `progress`. |boolean| No | All | Yes |
| indeterminate |If set to true, the indicator will spin and `progress` prop will be ignored. | boolean | No | All | Yes |
| indeterminateAnimationDuration |Sets animation duration in milliseconds when indeterminate is set. | number | No | All | Yes |
| progress |Progress of whatever the indicator is indicating. A number between 0 and 1. | number | No | All | Yes |
| color |Fill color of the indicator. | string | No | All | Yes |
| unfilledColor |Color of the remaining progress. | string | No | All | Yes |
| borderWidth |Width of outer border, set to `0` to remove. | number | No | All | Yes |
| borderColor |Color of outer border.| string | No | All | Yes |
### `Progress.Bar`:

All of the props under *Properties* in addition to the following:

| Name            | Description                                                  | Type                            | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ------------------------------- | -------- | -------- | ----------------- |
| width           | Full width of the progress bar, set to `null` to use automatic flexbox sizing. | number \| null                  | No       | All      | Yes               |
| height          | Height of the progress bar.                                  | number                          | No       | All      | Yes               |
| borderRadius    | Rounding of corners, set to `0` to disable.                  | number                          | No       | All      | Yes               |
| useNativeDriver | Use native driver for the animations.                        | boolean                         | No       | All      | Yes               |
| animationConfig | Config that is passed into the `Animated` function.          | function                        | No       | All      | Yes               |
| animationType   | Animation type to animate the progress, one of: `decay`, `timing`, `spring`. | 'decay' \| 'timing' \| 'spring' | No       | All      | Yes               |

### `Progress.Circle`:

All of the props under *Properties* in addition to the following:

| Name             | Description                                                  | Type                               | Required | Platform | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | ---------------------------------- | -------- | -------- | ----------------- |
| size             | Diameter of the circle.                                      | number                             | No       | All      | Yes               |
| endAngle         | Determines the endAngle of the circle. A number between `0` and `1`. The final endAngle would be the number multiplied by 2π | number                             | No       | All      | Yes               |
| thickness        | Thickness of the inner circle.                               | number                             | No       | All      | Yes               |
| showsText        | Whether or not to show a text representation of current progress. | boolean                            | No       | All      | Yes               |
| formatText       | A function returning a string to be displayed for the textual representation. | function                           | No       | All      | Yes               |
| textStyle        | Styles for progress text, defaults to a same `color` as circle and `fontSize` proportional to `size` prop. | TextStyle                          | No       | All      | Yes               |
| allowFontScaling | Whether or not to respect device font scale setting.         | boolean                            | No       | All      | Yes               |
| direction        | Direction of the circle `clockwise` or `counter-clockwise`.  | 'clockwise' \| 'counter-clockwise' | No       | All      | Yes               |
| strokeCap        | Stroke Cap style for the circle `butt`, `square` or `round`. | 'butt' \| 'square' \| 'round'      | No       | All      | Yes               |
| fill             | Fill color of the inner circle.                              | string                             | No       | All      | Yes               |

### `Progress.Pie`:

All of the props under *Properties* in addition to the following:

| Name | Description          | Type   | Required | Platform | HarmonyOS Support |
| ---- | -------------------- | ------ | -------- | -------- | ----------------- |
| size | Diameter of the pie. | number | No       | All      | Yes               |

### `Progress.CircleSnail`:

| Name             | Description                                                  | Type                               | Required | Platform | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | ---------------------------------- | -------- | -------- | ----------------- |
| animating        | If the circle should animate.                                | boolean                            | No       | All      | Yes               |
| hidesWhenStopped | If the circle should be removed when not animating.          | boolean                            | No       | All      | Yes               |
| size             | Diameter of the circle.                                      | number                             | No       | All      | Yes               |
| color            | Color of the circle, use an array of colors for rainbow effect. | string \| string[]                 | No       | All      | Yes               |
| thickness        | Thickness of the circle.                                     | number                             | No       | All      | Yes               |
| duration         | Duration of animation.                                       | number                             | No       | All      | Yes               |
| spinDuration     | Duration of spin (orbit) animation.                          | number                             | No       | All      | Yes               |
| strokeCap        | Stroke Cap style for the circle `butt`, `square` or `round`. | 'butt' \| 'square' \| 'round'      | No       | All      | Yes               |
| direction        | Direction in which the circle spins, either "clockwise" or "counter-clockwise" (default). | 'clockwise' \| 'counter-clockwise' | No       | All      | Yes               |

## 遗留问题

Progress.Circle中的属性fill在鸿蒙上默认显示黑色和默认无色不一致，定位是svg的属性配置有问题，当前通过修改Circle.js中默认fill的属性进行规避，后续svg修复该问题[issue#6](https://github.com/react-native-oh-library/react-native-svg/issues/6)后，修改的代码会移除。

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/oblador/react-native-progress/blob/master/LICENSE) ，请自由地享受和参与开源。
