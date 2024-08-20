> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-recaptcha-that-works</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/douglasjunior/react-native-recaptcha-that-works">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/douglasjunior/react-native-recaptcha-that-works/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/douglasjunior/react-native-recaptcha-that-works)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-recaptcha-that-works@2.0.0
```

#### **yarn**

```bash
yarn add react-native-recaptcha-that-works@2.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, {useRef, useCallback, useState} from 'react';
import {
  SafeAreaView,
  StyleSheet,
  View,
  Text,
  StatusBar,
  Button,
  Alert,
} from 'react-native';

import Recaptcha, { RecaptchaRef } from 'react-native-recaptcha-that-works';

const styles = StyleSheet.create({
  safeArea: {
    flex: 1,
  },
  container: {
    backgroundColor: '#00ff00',
    justifyContent: 'center',
    alignItems: 'center',
    flex: 1,
  },
});

const App = () => {
  const size = 'invisible';
  const [token, setToken] = useState('<none>');

  const $recaptcha = useRef<RecaptchaRef | null>(null);

  const handleOpenPress = useCallback(() => {
    $recaptcha.current?.open();
  }, []);

  const handleClosePress = useCallback(() => {
    $recaptcha.current?.close();
  }, []);

  return (
    <SafeAreaView style={styles.safeArea}>
      <StatusBar barStyle="dark-content" />
      <View style={styles.container}>
        <Button onPress={handleOpenPress} title="Open" />
        <Text>Token: {token}</Text>
        <Text>Size: {size}</Text>
      </View>

      <Recaptcha
        ref={$recaptcha}
        lang="pt"
        headerComponent={
          <Button title="Close modal" onPress={handleClosePress} />
        }
        footerComponent={<Text>Footer here</Text>}
        siteKey="6LeIxAcTAAAAAJcZVRqyHh71UMIEGNQ_MXjiZKhI"
        baseUrl="http://127.0.0.1"
        size={size}
        theme="dark"
        onLoad={() => Alert.alert('onLoad event')}
        onClose={() => Alert.alert('onClose event')}
        onError={(err) => {
          Alert.alert('onError event');
          console.warn(err);
        }}
        onExpire={() => Alert.alert('onExpire event')}
        onVerify={(token) => {
          Alert.alert('onVerify event');
          setToken(token);
        }}
        enterprise={false}
        hideBadge={false}
      />
    </SafeAreaView>
  );
};
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.28; OH SDK: HarmonyOS-Next-DB2 5.0.0.31 (API Version 12 Beta2); IDE: DevEco Studio: 5.0.3.500; ROM: 3.0.0.31;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name             | Description                                                                                                                                                                                                                                                                                        | Type                                                                                                       | Required | Platform    | HarmonyOS Support |
| ---------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| headerComponent  | A component to render on top of Modal.                                                                                                                                                                                                                                                             | `React Element`                                                                                            | no       | iOS,Android | yes               |
| footerComponent  | A component to render on bottom of Modal.                                                                                                                                                                                                                                                          | `React Element`                                                                                            | no       | iOS,Android | yes               |
| loadingComponent | A custom loading component.                                                                                                                                                                                                                                                                        | `React Element`                                                                                            | no       | iOS,Android | yes               |
| style            | Customize default style such as background color.                                                                                                                                                                                                                                                  | [`ViewStyle`](https://reactnative.dev/docs/view-style-props)                                               | no       | iOS,Android | yes               |
| modalProps       | Override the Modal props.                                                                                                                                                                                                                                                                          | [ModalProps](https://reactnative.dev/docs/modal)                                                           | no       | iOS,Android | yes               |
| webViewProps     | Override the WebView props.                                                                                                                                                                                                                                                                        | [WebViewProps](https://github.com/react-native-webview/react-native-webview/blob/master/docs/Reference.md) | no       | iOS,Android | yes               |
| lang             | [Language code](https://developers.google.com/recaptcha/docs/language).                                                                                                                                                                                                                            | `string`                                                                                                   | no       | iOS,Android | yes               |
| siteKey          | (Required) Your Web reCAPTCHA site key. (The Web key must be used, not for Android)                                                                                                                                                                                                                | `string`                                                                                                   | yes      | iOS,Android | yes               |
| baseUrl          | (Required) The URL (domain) configured in the reCAPTCHA console setup. (ex. http://my.domain.com) (See also https://github.com/douglasjunior/react-native-recaptcha-that-works/issues/34)                                                                                                          | `string`                                                                                                   | yes      | iOS,Android | yes               |
| size             | The size of the widget.                                                                                                                                                                                                                                                                            | `'invisible'`, `'normal'` or `'compact'`                                                                   | no       | iOS,Android | yes               |
| theme            | The color theme of the widget.                                                                                                                                                                                                                                                                     | `'dark'` or `'light'`                                                                                      | no       | iOS,Android | yes               |
| onLoad           | A callback function, executed when the reCAPTCHA is ready to use.                                                                                                                                                                                                                                  | `function()`                                                                                               | no       | iOS,Android | yes               |
| onVerify         | (Required) A callback function, executed when the user submits a successful response. The reCAPTCHA response token is passed to your callback.                                                                                                                                                     | `function(token)`                                                                                          | yes      | iOS,Android | yes               |
| onExpire         | A callback function, executed when the reCAPTCHA response expires and the user needs to re-verify. Only works if the `webview` still open after `onVerify` has been called for a long time.                                                                                                        | `function()`                                                                                               | no       | iOS,Android | yes               |
| onError          | A callback function, executed when reCAPTCHA encounters an error (usually network connectivity) and cannot continue until connectivity is restored. If you specify a function here, you are responsible for informing the user that they should retry.                                             | `function(error)`                                                                                          | no       | iOS,Android | yes               |
| onClose          | A callback function, executed when the Modal is closed.                                                                                                                                                                                                                                            | `function()`                                                                                               | no       | iOS,Android | yes               |
| recaptchaDomain  | The host name of the reCAPTCHA valid api. [See detail](https://developers.google.com/recaptcha/docs/faq#can-i-use-recaptcha-globally).                                                                                                                                                             | `string`                                                                                                   | no       | iOS,Android | yes               |
| hideBadge        | When `size = 'invisible'`, you are allowed to hide the badge as long as you include the reCAPTCHA branding visibly in the user flow. [See detail](https://developers.google.com/recaptcha/docs/faq#id-like-to-hide-the-recaptcha-badge.-what-is-allowed).                                          | `boolean`                                                                                                  | no       | iOS,Android | yes               |
| enterprise       | Use the new [reCAPTCHA Enterprise API](https://cloud.google.com/recaptcha-enterprise/docs/using-features). Note: for enterprise you need to choose the `size` [when creating the `siteKey`](https://github.com/douglasjunior/react-native-recaptcha-that-works/issues/55#issuecomment-2107089307). | `boolean` (enterprise)                                                                                     | no       | iOS,Android | yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name  | Description                | Type       | Required | Platform    | HarmonyOS Support |
| ----- | -------------------------- | ---------- | -------- | ----------- | ----------------- |
| open  | Open the reCAPTCHA Modal.  | `function` | no       | iOS,Android | yes               |
| close | Close the reCAPTCHA Modal. | `function` | no       | iOS,Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/douglasjunior/react-native-recaptcha-that-works/blob/master/LICENSE) ，请自由地享受和参与开源。
