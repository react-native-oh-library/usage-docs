> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-apple-authentication</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/invertase/react-native-apple-authentication">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/invertase/react-native-apple-authentication/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-apple-authentication)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-library/react-native-apple-authentication Releases](https://github.com/react-native-oh-library/react-native-apple-authentication/releases). For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-apple-authentication
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-apple-authentication
```

#### **Configuring Sign in with Apple for the Web**

Configure the client ID: [Initial Development Environment Setup](https://github.com/invertase/react-native-apple-authentication/blob/main/docs/INITIAL_SETUP.md).

Set the service: [Services setup](https://github.com/invertase/react-native-apple-authentication/blob/main/docs/ANDROID_EXTRA.md).

Configure the official Apple description: [Configure Sign in with Apple for the web](https://developer.apple.com/help/account/configure-app-capabilities/configure-sign-in-with-apple-for-the-web)

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React from "react";
import {
  appleAuthHarmony,
  AppleButton,
} from "@invertase/react-native-apple-authentication";

const AppleAuthenticationDemo: React.FC = (): JSX.Element => {
  return (
    <>
      <AppleButton
        onPress={async () => {
          appleAuthHarmony.configure({
            // For the following configuration,please refer to the original library AppleId login document:
            // https://github.com/invertase/react-native-apple-authentication/blob/main/docs/INITIAL_SETUP.md
            // https://github.com/invertase/react-native-apple-authentication/blob/main/docs/ANDROID_EXTRA.md
            clientId: "com.example.client",
            redirectUri: "https://example.com",
          });
          const singInRes = await appleAuthHarmony.signIn();
          console.log(singInRes);
        }}
      />
    </>
  );
};

export default AppleAuthenticationDemo;
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
    "@react-native-oh-tpl/react-native-apple-authentication": "file:../../node_modules/@react-native-oh-tpl/react-native-apple-authentication/harmony/react-native-apple-authentication.har"
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

### 3. Introducing RNAppleAuthPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNAppleAuthPackage } from '@react-native-oh-tpl/react-native-apple-authentication';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNAppleAuthPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-apple-authentication Releases](https://github.com/react-native-oh-library/react-native-apple-authentication/releases).

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**AppleButton**: Apple authentication button

| Name         | Description        | Type                                                         | Required | Platform | HarmonyOS Support |
| ------------ | ------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| style        | Button style.          | StyleProp< [ViewStyle](https://gitee.com/link?target=https%3A%2F%2Freactnative.dev%2Fdocs%2Fview%23props) > | no       | all      | yes               |
| textStyle    | Text style.    | StyleProp< [TextStyle](https://gitee.com/link?target=https%3A%2F%2Freactnative.dev%2Fdocs%2Ftext%23props) > | no       | all      | yes               |
| cornerRadius | Corner radius of the border.  | number                                                       | no       | all      | yes               |
| buttonStyle  | Button style (preset enumeration).| [AppleButtonStyle](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Finvertase%2Freact-native-apple-authentication%2Fblob%2Fmain%2Ftypedocs%2Fenums%2FAppleButtonStyle.md) | no       | all      | yes               |
| buttonType   | Button type (preset enumeration).| [AppleButtonType](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Finvertase%2Freact-native-apple-authentication%2Fblob%2Fmain%2Ftypedocs%2Fenums%2FAppleButtonType.md) | no       | all      | yes               |
| onPress      | Touch event.      | () => void                                                   | yes      | all      | yes               |
| leftView     | Left icon of the button.    | ReactNode                                                    | no       | all      | yes               |
| buttonText   | Button text.    | string                                                       | no       | all      | yes               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**appleAuthHarmony**: Apple authentication object, including two methods

| Name      | Description                                             | Type                                                         | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| configure | Configures Apple authentication information. This API must be called before **signIn**.| ([Config](https://github.com/invertase/react-native-apple-authentication/blob/main/typedocs/interfaces/AndroidConfig.md)) => void | no       | all      | yes               |
| signIn    | Pops up the WebView for Apple authentication.                     | () => Promise< [SigninResponse](https://github.com/invertase/react-native-apple-authentication/blob/main/typedocs/interfaces/AndroidSigninResponse.md) > | no       | all      | no                |

## Others

## Known Issues

- [ ] Due to Apple developer account authentication issues, the following API is not supported by HarmonyOS: [issue#1](https://github.com/react-native-oh-library/react-native-apple-authentication/issues/1).

## License

This project is licensed under [Apache License 2.0](https://github.com/invertase/react-native-apple-authentication/blob/main/LICENSE).
