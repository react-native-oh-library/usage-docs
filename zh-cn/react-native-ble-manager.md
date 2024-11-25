> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-ble-manager</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/innoveit/react-native-ble-manager">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms"/>
    </a>
    <a href="https://github.com/innoveit/react-native-ble-manager/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg"alt="License"/>
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-ble-manager)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-ble-manager Releases](https://github.com/react-native-oh-library/react-native-ble-manager/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-ble-manager
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-ble-manager
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState, useEffect } from 'react';
import { ScrollView, StyleSheet, Button, View, Text, NativeEventEmitter, NativeModules, TouchableHighlight, FlatList, Alert } from 'react-native';
import ReactNativeBleManager from 'react-native-ble-manager';
import { Peripheral } from 'react-native-ble-manager';
import { Colors } from 'react-native/Libraries/NewAppScreen';


declare module '@react-native-oh-tpl/react-native-ble-manager' {
    interface Peripheral {
        connected?: boolean;
        connecting?: boolean;
    }
}

export enum BleState {
    Unknown = "unknown",
    Resetting = "resetting",
    Unsupported = "unsupported",
    Unauthorized = "unauthorized",
    On = "on",
    Off = "off",
    TurningOn = "turning_on",
    TurningOff = "turning_off",
}

export enum BleScanMatchMode {
    Aggressive = 1,
    Sticky = 2,
}

export enum BleScanMode {
    Opportunistic = -1,
    LowPower = 0,
    Balanced = 1,
    LowLatency = 2,
}

const BleManagerModule = NativeModules.BleManager;
const bleManagerEmitter = new NativeEventEmitter(BleManagerModule);

