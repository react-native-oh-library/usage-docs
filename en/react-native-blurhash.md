> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-blurhash</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mrousavy/react-native-blurhash">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mrousavy/react-native-blurhash/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-blurhash)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-blurhash Releases](https://github.com/react-native-oh-library/react-native-blurhash/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-blurhash@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-blurhash@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import React, { useCallback, useMemo, useState } from 'react';
import { Blurhash } from 'react-native-blurhash';
import {
    ActivityIndicator,
    Alert,
    SafeAreaView,
    StatusBar,
    StyleSheet,
    Switch,
    Text,
    TextInput,
    TouchableOpacity,
    View
} from 'react-native';

const COLORS = {
    background: '#F5FCFF',
    statusBar: 'rgba(100, 0, 100, 0.6)',
    textInput: 'rgba(200, 0, 100, 0.5)',
    button: 'rgba(200, 0, 100, 0.4)',
    switchEnabled: 'rgba(200, 0, 100, 0.5)',
    switchDisabled: 'rgba(200, 0, 100, 0.2)',
    switchThumb: 'white',
    shadow: 'black',
};
const SWITCH_THUMB_COLORS = {
    false: COLORS.switchDisabled,
    true: COLORS.switchEnabled,
};

const BlurhashDemo: React.FC = (): JSX.Element => {

    //#region State & Props
    const [blurhash, setBlurhash] = useState('LHK1gsM,rzD+4-xn,vWT~q=_ixS]');
    const [decodeAsync, setDecodeAsync] = useState(true);
    const [encodingImageUri, setEncodingImageUri] = useState(
        'http://gips2.baidu.com/it/u=3150002139,2124277596&fm=3028&app=3028&f=JPEG&fmt=auto?w=2048&h=2048'
    );
    const [isEncoding, setIsEncoding] = useState(false);
    const [isValiding, setIsVailding] = useState(false);
    //#endregion

    //#region Memos
    const buttonOpacity = useMemo(
        () => (encodingImageUri.length < 5 || isEncoding ? 0.5 : 1),
        [encodingImageUri.length, isEncoding],
    );
    const encodeButtonStyle = useMemo(
        () => [styles.encodeButton, { opacity: buttonOpacity }],
        [buttonOpacity],
    );
    //#endregion

    //#region Callbacks
    const onLoadStart = useCallback(() => {
        console.log('onLoadStart called!');
    }, []);
    const onLoadEnd = useCallback(() => {
        console.log('onLoadEnd called!');
    }, []);
    const onLoadError = useCallback((message?: string) => {
        console.log(`onLoadError called! Message: ${message}`);
    }, []);
    const startEncoding = useCallback(async () => {
        try {
            if (encodingImageUri.length < 5) return;
            setIsEncoding(true);
            const _blurhash = await Blurhash.encode(encodingImageUri, 4, 3);
            setBlurhash(_blurhash);
            setIsEncoding(false);
        } catch (e: any) {
            setIsEncoding(false);
            console.warn('Failed to encode!', e);
            Alert.alert('Encoding error', e.message);
        }
    }, [encodingImageUri]);
    const isVaild = () => {
        console.log(blurhash);
        const data = Blurhash.isBlurhashValid(blurhash)
        Alert.alert("blurhash is valid? : " + data.isValid)
        console.log(data);
    }
    const CCache = useCallback(() => {
        Blurhash.clearCosineCache()
    }, [])
    //#endregion

    return (
        <>
            <StatusBar backgroundColor={COLORS.statusBar} />
            <SafeAreaView style={styles.container}>
                <View style={styles.blurhashContainer}>
                    <View style={styles.blurhashRadiusMask}>
                        <Blurhash
                            blurhash={blurhash}
                            decodeWidth={32}
                            decodeHeight={32}
                            decodePunch={1}
                            decodeAsync={decodeAsync}
                            onLoadStart={onLoadStart}
                            onLoadEnd={onLoadEnd}
                            onLoadError={onLoadError}
                            style={styles.blurhashImage}
                            resizeMode="cover"
                        />
                    </View>
                </View>
                <TextInput
                    value={String(blurhash)}
                    placeholder="Blurhash"
                    onChangeText={setBlurhash}
                    style={styles.textInput}
                />
                {/* To test if `decodeAsync` really doesn't block the UI thread, you can press this Touchable and see it reacting. */}
                <View style={styles.row}>
                    <Text style={styles.text}>Decode Async:</Text>
                    <Switch
                        thumbColor={COLORS.switchThumb}
                        trackColor={SWITCH_THUMB_COLORS}
                        ios_backgroundColor={COLORS.switchDisabled}
                        value={decodeAsync}
                        onValueChange={setDecodeAsync}
                    />
                </View>
                <TextInput
                    value={encodingImageUri}
                    placeholder="Image URL to encode"
                    onChangeText={setEncodingImageUri}
                    style={styles.textInput}
                />
                <TouchableOpacity
                    style={encodeButtonStyle}
                    disabled={encodingImageUri.length < 5}
                    onPress={startEncoding}>
                    {isEncoding ? (
                        <ActivityIndicator color="black" />
                    ) : (
                        <Text>Encode</Text>
                    )}
                </TouchableOpacity>
            </SafeAreaView>
        </>
    );
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: COLORS.background,
    },
    blurhashContainer: {
        shadowRadius: 3,
        shadowColor: COLORS.shadow,
        shadowOffset: {
            height: 2,
            width: 0,
        },
        shadowOpacity: 0.4,
        overflow: 'visible',
    },
    blurhashRadiusMask: {
        elevation: 5,
        // borderRadius has to be applied to the parent
        borderRadius: 5,
        overflow: 'hidden',
    },
    blurhashImage: {
        width: 300,
        height: 200,
        // Custom styling for width, height, scaling etc here
    },
    textInput: {
        marginTop: 20,
        borderRadius: 5,
        borderWidth: 1,
        borderColor: COLORS.textInput,
        width: '70%',
        height: 35,
        paddingHorizontal: 20,
        textAlign: 'center',
    },
    row: {
        marginTop: 30,
        flexDirection: 'row',
        alignItems: 'center',
    },
    text: {
        fontSize: 16,
        marginRight: 15,
    },
    encodeButton: {
        height: 37,
        width: 120,
        marginTop: 30,
        backgroundColor: COLORS.button,
        borderRadius: 10,
        paddingVertical: 10,
        paddingHorizontal: 35,
        justifyContent: 'center',
    },
});

