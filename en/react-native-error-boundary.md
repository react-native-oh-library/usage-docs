<!-- {% raw %} -->

> Template version: v0.2.2

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

> [!TIP] [ GitHub address](https://github.com/carloscuesta/react-native-error-boundary)

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```ts
import React, { PropsWithChildren, useState } from "react";
import { StyleSheet, Button } from "react-native";
import ErrorBoundary from "react-native-error-boundary";

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
      {shouldThrow && <MaybeThrows>Content</MaybeThrows>}
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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400; ROM: 3.0.0.25;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### ErrorBoundary

| Name              | Description                                                                                                                   | Type            | Required | Platform    | HarmonyOS Support |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------- | --------------- | -------- | ----------- | ----------------- |
| Children          | Any children that can throw an error                                                                                          | React.Children  | Yes      | iOS/Android | Yes               |
| FallbackComponent | The fallback component that will be rendered after catching an error. By default the library comes with a built-in component. | React.Component | No       | iOS/Android | Yes               |
| onError           | A function to log the errors that happen in your application                                                                  | Function        | No       | iOS/Android | Yes               |

#### FallbackComponent

| Name       | Description                                                                                             | Type     | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| error      | The error object                                                                                        | Error    | Yes      | iOS/Android | Yes               |
| resetError | A function to reset the error state. You'll want to call this function to recover from the error state. | Function | Yes      | iOS/Android | Yes               |

#### onError

```js
onError(error: Error, stackTrace: string): void
```

| Name       | Description                        | Type   | Required | Platform    | HarmonyOS Support |
| ---------- | ---------------------------------- | ------ | -------- | ----------- | ----------------- |
| error      | The error catched by the component | Error  | Yes      | iOS/Android | Yes               |
| stackTrace | The stacktrace of the error        | string | Yes      | iOS/Android | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/carloscuesta/react-native-error-boundary/blob/master/LICENSE).

<!-- {% endraw %} -->
