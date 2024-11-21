> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-spinkit</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/maxs15/react-native-spinkit">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/maxs15/react-native-spinkit/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-spinkit)


## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-spinkit Releases](https://github.com/react-native-oh-library/react-native-spinkit/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-spinkit
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-spinkit
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import Spinkit from 'react-native-spinkit';

const SpinKitDemo: React.FC = (): JSX.Element => {
    return (
    	<Spinkit 
        	type='9CubeGrid' 
        	color='#e74032' 
        	size={60} 
			style={{ backgroundColor: '#fcc424' }} 
            isVisible={true} 
		/>
    )
};

export default SpinKit;
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
    "@react-native-oh-tpl/react-native-spinkit": "file:../../node_modules/@react-native-oh-tpl/react-native-spinkit/harmony/spinKit.har"
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

### 3. Introducing SpinKitView Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { SpinKitView } from "@react-native-oh-tpl/react-native-spinkit"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === SpinKitView.NAME) {
+   SpinKitView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+   })
+ }
 ...
}
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added. 

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ SpinKitView.NAME
  ];
```
### 4. Introducing SpinKitPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNSpinKitPackage } from '@react-native-oh-tpl/react-native-spinkit/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNSpinKitPackage(ctx)
  ];
}
```

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```


Then build and run the code.

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.


Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-spinkit Releases](https://github.com/react-native-oh-library/react-native-spinkit/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**SpinKit**：Loading Animation Rendering Component, Accepts All Parameters [View](https://reactnative.dev/docs/view#props) 的props。

| props  | Description | Type | Required | Platform | HarmonyOS Support  |
| ----  | ----------- | ---- | -------- | ---- | ------------ |
| type                  | Types of Load Animations                                    | string  | No       | All      | Yes               |
| type: Plane           | One Direction Flip Loading Animation                        | string  | No       | All      | Yes               |
| type: CircleFlip      | A circle flips to load animation                            | string  | No       | All      | Yes               |
| type: Bounce          | A circular nested loading animation | string | No | All | Yes |
| type: Wave | Five-bar group loading animation | string | No | All | Yes |
| type: WanderingCubes | Two squares skip loading animation | string | No | All | Yes |
| type: Pulse | A circular diffusion loading animation | string | No | All | Yes |
| type: ChansingDots | Two Circles Bounce Loading Animation | string | No | All | Yes |
| type: ThreeBounce | Three circles display the loading animation in sequence. | string | No | All | Yes |
| type: Circle | Multiple circular circular motion loading animation | string | No | All | Yes |
| type: 9CubeGrid | The nine squares display the loading animation in sequence | string | No | All | Yes |
| type: WordPress | Round wheel inline hollow circle rotating Loading animation | string | No | IOS | Yes |
| type: FadingCircle | Multiple square circular motion loading animation | string | No | All | Yes |
| type: FadingCircleAlt | Multiple circular circular motion loading animation | string | No | All | Yes |
| type: Arc | Rotating ring with notch loading animation | string | No | IOS | Yes |
| type: ArcAlt | Circular progress bar style loading animation | string | No | IOS | Yes |
| isVisible | Visibility of the spinner | boolean | No | All | Yes |
| color | Color of the spinner | string | No | All | Yes |
| size | Visibility of the spinner | number | No | All | Yes |


## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/maxs15/react-native-spinkit/blob/master/LICENSE).
