> 模板版本：v0.2.2

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



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-blurhash)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-blurhash Releases](https://github.com/react-native-oh-library/react-native-blurhash/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-blurhash": "file:../../node_modules/@react-native-oh-tpl/react-native-blurhash/harmony/blurhash.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 配置 CMakeLists 和引入 BlurhashPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 在 ArkTs 侧引入 BlurhashPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
+ import {BlurhashPackage} from '@react-native-oh-tpl/react-native-blurhash/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new BlurhashPackage(ctx),
  ];
}

```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-blurhash Releases](https://github.com/react-native-oh-library/react-native-blurhash/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                                  | Type                                                         | Required | Platform | HarmonyOS Support |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| encode()           | Encodes the given image URI to a blurhash string             | (imageUri: string, componentsX: number, componentsY: number)=> Promise\<string>; | no       | All      | yes               |
| clearCosineCache() | Clears the cosine cache and frees up memory.                 | ()=> void                                                    | no       | All      | yes               |
| getAverageColor)   | Gets the average color in a given blurhash string.           | (blurhash: string)=> RGB \|undefined;                        | no       | All      | yes               |
| isBlurhashValid()  | Verifies if the given blurhash is valid by checking it's type, length and size flag. | (blurhash: string)=> ReturnType\<typeof isBlurhashValid>;    | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/mrousavy/react-native-blurhash/blob/master/LICENSE) ，请自由地享受和参与开源。