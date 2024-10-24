> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-voice/voice</code> </h1>
  </p>
<p align="center">
    <a href="https://github.com/react-native-voice/voice">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-voice/voice/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/voice)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/voice Releases](https://github.com/react-native-oh-library/voice/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/voice@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/voice@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import {
  StyleSheet,
  Text,
  View,
  Image,
  TouchableHighlight,
  ScrollView,
  Button,
} from "react-native";
import Voice, {
  SpeechRecognizedEvent,
  SpeechResultsEvent,
  SpeechErrorEvent,
} from "@react-native-voice/voice";

type Props = {};
type State = {
  recognized: string,
  error: string,
  end: string,
  started: string,
  results: string[],
  partialResults: string[],
  isAvailable: number,
  isRecognizing: number,
};

class VoiceTest extends Component<Props, State> {
  state = {
    recognized: "",
    error: "",
    end: "",
    started: "",
    results: [],
    partialResults: [],
    isAvailable: 0,
    isRecognizing: 0,
  };

  constructor(props: Props) {
    super(props);
    Voice.onSpeechStart = this.onSpeechStart;
    Voice.onSpeechRecognized = this.onSpeechRecognized;
    Voice.onSpeechEnd = this.onSpeechEnd;
    Voice.onSpeechError = this.onSpeechError;
    Voice.onSpeechResults = this.onSpeechResults;
    Voice.onSpeechPartialResults = this.onSpeechPartialResults;
  }

  componentWillUnmount() {
    Voice.destroy().then(Voice.removeAllListeners);
  }

  onSpeechStart = (e: any) => {
    console.log("onSpeechStart: ", e);
    this.setState({
      started: "√",
    });
  };

  onSpeechRecognized = (e: SpeechRecognizedEvent) => {
    console.log("onSpeechRecognized: ", e);
    this.setState({
      recognized: "√",
    });
  };

  onSpeechEnd = (e: any) => {
    console.log("onSpeechEnd: ", e);
    this.setState({
      end: "√",
    });
  };

  onSpeechError = (e: SpeechErrorEvent) => {
    console.log("onSpeechError: ", e);
    this.setState({
      error: JSON.stringify(e.error),
    });
  };

  onSpeechResults = (e: SpeechResultsEvent) => {
    console.log("onSpeechResults: ", e);
    this.setState({
      results: e.value,
    });
  };

  onSpeechPartialResults = (e: SpeechResultsEvent) => {
    console.log("onSpeechPartialResults: ", e);
    this.setState({
      partialResults: e.value,
    });
  };

  _startRecognizing = async () => {
    this.setState({
      recognized: "",
      error: "",
      started: "",
      results: [],
      partialResults: [],
      end: "",
    });

    try {
      await Voice.start("en-US");
    } catch (e) {
      console.error(e);
    }
  };

  _stopRecognizing = async () => {
    try {
      await Voice.stop();
    } catch (e) {
      console.error(e);
    }
  };

  _cancelRecognizing = async () => {
    try {
      await Voice.cancel();
      Voice.start;
    } catch (e) {
      console.error(e);
    }
  };

  _destroyRecognizer = async () => {
    try {
      await Voice.destroy();
    } catch (e) {
      console.error(e);
    }
    this.setState({
      recognized: "",
      error: "",
      started: "",
      results: [],
      partialResults: [],
      end: "",
    });
  };

  _isAvailable = async () => {
    try {
      Voice.isAvailable().then((available: 0 | 1) => {
        this.setState({
          isAvailable: available ? 1 : 0,
        });
      });
    } catch (e) {
      console.error(e);
      this.setState({
        isAvailable: 0,
      });
    }
  };

  _isRecognizing = async () => {
    try {
      Voice.isRecognizing().then((isRecognizing: 0 | 1) => {
        this.setState({
          isRecognizing: isRecognizing ? 1 : 0,
        });
      });
    } catch (e) {
      console.error(e);
    }
  };

