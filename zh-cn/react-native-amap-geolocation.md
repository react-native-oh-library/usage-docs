<!-- {% raw %} -->
> 模板版本：v0.2.2

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


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-amap-geolocation) 



## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-amap-geolocation Releases](https://github.com/react-native-oh-library/react-native-amap-geolocation/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-amap-geolocation@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-amap-geolocation@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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
import Geolocation from "react-native-amap-geolocation";

const style = StyleSheet.create({
  body: {
    padding: 16,
    paddingTop: Platform.OS === "ios" ? 48 : 16,
  },
  controls: {
    flexWrap: "wrap",
    alignItems: "flex-start",
    flexDirection: "row",
    marginBottom: 16,
  },
  button: {
    flexDirection: "column",
    marginRight: 8,
    marginBottom: 8,
    marginTop:50
  },
  result: {
    fontFamily: Platform.OS === "ios" ? "menlo" : "monospace",
  },
});

class AmapGeoLocationDemo extends React.Component {
  state = { location: null };
  
 componentDidMount(){
  Geolocation.init("aabbbcccc")
 }

start=()=>{
  console.log("geolocation start");
  Geolocation.start().then((result)=>{
    let location = result;
    this.setState({ location });
    console.log("geolocationupdateLocation:"+location);
   }).catch((error)=>{
    console.log(error);
   });
};

stop =()=>{
  console.log("geolocation stop");
  Geolocation.stop();
}

 onceLocation=  ()=>{
   Geolocation.setOnceLocation().then((result)=>{
    let location = result;
    this.setState({ location });
    console.log("geolocation onceLocation:"+location);
   }).catch((error)=>{
    console.log(error);
   });

};
getLastKnownLocation= () =>{
   Geolocation.getLastKnownLocation().then((result)=>{
    let location = result;
    this.setState({ location });
    console.log("geolocation lastLocation:"+location);
   }).catch((error)=>{
    console.log(error);
   });
}

setInterval10000 = ()=>{
  Geolocation.setInterval(10000);
}
setInterval2000 = ()=>{
  Geolocation.setInterval(2000);
}
setNeedAddressTrue=()=>{
  Geolocation.setNeedAddress(true);
}
setNeedAddressFalse =()=>{
  Geolocation.setNeedAddress(false);
}

setLangeChinese=()=>{
  Geolocation.setGeoLanguage(1);
}
setLangeEnglish=()=>{
 Geolocation.setGeoLanguage(2);
}
render() {
  const { location } = this.state;
 return (
     <ScrollView contentContainerStyle={style.body}>
         <View style={style.button}>
           <Button onPress={this.start} title="start" />
         </View>
         <View style={style.button}>
           <Button onPress={this.stop} title="stop" />
         </View>
         <View style={style.button}>
           <Button onPress={this.onceLocation} title="setOnceLocation" />
         </View>
         <View style={style.button}>
           <Button onPress={this.getLastKnownLocation} title="getLastKnownLocation" />
         </View>
         <View style={style.button}>
           <Button onPress={this.setInterval2000} title="setInterval(2000)" />
         </View>
         <View style={style.button}>
           <Button onPress={this.setInterval10000} title="setInterval(10000)" />
         </View>
         <View style={style.button}>
           <Button onPress={this.setNeedAddressTrue} title="setNeedAddress(true)" />
         </View>
         <View style={style.button}>
           <Button onPress={this.setNeedAddressFalse} title="setNeedAddress(false)" />
         </View>
         <View style={style.button}>
           <Button onPress={this.setLangeChinese} title="setLangeChinese" />
         </View>
         <View style={style.button}>
           <Button onPress={this.setLangeEnglish} title="setLangeEnglish" />
         </View>
       <Text style={style.result}>{`${JSON.stringify(location, null, 2)}`}</Text> 
     </ScrollView>
   );
}
}

export default AmapGeoLocationDemo;
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。


## Link

目前HarmonyOS暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides 字段

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
    "@react-native-oh-tpl/react-native-amap-geolocation": "file:../../node_modules/@react-native-oh-tpl/react-native-amap-geolocation/harmony/amap_geolocation.har"
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

