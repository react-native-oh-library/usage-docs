> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-safe-module</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lelandrichardson/react-native-safe-module">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lelandrichardson/react-native-safe-module/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-safe-module)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-safe-module Releases](https://github.com/react-native-oh-library/react-native-safe-module/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.


Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-safe-module
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-safe-module
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import { View } from 'react-native';
import SafeModule from 'react-native-safe-module';

const App = () => {
  const NativeLottieView = SafeModule.component({
    viewName: 'LottieAnimationView',
    mockComponent: View,
  });
  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      <NativeLottieView
        style={{backgroundColor: 'red', width: 100, height: 100}}
      />
    </View>
  );
};

export default App;
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-safe-module Releases](https://github.com/react-native-oh-library/react-native-safe-module/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


Name | Description | Type | Required | Platform | HarmonyOS   Support
-- | -- | -- | -- | -- | --
SafeModule.create(options) | create Module | Object | Yes | iOS/Android | Yes 

**options**：SafeModule.create(options)  Parameters

| Name                                                      | Description                                                                                                         | Type     | Required | Platform | HarmonyOS Support |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| options.moduleName                                             |  The name, or array of names, to look for the module at on the NativeModules namespace.                                                                                      | string/Array<string> | Yes       | iOS/Android      | Yes               |
| options.mock                                              | The mock implementation of the native module.                                        | mixed | Yes       | iOS/Android      | Yes               |
| options.getVersion                                | A function that returns the version of the native module. Only needed if you are specifying overrides and not exporting a VERSION property on your native module. Defaults to x => x.VERSION.                                                                                                  | (module) => string/number | No       | iOS/Android      | Yes                |
| options.overrides                                 | A map of version numbers to overridden implementations of the corresponding property/method. If an overridden property or method is a function, it will be called during SafeModule.create(...) with two arguments, the original value of that property on the original module, and the original module itself. The return value of this function will be put on the return value of SafeModule.create(...).                                                                                                  | [version: string]: mixed   | No       | iOS/Android      | Yes               |
| options.isEventEmitter                              |  A flag indicating that the native module is expected to be an EventEmitter. Puts the EventEmitter instance on the emitter property of the resulting module. Defaults to false.                                                                                                  | bool   | No       | iOS/Android      | Yes                |


## Known Issues


## Others

## License

This project is licensed under [MIT License](https://github.com/lelandrichardson/react-native-safe-module/blob/master/LICENSE).