  render() {
    return (
      <ScrollView>
        <View style={{ height: 20, marginBottom: 20, backgroundColor: "#fff" }}>
          <Text style={styles.stat}>{`${this.state.started}`}</Text>
        </View>

        <View style={{ height: 20, marginBottom: 20, backgroundColor: "#fff" }}>
          <Text style={styles.stat}>{`${this.state.recognized}`}</Text>
        </View>

        <View style={{ height: 30, marginBottom: 20, backgroundColor: "#fff" }}>
          <Text style={styles.stat}>{`${this.state.error}`}</Text>
        </View>

        <View
          style={{ minHeight: 30, marginBottom: 20, backgroundColor: "#fff" }}
        >
          {this.state.results.map((result, index) => {
            return (
              <Text key={`result-${index}`} style={styles.stat}>
                {result}
              </Text>
            );
          })}
        </View>

        <View
          style={{ minHeight: 50, marginBottom: 20, backgroundColor: "#fff" }}
        >
          {this.state.partialResults.map((result, index) => {
            return (
              <Text key={`partial-result-${index}`} style={styles.stat}>
                {result}
              </Text>
            );
          })}
        </View>

        <View style={{ height: 30, marginBottom: 20, backgroundColor: "#fff" }}>
          <Text style={styles.stat}>{` ${this.state.end}`}</Text>
        </View>

        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>{`${this.state.isAvailable}`}</Text>
          <Button
            title="isAvailable"
            color="#841584"
            onPress={this._isAvailable}
          ></Button>
        </View>

        <View style={styles.baseArea}>
          <Text style={{ flex: 1 }}>{`${this.state.isRecognizing}`}</Text>
          <Button
            title="isRecognizing"
            color="#841584"
            onPress={this._isRecognizing}
          ></Button>
        </View>

        <View style={{ marginBottom: 10 }}>
          <Button
            title="start"
            color="#841584"
            onPress={this._startRecognizing}
          />
        </View>
        <View style={{ marginBottom: 10 }}>
          <Button
            title="stop"
            color="#841584"
            onPress={this._stopRecognizing}
          />
        </View>

        <View style={{ padding: 5 }}>
          <Button
            title="cancel"
            color="#841584"
            onPress={() => {
              this._cancelRecognizing();
            }}
          ></Button>
        </View>

        <View style={{ padding: 5 }}>
          <Button
            title="destroy"
            color="#841584"
            onPress={() => {
              this._destroyRecognizer();
            }}
          ></Button>
        </View>
      </ScrollView>
    );
  }
}

const styles = StyleSheet.create({
  button: {
    width: 50,
    height: 50,
  },
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
  },
  welcome: {
    fontSize: 20,
    textAlign: "center",
    margin: 10,
  },
  action: {
    textAlign: "center",
    color: "#0000FF",
    marginVertical: 5,
    fontWeight: "bold",
  },
  instructions: {
    textAlign: "center",
    color: "#333333",
    marginBottom: 5,
  },
  stat: {
    textAlign: "center",
    color: "#B0171F",
    marginBottom: 1,
  },
  baseArea: {
    width: "100%",
    height: 30,
    borderRadius: 4,
    borderColor: "#000000",
    marginTop: 6,
    backgroundColor: "#FFFFFF",
    flexDirection: "row",
    alignItems: "center",
    paddingLeft: 8,
    paddingRight: 8,
    marginBottom: 20,
  },
});

export default VoiceTest;
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
    "@react-native-oh-tpl/voice": "file:../../node_modules/@react-native-oh-tpl/voice/harmony/voice.har"
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

### 3. Introducing RNVoicePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...

+  import { RNVoicePackage } from '@react-native-oh-tpl/voice/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNVoicePackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/voice Releases](https://github.com/react-native-oh-library/voice/releases)

### Permission Requirements

