> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-system-setting</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/c19354837/react-native-system-setting/tree/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/c19354837/react-native-system-setting/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-system-setting)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-system-setting Releases](https://github.com/react-native-oh-library/react-native-system-setting/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-system-setting@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-system-setting@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useEffect, useState } from 'react'
import SystemSetting, { EmitterSubscription } from 'react-native-system-setting'
import { ScrollView, Text, View, StyleSheet, TouchableOpacity } from 'react-native'

const SystemSettingDemo: React.FC = (): JSX.Element => {
    const [bluetoothEnabled, setBluetoothEnabled] = useState<boolean>()
    const isBluetoothEnabled = async () => {
        const enabled = await SystemSetting.isBluetoothEnabled()
        setBluetoothEnabled(enabled)
    }
    return (
        <>
            <ScrollView>
                <View style={styles.module}>
                    <Text
                        style={styles.moduleName}>
                        Bluetooth(蓝牙模块)
                    </Text>
                    <Text
                        style={styles.moduleContent}>
                        蓝牙状态:{bluetoothEnabled === true ? '开启' : '关闭'}
                    </Text>
                    <TouchableOpacity
                        onPress={() => {
                            isBluetoothEnabled()
                        }}
                        style={styles.moduleButton}
                    >
                        <Text style={styles.buttonText}>获取蓝牙状态</Text>
                    </TouchableOpacity>
                    <TouchableOpacity
                        onPress={() => {
                            SystemSetting.switchBluetooth(() => {
                                console.log('跳转完成')
                            })

                        }}
                        style={styles.moduleButton}
                    >
                        <Text style={styles.buttonText}>切换蓝牙状态(跳转设置)</Text>
                    </TouchableOpacity>
                    <TouchableOpacity
                        onPress={() => {
                            SystemSetting.switchBluetoothSilence(() => {
                                console.log('切换完成')
                            })
                        }}
                        style={styles.moduleButton}
                    >
                        <Text style={styles.buttonText}>切换蓝牙状态</Text>
                    </TouchableOpacity>
                    <TouchableOpacity
                        onPress={async () => {
                            bluetoothEvent = await SystemSetting.addBluetoothListener(e => {
                                console.log(JSON.stringify(e))
                                setBluetoothEnabled(e)
                            })
                        }}
                        style={styles.moduleButton}
                    >
                        <Text style={styles.buttonText}>开启蓝牙状态监听器</Text>
                    </TouchableOpacity>
                    <TouchableOpacity
                        onPress={() => {
                            SystemSetting.removeListener(bluetoothEvent)
                        }}
                        style={styles.moduleButton}
                    >
                        <Text style={styles.buttonText}>关闭蓝牙状态监听器</Text>
                    </TouchableOpacity>
                </View>
            </ScrollView>
        </>
    )
}
const styles = StyleSheet.create({
    module: {
        margin: 15,
    },
    moduleName: {
        fontSize: 25,
        fontWeight: '700',
        marginBottom: 4
    },
    moduleContent: {
        fontSize: 16,
        fontWeight: '500',
        marginBottom: 4
    },
    moduleButton: {
        marginBottom: 4,
        backgroundColor: 'deepskyblue',
        height: 34,
        borderRadius: 10
    },
    buttonText: {
        fontSize: 18,
        fontWeight: '400',
        color: 'white',
        textAlign: 'center',
        lineHeight: 32,
        verticalAlign: 'middle'
    }
})

export default SystemSettingDemo
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/rnoh-system-setting": "../../node_modules/@react-native-oh-tpl/react-native-system-setting/harmony/react_native_system_setting.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/rnoh-system-setting": "../../node_modules/@react-native-oh-tpl/react-native-system-setting/harmony/react_native_system_setting"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 在 ArkTs 侧引入 SoundPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { RNSystemSettingPackage } from '@react-native-oh-tpl/rnoh-system-setting/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNSystemSettingPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-system-setting Releases](https://github.com/react-native-oh-library/react-native-system-setting/releases)。

本文档内容基于以下版本验证通过：
1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1(full sdk); IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;

### 权限要求

由于此库涉及蓝牙、亮度等系统控制功能，使用对应接口时则需要配置对应的权限，权限需配置在entry/src/main目录下module.json5文件中。其中部分权限需弹窗向用户申请授权。具体权限配置见文档：[程序访问控制](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/Readme-CN.md#/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/app-permission-mgmt-overview.md)。

此库部分功能与接口需要normal权限：ohos.permission.ACCESS_BLUETOOTH、ohos.permission.GET_WIFI_INFO。

此库部分功能与接口需要full sdk与system_basic权限：ohos.permission.MANAGE_SECURE_SETTINGS、ohos.permission.MANAGE_WIFI_CONNECTION等，[full sdk获取地址](https://eco-betaclub.rnd.huawei.com/#/download/DevEco%20Studio/newest)，[system_basic权限获取方式](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/determine-application-mode-0000001774120042-V5)。

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-system-setting](https://github.com/c19354837/react-native-system-setting/tree/master)

| Name                        | Description                                                  | Type                     | Required | Platform    | HarmonyOS Support |
| --------------------------- | ------------------------------------------------------------ | ------------------------ | -------- | ----------- | ----------------- |
| getVolume                   | Get the system volume.                                       | string                   | No       | IOS/Android | yes               |
| setVolume                   | Set the system volume by specified value, from 0 to 1. 0 for mute, and 1 is max volume. | val:float, config:object | No       | IOS/Android | no                |
| addVolumeListener           | Listen the volume changing, and it will return the listener. | callback                 | No       | IOS/Android | yes               |
| removeVolumeListener        | Remove listener when it no longer needed.                    | listener                 | No       | IOS/Android | no                |
| getBrightness               | Get the system brightness.                                   | no                       | No       | IOS/Android | no                |
| setBrightness               | Set the system brightness by specified value, from 0 to 1. 0 for brightless, and 1 is max. | val:float                | No       | IOS/Android | no                |
| setBrightnessForce          | In Android, if the screen mode is auto, SystemSetting.setBrightness() will not work. You can call this to change the screen mode to MANUAL first. | val:float                | No       | Android     | no                |
| setAppBrightness            | For Android and Harmony, `setBrightness()` or `setBrightnessForce()` will change the system's brightness, while this just changes the app's brightness, and it has no permission trouble. | val:float                | No       | Android     | yes               |
| getAppBrightness            | Get the app brightness, and it will returns system brightness if you haven't call `setAppBrightness(val)` yet. (iOS allways returns system brightness) | no                       | No       | Android     | yes               |
| getScreenMode               | (Only for Android, iOS and Harmony will return -1). Get the screen mode, 0 is manual, while 1 is automatic. | no                       | No       | Android     | no                |
| setScreenMode               | (Only for Android, iOS and Harmony cannot change it). Change the screen mode, 0 is manual, while 1 is automatic. | mode:int                 | No       | Android     | no                |
| grantWriteSettingPermission | open app setting page. It's user-friendly when you need some permission. Normally, you can call it if `setScreenMode()`, `setBrightness()` or `setBrightnessForce()` return false | no                       | No       | IOS/Android | no                |
| saveBrightness              | It will save current brightness and screen mode.             | no                       | No       | IOS/Android | yes               |
| restoreBrightness           | Restore brightness and screen mode back to saveBrightness(). While iOS only restore the brightness, Android will restore both, Harmony will restore the app's rightness. | no                       | No       | IOS/Android | yes               |
| isWifiEnabled               | Get wifi state, true if wifi is on.                          | no                       | No       | IOS/Android | yes               |
| switchWifi                  | It will open **Wifi Setting Page**, and you can change it by yourself. When come back to the app, the `complete` will be call. | complete                 | No       | IOS/Android | yes               |
| switchWifiSilence           | It will open wifi if the wifi is off, and close wifi when the wifi is on now. When it has done, the `complete` will be call. | complete                 | No       | Android     | no                |
| addWifiListener             | Listen the wifi state changing, and it will return the listener. (Android only) | callback                 | No       | Android     | no                |
| isLocationEnabled           | Get location state, true if location is on.                  | no                       | No       | IOS/Android | yes               |
| switchLocation              | It will open **System Location Setting Page**, and you can change it by yourself. When come back to the app, the `complete` will be call. | complete                 | No       | IOS/Android | yes               |
| addLocationListener         | Listen the location state changing, and it will return the listener. (Android only) | callback                 | No       | Android     | no                |
| getLocationMode             | Get current location mode code: `0` - 'off', `1` - 'gps', `2` - 'network', `3` - 'gps & network'. (Android only) | no                       | No       | Android     | no                |
| addLocationModeListener     | Listen the location mode changing, and it will return the listener. (Android only) | callback                 | No       | Android     | no                |
| isBluetoothEnabled          | Get bluetooth state, true if bluetooth is on.                | no                       | No       | IOS/Android | yes               |
| switchBluetooth             | It will open **System Bluetooth Setting Page**, and you can change it by yourself. When come back to the app, the `complete` will be call. | complete                 | No       | IOS/Android | yes               |
| switchBluetoothSilence      | It will open bluetooth if the bluetooth is off, and close bluetooth when the bluetooth is on now. When it has done, the `complete` will be call. In android, it's done programmatically. | complete                 | No       | Android     | yes               |
| addBluetoothListener        | Listen the bluetooth state changing, and it will return the listener. | callback                 | No       | IOS/Android | yes               |
| isAirplaneEnabled           | Get airplane state, true if airplane is on.                  | no                       | No       | IOS/Android | no                |
| switchAirplane              | It will open **System Setting Page**, and you can change it by yourself. | complete                 | No       | IOS/Android | yes               |
| addAirplaneListener         | Listen the airplane state changing, and it will return the listener. (Android only) | callback                 | No       | Android     | no                |
| setAppStore                 | `true` means that you'll submit your app to App Store,`false` means that your app will not upload to App Store, and you can use any APIs at will. | isAppStore:bool          | No       | IOS         | no                |
| removeListener              | you can use this to remove the listener which return by `add*Listener(callback)` | listener                 | No       | IOS/Android | yes               |
| openAppSystemSettings       | open app's setting page                                      | no                       | No       | IOS/Android | yes               |

## 其他

## 遗留问题

- [ ] 由于system权限与OS API等问题，暂未支持setVolume、removeVolumeListener、getBrightness、setBrightness等接口，具体API支持度见上表，待后续跟进修复，问题：[issue#1](https://github.com/react-native-oh-library/react-native-system-setting/issues/2)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/c19354837/react-native-system-setting/blob/master/LICENSE.md) ，请自由地享受和参与开源。