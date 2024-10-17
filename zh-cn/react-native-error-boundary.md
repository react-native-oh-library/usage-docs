<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-error-boundary</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/carloscuesta/react-native-error-boundary">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/carloscuesta/react-native-error-boundary/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/carloscuesta/react-native-error-boundary)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm i react-native-error-boundary@1.2.4
```

#### **yarn**

```bash
yarn add react-native-error-boundary@1.2.4
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```ts
import React, { PropsWithChildren, useState } from 'react';
import { StyleSheet, Button } from 'react-native';
import ErrorBoundary from 'react-native-error-boundary';

export const ErrorBoundaryDefaultExample = () => {
    const [shouldThrow, setShouldThrow] = useState(false);

    return (
        <ErrorBoundary>
            <Button
                title="Click the button, it will throw a exception and show a default error page"
                onPress={() => {
                    setShouldThrow(true);
                }}
            />
            {shouldThrow && (<MaybeThrows>Content</MaybeThrows>)}
        </ErrorBoundary>
    );
};

function MaybeThrows({ children }: PropsWithChildren) {
    const valueToThrow = new Error("Throw a new exception");
    throw valueToThrow;
}

const styles = StyleSheet.create({
    buttonContainer: {
        width: 80,
        height: 80,
    },
    box: {
        height: 100,
        width: 50,
    },
});
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### ErrorBoundary

| Name              | Description                     | Type           | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------- | -------------- | -------- | ----------- | ----------------- |
| Children        | Any children that can throw an error       | React.Children | Yes       | iOS/Android | Yes               |
| FallbackComponent       | The fallback component that will be rendered after catching an error. By default the library comes with a built-in component.         | React.Component | No       | iOS/Android | Yes               |
| onError | A function to log the errors that happen in your application  | Function | No       | iOS/Android | Yes               |

#### FallbackComponent
| Name              | Description                     | Type           | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------- | -------------- | -------- | ----------- | ----------------- |
| error        | The error object       | Error | Yes       | iOS/Android | Yes               |
| resetError       | A function to reset the error state. You'll want to call this function to recover from the error state.         | Function | Yes       | iOS/Android | Yes               |

#### onError
```js
onError(error: Error, stackTrace: string): void
```
| Name              | Description                     | Type           | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------- | -------------- | -------- | ----------- | ----------------- |
| error        | The error catched by the component       | Error | Yes       | iOS/Android | Yes               |
| stackTrace       | The stacktrace of the error         | string | Yes       | iOS/Android | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/carloscuesta/react-native-error-boundary/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->