由于此库涉及语音识别会使用到系统录音功能，使用时需要配置对应的权限，权限需配置在 entry/src 目录下 module.json5 和 entry/src/main/resources/base/element 目录下 string.json 文件

打开 `module.json5`，添加：

```diff
...
"requestPermissions": [
...
+      {
+        "name": "ohos.permission.MICROPHONE",
+        "reason": "$string:reason",
+        "usedScene": {
+          "abilities": [
+            "EntryAbility"
+          ],
+          "when": "inuse"
+        }
+      }
    ]
```

打开 `string.json`，添加权限申请原因：

```diff
...
{
  "string": [
...
+    {
+      "name": "reason",
+      "value": "Used for recording recognition"
+    },
...
  ]
}
```

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> For details, see  [react-native-voice/voice](https://github.com/react-native-voice/voice)

| Name                                 | Description                                                                                                                                                           | Type              | Required | Platform     | HarmonyOS Support |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | -------- | ------------ | ----------------- |
| Voice.isAvailable()                  | Checks whether a speech recognition service is available on the system.                                                                                               | Promise<0 \| 1>   | no       | Android, iOS | yes               |
| Voice.start(locale)                  | Starts listening for speech for a specific locale. Returns null if no error occurs.                                                                                   | Promise<unknown>  | no       | Android, iOS | yes               |
| Voice.stop()                         | Stops listening for speech. Returns null if no error occurs.                                                                                                          | Promise<unknown>  | no       | Android, iOS | yes               |
| Voice.cancel()                       | Cancels the speech recognition. Returns null if no error occurs.                                                                                                      | Promise<unknown>  | no       | Android, iOS | yes               |
| Voice.destroy()                      | Destroys the current SpeechRecognizer instance. Returns null if no error occurs.                                                                                      | Promise<unknown>  | no       | Android, iOS | yes               |
| Voice.removeAllListeners()           | Cleans/nullifies overridden Voice static methods.                                                                                                                     | void              | no       | Android, iOS | yes               |
| Voice.isRecognizing()                | Return if the SpeechRecognizer is recognizing.                                                                                                                        | Promise<0 \| 1>   | no       | Android, iOS | yes               |
| Voice.getSpeechRecognitionServices() | Returns a list of the speech recognition engines available on the device. (Example: ['com.google.android.googlequicksearchbox'] if Google is the only one available.) | Promise<string[]> | no       | Android      | no                |

## 事件回调

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                  | Description                                            | Type     | Required | Platform     | HarmonyOS Support |
| ------------------------------------- | ------------------------------------------------------ | :------- | -------- | ------------ | ----------------- |
| `Voice.onSpeechStart(event)`          | Invoked when .start() is called without error.         | function | no       | Android, iOS | yes               |
| `Voice.onSpeechRecognized(event)`     | Invoked when speech is recognized.                     | function | no       | Android, iOS | yes               |
| `Voice.onSpeechEnd(event)`            | Invoked when SpeechRecognizer stops recognition.       | function | no       | Android, iOS | yes               |
| `Voice.onSpeechError(event)`          | Invoked when an error occurs.                          | function | no       | Android, iOS | yes               |
| `Voice.onSpeechResults(event)`        | Invoked when SpeechRecognizer is finished recognizing. | function | no       | Android, iOS | yes               |
| `Voice.onSpeechPartialResults(event)` | Invoked when any results are computed.                 | function | no       | Android, iOS | yes               |
| `Voice.onSpeechVolumeChanged(event)`  | Invoked when pitch that is recognized changed.         | function | no       | Android      | no                |

## Known Issues

- [ ] 原库支持在线和离线模式，HarmonyOS 侧暂只支持离线 问题: [issue#2](https://github.com/react-native-oh-library/voice/issues/2)
- [ ] 原库支持多种区域和语言，HarmonyOS 侧暂只支持中文 问题: [issue#3](https://github.com/react-native-oh-library/voice/issues/3)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-voice/voice/blob/master/LICENSE).
