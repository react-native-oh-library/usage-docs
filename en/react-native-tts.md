> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-tts)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-tts Releases](https://github.com/react-native-oh-library/react-native-tts/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { useState, useCallback } from "react";
import { Text, View, StyleSheet, SafeAreaView } from "react-native";
import Tts from "react-native-tts";

const cnText = `炎炎夏日，阳光如烈火般炙烤大地，空气中弥漫着热浪的气息。树荫下，蝉鸣声如同热浪中跳跃的音符，微风吹过，带来一丝清凉。远处的田野上，金黄的麦浪随风起伏，仿佛在舞动着夏天的节奏。天空湛蓝如洗，白云悠然飘过，似是一幅宁静而美丽的夏日画卷。`;

export function TTSDemo() {
  const [speakText, setSpeakText] = useState < string > cnText;

  const addEvent = useCallback(() => {
    Tts.addEventListener("tts-start", (res) => {
      console.log("tts-start", res);
    });
  }, []);

  const removeEvent = useCallback(() => {
    Tts.addEventListener("tts-start", (res) => {
      console.log("tts-start", res);
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
      console.log("initialization completed");
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
    Tts.voices().then((res) => {
      const resTr = JSON.stringify(res);
      setSpeakText(resTr);
    });
  }, []);

  return (
    <>
      <SafeAreaView style={styles.constainer}>
        <Text style={styles.title}>react-native-tts functional verification</Text>
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
    display: "flex",
  },
  btnWrap: {
    width: "auto",
    backgroundColor: "gray",
    display: "flex",
    flexDirection: "row",
    flexWrap: "wrap",
    paddingLeft: 20,
  },
  text: {
    padding: 20,
    fontSize: 20,
  },
  title: {
    padding: 10,
    fontSize: 30,
    textAlign: "center",
  },
  button: {
    paddingVertical: 6,
    paddingHorizontal: 12,
    backgroundColor: "hsl(193, 95%, 68%)",
    borderWidth: 2,
    borderColor: "hsl(193, 95%, 30%)",
  },
});
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-tts": "file:../../node_modules/@react-native-oh-tpl/react-native-tts/harmony/rn_tts.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing RNTTSPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-tts Releases](https://github.com/react-native-oh-library/react-native-tts/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                                             | Type     | Required | Platform | HarmonyOS Support |
| --------------------- | ----------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| getInitStatus         | Returns a promise that resolves when the TTS engine is initialized.     | Function | no       | All      | yes               |
| requestInstallEngine  | Requests installation of the TTS engine if not already installed.       | Function | no       | Android  | no                |
| requestInstallData    | Requests installation of the TTS data if not already installed.         | Function | no       | Android  | no                |
| setDucking            | Sets whether the TTS engine should duck other audio when speaking.      | Function | no       | All      | no                |
| setDefaultEngine      | Sets the default TTS engine.                                            | Function | no       | Android  | no                |
| setDefaultVoice       | Sets the default voice for the TTS engine.                              | Function | no       | All      | no                |
| setDefaultRate        | Sets the default speech rate for the TTS engine.                        | Function | no       | All      | yes               |
| setDefaultPitch       | Sets the default pitch for the TTS engine.                              | Function | no       | All      | yes               |
| setDefaultLanguage    | Sets the default language for the TTS engine.                           | Function | no       | All      | no                |
| setIgnoreSilentSwitch | Sets whether to ignore the silent button.                               | Function | no       | iOS      | no                |
| voices                | Retrieves a list of available voices from the TTS engine.               | Function | no       | All      | yes               |
| engines               | Retrieves a list of available TTS engines.                              | Function | no       | Android  | no                |
| speak                 | Speaks the given utterance and returns a promise with the utterance ID. | Function | no       | All      | yes               |
| stop                  | Stops the current TTS utterance.                                        | Function | no       | All      | yes               |
| pause                 | Pause the current TTS utterance.                                        | Function | no       | All      | yes               |
| resume                | Resume the current TTS utterance.                                       | Function | no       | All      | yes               |
| addEventListener      | Adding an Event Listener                                                | Function | no       | All      | yes               |
| removeEventListener   | Remove Event Listener                                                   | Function | no       | All      | yes               |

## Known Issues

- [ ] 三方引擎相关功能无法实现的问题：[issue#2](https://github.com/react-native-oh-library/react-native-tts/issues/2)
- [ ] 语言类型只支持中文的问题：[issue#3](https://github.com/react-native-oh-library/react-native-tts/issues/3)
- [ ] setDucking 无法实现的问题：[issue#4](https://github.com/react-native-oh-library/react-native-tts/issues/4)
- [ ] setIgnoreSilentSwitch 无法实现的问题：[issue#5](https://github.com/react-native-oh-library/react-native-tts/issues/5)
- [ ] setDefaultVoice 无法实现的问题：[issue#6](https://github.com/react-native-oh-library/react-native-tts/issues/6)
- [ ] 边合成边播放的问题：[issue#7](https://github.com/react-native-oh-library/react-native-tts/issues/7)
- [ ] 参数 skipTransform、onWordBoundary 无效的问题：[issue#8](https://github.com/react-native-oh-library/react-native-tts/issues/8)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ak1394/react-native-tts/blob/master/README.md#license).