export default BlurhashDemo
```

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

### 2.Introducing Native Code

Currently, two methods are available:

 

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-blurhash": "file:../../node_modules/@react-native-oh-tpl/react-native-blurhash/harmony/blurhash.har"
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

### 3. Configuring CMakeLists and Introducing BlurhashPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-blurhash/src/main/cpp" ./blurhash)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_blurhash)
# RNOH_END: manual_package_linking_2

```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "BlurhashPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
    	std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<BlurhashPackage>(ctx)
    };
}
```

### 4. Introducing BlurhashPackage to ArkTS

 Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import {BlurhashPackage} from '@react-native-oh-tpl/react-native-blurhash/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new BlurhashPackage(ctx),
  ];
}

```

### 5.Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-blurhash Releases](https://github.com/react-native-oh-library/react-native-blurhash/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                       | Description                                                  | Type      | Required | Platform | HarmonyOS Support |
| ------------------------------------------ | ------------------------------------------------------------ | --------- | -------- | -------- | ----------------- |
| `blurhash`                                 | The blurhash string to use. Example: `LGFFaXYk^6#M@-5c,1J5@[or[Q6.` | string    | yes      | All      | yes               |
| `decodeWidth?`                             | The width (resolution) to decode to. Higher values decrease performance, use `16` for large lists, otherwise you can increase it to `32`. | number    | no       | All      | yes               |
| `decodeHeight?`                            | The height (resolution) to decode to. Higher values decrease performance, use `16` for large lists, otherwise you can increase it to `32`. | number    | no       | All      | yes               |
| `decodePunch?`                             | Adjusts the contrast of the output image. Tweak it if you want a different look for your placeholders. | number    | no       | All      | yes               |
| `decodeAsync?`                             | Asynchronously decode the Blurhash on a background Thread instead of the UI-Thread. | boolean   | no       | All      | yes               |
| `resizeMode?`                              | Sets the resize mode of the image. (no, `'repeat'` is not supported.) | enum      | no       | All      | yes               |
| `onLoadStart?: () => void`                 | A callback to call when the Blurhash started to decode the given `blurhash` string. | function  | no       | All      | yes               |
| `onLoadEnd?: () => void`                   | A callback to call when the Blurhash successfully decoded the given `blurhash` string and rendered the image to the `<Blurhash>` view. | function  | no       | All      | yes               |
| `onLoadError?: (message?: string) => void` | A callback to call when the Blurhash failed to load. Use the `message` parameter to get the error message. | function  | no       | All      | yes               |
| All `View` props                           | All properties from the React Native `View`. Use `style.width` and `style.height` for display-sizes. Also, `style.borderRadius` is natively supported on iOS. | ViewProps | no       | All      | yes               |


## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                                                  | Type                                                         | Required | Platform | HarmonyOS Support |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| encode()           | Encodes the given image URI to a blurhash string             | (imageUri: string, componentsX: number, componentsY: number)=> Promise\<string>; | no       | All      | yes               |
| clearCosineCache() | Clears the cosine cache and frees up memory.                 | ()=> void                                                    | no       | All      | yes               |
| getAverageColor)   | Gets the average color in a given blurhash string.           | (blurhash: string)=> RGB \|undefined;                        | no       | All      | yes               |
| isBlurhashValid()  | Verifies if the given blurhash is valid by checking it's type, length and size flag. | (blurhash: string)=> ReturnType\<typeof isBlurhashValid>;    | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mrousavy/react-native-blurhash/blob/master/LICENSE).