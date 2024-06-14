> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>rn-tourguide</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/xcarpentier/rn-tourguide">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/xcarpentier/rn-tourguide/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
         <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/rn-tourguide)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[https://github.com/react-native-oh-library/rn-tourguide Releases](https://github.com/react-native-oh-library/rn-tourguide/releases)，并下载适用版本的 tgz 包

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/rn-tourguide@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/rn-tourguide@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import * as React from 'react'
import {
  Image,
  Platform,
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
} from 'react-native'
import {
  TourGuideProvider,
  TourGuideZone,
  TourGuideZoneByPosition,
  useTourGuideController
} from 'rn-tourguide'

const uri =
  'https://pbs.twimg.com/profile_images/1223192265969016833/U8AX9Lfn_400x400.jpg'

export default function () {
  return (
    <TourGuideProvider {...{ borderRadius: 16, androidStatusBarVisible: true }}>
      <AppContent />
    </TourGuideProvider>
  )
}

const AppContent = () => {
  const iconProps = { size: 40, color: '#888' }

  const { start, canStart, stop, eventEmitter } = useTourGuideController()

  React.useEffect(() => {
    if (canStart) {
      start()
    }
  }, [canStart]) 

  React.useEffect(() => {
    eventEmitter.on('start', () => console.log('start'))
    eventEmitter.on('stop', () => console.log('stop'))
    eventEmitter.on('stepChange', () => console.log(`stepChange`))
    return () => eventEmitter.off('*', null)
  }, [])
  return (
    <View style={styles.container}>
      <TourGuideZone
        keepTooltipPosition
        zone={1}
        text={'A react-native-copilot remastered! 🎉'}
        borderRadius={16}
      >
        <Text style={styles.title}>
          {'Welcome to the demo of\n"rn-tourguide"'}
        </Text>
      </TourGuideZone>
      <View style={styles.middleView}>
        <TouchableOpacity style={styles.button} onPress={() => start()}>
          <Text style={styles.buttonText}>START THE TUTORIAL!</Text>
        </TouchableOpacity>

        <TourGuideZone zone={2} shape={'rectangle_and_keep'}>
          <TouchableOpacity style={styles.button} onPress={() => start(4)}>
            <Text style={styles.buttonText}>Step 4</Text>
          </TouchableOpacity>
        </TourGuideZone>
        <TouchableOpacity style={styles.button} onPress={() => start(2)}>
          <Text style={styles.buttonText}>Step 2</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.button} onPress={stop}>
          <Text style={styles.buttonText}>Stop</Text>
        </TouchableOpacity>
        <TourGuideZone
          zone={6}
          shape='circle'
          text={'With animated SVG morphing with awesome flubber 🍮💯'}
        >
          <Image source={{uri}} style={styles.profilePhoto} />
        </TourGuideZone>
      </View>
      <View style={styles.row}>
        <TourGuideZone zone={3} shape={'circle'} tooltipBottomOffset={200}>
          <Text style={styles.text}>Text1</Text>
        </TourGuideZone>
        <Text style={styles.text}>Text2</Text>
        <Text style={styles.text}>Text3</Text>
     
        <TourGuideZone zone={4} shape={'rectangle'}>
          <Text style={styles.text}>Text4</Text>
        </TourGuideZone>
        <TourGuideZone zone={5} shape={'circle'}>
          <Text style={styles.text}>Text5</Text>
        </TourGuideZone>
      </View>
      {Platform.OS !== 'web' ? (
        <TourGuideZoneByPosition
          zone={1}
          shape={'circle'}
          isTourGuide
          top={250}
          left={50}
          width={64}
          height={64}
        />
      ) : null}
    </View>
  )
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff',
    alignItems: 'center',
    paddingTop: 40,
  },
  title: {
    fontSize: 24,
    textAlign: 'center',
  },
  profilePhoto: {
    width: 140,
    height: 140,
    borderRadius: 70,
    marginVertical: 20,
  },
  middleView: {
    flex: 1,
    alignItems: 'center',
  },
  button: {
    backgroundColor: '#2980b9',
    paddingVertical: 10,
    paddingHorizontal: 15,
    margin: 2,
  },
  buttonText: {
    color: 'white',
    fontSize: 16,
  },
  row: {
    width: '100%',
    padding: 15,
    flexDirection: 'row',
    justifyContent: 'space-between',
  },
  text: {
    fontSize: 20,
  }
})

