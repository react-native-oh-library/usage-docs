> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/voice)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/voice Releases](https://github.com/react-native-oh-library/voice/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/voice
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/voice
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, {Component} from 'react';
import {
    StyleSheet,
    Text,
    View,
    Image,
    TouchableHighlight,
    ScrollView,
    Button,
} from 'react-native';
import Voice, {
    SpeechRecognizedEvent,
    SpeechResultsEvent,
    SpeechErrorEvent,
} from '@react-native-voice/voice';

type Props = {};
type State = {
    recognized: string;
    error: string;
    end: string;
    started: string;
    results: string[];
    partialResults: string[];
    isAvailable: number;
    isRecognizing: number;
};

class VoiceTest extends Component<Props, State> {
    state = {
        recognized: '',
        error: '',
        end: '',
        started: '',
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
        console.log('onSpeechStart: ', e);
        this.setState({
            started: '√',
        });
    };

    onSpeechRecognized = (e: SpeechRecognizedEvent) => {
        console.log('onSpeechRecognized: ', e);
        this.setState({
            recognized: '√',
        });
    };

    onSpeechEnd = (e: any) => {
        console.log('onSpeechEnd: ', e);
        this.setState({
            end: '√',
        });
    };

    onSpeechError = (e: SpeechErrorEvent) => {
        console.log('onSpeechError: ', e);
        this.setState({
            error: JSON.stringify(e.error),
        });
    };

    onSpeechResults = (e: SpeechResultsEvent) => {
        console.log('onSpeechResults: ', e);
        this.setState({
            results: e.value,
        });
    };

    onSpeechPartialResults = (e: SpeechResultsEvent) => {
        console.log('onSpeechPartialResults: ', e);
        this.setState({
            partialResults: e.value,
        });
    };

    _startRecognizing = async () => {
        this.setState({
            recognized: '',
            error: '',
            started: '',
            results: [],
            partialResults: [],
            end: '',
        });

        try {
            await Voice.start('en-US');
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
            recognized: '',
            error: '',
            started: '',
            results: [],
            partialResults: [],
            end: '',
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
                <View style={{height: 20, marginBottom: 20, backgroundColor: '#fff'}}>
                    <Text style={styles.stat}>{`${this.state.started}`}</Text>
                </View>

                <View style={{height: 20, marginBottom: 20, backgroundColor: '#fff'}}>
                    <Text style={styles.stat}>{`${this.state.recognized}`}</Text>
                </View>

                <View style={{height: 30, marginBottom: 20, backgroundColor: '#fff'}}>
                    <Text style={styles.stat}>{`${this.state.error}`}</Text>
                </View>

                <View
                    style={{minHeight: 30, marginBottom: 20, backgroundColor: '#fff'}}>
                    {this.state.results.map((result, index) => {
                        return (
                            <Text key={`result-${index}`} style={styles.stat}>
                                {result}
                            </Text>
                        );
                    })}
                </View>

                <View
                    style={{minHeight: 50, marginBottom: 20, backgroundColor: '#fff'}}>
                    {this.state.partialResults.map((result, index) => {
                        return (
                            <Text key={`partial-result-${index}`} style={styles.stat}>
                                {result}
                            </Text>
                        );
                    })}
                </View>

                <View style={{height: 30, marginBottom: 20, backgroundColor: '#fff'}}>
                    <Text style={styles.stat}>{` ${this.state.end}`}</Text>
                </View>

                <View style={styles.baseArea}>
                    <Text style={{flex: 1}}>{`${this.state.isAvailable}`}</Text>
                    <Button
                        title="isAvailable"
                        color="#841584"
                        onPress={this._isAvailable}></Button>
                </View>

                <View style={styles.baseArea}>
                    <Text style={{flex: 1}}>{`${this.state.isRecognizing}`}</Text>
                    <Button
                        title="isRecognizing"
                        color="#841584"
                        onPress={this._isRecognizing}></Button>
                </View>

                <View style={{marginBottom: 10}}>
                    <Button
                        title="start"
                        color="#841584"
                        onPress={this._startRecognizing}
                    />
                </View>
                <View style={{marginBottom: 10}}>
                    <Button
                        title="stop"
                        color="#841584"
                        onPress={this._stopRecognizing}
                    />
                </View>

                <View style={{padding: 5}}>
                    <Button
                        title="cancel"
                        color="#841584"
                        onPress={() => {
                            this._cancelRecognizing();
                        }}></Button>
                </View>

                <View style={{padding: 5}}>
                    <Button
                        title="destroy"
                        color="#841584"
                        onPress={() => {
                            this._destroyRecognizer();
                        }}></Button>
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
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: '#F5FCFF',
    },
    welcome: {
        fontSize: 20,
        textAlign: 'center',
        margin: 10,
    },
    action: {
        textAlign: 'center',
        color: '#0000FF',
        marginVertical: 5,
        fontWeight: 'bold',
    },
    instructions: {
        textAlign: 'center',
        color: '#333333',
        marginBottom: 5,
    },
    stat: {
        textAlign: 'center',
        color: '#B0171F',
        marginBottom: 1,
    },
    baseArea: {
        width: '100%',
        height: 30,
        borderRadius: 4,
        borderColor: '#000000',
        marginTop: 6,
        backgroundColor: '#FFFFFF',
        flexDirection: 'row',
        alignItems: 'center',
        paddingLeft: 8,
        paddingRight: 8,
        marginBottom: 20,
    },
});

export default VoiceTest;
```
## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/voice": "file:../../node_modules/@react-native-oh-tpl/voice/harmony/voice.har"
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

### 3.在 ArkTs 侧引入 RNVoicePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

### 4.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/voice Releases](https://github.com/react-native-oh-library/voice/releases)

### 权限要求
由于此库涉及语音识别会使用到系统录音功能，使用时需要配置对应的权限，权限需配置在entry/src/main目录下module.json5和entry/src/main/resources/base/element目录下string.json文件

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

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> 详情见 [react-native-voice/voice](https://github.com/react-native-voice/voice)

| Name                        | Description                                                                       | Type              | Required | Platform | HarmonyOS Support |
|-----------------------------|-----------------------------------------------------------------------------------|-------------------|----------|----------|-------------------|
| isAvailable()：Promise<isAvailable:<0 \| 1 > | Checks whether a speech recognition service is available on the system. | function  | no      | Android, iOS  | yes               |
| start(locale: any, options = {})：Promise<unknown>| Starts listening for speech for a specific locale. Returns null if no error occurs. | function  | no       | Android, iOS | yes               |
| stop()：Promise<unknown>  | Stops listening for speech. Returns null if no error occurs.   | function  | no      | Android, iOS | yes               |
| cancel()：Promise<unknown>  | Cancels the speech recognition. Returns null if no error occurs.    | function | no       | Android, iOS     | yes               |
| destroy()：Promise<unknown>  | Destroys the current SpeechRecognizer instance. Returns null if no error occurs. | function  | no      | Android, iOS | yes               |
| removeAllListeners()：Promise<unknown>  | Cleans/nullifies overridden Voice static methods.   | void              | no       | Android, iOS  | no               |
| isRecognizing()：Promise<isRecognizing:<0 \| 1 > | Return if the SpeechRecognizer is recognizing.  | function  | no      | Android, iOS  | yes               |
| getSpeechRecognitionServices() | Returns a list of the speech recognition engines available on the device. (Example: ['com.google.android.googlequicksearchbox'] if Google is the only one available.) | function| no   | Android  | no  |

## 事件回调

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description                                                                                                                       | Type     | Required | Platform                                       | HarmonyOS Support |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------- | :------- |--------| ---------------------------------------------- |-----------------|
| `Voice.onSpeechStart(event)` | Invoked when .start() is called without error. | function | no | Android, iOS   | yes |
| `Voice.onSpeechRecognized(event)` | Invoked when speech is recognized.  | function | no | Android, iOS   | yes |
| `Voice.onSpeechEnd(event)` | Invoked when SpeechRecognizer stops recognition. | function | no | Android, iOS | yes |
| `Voice.onSpeechError(event)` | Invoked when an error occurs. | function | no | Android, iOS   | yes |
| `Voice.onSpeechResults(event)`  | Invoked when SpeechRecognizer is finished recognizing.  | function | no | Android, iOS   | yes |
| `Voice.onSpeechPartialResults(event)`  | Invoked when any results are computed.  | function | no  | Android, iOS     | yes |
| `Voice.onSpeechVolumeChanged(event)` | Invoked when pitch that is recognized changed.   | function | no | Android | no  |

## 遗留问题

- [ ] 原库支持在线和离线模式，HarmonyOS侧暂只支持离线 问题: [issue#2](https://github.com/react-native-oh-library/voice/issues/2)
- [ ] 原库支持多种区域和语言，HarmonyOS侧暂只支持中文 问题: [issue#3](https://github.com/react-native-oh-library/voice/issues/3)

## 其他
- removeAllListeners方法未生效，与iOS效果一致。问题:  [issue#491]((https://github.com/react-native-voice/voice/issues/491)
## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-voice/voice/blob/master/LICENSE) ，请自由地享受和参与开源。