### 在 ArkTs 侧引入 AmapGeolocationPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {AmapGeolocationPackage} from '@react-native-oh-tpl/react-native-amap-geolocation';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new AmapGeolocationPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-amap-geolocation Releases](https://github.com/react-native-oh-library/react-native-amap-geolocation/releases)


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| code  | 错误代码         | number  | yes | iOS/Android      | yes |
| message  | 错误信息         | string  | yes | iOS/Android      | yes |
| android  | Android平台         | string | yes | iOS/Android      | yes |
| iOS  | iOS平台         | string  | yes | iOS/Android      | yes |
| accuracy  | 定位精度 (米)        | number  | yes | iOS/Android      | yes |
| altitude  | 海拔（米），需要 GPS         | number  | yes | iOS/Android      | yes |
| altitudeAccuracy  | 海拔精度         | number  | yes | iOS/Android      | yes |
| latitude  | 经度，[-180, 180]         | number  | yes | iOS/Android      | yes |
| longitude  | 纬度，[-90, 90]         | number  | yes | iOS/Android      | yes |
| speed  | 移动速度（米/秒），需要 GPS         | number  | yes | iOS/Android      | yes |
| coordinateType  | 坐标系类型       | string  | yes | Android      | yes |
| errorInfo  | 错误信息         | string | yes | iOS/Android      | yes |
| heading  | 移动方向，需要 GPS         | number  | yes | iOS/Android      | yes |
| locationDetail  | 定位信息描述         | string  | yes | Android      | yes |
| timestamp  | 定位时间（毫秒）         | number  | yes | iOS/Android      | yes |
| distanceFilter  | 位置信息的距离过滤器，用于限制位置更新的触发频率         | number  | yes | iOS/Android      | yes |
| enableHighAccuracy  | 是否启用高精度模式来获取位置信息。        | boolean | yes | iOS/Android      | yes |
| maximumAge  | 获取位置信息的最大缓存时间        | number  | yes | iOS/Android      | yes |
| timeout  |  获取位置信息的超时时间   | number  | yes | iOS/Android      | yes |
| address  | 详细地址         | number  | yes | iOS/Android      | yes |
|city  | 城市         | string  | yes | iOS/Android      | yes |
| cityCode  | 城市编码        | string | yes | iOS/Android      | yes |
| country  | 国家        | string  | yes | iOS/Android      | yes |
| district  | 地区         | string  | yes | iOS/Android      | yes |
| poiName | 兴趣点        | string  | yes | iOS/Android      | yes |
| province  | 省份       | string  | yes | iOS/Android      | yes |
| street  | 街道         | string | yes | iOS/Android      | yes |
| streetNumber  | 门牌号        | string  | yes | iOS/Android      | yes |


## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- |-------------------|
| init  | 初始化 SDK | Promise<void>  | yes| iOS/Android      | yes               |
| isStarted  | 获取当前是否正在定位的状态 | boolean | yes | Android      | no                |
| setAllowsBackgroundLocationUpdates  | 是否允许后台定位 | void  | yes | iOS      | yes               |
| setDesiredAccuracy  | 设定期望的定位精度（米） | void  | yes | iOS     | yes               |
| setDistanceFilter  | 设定定位的最小更新距离（米） | void  | yes | iOS     | yes               |
| setGeoLanguage  | 设置逆地理信息的语言，目前支持中文和英文 | void  | yes | iOS/Android      | yes               |
| setGpsFirst  | 设置首次定位是否等待卫星定位结果 | void  | yes | Android      | no                |
| setGpsFirstTimeout  | 设置优先返回卫星定位信息时等待卫星定位结果的超时时间（毫秒） | void  | yes | Android      | no                |
| setHttpTimeout  | 设置联网超时时间（毫秒） | void  | yes | Android      | no                |
| setInterval  | 设置发起定位请求的时间间隔（毫秒），默认 2000，最小值为 1000 | void  | yes | Android      | yes               |
| setLocatingWithReGeocode  | 连续定位是否返回逆地理编码 | void  | yes | iOS      | yes               |
| setLocationCacheEnable  | 设置是否使用缓存策略 | void  | yes | Android     | no                |
| setLocationMode  | 设置定位模式 | void  | yes | Android     | no                |
| setLocationPurpose  | 设置定位场景 | void  | yes | Android      | no                |
| setLocationTimeout  | 指定单次定位超时时间（秒） | void  | yes | iOS      | yes               |
| setMockEnable  | 设置是否允许模拟位置 | void  | yes | Android      | no                |
| setNeedAddress  | 设置是否返回地址信息，默认返回地址信息 | void  | yes | Android      | yes               |
| setOnceLocation  | 设置是否单次定位 | void  | yes | Android      | yes               |
| setOnceLocationLatest  | 设置定位是否等待 WiFi 列表刷新 | void  | yes | Android      | no                |
| setOpenAlwaysScanWifi  | 设置是否开启wifi始终扫描 | void  | yes | Android     | no                |
| setPausesLocationUpdatesAutomatically  | 指定定位是否会被系统自动暂停 | void  | yes | iOS      | no                |
| setReGeocodeTimeout  | 指定单次定位逆地理超时时间（秒）最小值是 2s。注意在单次定位请求前设置。 | void  | yes | iOS     | no                |
| setSensorEnable  | 设置是否使用设备传感器 | void  | yes | Android      | no                |
| setWifiScan  | 设置是否允许调用 WiFi 刷新 | void  | yes | Android      | no                |
| start  | 开始持续定位 | void  | yes | iOS/Android      | yes               |
| stop  | 停止持续定位 | void  | yes | iOS/Android      | yes               |

## 遗留问题

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


## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/qiuxiang/react-native-amap-geolocation/blob/main/license) ，请自由地享受和参与开源。

<!-- {% endraw %} -->