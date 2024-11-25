> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-typing-animation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/watadarkstar/react-native-typing-animation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/watadarkstar/react-native-typing-animation/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/watadarkstar/react-native-typing-animation)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-typing-animation@0.1.7
```

#### **yarn**

```bash
yarn add react-native-typing-animation@0.1.7
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React, { useEffect, useRef, useState } from 'react';
import {
  Animated,
  View,
  Text,
  PanResponder,
  Button,
  StyleSheet,
  TouchableHighlight,
  Alert,
  TouchableOpacity,
  ScrollView,
} from 'react-native';
import { TestSuite, Tester, TestCase } from '@rnoh/testerino';
import { TypingAnimation } from 'react-native-typing-animation';

const TypingAnimationDemos = () => {
  const typingAnimationProps = [
    {
      key: 'dotColor',
      value: {
        dotColor: 'green'
      }
    },
    {
      key: 'dotColor',
      value: {
        dotColor: 'red'
      }
    },
    {
      key: 'dotRadius',
      value: {
        dotRadius: 5
      }
    },
    {
      key: 'dotRadius',
      value: {
        dotRadius: 10
      }
    },
    {
      key: 'dotMargin',
      value: {
        dotMargin: 10
      }
    },
    {
      key: 'dotMargin',
      value: {
        dotMargin: 15
      }
    },
    {
      key: 'dotAmplitude',
      value: {
        dotAmplitude: 1
      }
    },
    {
      key: 'dotAmplitude',
      value: {
        dotAmplitude: 1
      }
    },
    {
      key: 'dotSpeed',
      value: {
        dotSpeed: 10
      }
    },
    {
      key: 'dotSpeed',
      value: {
        dotSpeed: 0.5
      }
    },
    {
      key: 'dotY',
      value: {
        dotY: 30
      }
    },
    {
      key: 'dotY',
      value: {
        dotY: 20
      }
    },
    {
      key: 'dotX',
      value: {
        dotX: 12
      }
    },
    {
      key: 'dotX',
      value: {
        dotX: 15
      },
    },
  ];
  return (
    <ScrollView>
      <Tester>
        {typingAnimationProps.map((item) => {
          return (

            <TestCase itShould={item.key} tags={['C_API']}>
              <View
                style={{
                  height: 30,
                  display: 'flex',
                  flexDirection: 'row',
                  justifyContent: 'center',
                }}>
                <TypingAnimation
                  {...item.value}
                ></TypingAnimation>
              </View>
            </TestCase>
          );
        })}
      </Tester>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: 'white',
  },
  button: {
    backgroundColor: 'blue',
    paddingHorizontal: 20,
    paddingVertical: 10,
    borderRadius: 5,
    marginBottom: 20,
  },
  buttonText: {
    color: 'white',
    fontSize: 16,
  },
  animationContainer: {
    alignItems: 'center',
  },
  text: {
    fontSize: 20,
    marginBottom: 20,
  },
  typingAnimation: {
    flexDirection: 'row',
  },
});

export default TypingAnimationDemos;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1.RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

2.RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|     Name     |                         Description                          |  Type   | Required |  Platform   | HarmonyOS Support |
| :----------: | :----------------------------------------------------------: | :-----: | :------: | :---------: | :---------------: |
|    style     |              Container styles; default is `{}`               | Object  |    No    | Android/ios |        Yes        |
|   dotColor   |             Dot color; default is `#000` (black)             | String  |    No    | Android/ios |        Yes        |
|  dotStyles   |                 Dot styles; default is `{}`                  | Object  |    No    |   Android   |        No         |
|  dotRadius   |                 Dot radius; default is `2.5`                 | Integer |    No    | Android/ios |        Yes        |
|  dotMargin   |      Dot margin, the space between dots; default is `3`      | Integer |    No    | Android/ios |        Yes        |
| dotAmplitude |                Dot amplitude; default is `3`                 | Integer |    No    | Android/ios |        Yes        |
|   dotSpeed   | Dot speed, the speed of the whole animation view; default is `0.15` | Integer |    No    | Android/ios |        Yes        |
|     dotY     |        Dot y, the starting y coordinate; default is 6        | Integer |    No    | Android/ios |        Yes        |
|     dotX     |  Dot x, the x coordinate of the center dot; default is `12`  | Integer |    No    | Android/ios |        Yes        |
|     show     |  Visibility, whether the whole animation view is displayed or not; default is true  | Boolean |    No    | Android/ios |        Yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于  [The MIT License (MIT)](https://github.com/watadarkstar/react-native-typing-animation/blob/master/LICENSE) ，请自由地享受和参与开源。

