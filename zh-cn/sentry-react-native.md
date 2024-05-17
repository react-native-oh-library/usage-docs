> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>sentry-react-native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/getsentry/sentry-react-native">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/getsentry/sentry-react-native/blob/main/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/getsentry/sentry-react-native)

## 安装与使用

进入到工程目录并输入以下命令：


<!-- tabs:start -->

####  npm

```bash
npm install @sentry/react-native@5.22.2
```

#### yarn

```bash
yarn add @sentry/react-native@5.22.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx

// ============ index.js ==============
import * as Sentry from "@sentry/react-native";
Sentry.init({
  // 该参数为官网申请的
  dsn: "__DSN__",  
  // 暂不支持捕获harmony侧error
  autoInitializeNativeSdk: false, 
  enableNative: false,
  // ... 更多初始化参数参考官方文档
});

// 包裹App（项目根）组件
Sentry.wrap(App);


// ============ sentryDemo.tsx =============
import React, { useEffect } from 'react';
import { Button, View, GestureResponderEvent,
   ScrollView, ToastAndroid as Toast, StyleSheet } from 'react-native';
import * as Sentry from "@sentry/react-native";

interface ButtonWithClickCb {
  title: string;
  pressCallback: (ev: GestureResponderEvent) => void
}
const user: Sentry.User = {
    username: 'wangml',
    email: 'tester@xxx.com',
    id: 10
};

export default function SentryDemo() {

  useEffect(() => {
    // 添加面包屑
    Sentry.addBreadcrumb({
      category: 'auth_110',
      message: 'Authenticated user Wml',
      level: 'info'
    });
    // 设置用户
    Sentry.setUser(user);
    // 设置 context
    Sentry.setContext('character', {
      name: 'Mighty Fighter',
      age: 19,
      attack_type: 'melee',
    });
    // 设置标签
    Sentry.setTag('wmlTag', 'ook');
    // 设置附件
    Sentry.getCurrentScope().addAttachment({
      filename: 'attachment.txt',
      data: 'Some content',
    });
    
    return () => {
      Sentry.getCurrentScope().clearAttachments();
    };
  }, []);

  const btnWithCbList: ButtonWithClickCb[] = [
    {
      title: 'Sentry Crash',
      pressCallback: () => {
        throw new Error('rnoh error!');
      }
    },
    {
      title: 'Sentry Native Crash',
      pressCallback: () => {
        Sentry.nativeCrash();
      }
    },
    {
      title: 'captureMessage',
      pressCallback: () => {
        Toast.show('rnoh captureMessage', 2000);
        Sentry.captureMessage('rnoh captureMessage!');
      }
    },
    {
      title: 'captureException',
      pressCallback: () => {
        try {
          throw new Error('rnoh captureException!')
        } catch (err) {
          Sentry.captureException(err);
        }
      }
    },
    {
      title: 'captureUserFeedBack',
      pressCallback: () => {
        const eventId = Sentry.captureMessage('User Feedback');
        const userFeedback = {
          event_id: eventId,
          name: 'John Doe',
          email: 'john@doe.com',
          comments: 'I really like your App, thanks!',
        };
        Sentry.captureUserFeedback(userFeedback);
      }
    },
    {
      title: 'configStore',
      pressCallback: () => {
        Sentry.configureScope(scope => {
          scope.setExtra( 'extData', 'abccc');
          scope.setTag('testScope', 'wmltest');
          scope.setUser({
            id: 110, email: 'wangml@xxx.com'
          })
        });
        Sentry.withScope(scope => {
          scope.setExtra( 'extData', 'abccc');
          scope.setTag('testScope', 'wmltest');
          scope.setUser({
            id: 110, email: 'wangml@xxx.com'
          })
          Sentry.captureMessage('test configStore');
        })
      }
    },
  ];

  return (
    <ScrollView>
      <View style={{ height: '100%', backgroundColor: 'white', padding: 20 }}>
        {
          btnWithCbList.map((bv) =>
            <View style={{ width: 300, height: 50, alignSelf: "center" }} key={bv.title}>
              <Button onPress={bv.pressCallback} title={bv.title} />
            </View>
          )
        }
      </View>
    </ScrollView>
  );
}
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：
1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

常用api如下，详细请参考sentry官网: [https://docs.sentry.io/platforms/react-native/](https://docs.sentry.io/platforms/react-native/)

| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| addBreadcrumb    | 错误详情面板添加面包屑. | function | No       | IOS/Android | yes               |
| setUser       | 设置用户信息.       | function | No       | IOS/Android | yes  |
| setContext       | 错误详情面板设置context.       | function | No       | IOS/Android | yes  |
| setTag      | 设置标签.       | function | No       | IOS/Android | yes  |
| captureMessage       | 主动上报消息.       | function | No       | IOS/Android | yes  |
| captureException       | 主动上报错误.       | function | No       | IOS/Android | yes  |
| captureUserFeedBack       | 上报用户反馈信息.       | function | No       | IOS/Android | yes  |
| withScope       | 隔离上下文环境.       | function | No       | IOS/Android | yes  |
| addAttachment       | 设置附件.       | function | No       | IOS/Android | no  |
| nativeCrash       | 抛出一个原生层错误. | function | No       | IOS/Android | no  |

## 遗留问题

- [ ] 暂不支持harmony层Error捕获: [issue#1](https://github.com/react-native-oh-library/sentry-react-native/issues/1) 
- [ ] addAttachment添加附件无效果: [issue#2](https://github.com/react-native-oh-library/sentry-react-native/issues/2)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/getsentry/sentry-react-native/blob/main/LICENSE.md) ，请自由地享受和参与开源。