export default function BleManagerDemo() {
    useEffect(() => {
        listeners
    })

    const [result, setResult] = useState<string>('');
    const [deviceId, setDeviceId] = useState('')


    const [peripherals, setPeripherals] = useState(
        new Map<Peripheral['id'], Peripheral>(),
    );


    const handleDiscoverPeripheral = (peripheral: Peripheral) => {
        setResult(JSON.stringify(peripheral))
        setDeviceId(peripheral.id);
        if (!peripheral.name) {
            peripheral.name = 'NO NAME';
        }
        setPeripherals(map => {
            return new Map(map.set(peripheral.id, peripheral));
        });
    };

    const listeners = [
        bleManagerEmitter.addListener('BleManagerDiscoverPeripheral', handleDiscoverPeripheral),
    ];

    const renderItem = ({ item }: { item: Peripheral }) => {
        return (
            <TouchableHighlight>
                <View style={[styles.row]}>
                    <Text style={styles.peripheralName}>
                        {item.name} - {item?.advertising?.localName}
                        {item.connecting && ' - Connecting...'}
                    </Text>
                    <Text style={styles.rssi}>RSSI: {item.rssi}</Text>
                    <Text style={styles.peripheralId}>{item.id}</Text>
                    <Text style={styles.peripheralId}>{`${item.advertising.isConnectable}`}</Text>
                    <View style={{ height: 50 }}>
                        <Button title='connect' onPress={() => {
                            ReactNativeBleManager.connect(item.id)
                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='createBond' onPress={() => {
                            ReactNativeBleManager.createBond(item.id)
                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='获取serves' onPress={() => {
                            ReactNativeBleManager.retrieveServices(item.id, ['00001888-0000-1000-8000-00805F9B34FB'])
                        }}></Button>
                    </View>
                    <View style={{ height: 50 }}>
                        <Button title='getBondedPeripherals' onPress={async () => {
                            const list = await ReactNativeBleManager.getBondedPeripherals()
                            console.log('返回已绑定的设备' + JSON.stringify(list))
                        }}></Button>
                    </View>
                    <View style={{ height: 50 }}>
                        <Button title='getConnectedPeripherals' onPress={async () => {
                            const list = await ReactNativeBleManager.getConnectedPeripherals()
                            Alert.alert(JSON.stringify(list))
                        }}></Button>
                    </View>

                    <View style={{ height: 50 }}>
                        <Button title='getDiscoveredPeripherals' onPress={async () => {
                            const list = await ReactNativeBleManager.getDiscoveredPeripherals()
                            Alert.alert(JSON.stringify(list))
                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='写入value' onPress={() => {
                            ReactNativeBleManager.write(item.id, '00001888-0000-1000-8000-00805F9B34FB', '00001820-0000-1000-8000-00805F9B34FB', [1])
                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='写入des' onPress={() => {
                            ReactNativeBleManager.writeDescriptor(item.id, '00001888-0000-1000-8000-00805F9B34FB', '00001820-0000-1000-8000-00805F9B34FB', '00002902-0000-1000-8000-00805F9B34FB', [1])

                        }}></Button>
                    </View>
                    <View style={{ height: 50 }}>
                        <Button title='readCharacteristicValue' onPress={() => {
                            ReactNativeBleManager.read(item.id, '00001888-0000-1000-8000-00805F9B34FB', '00001820-0000-1000-8000-00805F9B34FB').then((res)=>{
                                Alert.alert(JSON.stringify(res))
                            })

                        }}></Button>
                    </View>
                    <View style={{ height: 50 }}>
                        <Button title='readDescriptor' onPress={() => {
                            ReactNativeBleManager.readDescriptor(item.id, '00001888-0000-1000-8000-00805F9B34FB', '00001820-0000-1000-8000-00805F9B34FB', '00002902-0000-1000-8000-00805F9B34FB')

                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='readRSSI' onPress={() => {
                            ReactNativeBleManager.readRSSI(item.id).then((data) => {
                                Alert.alert(data + "")
                            })
                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='requestMTU' onPress={() => {
                            ReactNativeBleManager.requestMTU(item.id, 10).then((res)=>{
                                Alert.alert(res + "")
                            })
                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='checkState' onPress={() => {
                            ReactNativeBleManager.checkState().then((res)=>{
                                Alert.alert(JSON.stringify(res))
                            })
                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='startNotification' onPress={() => {
                            ReactNativeBleManager.startNotification(item.id,'00001888-0000-1000-8000-00805F9B34FB', '00001820-0000-1000-8000-00805F9B34FB')
                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='stopScan' onPress={() => {
                            ReactNativeBleManager.stopScan()
                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='disconnect' onPress={() => {
                            ReactNativeBleManager.disconnect(item.id, true)
                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='removeBond' onPress={() => {
                            ReactNativeBleManager.removeBond(item.id).then(() => {
                                Alert.alert('此接口为系统接口，三方库无法调用')
                            })
                        }}></Button>
                    </View>
                </View>
            </TouchableHighlight>
        );
    };

    return (
        <View style={styles.container}>
            <View style={styles.titleArea}>
                <Text style={styles.title}>BleManager</Text>
            </View>
           
            <View style={{ width: '100%', display: 'flex', flexDirection: "row", justifyContent: 'space-around', alignItems: 'center',marginTop:10 }}>
            <View style={{ height: 50, width: 'auto'}}>
                        <Button title='enableBluetooth' onPress={() => {
                            ReactNativeBleManager.enableBluetooth()
                        }}></Button>
                    </View>
                    <View style={{ height: 50,width: 'auto' }}>
                        <Button title='start' onPress={() => {
                            ReactNativeBleManager.start()
                        }}></Button>
                    </View>
                    <View style={{ height: 50,width: 'auto' }}>
                        <Button title='scan' onPress={() => {
                            ReactNativeBleManager.scan(['00001888-0000-1000-8000-00805F9B34FB'], 0, true, {
                                companion: true,
                                matchMode: BleScanMatchMode,
                                scanMode: BleScanMode,
                                reportDelay: 1,
                                exactAdvertisingName: ''
                            })
                        }}></Button>
                    </View>
            </View>
             <FlatList
                data={Array.from(peripherals.values())}
                contentContainerStyle={{ rowGap: 12 }}
                renderItem={renderItem}
                keyExtractor={item => item.id}
                style={{ width: '100%' }}
            />
        </View>
    )
}

const boxShadow = {
    shadowColor: '#000',
    shadowOffset: {
        width: 0,
        height: 2,
    },
    shadowOpacity: 0.25,
    shadowRadius: 3.84,
    elevation: 5,
};

const styles = StyleSheet.create({
    container: {
        width: '100%',
        height: '100%',
        flexDirection: 'column',
        alignItems: 'center',
        backgroundColor: '#F1F3F5',
    },
    baseText: {
        width: '100%',
        height: '100%',
        fontWeight: 'bold',
        textAlign: 'center',
        fontSize: 16,
        ellipsizeMode: 'tail',
        numberOfLines: 2
    },
    titleArea: {
        width: '90%',
        height: '8%',
        alignItems: 'center',
        flexDirection: 'row',
    },
    title: {
        width: '90%',
        color: '#000000',
        textAlign: "center",
        fontSize: 30,
        border:5,
    },
    scrollView: {
        width: '90%',
        marginHorizontal: 10,
    },

    inputArea: {
        width: '90%',
        height: '10%',
        borderWidth: 2,
        borderColor: '#000000',
        marginTop: 8,
        justifyContent: 'center',
        alignItems: 'center',
    },
    baseArea: {
        width: '100%',
        height: 60,
        borderRadius: 4,
        borderColor: '#000000',
        marginTop: 6,
        backgroundColor: '#FFFFFF',
        flexDirection: 'row',
        alignItems: 'center',
        paddingLeft: 8,
        paddingRight: 8
    },
    engine: {
        position: 'absolute',
        right: 10,
        bottom: 0,
        color: Colors.black,
    },
    buttonGroup: {
        flexDirection: 'row',
        width: '100%'
    },
    scanButton: {
        alignItems: 'center',
        justifyContent: 'center',
        paddingVertical: 16,
        paddingHorizontal: 16,
        backgroundColor: '#0a398a',
        margin: 10,
        borderRadius: 12,
        flex: 1,
        ...boxShadow,
    },
    scanButtonText: {
        fontSize: 16,
        letterSpacing: 0.25,
        color: Colors.white,
    },
    body: {
        backgroundColor: '#0082FC',
        flex: 1,
    },
    sectionContainer: {
        marginTop: 32,
        paddingHorizontal: 24,
    },
    sectionTitle: {
        fontSize: 24,
        fontWeight: '600',
        color: Colors.black,
    },
    sectionDescription: {
        marginTop: 8,
        fontSize: 18,
        fontWeight: '400',
        color: Colors.dark,
    },
    highlight: {
        fontWeight: '700',
    },
    footer: {
        color: Colors.dark,
        fontSize: 12,
        fontWeight: '600',
        padding: 4,
        paddingRight: 12,
        textAlign: 'right',
    },
    peripheralName: {
        fontSize: 16,
        textAlign: 'center',
        padding: 10,
    },
    rssi: {
        fontSize: 12,
        textAlign: 'center',
        padding: 2,
    },
    peripheralId: {
        fontSize: 12,
        textAlign: 'center',
        padding: 2,
        paddingBottom: 20,
    },
    row: {
        marginLeft: 10,
        marginRight: 10,
        borderRadius: 20,
        ...boxShadow,
        alignItems: 'center'
    },
    noPeripherals: {
        margin: 10,
        textAlign: 'center',
        color: Colors.white,
    },
});
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/codegen.md)。

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

>[!TIP] 因本库需要两台手机去进行对端扫描和连接，所以两台手机各装一个har包编译（`ble_managerGatt.har` 和 `ble_managerServers.har`）

第一台手机：`ble_managerGatt.har`

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
     "@react-native-oh-tpl/react-native-ble-manager": "file:../../node_modules/@react-native-oh-tpl/react-native-ble-manager/harmony/ble_managerGatt.har"，
  }
```

第二台手机：`ble_managerServers.har`

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
     "@react-native-oh-tpl/react-native-ble-manager": "file:../../node_modules/@react-native-oh-tpl/react-native-ble-manager/harmony/ble_managerServers.har"，
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

### 3.在 ArkTs 侧引入 BlePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { BlePackage } from '@react-native-oh-tpl/react-native-ble-manager/ts';


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+    new BlePackage(ctx)
  ];
}
```

### 4.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-ble-manager Releases](https://github.com/react-native-oh-library/react-native-ble-manager/releases)

### 权限要求

- 由于此库涉及蓝牙系统控制功能，使用对应接口时则需要配置对应的权限，权限需配置在entry/src/main目录下module.json5文件中。其中部分权限需弹窗向用户申请授权。具体权限配置见文档：[程序访问控制](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/Readme-CN.md#/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/app-permission-mgmt-overview.md)。

- 此库部分功能与接口需要normal权限：ohos.permission.ACCESS_BLUETOOTH。

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                         | Description                                                  | Required | Platform    | HarmonyOS Support |
| -------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| start                                        | Init the module. Returns a `Promise` object. Don’t call this multiple times. | No       | IOS/Android | Yes               |
| scan                                         | Scan for available peripherals                               | No       | IOS/Android | Yes               |
| stopScan                                     | Stop the scanning                                            | No       | IOS/Android | yes               |
| connect                                      | Attempts to connect to a peripheral. In many case if you can’t connect you have to scan for the peripheral before | No       | IOS/Android | Yes               |
| disconnect                                   | Disconnect from a peripheral                                 | No       | IOS/Android | Yes               |
| enableBluetooth                              | Create the ACTION_REQUEST_ENABLE to ask the user to activate the bluetooth | No       | Android     | Yes               |
| checkState                                   | Force the module to check the state of the native BLE manager and trigger a BleManagerDidUpdateState event | No       | IOS/Android | Yes               |
| readRSSI                                     | Read the current value of the RSSI                           | No       | IOS/Android | Yes               |
| createBond                                   | Start the bonding (pairing) process with the remote device   | No       | Android     | Yes               |
| retrieveServices                             | Retrieve the peripheral’s services and characteristics       | No       | IOS/Android | Yes               |
| startNotification                            | Start the notification on the specified characteristic, you need to call `retrieveServices` method before | No       | IOS/Android | Yes               |
| read                                         | Read the current value of the specified characteristic, you need to call `retrieveServices` method before | No       | IOS/Android | Yes               |
| write                                        | Write with response to the specified characteristic, you need to call `retrieveServices` method before | No       | IOS/Android | Yes               |
| readDescriptor                               | Read the current value of the specified descriptor, you need to call `retrieveServices` method before | No       | IOS/Android | Yes               |
| writeDescriptor                              | Write a value to the specified descriptor, you need to call `retrieveServices` method before | No       | IOS/Android | Yes               |
| requestMTU                                   | Request an MTU size used for a given connection              | No       | Android     | Yes               |
| getConnectedPeripherals                      | Return the connected peripherals                             | No       | IOS/Android | Yes               |
| getBondedPeripherals                         | Return the bonded peripherals                                | No       | IOS/Android | Yes               |
| getDiscoveredPeripherals                     | Return the discovered peripherals after a scan               | No       | IOS/Android | Yes               |
| removeBond                                   | Remove a paired device                                       | No       | Android     | No                |
| refreshCache                                 | refreshes the peripheral’s services and characteristics cache Returns a `Promise` object. | No       | Android     | No                |
| requestConnectionPriority                    | Request a connection parameter update                        | No       | Android     | No                |
| startNotificationUseBuffer                   | Start the notification on the specified characteristic, you need to call `retrieveServices` method before | No       | Android     | No                |
| removePeripheral                             | Removes a disconnected peripheral from the cached list       | No       | Android     | Yes               |
| CompanionScan                                | Scan for companion devices                                   | No       | Android     | No                |
| getAssociatedPeripherals                     | Retrive associated peripherals (from companion manager)      | No       | Android     | No                |
| removeAssociatedPeripheral                   | Remove a associated peripheral                               | No       | Android     | No                |
| setName                                      | Create the request to set the name of the bluetooth adapter  | No       | Android     | No                |
| isScanning                                   | Checks whether the scan is in progress and return `true` or `false` | No       | IOS/Android | Yes               |
| writeWithoutResponse                         | Write without response to the specified characteristic, you need to call `retrieveServices` method before | No       | IOS/Android | No                |
| getMaximumWriteValueLengthForWithoutResponse | Return the maximum value length for WriteWithoutResponse     | No       | IOS         | No                |
| getMaximumWriteValueLengthForWithResponse    | Return the maximum value length for WriteWithResponse        | No       | IOS         | No                |
| isPeripheralConnected                        | Check whether a specific peripheral is connected and return `true` or `false` | No       | IOS         | Yes               |
| supportsCompanion                            | Check if current device supports companion device manager    | No       | Android     | No                |
| stopNotification                             | Stop the notification on the specified characteristic        | No       | IOS/Android | No                |

## 遗留问题

- [ ] refreshCache 用于清理和刷新蓝牙设备缓存的一部分 [issue#3](https://github.com/react-native-oh-library/react-native-ble-manager/issues/3)
- [ ] requestConnectionPriority 用于请求蓝牙连接优先级 [issue#4](https://github.com/react-native-oh-library/react-native-ble-manager/issues/4)
- [ ] startNotificationUseBuffer 用来启动一个带缓冲区的通知服务 [issue#6](https://github.com/react-native-oh-library/react-native-ble-manager/issues/6)
- [ ] CompanionScan 扫描配套设备[issue#5](https://github.com/react-native-oh-library/react-native-ble-manager/issues/5)
- [ ] getAssociatedPeripherals 检索相关外围设备（从配套管理器） [issue#7](https://github.com/react-native-oh-library/react-native-ble-manager/issues/7)
- [ ] removeAssociatedPeripheral 移除相关外围设备  [issue#8](https://github.com/react-native-oh-library/react-native-ble-manager/issues/8)
- [ ] setName 创建设置蓝牙适配器名称  [issue#9](https://github.com/react-native-oh-library/react-native-ble-manager/issues/9)
- [ ] supportsCompanion 检查当前设备是否支持配套设备管理器 [issue#10](https://github.com/react-native-oh-library/react-native-ble-manager/issues/10)
- [ ] stopNotification 停止指定特征的通知 [issue#11](https://github.com/react-native-oh-library/react-native-ble-manager/issues/11)
- [ ] writeWithoutResponse 写入不响应指定特性 [issue#12](https://github.com/react-native-oh-library/react-native-ble-manager/issues/12)
- [ ] removeBond 删除已配对的设备 [issue#13](https://github.com/react-native-oh-library/react-native-ble-manager/issues/13)
- [ ] getMaximumWriteValueLengthForWithoutResponse 用于获取在不带响应的情况下可以写入的最大数据长度 [issue#14](https://github.com/react-native-oh-library/react-native-ble-manager/issues/14)
- [ ] getMaximumWriteValueLengthForWithResponse 它用于获取在带有响应的情况下可以写入的最大数据长度  [issue#15](https://github.com/react-native-oh-library/react-native-ble-manager/issues/15)

## 其他

## 开源协议

本项目基于[The MIT License (MIT)](https://github.com/innoveit/react-native-ble-manager/blob/master/LICENSE) ，请自由地享受和参与开源。


