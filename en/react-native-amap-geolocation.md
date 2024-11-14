> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-amap-geolocation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/qiuxiang/react-native-amap-geolocation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/qiuxiang/react-native-amap-geolocation/blob/main/license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-amap-geolocation) 

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-amap-geolocation Releases](https://github.com/react-native-oh-library/react-native-amap-geolocation/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-amap-geolocation
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-amap-geolocation
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from "react";
import {
    Button,
    Platform,
    ScrollView,
    StyleSheet,
    Text,
    View,
} from "react-native";
import {
    Geolocation, setInterval, addLocationListener, setAllowsBackgroundLocationUpdates,
    setGeoLanguage, setDistanceFilter, setDesiredAccuracy, init, setNeedAddress, start,
    stop, setLocationTimeout, setOnceLocation, GeoLanguage
} from "react-native-amap-geolocation";


const style = StyleSheet.create({
    body: {
        padding: 16,
        paddingTop: Platform.OS === "ios" ? 48 : 16,
    },
    button: {
        flexDirection: "column",
        marginRight: 8,
        marginBottom: 5,
        marginTop: 5
    },
    result: {
        fontFamily: Platform.OS === "ios" ? "menlo" : "monospace",
    },
});

class AmapGeoLocationDemo extends React.Component {
    state = {
        location: null, needAddressText: "setNeedAddress(false)",
        language: "setLanguage(chinese)", interval: "setInterval(默认2000)", onceText: "setOnceLocation(false) 设置单次定位",
        startText: "start 持续定位", timeoutText: "setLocationTimeout 设置请求定位超时时间",distanceText:"setDistanceFilter(0) 设置定位的最小更新距离"
    };
    watchId = 0;
    needAddress = true;
    currLanguage = GeoLanguage.ZH;
    currInterval = false;
    onceLocationJudge = false;
    timeout5000 = false;
    distanseJudge = true;
    init = () => {
        console.log("rn AMapLocationManagerImpl init");
        init("5f7389b845cbd89b1c32e24f526728f4").then(() => {
            console.log("rn AMapLocationManagerImpl init success");
        });

    };
    addLocationListener = () => {
        console.log("rn AMapLocationManagerImpl addLocationListener");
        addLocationListener((locationData) => {
            console.log("rn AMapLocationManagerImpl callback success:" + JSON.stringify(locationData, null, 2));
            let location = locationData;
            this.setState({ location: location });
        });
    };
    setDistanceFilter = () => {
        console.log("rn AMapLocationManagerImpl setDistanceFilter");
        this.distanseJudge = !this.distanseJudge;
        if (this.distanseJudge) {
            setDistanceFilter(0);
            this.setState({ distanceText: "setDistanceFilter(0) 设置定位的最小更新距离" });
        } else {
            setDistanceFilter(1);
            this.setState({ distanceText: "setDistanceFilter(1) 设置定位的最小更新距离" });
        }

    };
    setLocationTimeout = () => {
        console.log("rn AMapLocationManagerImpl setLocationTimeout");
        this.timeout5000 = !this.timeout5000;
        if (this.timeout5000) {
            setLocationTimeout(5000);
            this.setState({ timeoutText: "setLocationTimeout(5000) 设置请求定位超时时间" });
        } else {
            setLocationTimeout(10000);
            this.setState({ timeoutText: "setLocationTimeout(10000) 设置请求定位超时时间" });
        }
    };
    start = () => {
        console.log("rn AMapLocationManagerImpl start");
        start();
    };
    stop = () => {
        console.log("rn AMapLocationManagerImpl stop");
        stop();
    }
    onceLocation = () => {
        this.onceLocationJudge = !this.onceLocationJudge;
        if (this.onceLocationJudge) {
            setOnceLocation(true);
            this.setState({ onceText: "setOnceLocation(true) 设置单次定位", startText: "start 单次定位" });
        } else {
            setOnceLocation(false);
            this.setState({ onceText: "setOnceLocation(false) 设置单次定位", startText: "start 持续定位" });
        }
        console.log("rn AMapLocationManagerImpl current onceLocation:" + this.onceLocationJudge);
    };
    setInterval = () => {
        if (this.currInterval) {
            setInterval(2000);
            this.setState({ interval: "setInterval:2000" });
        } else {
            setInterval(10000);
            this.setState({ interval: "setInterval:10000" });
        }
        this.currInterval = !this.currInterval;
    }
    setNeedAddress = () => {
        this.needAddress = !this.needAddress;
        console.log("rn AMapLocationManagerImpl setNeedAddress:" + this.needAddress);
        if (this.needAddress) {
            setNeedAddress(true);
            this.setState({ needAddressText: "setNeedAddress(true)" });
        } else {
            setNeedAddress(false);
            this.setState({ needAddressText: "setNeedAddress(false)" });
        }
    }
    setLanguage = () => {
        // default = 0,chinese = 1, engilish=2;
        console.log("rn AMapLocationManagerImpl setLanguage");
        if (this.currLanguage == GeoLanguage.ZH) {
            this.currLanguage = GeoLanguage.EN;
            setGeoLanguage(GeoLanguage.EN);
            this.setState({ language: "setLanguage(engilish)" });
        } else {
            this.currLanguage = GeoLanguage.ZH;
            setGeoLanguage(GeoLanguage.ZH);
            this.setState({ language: "setLanguage(chinese)" });
        }

    }
    updateLocationState(location: any) {
    console.log("rn AMapLocationManagerImpl updateLocationState");
    if (location) {
        this.setState({ location: location });
        console.log(location);
    }
}
getCurrentPosition = () => {
    Geolocation.getCurrentPosition(
        (position) => this.updateLocationState(position),
        (error) => this.updateLocationState(error)
    );
};
watchPosition = () => {
    if (!this.watchId) {
        this.watchId = Geolocation.watchPosition(
            (position) => this.updateLocationState(position),
            (error) => this.updateLocationState(error)
        );
        console.log("rn AMapLocationManagerImpl watchPosition watchId:" + this.watchId);
    }
};
clearWatch = () => {
    if (this.watchId) {
        console.log("rn AMapLocationManagerImpl clearWatch watchId:" + this.watchId);
        Geolocation.clearWatch(this.watchId);
        this.watchId = 0;
    }
    stop();
    this.setState({ location: null });
};
render() {
    const location = this.state.location;
    const needAddressText = this.state.needAddressText;
    const language = this.state.language;
    const currInterval = this.state.interval;
    const onceText = this.state.onceText;
    const startText = this.state.startText;
    const timeoutText = this.state.timeoutText;
    const distanceText = this.state.distanceText;
    return (
        <ScrollView contentContainerStyle={style.body}>
        <View style={style.button}>
        <Button onPress={this.init} title="init 初始化接口" />
        </View>
        <View style={style.button}>
        <Button onPress={this.addLocationListener} title="addLocationListener 设置监听回调,原生接口不设置监听回调,text不会显示数据" />
        </View>
        <View style={style.button}>
        <Button onPress={this.setDistanceFilter} title={distanceText} />
        </View>
        <View style={style.button}>
        <Button onPress={this.setLocationTimeout} title={timeoutText} />
        </View>
        <View style={style.button}>
        <Button onPress={this.onceLocation} title={onceText} />
        </View>
        <View style={style.button}>
        <Button onPress={this.start} title={startText} />
        </View>
        <View style={style.button}>
        <Button onPress={this.stop} title="stop 结束持续定位" />
        </View>
        <View style={style.button}>
        <Button onPress={this.setInterval} title={currInterval} />
        </View>
        <View style={style.button}>
        <Button onPress={this.setNeedAddress} title={needAddressText} />
        </View>
        <View style={style.button}>
        <Button onPress={this.setLanguage} title={language} />
        </View>
        <View style={style.button}>
        <Button onPress={this.getCurrentPosition} title="Geolocation.getCurrentPosition 获取当前位置，相当于单次请求" />
        </View>
        <View style={style.button}>
        <Button onPress={this.watchPosition} title="Geolocation.watchPosition 开启持续定位" />
        </View>
        <View style={style.button}>
        <Button onPress={this.clearWatch} title="Geolocation.clearWatch 结束持续定位" />
        </View>
        <Text style={style.result}>{`${JSON.stringify(location, null, 2)}`}</Text>
    </ScrollView>
);
}

}

export default AmapGeoLocationDemo;
```

## Use Codegen

This repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).


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
    "@react-native-oh-tpl/react-native-amap-geolocation": "file:../../node_modules/@react-native-oh-tpl/react-native-amap-geolocation/harmony/amap_geolocation.har"
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

### 3. Introducing AmapGeolocationPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...
+  import {AMapGeolocationPackage} from '@react-native-oh-tpl/react-native-amap-geolocation/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new AMapGeolocationPackage(ctx)
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

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-amap-geolocation Releases](https://github.com/react-native-oh-library/react-native-amap-geolocation/releases)

### Permission Requirements

#### Add permissions in the module.json5 file under the entry directory.

Open `entry/src/main/module.json5`, add the following permission：

```
...
"requestPermissions": [
  {
    "name": "ohos.permission.LOCATION",
    "reason": "$string:Access_Location",
    "usedScene": {
      "when":"inuse"
    }
  },
  {
    "name": "ohos.permission.APPROXIMATELY_LOCATION",
    "reason": "$string:Access_AppRoximatelyLocation",
    "usedScene": {
      "when":"inuse"
    }
  },
  {
    "name": "ohos.permission.INTERNET",
  }
]
```

#### Adding the description of location permissions in the entry directory

open `entry/src/main/resources/base/element/string.json`, add the following content：

```
...
{
  "string": [
    {
      "name": "Access_Location",
      "value": "access Location"
    },
    {
      "name": "Access_AppRoximatelyLocation",
      "value": "access AppRoximatelyLocation"
    }
  ]
}
```


## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type          | Required | Platform | HarmonyOS Support |
| ---- | ----------- |---------------|----------| -------- |-------------------|
| init  | 初始化 SDK | Promise<void> | yes      | iOS/Android      | yes               |
| addLocationListener  | 添加定位监听函数 | void          | yes      | iOS/Android      | yes               |
| isStarted  | 获取当前是否正在定位的状态 | boolean       | no       | Android      | no                |
| setAllowsBackgroundLocationUpdates  | 是否允许后台定位 | void          | no       | iOS      | no                |
| setDesiredAccuracy  | 设定期望的定位精度（米） | void          | no       | iOS     | no                |
| setDistanceFilter  | 设定定位的最小更新距离（米） | void          | no       | iOS     | yes               |
| setGeoLanguage  | 设置逆地理信息的语言，目前支持中文和英文 | void          | no       | iOS/Android      | yes               |
| setGpsFirst  | 设置首次定位是否等待卫星定位结果 | void          | no       | Android      | no                |
| setGpsFirstTimeout  | 设置优先返回卫星定位信息时等待卫星定位结果的超时时间（毫秒） | void          | no       | Android      | no                |
| setHttpTimeout  | 设置联网超时时间（毫秒） | void          | no       | Android      | no                |
| setInterval  | 设置发起定位请求的时间间隔（毫秒），默认 2000，最小值为 1000 | void          | no       | Android      | yes               |
| setLocatingWithReGeocode  | 连续定位是否返回逆地理编码 | void          | no       | iOS      | no                |
| setLocationCacheEnable  | 设置是否使用缓存策略 | void          | no      | Android     | no                |
| setLocationMode  | 设置定位模式 | void          | no      | Android     | no                |
| setLocationPurpose  | 设置定位场景 | void          | no      | Android      | no                |
| setLocationTimeout  | 指定单次定位超时时间（秒） | no          | yes      | iOS      | yes               |
| setMockEnable  | 设置是否允许模拟位置 | void          | no      | Android      | no                |
| setNeedAddress  | 设置是否返回地址信息，默认返回地址信息 | no          | yes      | Android      | yes               |
| setOnceLocation  | 设置是否单次定位 | void          | no      | Android      | yes               |
| setOnceLocationLatest  | 设置定位是否等待 WiFi 列表刷新 | void          | no      | Android      | no                |
| setOpenAlwaysScanWifi  | 设置是否开启wifi始终扫描 | void          | no      | Android     | no                |
| setPausesLocationUpdatesAutomatically  | 指定定位是否会被系统自动暂停 | void          | no      | iOS      | no                |
| setReGeocodeTimeout  | 指定单次定位逆地理超时时间（秒）最小值是 2s。注意在单次定位请求前设置。 | void          | no      | iOS     | no                |
| setSensorEnable  | 设置是否使用设备传感器 | void          | no      | Android      | no                |
| setWifiScan  | 设置是否允许调用 WiFi 刷新 | void          | no      | Android      | no                |
| start  | 开始持续定位 | void          | no      | iOS/Android      | yes               |
| stop  | 停止持续定位 | void          | no      | iOS/Android      | yes               |
| Geolocation.getCurrentPosition  | 获取当前位置信息 | void          | no      | iOS/Android        | yes               |
| Geolocation.watchPosition  | 注册监听器进行持续定位 | void          | no      | iOS/Android      | yes               |
| Geolocation.clearWatch  | 移除位置监听 | void          | no      | iOS/Android      | yes               |

## Known Issues

- [ ] isStarted()接口获取当前是否正在定位的状态,harmony暂不支持[issue#2](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/2)
- [ ] setGpsFirst()接口获取当前是否正在定位的状态,harmony暂不支持[issue#3](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/3)
- [ ] setGpsFirstTimeout()接口获取当前是否正在定位的状态,harmony暂不支持[issue#4](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/4)
- [ ] setHttpTimeout()接口获取当前是否正在定位的状态,harmony暂不支持[issue#5](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/5)
- [ ] setMockEnable()接口获取当前是否正在定位的状态,harmony暂不支持[issue#6](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/6)
- [ ] setOnceLocationLatest()接口获取当前是否正在定位的状态,harmony暂不支持[issue#7](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/7)
- [ ] setOpenAlwaysScanWifi()接口获取当前是否正在定位的状态,harmony暂不支持[issue#8](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/8)
- [ ] setPausesLocationUpdatesAutomatically()接口获取当前是否正在定位的状态,harmony暂不支持[issue#9](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/9)
- [ ] setReGeocodeTimeout()接口获取当前是否正在定位的状态,harmony暂不支持[issue#10](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/10)
- [ ] setSensorEnable()接口获取当前是否正在定位的状态,harmony暂不支持[issue#11](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/11)
- [ ] setWifiScan()接口获取当前是否正在定位的状态,harmony暂不支持[issue#12](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/12)
- [ ] setLocationCacheEnable()接口获取当前是否正在定位的状态,harmony暂不支持[issue#13](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/13)
- [ ] setLocationMode()接口获取当前是否正在定位的状态,harmony暂不支持[issue#14](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/14)
- [ ] setLocationPurpose()接口获取当前是否正在定位的状态,harmony暂不支持[issue#15](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/15)
- [ ] setLocatingWithReGeocode()接口获取当前是否正在定位的状态设置连续定位是否返回逆地理编码,harmony暂不支持[issue#19](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/19)
- [ ] setDesiredAccuracy()接口设定期望的定位精度,harmony暂不支持[issue#22](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/22)
- [ ] setAllowsBackgroundLocationUpdates()接口是否允许后台定位,harmony暂不支持[issue#23](https://github.com/react-native-oh-library/react-native-amap-geolocation/issues/23)


## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/qiuxiang/react-native-amap-geolocation/blob/main/license).
