<!-- {% raw %} -->
>  模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-tts</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ak1394/react-native-tts">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
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
import {Text, StyleSheet, ScrollView} from 'react-native';
import {Tester, TestSuite, TestCase} from '@rnoh/testerino';
import Tts, {TtsEvents} from 'react-native-tts';

const speakText = `炎炎夏日，阳光如烈火般炙烤大地。`;

const speakText2 = `秋天，一抹深沉的金黄漫过天际，叶片如蝶般飘零。微风拂过，树叶沙沙作响，落叶编织地面的金色地毯。秋天的色彩斑斓而美丽，仿佛大自然为世界穿上一袭金黄的盛装，宁静而充满生机。`;

type SetStateProps = React.Dispatch<React.SetStateAction<boolean>>;

type fnBackProps = Promise<boolean | string | number | void>;

export default function TTSDemo() {
  const eventTypes: TtsEvents[] = [
    'tts-start',
    'tts-finish',
    'tts-error',
    'tts-cancel',
    'tts-progress',
  ];

  const caseAddEventList = eventTypes.map(event => {
    return {
      describe: `addEventListener（${event}）`,
      cn: '添加事件监听',
      key: `addEventListener （${event}）`,
      name: 'addEventListener',
      value: event,
      defineFn: (setState?: SetStateProps) => {
        Tts.addEventListener(event, () => {
          setState?.(true);
        });
      },
    };
  });

  const caseRemoveEventList = eventTypes.map(event => {
    return {
      describe: `removeEventListener（${event}）`,
      cn: '移除事件监听',
      key: `removeEventListener （${event}）`,
      name: 'removeEventListener',
      value: event,
      defineFn: (setState?: SetStateProps) => {
        Tts.removeEventListener(event, () => {
          setState?.(true);
        });
      },
    };
  });

  const caseList = [
    {
      describe: 'getInitStatus',
      cn: '获取初始化状态',
      key: 'getInitStatus',
      name: 'getInitStatus',
      value: '',
      fn: (): fnBackProps => Tts.getInitStatus(),
    },
    {
      describe: 'speak（short）',
      cn: '合成语音并播放',
      key: 'speak_a',
      name: 'speak',
      value: speakText,
      defineFn: (setState?: SetStateProps) => {
        const id = Tts.speak(speakText);
        setState?.(!!id);
      },
    },
    {
      describe: 'speak（long）',
      cn: '合成语音并播放',
      key: 'speak_b',
      name: 'speak',
      value: speakText2,
      defineFn: (setState?: SetStateProps) => {
        const id = Tts.speak(speakText2);
        setState?.(!!id);
      },
    },
    {
      describe: 'stop',
      cn: '结束播放',
      key: 'stop',
      name: 'stop',
      value: false,
      fn: (): fnBackProps => Tts.stop(false),
    },
    {
      describe: 'pause',
      cn: '暂停播放',
      key: 'pause',
      name: 'pause',
      value: false,
      fn: (): fnBackProps => Tts.pause(false),
    },
    {
      describe: 'resume',
      cn: '继续播放',
      key: 'resume',
      name: 'resume',
      value: '',
      fn: (): fnBackProps => Tts.resume(),
    },
    {
      describe: 'setDefaultRate（2）',
      cn: '设置默认语速，语速为2',
      key: 'setDefaultRate(2)',
      name: 'setDefaultRate',
      value: 2,
      fn: (): fnBackProps => Tts.setDefaultRate(2),
    },
    {
      describe: 'setDefaultRate（0.5）',
      cn: '设置默认语速，语速为0.5',
      key: 'setDefaultRate(0.5)',
      name: 'setDefaultRate',
      value: 0.5,
      fn: (): fnBackProps => Tts.setDefaultRate(0.5),
    },
    {
      describe: 'setDefaultPitch(2)',
      cn: '设置默认音调',
      key: 'setDefaultPitch(2)',
      name: 'setDefaultPitch',
      value: 2,
      fn: (): fnBackProps => Tts.setDefaultPitch(2),
    },
    {
      describe: 'setDefaultPitch(0.5)',
      cn: '设置默认音调',
      key: 'setDefaultPitch(0.5)',
      name: 'setDefaultPitch',
      value: 0.5,
      fn: (): fnBackProps => Tts.setDefaultPitch(0.5),
    },
    {
      describe: 'voices',
      cn: '获取音色列表',
      key: 'voices',
      name: 'voices',
      value: '',
      defineFn: (setState?: SetStateProps) => {
        Tts.voices().then(res => {
          setState?.(!!res.length);
        });
      },
    },
    ...caseAddEventList,
    ...caseRemoveEventList,
  ];
  return (
    <Tester>
      <ScrollView>
        <TestSuite name="react-native-tts">
          <TestCase tags={['C_API']} itShould="error回调专用">
            <Text
              style={styles.button}
              onPress={() => {
                Tts.speak(123);
              }}>
              触发异常
            </Text>
          </TestCase>
          {caseList.map(item => {
            return (
              <TestCase
                tags={['C_API']}
                itShould={item.describe + `（${item.cn}）`}
                initialState={false}
                key={item.key}
                arrange={({setState}) => {
                  return (
                    <Text
                      style={styles.button}
                      onPress={() =>
                        item.defineFn
                          ? item.defineFn(setState)
                          : item.fn().then(() => setState(true))
                      }>
                      {item.name}
                    </Text>
                  );
                }}
                assert={async ({expect, state}) => {
                  expect(state).to.be.true;
                }}
              />
            );
          })}
        </TestSuite>
        <Text style={{marginBottom: 100}}></Text>
      </ScrollView>
    </Tester>
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
    color: 'white',
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

### 在工程根目录的 `oh-package.json` 添加 overrides 字段

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
+ import { RNTTSPackage } from '@react-native-oh-tpl/react-native-tts/ts';

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
| getInitStatus         | Returns a promise that resolves when the TTS engine is initialized.     | Function | No       | No       | All               |
| requestInstallEngine  | Requests installation of the TTS engine if not already installed.       | Function | No       | android  | no                |
| requestInstallData    | Requests installation of the TTS data if not already installed.         | Function | No       | android  | no                |
| setDucking            | Sets whether the TTS engine should duck other audio when speaking.      | Function | No       | All      | no                |
| setDefaultEngine      | Sets the default TTS engine.                                            | Function | No       | android  | no                |
| setDefaultVoice       | Sets the default voice for the TTS engine.                              | Function | No       | All      | no                |
| setDefaultRate        | Sets the default speech rate for the TTS engine.                        | Function | No       | All      | yes               |
| setDefaultPitch       | Sets the default pitch for the TTS engine.                              | Function | No       | All      | yes               |
| setDefaultLanguage    | Sets the default language for the TTS engine.                           | Function | No       | All      | no                |
| setIgnoreSilentSwitch | Function                                                                | No       | ios      | no       |
| voices                | Retrieves a list of available voices from the TTS engine.               | Function | No       | All      | yes               |
| engines               | Retrieves a list of available TTS engines.                              | Function | No       | android  | no                |
| speak                 | Speaks the given utterance and returns a promise with the utterance ID. | Function | No       | All      | yes               |
| stop                  | Stops the current TTS utterance.                                        | Function | No       | All      | yes               |
| pause                 | Pause the current TTS utterance.                                        | Function | No       | All      | yes               |
| resume                | Resume the current TTS utterance.                                       | Function | No       | All      | yes               |
| addEventListener      | Adding an Event Listener                                                | Function | No       | All      | yes               |
| removeEventListener   | Remove Event Listener                                                   | Function | No       | All      | yes               |

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
<!-- {% endraw %} -->