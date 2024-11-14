模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-localization</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/stefalda/ReactNativeLocalization">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/stefalda/ReactNativeLocalization/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/react-native-oh-library/ReactNativeLocalization)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-localization Releases](https://github.com/react-native-oh-library/ReactNativeLocalization/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-localization
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-localization
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react';
import { View, Text, Button, StyleSheet } from 'react-native';
import Localize from 'react-native-localization';

// 定义本地化内容
const strings = new Localize({
  en: {//英语
    welcome: 'Welcome',
    question: 'I\'d like some {0} and {1}, or just {0}',
    bread: 'bread',
    butter: 'butter',
    greeting: 'Hello, {0}!   ',
    currentlanguage: 'Current Language',
    availableLanguages: 'Available Languages',
    interfaceLanguage: 'The System Language'
  },
  fr: {//法语
    welcome: 'Bienvenue',
    question: 'Je voudrais un peu de {0} et {1}, ou juste {0}',
    bread: 'pain',
    butter: 'beurre',
    greeting: 'Bonjour, {0}!',
    currentlanguage: 'Langue actuelle',
    availableLanguages: 'Langues disponibles',
    interfaceLanguage: 'Langue du système'
  },
  bo: {//藏语
    welcome: 'བསྐུལ་མཁན།',
    question: 'ང་ལུས་འདི་ལས། {0} དང། {1} ཡང་ཡིན། གང་ཡིན་ནི། {0}',
    bread: 'བཀྲུངས',
    butter: 'བརྡེན',
    greeting: 'བཀའ་བདག་ {0}!',
    currentlanguage: 'ད་དུས་ལག་འཁྱེར།',
    availableLanguages: 'ད་དུས་ལག་འཁྱེར་སྒྲིགས།',
    interfaceLanguage: 'རྩམ་གཞི་སྒྲིག་ལེན་དེ་རྒྱལ་སྤོད་'
  },
  zh: {//中文
    welcome: '欢迎',
    question: '我想要一些{0}和{1}，或者只要{0}',
    bread: '面包',
    butter: '黄油',
    greeting: '你好, {0}!',
    currentlanguage: '当前语言',
    availableLanguages: '当前可用语言列表',
    interfaceLanguage: '当前系统语言'
  },
});

export function LocalizationDemo() {
  // getLanguage API
  const [language, setLanguage] = useState(strings.getLanguage());
  const changeLanguage = (lang: string) => {
    // setLanguage API
    strings.setLanguage(lang);
    setLanguage(strings.getLanguage());
  };

  return (
    <View style={styles.screen}>
      <View style={{ height: 180, justifyContent: 'space-between', marginBottom: 30 }}>
        <Button
          color="#144400"
          title="切换成中文"
          onPress={() => changeLanguage('zh')}
        />
        <Button
          color="#841584"
          title="切换成法语"
          onPress={() => changeLanguage('fr')}
        />
        <Button
          color="#645555"
          title="切换成英语"
          onPress={() => changeLanguage('en')}
        />
        <Button
          color="#241595"
          title="切换成藏语"
          onPress={() => changeLanguage('bo')}
        />
      </View>

      <Text style={styles.text}>
        {strings.welcome}
      </Text>
      <Text style={styles.text}>
        {/* formatString API */}
        {strings.formatString(strings.question, strings.bread, strings.butter)}
      </Text>
      <Text style={styles.text}>
        {strings.currentlanguage}: {language}
      </Text>
      {/* getAvailableLanguages API */}
      <Text style={styles.text}>
        {strings.availableLanguages}: {strings.getAvailableLanguages().join(', ')}
      </Text>
      {/* getInterfaceLanguage API */}
      <Text style={styles.text}>
        {strings.interfaceLanguage}: {strings.getInterfaceLanguage()}
      </Text>
    </View>
  );
}

const styles = StyleSheet.create({
  text: {
    fontSize: 18,
    marginBottom: 10,
    color: 'white'
  },

  screen: {
    flex: 1,
    padding: 4,
    paddingTop: 10,
    backgroundColor: 'black',
    marginHorizontal: 4,
    marginVertical: 8,
    paddingHorizontal: 8,
  },
});
```
## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
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
    "@react-native-oh-tpl/react-native-localization": "file:../../node_modules/@react-native-oh-tpl/react-native-localization/harmony/react_localization.har"
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


### 3.在 ArkTs 侧引入 RNReactLocalizationPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNReactLocalizationPackage } from '@react-native-oh-tpl/react-native-localization';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNReactLocalizationPackage(ctx),
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-localization Releases](https://github.com/react-native-oh-library/ReactNativeLocalization/releases)



## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | :---------- | ---- | :------: | :------: | :----------------: |
| setLanguage(languageCode)                 | force manually a particular language                         | void     |   yes    | iOS/Android |        yes        |
| getLanguage()                             | get the current displayed language                           | string   |   yes    | iOS/Android |        yes        |
| getInterfaceLanguage()                    | get the current device interface language                    | string   |   yes    | iOS/Android |        yes        |
| formatString()                            | format the passed string replacing its placeholders with the other arguments strings | string   |   yes    | iOS/Android |        yes        |
| getAvailableLanguages()                   | get an array of the languages passed in the constructor      | string[] |   yes    | iOS/Android |        yes        |
| getString(key: string, language?: string) | character information based on the key value | string | yes | iOS/Android | yes |
| setContent(props: any) | replace the NamedLocalization object without reinstantiating the object | void | yes | iOS/Android | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/stefalda/ReactNativeLocalization/blob/master/LICENSE) ，请自由地享受和参与开源。