
> Template version：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-file-selector</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/prscX/react-native-file-selector">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/prscX/react-native-file-selector/blob/master/README.md">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-file-selector)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-file-selector Releases](https://github.com/react-native-oh-library/react-native-file-selector/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:




#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-file-selector
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-file-selector
```


The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import FileSelector from 'react-native-file-selector';
import React from 'react';
function App(): React.JSX.Element {
  
  return (
    <FileSelector
      onDone={(path) => {console.log("file selected: " + path);}}
      onCancel={() => {console.log("cancelled");}}
    />)
};
export default App;
```

## Use Codegen

If this repository has been adapted to Codegen, generate the bridge code of the third-party library by using the Codegen. For details, see[ Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the harmony directory of the HarmonyOS project in DevEco Studio.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

1. Use the HAR file.（recommended）；
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-file-selector": "file:../../node_modules/@react-native-oh-tpl/react-native-file-selector/harmony/file_selector.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see[Directly Linking Source Code](/en/link-source-code.md)


### 3.Introducing RNFileSelectorPackage Package to ArkTS

Open the entry/src/main/ets/RNPackagesFactory.ts file and add the following code:

```diff
  ...
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';
+import {RNFileSelectorPackage}  from '@react-native-oh-tpl/react-native-file-selector/ts';


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new RNFileSelectorPackage(ctx)
  ];
}
```

### 4.Running

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-file-selector Releases](https://github.com/react-native-oh-library/react-native-file-selector/releases)

## Properties

 FileSelector

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| :--- | ----------- | ---- | -------- | -------- | ------------------ |
| filter | Filter to sort the files | string | no | All | yes |
| path | Path of directory | string | no | All | yes |
| onDone | Function called when file is selected | func | no | All | yes |
| onCancel | Function called when file selector is closed without selecting any file | func | no | All | yes |
| title | Title on the toolbar | string | no | Android iOS | no |
| closeMenu | Color of tint | string | no | Android iOS | no |
| hiddenFiles | If true it shows hidden files as well | bool | no | Android | no |
| filterDirectories | Filter should be applied on directories or not | bool | no | Android | no |

## API

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Show | present a fileselector  | function  | no | All      | yes |

 Show

```js
Show(filter?: string, path?: string, onDone?: func, onCancel?: func, title?: string, closeMenu?: string, hiddenFiles?: bool, filterDirectories?: bool);
```

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| :--- | ----------- | ---- | -------- | -------- | ------------------ |
| filter | Filter to sort the files | string | no | All | yes |
| path | Path of directory | string | no | All | yes |
| onDone | Function called when file is selected | func | no | All | yes |
| onCancel | Function called when file selector is closed without selecting any file | func | no | All | yes |
| title | Title on the toolbar | string | no | Android iOS | no |
| closeMenu | Color of tint | string | no | Android iOS | no |
| hiddenFiles | If true it shows hidden files as well | bool | no | Android | no |
| filterDirectories | Filter should be applied on directories or not | bool | no | Android | no |

## Known Issues


- [ ] FileSelector title：harmony issue: [issue#4](https://github.com/react-native-oh-library/react-native-file-selector/issues/4)
- [ ] FileSelector closeMenu：harmony issue: [issue#5](https://github.com/react-native-oh-library/react-native-file-selector/issues/5)
- [ ] FileSelector hiddenFiles：harmony issue: [issue#6](https://github.com/react-native-oh-library/react-native-file-selector/issues/6)
- [ ] FileSelector filterDirectories：harmony issue: [issue#7](https://github.com/react-native-oh-library/react-native-file-selector/issues/7)

- [ ] Show title：harmony issue: [issue#4](https://github.com/react-native-oh-library/react-native-file-selector/issues/4)
- [ ] Show closeMenu：harmony issue: [issue#5](https://github.com/react-native-oh-library/react-native-file-selector/issues/5)
- [ ] Show hiddenFiles：harmony issue: [issue#6](https://github.com/react-native-oh-library/react-native-file-selector/issues/6)
- [ ] Show filterDirectories：harmony issue: [issue#7](https://github.com/react-native-oh-library/react-native-file-selector/issues/7)

## Others

## License

This project is licensed under [Apache License 2.0](https://github.com/prscX/react-native-file-selector/blob/master/LICENSE).