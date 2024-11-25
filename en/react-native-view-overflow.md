> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-view-overflow</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/entria/react-native-view-overflow">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/entria/react-native-view-overflow/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-view-overflow)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-view-overflow Releases](https://github.com/react-native-oh-library/react-native-view-overflow/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-view-overflow
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-view-overflow
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import {View} from 'react-native';

import ViewOverflow from 'react-native-view-overflow';

export function ViewOverflowDemo() {
  return (
  <View style={{height: '100%', backgroundColor: 'white', padding: 10}}>

    <View style={{width: 200, height: 100, backgroundColor: 'red'}}>
      <ViewOverflow style={{width: 100, height: 50, backgroundColor: 'blue'}}>
          <ViewOverflow style={{width: 50, height: 25, backgroundColor: 'skyblue', left: 60, top: 30}}>
            <View style={{backgroundColor: 'yellow', height: '100%', left: 20, top: 10}} />
          </ViewOverflow>
      </ViewOverflow>
    </View>

  </View>
  );
}
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [react-native-view-overflow Releases](https://github.com/react-native-oh-library/react-native-view-overflow/releases)

## Properties
[!TIP] This library can be used as a container component similar to the View component, allowing child controls to overflow and be displayed outside the parent layout. It can be used with public properties only and does not involve private properties or API methods.

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/entria/react-native-view-overflow/blob/master/LICENSE).
