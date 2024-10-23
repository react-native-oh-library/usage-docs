### 2. Introducing Native Code

#### Direct Linking of Source Code

Currently, DevEco Studio does not support the introduction of external modules through source code. We recommend using the HAR package method for this purpose. However, if you need to directly link source code, please follow the steps below to integrate the source code into an internal module of the Harmony project.

> [!TIP] The source code is located in the `harmony` folder under the installation path of the third-party library.

Copy the source code `<xxx>` from the `<RN Project>/node_modules/@react-native-oh-tpl/<Package_Name>/harmony/` directory to the root directory of the `harmony` project.

Add the following module to the `build-profile.template.json5` (if exists) and `build-profile.json5` at the root directory of the `harmony` project:

```json
modules:[
  ...
  {
    name: '<xxx>',
    srcPath: './<xxx>',
  }
  // example:
  //      {
  //        name: 'safe_area',
  //        srcPath: './safe_area',
  //      } 
]
```

Open `entry/oh-package.json5` and add the following dependency:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/<Package_Name>": "file:../<xxx>"
    // 提示: "@react-native-oh-tpl/react-native-safe-area-context": "file:../safe_area"
  }
```

Click on the `sync` button in the upper right corner.

Or run the following in the terminal:

```bash
cd entry
ohpm install
```
