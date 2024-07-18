>  模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-tts</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ak1394/react-native-tts">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20Windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ak1394/react-native-tts/blob/master/README.md#license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-tts)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-tts Releases](https://github.com/react-native-oh-library/react-native-tts/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-tts@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-tts@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import {useState, useCallback} from 'react';
import {Text, View, StyleSheet, SafeAreaView} from 'react-native';
import Tts from 'react-native-tts';

const cnText = `炎炎夏日，阳光如烈火般炙烤大地，空气中弥漫着热浪的气息。树荫下，蝉鸣声如同热浪中跳跃的音符，微风吹过，带来一丝清凉。远处的田野上，金黄的麦浪随风起伏，仿佛在舞动着夏天的节奏。天空湛蓝如洗，白云悠然飘过，似是一幅宁静而美丽的夏日画卷。`;

export function TTSDemo() {
  const [speakText, setSpeakText] = useState<string>(cnText);

  const addEvent = useCallback(() => {
    Tts.addEventListener('tts-start', res => {
      console.log('tts-start', res);
    });
  }, []);

  const removeEvent = useCallback(() => {
    Tts.addEventListener('tts-start', res => {
      console.log('tts-start', res);
    });
  }, []);

  const stopSpeak = useCallback(() => {
    Tts.stop();
  }, []);

  const speakFc = useCallback(() => {
    Tts.speak(speakText);
  }, []);

  const getInitStatus = useCallback(() => {
    Tts.getInitStatus().then(() => {
      console.log('初始化已完成');
    });
  }, []);

  const pauseFc = useCallback(() => {
    Tts.pause();
  }, []);

  const resumeFc = useCallback(() => {
    Tts.resume();
  }, []);

  const setSpeakRate = useCallback(() => {
    Tts.setDefaultRate(2);
  }, []);

  const setSpeakPitch = useCallback(() => {
    Tts.setDefaultPitch(2);
  }, []);

  const queryVoices = useCallback(() => {
    Tts.voices().then(res => {
      const resTr = JSON.stringify(res);
      setSpeakText(resTr);
    });
  }, []);

  return (
    <>
      <SafeAreaView style={styles.constainer}>
        <Text style={styles.title}>react-native-tts功能验证</Text>
        <View style={styles.content}>
          <View style={styles.btnWrap}>
            <Text style={styles.button} onPress={getInitStatus}>
              getInitStatus
            </Text>
            <Text style={styles.button} onPress={speakFc}>
              speak（zh）
            </Text>
            <Text style={styles.button} onPress={stopSpeak}>
              stop
            </Text>
            <Text style={styles.button} onPress={pauseFc}>
              pause
            </Text>
            <Text style={styles.button} onPress={resumeFc}>
              resume
            </Text>
            <Text style={styles.button} onPress={setSpeakRate}>
              setDefaultRate
            </Text>
            <Text style={styles.button} onPress={setSpeakPitch}>
              setDefaultPitch
            </Text>
            <Text style={styles.button} onPress={queryVoices}>
              voices
            </Text>
            <Text style={styles.button} onPress={addEvent}>
              addEventListener
            </Text>
            <Text style={styles.button} onPress={removeEvent}>
              removeEventListener
            </Text>
          </View>
        </View>
      </SafeAreaView>
    </>
  );
}

const styles = StyleSheet.create({
  constainer: {
    flex: 1,
  },
  content: {
    flex: 1,
    display: 'flex',
  },
  btnWrap: {
    width: 'auto',
    backgroundColor: 'gray',
    display: 'flex',
    flexDirection: 'row',
    flexWrap: 'wrap',
    paddingLeft: 20,
  },
  text: {
    padding: 20,
    fontSize: 20,
  },
  title: {
    padding: 10,
    fontSize: 30,
    textAlign: 'center',
  },
  button: {
    paddingVertical: 6,
    paddingHorizontal: 12,
    backgroundColor: 'hsl(193, 95%, 68%)',
    borderWidth: 2,
    borderColor: 'hsl(193, 95%, 30%)',
  },
});

```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-tts": "file:../../node_modules/@react-native-oh-tpl/react-native-tts/harmony/rn_tts.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 在 ArkTs 侧引入 RNTTSPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...

+   import { RNTTSPackage } from '@react-native-oh-tpl/react-native-tts/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNTTSPackage(ctx)
  ];
}
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-tts Releases](https://github.com/react-native-oh-library/react-native-tts/releases)

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                             | Type     | Required | Platform | HarmonyOS Support |
| --------------------- | ----------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| getInitStatus         | Returns a promise that resolves when the TTS engine is initialized.     | Function | no     | All    | yes            |
| requestInstallEngine  | Requests installation of the TTS engine if not already installed.       | Function | no     | Android | no                |
| requestInstallData    | Requests installation of the TTS data if not already installed.         | Function | no     | Android | no                |
| setDucking            | Sets whether the TTS engine should duck other audio when speaking.      | Function | no     | All      | no                |
| setDefaultEngine      | Sets the default TTS engine.                                            | Function | no     | Android | no                |
| setDefaultVoice       | Sets the default voice for the TTS engine.                              | Function | no     | All      | no                |
| setDefaultRate        | Sets the default speech rate for the TTS engine.                        | Function | no     | All      | yes               |
| setDefaultPitch       | Sets the default pitch for the TTS engine.                              | Function | no     | All      | yes               |
| setDefaultLanguage    | Sets the default language for the TTS engine.                           | Function | no     | All      | no                |
| setIgnoreSilentSwitch | Sets whether to ignore the silent button.                 | Function | no    | iOS |no|
| voices                | Retrieves a list of available voices from the TTS engine.               | Function | no     | All      | yes               |
| engines               | Retrieves a list of available TTS engines.                              | Function | no     | Android | no                |
| speak                 | Speaks the given utterance and returns a promise with the utterance ID. | Function | no     | All      | yes               |
| stop                  | Stops the current TTS utterance.                                        | Function | no     | All      | yes               |
| pause                 | Pause the current TTS utterance.                                        | Function | no     | All      | yes               |
| resume                | Resume the current TTS utterance.                                       | Function | no     | All      | yes               |
| addEventListener      | Adding an Event Listener                                                | Function | no     | All      | yes               |
| removeEventListener   | Remove Event Listener                                                   | Function | no     | All      | yes               |

## 遗留问题

- [ ] 三方引擎相关功能无法实现的问题：[issue#2](https://github.com/react-native-oh-library/react-native-tts/issues/2)
- [ ] 语言类型只支持中文的问题：[issue#3](https://github.com/react-native-oh-library/react-native-tts/issues/3)
- [ ] setDucking无法实现的问题：[issue#4](https://github.com/react-native-oh-library/react-native-tts/issues/4)
- [ ] setIgnoreSilentSwitch无法实现的问题：[issue#5](https://github.com/react-native-oh-library/react-native-tts/issues/5)
- [ ] setDefaultVoice无法实现的问题：[issue#6](https://github.com/react-native-oh-library/react-native-tts/issues/6)
- [ ] 边合成边播放的问题：[issue#7](https://github.com/react-native-oh-library/react-native-tts/issues/7)
- [ ] 参数skipTransform、onWordBoundary无效的问题：[issue#8](https://github.com/react-native-oh-library/react-native-tts/issues/8)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ak1394/react-native-tts/blob/master/README.md#license)，请自由地享受和参与开源。