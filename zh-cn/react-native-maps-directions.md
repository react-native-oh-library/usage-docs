> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-maps-directions</code> </h1>
</p>
<p align="center">
    <a href=https://github.com/bramus/react-native-maps-directions>
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bramus/react-native-maps-directions/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-maps-directions)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-maps-directions Releases](https://github.com/react-native-oh-library/react-native-maps-directions/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-maps-directions@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-maps-directions@file:#
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react';
import { Dimensions, StyleSheet, View, Text } from 'react-native';
import MapViewDirections from 'react-native-maps-directions';
import MapView, { Marker } from "react-native-maps";

const { width, height } = Dimensions.get('window');
const ASPECT_RATIO = width / height;
const LATITUDE = 37.771707;
const LONGITUDE = -122.4053769;
const LATITUDE_DELTA = 0.0922;
const LONGITUDE_DELTA = LATITUDE_DELTA * ASPECT_RATIO;
const MAPS_APIKEY = 'xxxxxx';

class MapExample extends Component {
  constructor(props) {
    super(props);
    this.state = {
      coordinates: [
        {
          latitude: 37.3317876,
          longitude: -122.0054812,
        },
        {
          latitude: 37.771707,
          longitude: -122.4053769,
        },
      ],
    };
    this.mapView = null;
  }

  onMapPress = (e) => {
    this.setState({
      coordinates: [
        ...this.state.coordinates,
        e.nativeEvent.coordinate,
      ],
    });
  }

  render() {
    const { coordinates} = this.state;
    return (
      <View style={styles.container}>
      <MapView
        initialRegion={{
          latitude: LATITUDE,
          longitude: LONGITUDE,
          latitudeDelta: LATITUDE_DELTA,
          longitudeDelta: LONGITUDE_DELTA,
        }}
        style={StyleSheet.absoluteFill}
        ref={c => this.mapView = c}
        onPress={this.onMapPress}>
      
        {this.state.coordinates.map((coordinate, index) =>
          <Marker key={`coordinate_${index}`} coordinate={coordinate} />
        )}
        {(this.state.coordinates.length >= 2) && (
          <MapViewDirections
            origin={this.state.coordinates[0]}
            destination={this.state.coordinates[this.state.coordinates.length-1]}
            apikey={MAPS_APIKEY}
            mode='BICYCLING'
            strokeWidth={6}
            strokeColor={"#0000FF"}
            resetOnChange={true}
            onStart={(params) => {
              console.log(`Started routing between "${params.origin}" and "${params.destination}"`);
            }}
            onReady={result => {
              console.log(`Distance: ${result.distance} km`)
              console.log(`Duration: ${result.duration} min.`)
              this.mapView.fitToCoordinates(result.coordinates, {
                edgePadding: {
                  right: (width / 20),
                  bottom: (height / 20),
                  left: (width / 20),
                  top: (height / 20),
                }
              });
            }}
            onError={(errorMessage) => {
              console.log('GOT AN ERROR');
            }}
          />
         )} 
      </MapView>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    ...StyleSheet.absoluteFillObject,
    justifyContent: "flex-end",
    alignItems: "center",
    height: 300,
  },
  map: {
    ...StyleSheet.absoluteFillObject,
  },
});

export default MapExample;

```

## Link

本库在HarmonyOS NEXT侧实现依赖@react-native-oh-tpl/react-native-maps 的原生端代码，如已在HarmonyOS NEXT工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-maps 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-maps.md#link)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-maps-directions Releases](https://github.com/react-native-oh-library/react-native-maps-directions/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
> 由于渲染在屏幕上的结果是 `MapView.Polyline` 组件，因此也支持 `MapView.Polyline` 属性，`MapView.Polyline`属性参见[**react-native-maps**](/zh-cn/react-native-maps.md#polyline)。

| Name                     | **Description**                                              | Type                   | Required | **Default** | Platform    | HarmonyOS Support                                           |
| ------------------------ | ------------------------------------------------------------ | ---------------------- | -------- | ----------- | ----------- | ----------------------------------------------------------- |
| `origin`                 | The origin location to start routing from.                   | LatLng` or `String     | true     |             | iOS/Android | yes                                                         |
| destination              | The destination location to start routing to.                | LatLng` or `String     | true     |             | iOS/Android | yes                                                         |
| apikey                   | Your Google Maps API Key or HUWEI Map API Key. HUWEI Map API Key see [here](https://developer.huawei.com/consumer/cn/doc/HMSCore-Guides/preparations-0000001185174404#section169441820428) | String                 | true     |             | iOS/Android | yes                                                         |
| waypoints                | Array of waypoints to use between origin and destination.    | [`LatLng` or `String`] | false    | []          | iOS/Android | no                                                          |
| language                 | The language to use when calculating directions. See [here](https://developers.google.com/maps/documentation/javascript/localization) for more info. | String                 | false    | en          | iOS/Android | no                                                          |
| mode                     | Which transportation mode to use when calculating directions. Allowed values are `"DRIVING"`, `"BICYCLING"`, `"WALKING"`, and `"TRANSIT"`. | String                 | false    | "DRIVING"   | iOS/Android | partially (Support `"DRIVING"`, `"BICYCLING"`, `"WALKING"`) |
| resetOnChange            | Tweak if the rendered `MapView.Polyline` should reset or not when calculating the route between `origin` and `destionation`. Set to `false` if you see the directions line glitching. | boolean                | false    | true        | iOS/Android | yes                                                         |
| optimizeWaypoints        | Set it to true if you would like Google Maps to re-order all the waypoints to optimize the route for the fastest route. Please be aware that if this option is enabled, you will be billed at a higher rate by Google as stated [here](https://developers.google.com/maps/documentation/javascript/directions#Waypoints). | boolean                | false    | false       | iOS/Android | no                                                          |
| splitWaypoints           | Directions API has a [limit](https://developers.google.com/maps/documentation/directions/usage-and-billing#directions-advanced) of 10 or 25 (depends on the billing plan) waypoints per route. When exceeding this limit you will be billed at a higher reate by Google. Set this to `true` if you would like to automatically split waypoints into multiple routes, thus bypassing this waypoints limit. | boolean                | false    | false       | iOS/Android | no                                                          |
| directionsServiceBaseUrl | Base URL of the Directions Service (API) you are using.      | string                 | false    | (Google's)  | iOS/Android | yes                                                         |
| region                   | If you are using strings for **origin** or **destination**, sometimes you will get an incorrect route because Google Maps API needs the region where this places belong to. See [here](https://developers.google.com/maps/documentation/javascript/localization#Region) for more info. | String                 | false    |             | iOS/Android | no                                                          |
| precision                | The precision level of detail of the drawn polyline. Allowed values are "high", and "low". Setting to "low" will yield a polyline that is an approximate (smoothed) path of the resulting directions. Setting to "high" may cause a hit in performance in case a complex route is returned. | String                 | false    | "low"       | iOS/Android | no                                                          |
| timePrecision            | The timePrecision to get Realtime traffic info. Allowed values are "none", and "now". Defaults to "none". | String                 | false    | "none"      | iOS/Android | no                                                          |
| channel                  | If you include the channel parameter in your requests, you can generate a Successful Requests report that shows a breakdown of your application's API requests across different applications that use the same client ID (such as externally facing access vs. internally facing access). | String                 | false    | null        | iOS/Android | no                                                          |

### 事件和返回

| Event Name | **Description**                                              | Type     | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| `onStart`  | Callback that is called when the routing has started.        | Function | false    | iOS/Android | yes               |
| `onReady`  | Callback that is called when the routing has succesfully finished. note: distance returned in kilometers and duration in minutes. | Function | false    | iOS/Android | yes               |
| `onError`  | Callback that is called in case the routing has failed.      | Function | false    | iOS/Android | yes               |

#### onStart

```
 onStart(params:Object):void
```

| Name   | **Description**                                              | Type   | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| params | 回调函数返回值，包含起点、终点和中间点的经纬度信息。数据格式为：{ origin, destination, waypoints: [] } | Object | True     | iOS/Android | yes               |

#### onReady

```
 onReady(result:Object):void
```

| Name   | **Description**                                              | Type   | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| result | 回调函数返回值，包含起点到终点的距离、路程时间、和途径路径的经纬度等信息。数据格式：{ distance: Number, duration: Number, coordinates: [], fare: Object, waypointOrder: [[]] } | Object | True     | iOS/Android | yes               |

#### onError

```
 onError(errorMessage:Object):void
```

| Name         | **Description**                                   | Type   | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| errorMessage | 回调函数返回值，访问directions rest api的报错信息 | Object | True     | iOS/Android | yes               |

## 遗留问题

- [ ] waypoints属性不支持，不支持的原因是由于华为侧Directions API不支持中间点参数查询：[issue#13](https://github.com/react-native-oh-library/react-native-maps-directions/issues/13)
- [ ] language属性不支持，不支持的原因是由于华为侧Directions API只支持文字指引的语种和谷歌地图api的语言本地化本地化功能不一样：[issue#14](https://github.com/react-native-oh-library/react-native-maps-directions/issues/14)
- [ ] optimizeWaypoints属性不支持，不支持的原因是由于华为侧Directions API不支持中间点优化，获取更快路线：[issue#15](https://github.com/react-native-oh-library/react-native-maps-directions/issues/15)
- [ ] splitWaypoints属性不支持，不支持的原因是由于华为侧Directions API不支持将中间点个数设置，将其分割成多条路线：[issue#16](https://github.com/react-native-oh-library/react-native-maps-directions/issues/16)
- [ ] region属性不支持，不支持的原因是由于华为侧Directions API不支持地区代码和地点的映射：[issue#17](https://github.com/react-native-oh-library/react-native-maps-directions/issues/17)
- [ ] precision属性不支持，不支持的原因是由于华为侧Directions API不支持更精细的绘画路程线路：[issue#18](https://github.com/react-native-oh-library/react-native-maps-directions/issues/18)
- [ ] timePrecision属性不支持，不支持的原因是由于华为侧Directions API不支持实时查询路线：[issue#19](https://github.com/react-native-oh-library/react-native-maps-directions/issues/19)
- [ ] channel属性不支持，不支持的原因是由于华为侧Directions API不支持渠道查询：[issue#20](https://github.com/react-native-oh-library/react-native-maps-directions/issues/20)

## 其他

华为地图apikey申请参见[获取API key](https://developer.huawei.com/consumer/cn/doc/HMSCore-Guides/preparations-0000001185174404#section169441820428)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/bramus/react-native-maps-directions/blob/master/LICENSE.md) ，请自由地享受和参与开源。