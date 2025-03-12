> Template version: v0.2.2

<p align="center">
  <h1 align="center"> 
    <code>react-native-incall-manager</code> 
  </h1>
</p>

<p align="center">
    <a href="https://github.com/react-native-webrtc/react-native-incall-manager">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-webrtc/react-native-incall-manager/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-ISC-red.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-incall-manager)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-incall-manager Releases](https://github.com/react-native-oh-library/react-native-incall-manager/releases).

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-incall-manager
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-incall-manager
```

<!-- tabs:end -->

**Storing Audio Files**

> [!WARNING] HarmonyOS does not allow common applications to obtain system ringtones. You need to import audio files
> to the **/entry/src/main/resources/rawfile** folder of the HarmonyOS project. The audio files should be named as follows:
> incallmanager_busytone.mp3  
> incallmanager_ringback.mp3  
> incallmanager_ringtone.mp3

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js

import { useState, useEffect } from 'react';
import * as React from 'react';
import {
    DeviceEventEmitter,
    NativeModules,
    NativeEventEmitter,
    Platform,
    SafeAreaView,
    View,
    Text,
    ScrollView,
    TouchableOpacity,
    TurboModuleRegistry,
} from 'react-native';
import InCallManager from 'react-native-incall-manager';
const InCallManagerEmitter = new NativeEventEmitter(TurboModuleRegistry.getEnforcing('InCallManagerTurboModule') ? TurboModuleRegistry.getEnforcing('InCallManagerTurboModule') : NativeModules.InCallManager);


enum InCallStartType {
    START = 'start',
    RINGBACK = 'ringback',
    BUSYTONE = 'busytone',
    RINGTONE = 'ringtone',
}

export default function InCallManagerExample() {
    const [changeType, setChangeType] = useState<'audio' | 'video' | undefined>(
        'audio',
    );
    const [audioUriJS, setAudioUri] = useState('');
    const [wiredHeadsetPluggedInObj, setWiredHeadsetPluggedInObj] =
        useState<Object>();
    const [audioRoute, setAudioRoute] = useState('');
    const [proximityEvent, setProximityEvent] = useState<Object>();
    const [wiredHeadsetEvent, setWiredHeadsetEvent] = useState<Object>();
    const [noisyAudioEvent, setNoisyAudioEvent] = useState<Object>();
    const [mediaButtonEvent, setMediaButtonEvent] = useState<Object>();
    const [onAudioFocusChange, setAudioFocusChangeEvent] = useState<Object>();

    const proximityHandleFuc = (data: any) => {
        // data: {'isNear': boolean}
        console.log('Proximity', data);
        setProximityEvent(data);
    };

    useEffect(() => {
        const proximityHandle = InCallManagerEmitter.addListener(
            'Proximity',
            proximityHandleFuc,
        );

        const wiredHeadsetHandle = InCallManagerEmitter.addListener(
            'WiredHeadset',
            wiredHeadsetHandleFuc,
        );

        return () => {
            proximityHandle.remove();
            wiredHeadsetHandle.remove();
        };
    }, []);

    useEffect(() => {
        if (Platform.OS === 'android' || Platform.OS === 'harmony') {
            const noisyAudioHandle = InCallManagerEmitter.addListener(
                'NoisyAudio',
                noisyAudioHandleFuc,
            );

            const mediaButtonHandle = InCallManagerEmitter.addListener(
                'MediaButton',
                mediaButtonHandleFuc,
            );

            const onAudioFocusChangeHandle = InCallManagerEmitter.addListener(
                'onAudioFocusChange',
                onAudioFocusChangeHandleFuc,
            );

            return () => {
                noisyAudioHandle.remove();
                mediaButtonHandle.remove();
                onAudioFocusChangeHandle.remove();
            };
        }
    }, []);

    function wiredHeadsetHandleFuc(data: any) {
        // data: {'isPlugged': boolean, 'hasMic': boolean, 'deviceName': string }
        console.log('WiredHeadset', data);
        setWiredHeadsetEvent(data);
    }

    function noisyAudioHandleFuc(data: any) {
        // data: {}
        console.log('NoisyAudio', data);
        setNoisyAudioEvent(data);
    }

    function mediaButtonHandleFuc(data: any) {
        // data: {'eventText': string, 'eventCode': number }
        console.log('MediaButton', data);
        setMediaButtonEvent(data);
    }

    function onAudioFocusChangeHandleFuc(data: any) {
        // data: {'eventText': string, 'eventCode': number }
        console.log('onAudioFocusChange', data);
        setAudioFocusChangeEvent(data);
    }

    const startAudio = (
        typeStr: string,
        ringType = '_DEFAULT_',
        mediaType: 'audio' | 'video' | undefined = 'audio',
    ) => {

        if (typeStr === InCallStartType.START) {
            InCallManager.start({ media: mediaType }); // audio/video, default: audio
        }
        if (typeStr === InCallStartType.RINGBACK) {
            InCallManager.start({ media: mediaType, ringback: ringType }); // or _DEFAULT_ or _DTMF_ or _BUNDLE_
        }
        if (typeStr === InCallStartType.RINGTONE) {
            InCallManager.startRingtone(ringType, [0,500,1000,500], 'playback', 1000);
        }
    };

    const stopAudio = (typeStr: string, ringType = '_DEFAULT_') => {
        // --- On Call Hangup:
        if (typeStr === InCallStartType.START) {
            InCallManager.stop();
        }
        if (typeStr === InCallStartType.RINGBACK) {
            InCallManager.stopRingback();
        }
        if (typeStr === InCallStartType.BUSYTONE) {
            // busytone is basically for OUTGOING call. and is part of stop()
            // If the call failed or callee are busing,
            // you may want to stop the call and play busytone
            InCallManager.stop({ busytone: ringType }); // or _BUNDLE_ or _DEFAULT_ or _DTMF_
        }
        if (typeStr === InCallStartType.RINGTONE) {
            InCallManager.stopRingtone();
        }
        // ... it will also remove event listeners ...
    };

    const turnScreenOn = () => {
        InCallManager.turnScreenOn();
    };

    const turnScreenOff = () => {
        InCallManager.turnScreenOff();
    };

    const setKeepScreenOn = (enable: boolean) => {
        InCallManager.setKeepScreenOn(enable);
    };

    const getAudioUriJS = async (audioType: string, fileType: string) => {
        let url = await InCallManager.getAudioUri(audioType, fileType);
        setAudioUri(url ? url : '');
    };

    const getIsWiredHeadsetPluggedIn = async (
        audioType: string,
        fileType: string,
    ) => {
        let isWiredHeadsetPluggedInObj =
            await InCallManager.getIsWiredHeadsetPluggedIn();
        setWiredHeadsetPluggedInObj(
            isWiredHeadsetPluggedInObj ? isWiredHeadsetPluggedInObj : '',
        );
    };

    const setFlashOn = async (enable: boolean, brightness: number) => {
        InCallManager.setFlashOn(enable, brightness);
    };

    const startProximitySensor = () => {
        InCallManager.startProximitySensor();
    };

    const stopProximitySensor = () => {
        InCallManager.stopProximitySensor();
    };


    return (
        <SafeAreaView style={{ flex: 1, backgroundColor: '#fff' }}>
            <View>
                <Text numberOfLines={0} style={{ color: 'blue' }}>
                    EVENT:
                </Text>

                <Text numberOfLines={0} style={{ color: 'blue' }}>
                    proximityEvent:{JSON.stringify(proximityEvent)}
                </Text>

                <Text numberOfLines={0} style={{ color: 'blue' }}>
                    wiredHeadsetEvent:{JSON.stringify(wiredHeadsetEvent)}
                </Text>

                <Text numberOfLines={0} style={{ color: 'blue' }}>
                    noisyAudioEvent(iOS is not supported):{JSON.stringify(noisyAudioEvent)}
                </Text>

                <Text numberOfLines={0} style={{ color: 'blue' }}>
                    mediaButtonEvent(iOS is not supported):{JSON.stringify(mediaButtonEvent)}
                </Text>

                <Text numberOfLines={0} style={{ color: 'blue' }}>
                    onAudioFocusChange(iOS is not supported):{JSON.stringify(onAudioFocusChange)}
                </Text>

                <TouchableOpacity
                    style={{ padding: 5 }}
                    onPress={() => {
                        stopAudio(InCallStartType.START);
                        setChangeType(changeType == 'audio' ? 'video' : 'audio');
                    }}>
                    <Text style={{ color: 'red' }}>
                        Switch to{changeType == 'audio' ? 'video' : 'audio'}
                    </Text>
                </TouchableOpacity>
            </View>

            <ScrollView style={{ flex: 1 }}>
                <TouchableOpacity
                    onPress={() => {
                        startAudio(InCallStartType.START, '_DEFAULT_', changeType);
                    }}>
                    <Text style={{ color: '#000' }}>start{changeType}</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        stopAudio(InCallStartType.START);
                    }}>
                    <Text style={{ color: '#000' }}>stop{changeType}</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        startAudio(InCallStartType.RINGTONE, '_BUNDLE_', changeType);
                    }}>
                    <Text style={{ color: '#000' }}>
                        start{changeType}RINGTONE:_BUNDLE_
                    </Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        startAudio(InCallStartType.RINGTONE, '_DEFAULT_', changeType);
                    }}>
                    <Text style={{ color: '#000' }}>
                        start{changeType}RINGTONE:_DEFAULT_
                    </Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        stopAudio(InCallStartType.RINGTONE);
                    }}>
                    <Text style={{ color: '#000' }}>stop{changeType}RINGTONE</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        startAudio(InCallStartType.RINGBACK, '_BUNDLE_', changeType);
                    }}>
                    <Text style={{ color: '#000' }}>
                        start{changeType}RINGBACK:_BUNDLE_
                    </Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        startAudio(InCallStartType.RINGBACK, '_DEFAULT_', changeType);
                    }}>
                    <Text style={{ color: '#000' }}>
                        start{changeType}RINGBACK:_DEFAULT_
                    </Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        startAudio(InCallStartType.RINGBACK, '_DTMF_', changeType);
                    }}>
                    <Text style={{ color: '#000' }}>start{changeType}RINGBACK:_DTMF_</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        stopAudio(InCallStartType.RINGBACK);
                    }}>
                    <Text style={{ color: '#000' }}>stop{changeType}RINGBACK</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        stopAudio(InCallStartType.BUSYTONE, '_BUNDLE_');
                    }}>
                    <Text style={{ color: '#000' }}>stop{changeType}BUSYTONE:_BUNDLE_</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        stopAudio(InCallStartType.BUSYTONE, '_DEFAULT_');
                    }}>
                    <Text style={{ color: '#000' }}>
                        stop{changeType}BUSYTONE:_DEFAULT_
                    </Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        stopAudio(InCallStartType.BUSYTONE, '_DTMF_');
                    }}>
                    <Text style={{ color: '#000' }}>stop{changeType}BUSYTONE:_DTMF_</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        turnScreenOn();
                    }}>
                    <Text style={{ color: '#000' }}>turnScreenOn (not supported by iOS)</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        turnScreenOff();
                    }}>
                    <Text style={{ color: '#000' }}>turnScreenOff (not supported by iOS)</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        setKeepScreenOn(true);
                    }}>
                    <Text style={{ color: '#000' }}>setKeepScreenOn=true</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        setKeepScreenOn(false);
                    }}>
                    <Text style={{ color: '#000' }}>setKeepScreenOn=false</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={async () => {
                        await getAudioUriJS(InCallStartType.RINGTONE, '');
                    }}>
                    <Text style={{ color: '#000' }}>
                        getAudioUriJS={InCallStartType.RINGTONE}
                    </Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={async () => {
                        await getAudioUriJS(InCallStartType.BUSYTONE, '');
                    }}>
                    <Text style={{ color: '#000' }}>
                        getAudioUriJS={InCallStartType.BUSYTONE}
                    </Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={async () => {
                        await getAudioUriJS(InCallStartType.RINGBACK, '');
                    }}>
                    <Text style={{ color: '#000' }}>
                        getAudioUriJS={InCallStartType.RINGBACK}
                    </Text>
                </TouchableOpacity>

                <TouchableOpacity onPress={() => { }}>
                    <Text style={{ color: 'green' }}>audioUriJS={audioUriJS}</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={async () => {
                        await getIsWiredHeadsetPluggedIn('', '');
                    }}>
                    <Text style={{ color: '#000' }}>getIsWiredHeadsetPluggedIn</Text>
                </TouchableOpacity>

                <TouchableOpacity onPress={() => { }}>
                    <Text style={{ color: 'green' }}>
                        getIsWiredHeadsetPluggedIn=
                        {JSON.stringify(wiredHeadsetPluggedInObj)}
                    </Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        setFlashOn(true, 100);
                    }}>
                    <Text style={{ color: '#000' }}>setFlashOn=true(Android is not supported)</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        setFlashOn(false, 50);
                    }}>
                    <Text style={{ color: '#000' }}>setFlashOn=false(Android is not supported)</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        startProximitySensor();
                    }}>
                    <Text style={{ color: '#000' }}>startProximitySensor</Text>
                </TouchableOpacity>

                <TouchableOpacity
                    onPress={() => {
                        stopProximitySensor();
                    }}>
                    <Text style={{ color: '#000' }}>stopProximitySensor</Text>
                </TouchableOpacity>

            </ScrollView>
        </SafeAreaView>
    );
}


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

    "@react-native-oh-tpl/react-native-incall-manager": "file:../../node_modules/@react-native-oh-tpl/react-native-incall-manager/harmony/in_call_manager.har"
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

### 3. Configuring CMakeLists and Introducing RNInCallManagerPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-incall-manager/src/main/cpp" ./in_call_manager)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_in_call_manager)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNInCallManagerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNInCallManagerPackage>(ctx)
    };
}
```

### 4. Introducing RNInCallManagerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import { RNInCallManagerPackage } from '@react-native-oh-tpl/react-native-incall-manager/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNInCallManagerPackage(ctx),
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

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-incall-manager Releases](https://github.com/react-native-oh-library/react-native-incall-manager/releases)

### Permission Requirements

> [!TIP]The permission level of **ohos.permission.RUNNING_LOCK** and **ohos.permission.KEEP_BACKGROUND_RUNNING** is **normal** and the authorization mode is **system_grant**.
> The permission level of **ohos.permission.MICROPHONE** is **normal**, and the authorization mode is **user_grant**. For details, see [Requesting ACL Permissions](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V2/signing-0000001587684945-V2#section157591551175916).

#### Include applicable permissions in the module.json5 file within the entry directory.

Add configuration to `YourProject/entry/src/main/module.json5`

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

    "requestPermissions": [
+     { "name": "ohos.permission.RUNNING_LOCK" },
+     {
+       "name": "ohos.permission.MICROPHONE",
+       "reason": "$string:Access_micphone",
+       "usedScene": {"when": "inuse"}
+     },
+     { "name": "ohos.permission.KEEP_BACKGROUND_RUNNING",
+       "usedScene": {
+          "when": "always"
+        }
+     }
    ]
  }
}
```

Add configuration to `YourProject/entry/src/main/resources/base/element/string.json`

#### Apply the reasons for applicable permission in the entry directory.

Open `entry/src/main/resources/base/element/string.json` file and add:

```diff
...
{
  "string": [
+    {
+      "name": "Access_micphone",
+      "value": "access micphone"
+    }
  ]
}
```

## Static method

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| vibrate  | set vibrate true / false         | boolean  | no | all      | yes |
| start  | start incall manager.ringback accept non-empty string or it won't play default: \{media:'audio', auto: true, ringback: ''\}         | (setup?: \{auto?: boolean;media?: "video" \| "audio";ringback?: string;\}) => void | no | all      | yes |
| stop  | stop incall manager,busytone accept non-empty string or it won't play,default: \{busytone: ''\}         | (setup?: \{ busytone?: string \}) => void  | no | all      | partially |
| turnScreenOn  | force turn screen on         | () => void  | no | Android      | yes |
| turnScreenOff  | turn screen off         | () => void  | no | Android      | yes |
| setKeepScreenOn  | set KeepScreenOn flag = true or false,default: false         | (enable: boolean) => void  | no | all      | yes |
| setSpeakerphoneOn  | toggle speaker ON/OFF once. but not force,default: false         | (enable: boolean) => void  | no | all      | no |
| setForceSpeakerphoneOn  | true -> force speaker on,false -> force speaker off,null -> use default behavior according to media type,default: null         | (flag: boolean) => void  | no | all      | no |
| setMicrophoneMute  | mute/unmute micophone,default: false,p.s. if you use webrtc, you can just use track.enabled = false to mute         | (enable: boolean) => void  | no | Android      | no |
| getAudioUri  | get audio Uri path. this would be useful when you want to pass Uri into another module.         | (audioType: string, fileType: string) => Promise<string \| null>  | no | all      | yes |
| startRingtone  | play ringtone.ringtone: 'DEFAULT' or 'BUNDLE',vibrate_pattern: same as RN, but does not support repeat,ios_category: ios only, if you want to use specific audio category,seconds: android only, specify how long do you want to play rather than play once nor repeat. in sec.         | (ringtone: string,vibrate_pattern: number | number\[],ios_category: string,seconds: number) => void  | no | all      | partially |
| stopRingtone  | stop play ringtone if previous started via         | () => void  | no | all      | yes |
| startRingback  | play ringback.,ringback: '_DEFAULT_' or '_DTMF_'         | (ringback: string) => void;  | no | all      | partially |
| stopRingback  | stop play ringback if previous started via start()         | () => void  | no | all      | yes |
| stopProximitySensor  | stop ProximitySensor          | () => void  | no | all      | yes |
| startProximitySensor  | start proximitySensor          | () => void  | no | all      | yes |
| pokeScreen  | poke screen          | (timeout: number) => void  | no | Android      | no |
| chooseAudioRoute  | choose audio route          | (route: string) => Promise<any>  | no | Android      | no |
| requestAudioFocus  | request audio focus          | () => Promise<any>  | no | Android      | no |
| abandonAudioFocus  | abandon audio focus          | () => Promise<any>  | no | Android      | no |
| setFlashOn  | set flash light on/off          | (enable: boolean, brightness: number) => void  | no | iOS      | yes |
| getIsWiredHeadsetPluggedIn  | return wired headset plugged in state          | () => Promise<\{ isWiredHeadsetPluggedIn: boolean \}>  | no | all      | yes |

### Event(Event Listening)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                                                                                     | Type                                                                               | Required | Platform | HarmonyOS Support |
| ------------------ | ----------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| Proximity          | proximity sensor detected changes.                                                              | (data: \{'isNear': boolean\}) => void                                              | no       | all      | yes               |
| WiredHeadset       | fire when wired headset plug/unplug                                                             | (data: \{'isPlugged': boolean, 'hasMic': boolean, 'deviceName': string \}) => void | no       | all      | yes               |
| NoisyAudio         | a hint for applications that audio is about to become 'noisy' due to a change in audio outputs. | () => void                                                                         | no       | Android  | yes               |
| MediaButton        | when external device controler pressed button                                                   | (data: \{'eventText': string, 'eventCode': number \}) => void                      | no       | Android  | no               |
| onAudioFocusChange | Called on the listener to notify it the audio focus for this listener has been changed.         | (data: \{'eventText': string, 'eventCode': number }) => void                       | no       | Android  | yes               |

## Known Issues

- [ ] The **setMicrophoneMute** API is not supported on HarmonyOS: [issue#1](https://github.com/react-native-oh-library/react-native-incall-manager/issues/1).
- [ ] The system ringtones cannot be played on HarmonyOS: [issue#2](https://github.com/react-native-oh-library/react-native-incall-manager/issues/2).
- [ ] The **setSpeakerphoneOn** and **setForceSpeakerphoneOn** APIs are not supported on HarmonyOS: [issue#3](https://github.com/react-native-oh-library/react-native-incall-manager/issues/3).
- [ ] The **chooseAudioRoute** API is not supported on HarmonyOS: [issue#4](https://github.com/react-native-oh-library/react-native-incall-manager/issues/4).
- [ ] Listening for the **MediaButton** event is not supported on HarmonyOS: [issue#18](https://github.com/react-native-oh-library/react-native-incall-manager/issues/18).

## Others

## License

This project is licensed under [ISC License](https://github.com/react-native-webrtc/react-native-incall-manager/blob/master/LICENSE).