```

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg-capi.md#link)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/rn-tourguide Releases](https://github.com/react-native-oh-library/rn-tourguide/releases)

## 属性

详情见[rn-tourguide](https://github.com/xcarpentier/rn-tourguide)

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### TourGuideProvider
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| tooltipComponent  |  tooltip component       | React.ComponentType<TooltipProps>  | YES | ALL      | YES |
| tooltipStyle  |   tooltip style      | StyleProp<ViewStyle>  | YES | ALL      | YES |
| labels  |   Button text display in tooltip(skip、previous、next、finish)      | Labels | YES | ALL      | YES |
| startAtMount  |         | boolean/string | YES | ALL      | YES |
| androidStatusBarVisible  | android status bar visible        | boolean | YES | Android      | NO |
| backdropColor  |   background color | string | YES | ALL      | YES |
| verticalOffset |  vertical offset | number | YES | ALL      | YES |
| wrapperStyle  |   wrap style    | StyleProp<ViewStyle> | YES | ALL      | YES |
| maskOffset  |  offset around zone | number | YES | ALL      | YES |
| borderRadius  |    round corner when rectangle | number | YES | ALL      | YES |
| animationDuration  |  Animation duration | number | YES | ALL      | YES |
| children  |  React.ReactNode components      | React.ReactNode | YES | ALL      | YES |
| dismissOnPress  |  whether to display touchable | boolean | YES | ALL      | YES |
| preventOutsideInteraction  |    Block default events | boolean | YES | ALL      | YES |

### TourGuideZone
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| zone  | A positive number indicating the order of the step in the entire walkthrough.        | number  | YES | ALL      | YES |
| tourKey  |        | string  | YES | ALL      | YES |
| isTourGuide  |  return children without wrapping id false        | boolean  | YES | ALL      | YES |
| text  |     text in tooltip     | string  | YES | ALL      | YES |
| shape  |     which shape     | Shape  | YES | ALL      | YES |
| maskOffset  |   offset around zone    | number  | YES | ALL      | YES |
| borderRadius  |   round corner when rectangle      | number  | YES | ALL      | YES |
| children  |   React.ReactNode components       | React.ReactNode  | YES | ALL      | YES |
| style  |         | StyleProp<ViewStyle>  | YES | ALL      | YES |
| keepTooltipPosition  |  tooltip positioning    | boolean  | YES | ALL      | YES |
| tooltipBottomOffset  |   The distance between the tooltip and the bottom of the container      | number  | YES | ALL      | YES |
| borderRadiusObject  |   Mask layer highlight area rounded corner settings      | BorderRadiusObject  | YES | ALL      | YES |

### Tooltip
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| isFirstStep  | Is it the first step | boolean  | YES | ALL      | YES |
| isLastStep  |  Is it the last step   | boolean  | YES | ALL      | YES |
| currentStep  |  current step | IStep  | YES | ALL      | YES |
| labels  |     Button text display in tooltip(skip、previous、next、finish)     | Labels  | YES | ALL      | YES |
| handleNext  |  A function that handle next step  | Function  | YES | ALL      | YES
| handlePrev  |  A function that handle prev step     | Function  | YES | ALL      | YES
| handleStop  |  A function that handle stop       | Function  | YES | ALL      | YES

### TourGuideZoneByPosition
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| zone  |         | number  | YES | ALL      | YES |
| tourKey  |         | string  | YES | ALL      | YES |
| isTourGuide  |  return children without wrapping id false        | boolean  | YES | ALL      | YES |
| top  |   tour guide zone distance from top    | number/string  | YES | ALL      | YES |
| left  | tour guide zone distance from left        | number/string  | YES | ALL      | YES |
| right  |   tour guide zone distance from right      | number/string  | YES | ALL      | YES |
| bottom  |  tour guide zone distance from bottom       | number/string  | YES | ALL      | YES |
| width  |   The width of the highlight area of ​​the mask layer  | number/string  | YES | ALL      | YES |
| height  |     The height of the highlight area of ​​the mask layer    | number/string  | YES | ALL      | YES |
| shape  |   which shape      | Shape  | YES | ALL      | YES |
| borderRadiusObject  |   Mask layer highlight area rounded corner settings      | BorderRadiusObject  | YES | ALL      | YES |
| containerStyle  |   Mask layer wrapping layer style      | StyleProp<ViewStyle>  | YES | ALL      | YES |
| keepTooltipPosition  |   tooltip positioning       | boolean  | YES | ALL      | YES |
| tooltipBottomOffset  |   The distance between the tooltip and the bottom of the container      | number  | YES | ALL      | YES |
| text  |    text in tooltip     | string  | YES | ALL      | YES |

### useTourGuideController
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| start  | start tour guide         | Funtion  | YES | ALL      | YES |
| eventEmitter  | event emitter           | Funtion/undefined  | YES | ALL      | YES |
| getCurrentStep  | Get the mask layer pop-up component         | Funtion/undefined  | YES | ALL      | YES |
| canStart  | whether to support  tour guide         | boolean/undefined  | YES | ALL      | YES |
| tourKey  | tour guide key         | string  | YES | ALL      | YES |
| TourGuideZone  | boot area         | Funtion  | YES | ALL      | YES |
| TourGuideZoneByPosition  | tourGuide area location | Funtion  | YES | ALL      | YES |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/xcarpentier/rn-tourguide/blob/master/LICENSE) ，请自由地享受和参与开源。
