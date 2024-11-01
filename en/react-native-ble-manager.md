> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-ble-manager)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-ble-manager Releases](https://github.com/react-native-oh-library/react-native-ble-manager/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-ble-manager@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-ble-manager@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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
                        <Button title='get serves' onPress={() => {
                            ReactNativeBleManager.retrieveServices(item.id, ['00001888-0000-1000-8000-00805F9B34FB'])
                        }}></Button>
                    </View>
                    <View style={{ height: 50 }}>
                        <Button title='getBondedPeripherals' onPress={async () => {
                            const list = await ReactNativeBleManager.getBondedPeripherals()
                            console.log('returns bound devices' + JSON.stringify(list))
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
                        <Button title='write value' onPress={() => {
                            ReactNativeBleManager.write(item.id, '00001888-0000-1000-8000-00805F9B34FB', '00001820-0000-1000-8000-00805F9B34FB', [1])
                        }}></Button>
                    </View>
                    <View style={{ height: 50, width: 120 }}>
                        <Button title='write des' onPress={() => {
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
                                Alert.alert('the interface is system interface and cannot be called by third-party libraries')
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

> [!TIP] 因本库需要两台手机去进行对端扫描和连接，所以两台手机各装一个 har 包编译（`ble_managerGatt.har` 和 `ble_managerServers.har`）

the first mobile phone: `ble_managerGatt.har`

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
     "@react-native-oh-tpl/react-native-ble-manager": "file:../../node_modules/@react-native-oh-tpl/react-native-ble-manager/harmony/ble_managerGatt.har"，
  }
```

the second mobile phone: `ble_managerServers.har`

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
     "@react-native-oh-tpl/react-native-ble-manager": "file:../../node_modules/@react-native-oh-tpl/react-native-ble-manager/harmony/ble_managerServers.har"，
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

### 3. Introducing BlePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 4. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-ble-manager Releases](https://github.com/react-native-oh-library/react-native-ble-manager/releases)

### Permission Requirements

- 由于此库涉及蓝牙系统控制功能，使用对应接口时则需要配置对应的权限，权限需配置在 entry/src/main 目录下 module.json5 文件中。其中部分权限需弹窗向用户申请授权。具体权限配置见文档：[程序访问控制](https://gitee.com/openharmony/docs/blob/master/en/application-dev/security/AccessToken/Readme-CN.md#/openharmony/docs/blob/master/en/application-dev/security/AccessToken/app-permission-mgmt-overview.md)。

- 此库部分功能与接口需要 normal 权限：ohos.permission.ACCESS_BLUETOOTH。

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                         | Description                                                                                                       | Required | Platform    | HarmonyOS Support |
| -------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| start                                        | Init the module. Returns a `Promise` object. Don’t call this multiple times.                                      | No       | IOS/Android | Yes               |
| scan                                         | Scan for available peripherals                                                                                    | No       | IOS/Android | Yes               |
| stopScan                                     | Stop the scanning                                                                                                 | No       | IOS/Android | yes               |
| connect                                      | Attempts to connect to a peripheral. In many case if you can’t connect you have to scan for the peripheral before | No       | IOS/Android | Yes               |
| disconnect                                   | Disconnect from a peripheral                                                                                      | No       | IOS/Android | Yes               |
| enableBluetooth                              | Create the ACTION_REQUEST_ENABLE to ask the user to activate the bluetooth                                        | No       | Android     | Yes               |
| checkState                                   | Force the module to check the state of the native BLE manager and trigger a BleManagerDidUpdateState event        | No       | IOS/Android | Yes               |
| readRSSI                                     | Read the current value of the RSSI                                                                                | No       | IOS/Android | Yes               |
| createBond                                   | Start the bonding (pairing) process with the remote device                                                        | No       | Android     | Yes               |
| retrieveServices                             | Retrieve the peripheral’s services and characteristics                                                            | No       | IOS/Android | Yes               |
| startNotification                            | Start the notification on the specified characteristic, you need to call `retrieveServices` method before         | No       | IOS/Android | Yes               |
| read                                         | Read the current value of the specified characteristic, you need to call `retrieveServices` method before         | No       | IOS/Android | Yes               |
| write                                        | Write with response to the specified characteristic, you need to call `retrieveServices` method before            | No       | IOS/Android | Yes               |
| readDescriptor                               | Read the current value of the specified descriptor, you need to call `retrieveServices` method before             | No       | IOS/Android | Yes               |
| writeDescriptor                              | Write a value to the specified descriptor, you need to call `retrieveServices` method before                      | No       | IOS/Android | Yes               |
| requestMTU                                   | Request an MTU size used for a given connection                                                                   | No       | Android     | Yes               |
| getConnectedPeripherals                      | Return the connected peripherals                                                                                  | No       | IOS/Android | Yes               |
| getBondedPeripherals                         | Return the bonded peripherals                                                                                     | No       | IOS/Android | Yes               |
| getDiscoveredPeripherals                     | Return the discovered peripherals after a scan                                                                    | No       | IOS/Android | Yes               |
| removeBond                                   | Remove a paired device                                                                                            | No       | Android     | No                |
| refreshCache                                 | refreshes the peripheral’s services and characteristics cache Returns a `Promise` object.                         | No       | Android     | No                |
| requestConnectionPriority                    | Request a connection parameter update                                                                             | No       | Android     | No                |
| startNotificationUseBuffer                   | Start the notification on the specified characteristic, you need to call `retrieveServices` method before         | No       | Android     | No                |
| removePeripheral                             | Removes a disconnected peripheral from the cached list                                                            | No       | Android     | Yes               |
| CompanionScan                                | Scan for companion devices                                                                                        | No       | Android     | No                |
| getAssociatedPeripherals                     | Retrive associated peripherals (from companion manager)                                                           | No       | Android     | No                |
| removeAssociatedPeripheral                   | Remove a associated peripheral                                                                                    | No       | Android     | No                |
| setName                                      | Create the request to set the name of the bluetooth adapter                                                       | No       | Android     | No                |
| isScanning                                   | Checks whether the scan is in progress and return `true` or `false`                                               | No       | IOS/Android | Yes               |
| writeWithoutResponse                         | Write without response to the specified characteristic, you need to call `retrieveServices` method before         | No       | IOS/Android | No                |
| getMaximumWriteValueLengthForWithoutResponse | Return the maximum value length for WriteWithoutResponse                                                          | No       | IOS         | No                |
| getMaximumWriteValueLengthForWithResponse    | Return the maximum value length for WriteWithResponse                                                             | No       | IOS         | No                |
| isPeripheralConnected                        | Check whether a specific peripheral is connected and return `true` or `false`                                     | No       | IOS         | Yes               |
| supportsCompanion                            | Check if current device supports companion device manager                                                         | No       | Android     | No                |
| stopNotification                             | Stop the notification on the specified characteristic                                                             | No       | IOS/Android | No                |

## Known Issues

- [ ] refreshCache 用于清理和刷新蓝牙设备缓存的一部分 [issue#3](https://github.com/react-native-oh-library/react-native-ble-manager/issues/3)
- [ ] requestConnectionPriority 用于请求蓝牙连接优先级 [issue#4](https://github.com/react-native-oh-library/react-native-ble-manager/issues/4)
- [ ] startNotificationUseBuffer 用来启动一个带缓冲区的通知服务 [issue#6](https://github.com/react-native-oh-library/react-native-ble-manager/issues/6)
- [ ] CompanionScan 扫描配套设备[issue#5](https://github.com/react-native-oh-library/react-native-ble-manager/issues/5)
- [ ] getAssociatedPeripherals 检索相关外围设备（从配套管理器） [issue#7](https://github.com/react-native-oh-library/react-native-ble-manager/issues/7)
- [ ] removeAssociatedPeripheral 移除相关外围设备 [issue#8](https://github.com/react-native-oh-library/react-native-ble-manager/issues/8)
- [ ] setName 创建设置蓝牙适配器名称 [issue#9](https://github.com/react-native-oh-library/react-native-ble-manager/issues/9)
- [ ] supportsCompanion 检查当前设备是否支持配套设备管理器 [issue#10](https://github.com/react-native-oh-library/react-native-ble-manager/issues/10)
- [ ] stopNotification 停止指定特征的通知 [issue#11](https://github.com/react-native-oh-library/react-native-ble-manager/issues/11)
- [ ] writeWithoutResponse 写入不响应指定特性 [issue#12](https://github.com/react-native-oh-library/react-native-ble-manager/issues/12)
- [ ] removeBond 删除已配对的设备 [issue#13](https://github.com/react-native-oh-library/react-native-ble-manager/issues/13)
- [ ] getMaximumWriteValueLengthForWithoutResponse 用于获取在不带响应的情况下可以写入的最大数据长度 [issue#14](https://github.com/react-native-oh-library/react-native-ble-manager/issues/14)
- [ ] getMaximumWriteValueLengthForWithResponse 它用于获取在带有响应的情况下可以写入的最大数据长度 [issue#15](https://github.com/react-native-oh-library/react-native-ble-manager/issues/15)

## Others

## License

This project is licensed under[The MIT License (MIT)](https://github.com/innoveit/react-native-ble-manager/blob/master/LICENSE).

