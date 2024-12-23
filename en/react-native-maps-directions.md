> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-maps-directions)

## Installation and Usage

> [!TIP] This library depends on react-native-maps，Can be referred to [react-native-maps documentation](./react-native-maps.md) install

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-maps-directions Releases](https://github.com/react-native-oh-library/react-native-maps-directions/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-maps-directions
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-maps-directions
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import { Dimensions, StyleSheet, View, Text } from "react-native";
import MapViewDirections from "react-native-maps-directions";
import MapView, { Marker } from "react-native-maps";

const { width, height } = Dimensions.get("window");
const ASPECT_RATIO = width / height;
const LATITUDE = 37.771707;
const LONGITUDE = -122.4053769;
const LATITUDE_DELTA = 0.0922;
const LONGITUDE_DELTA = LATITUDE_DELTA * ASPECT_RATIO;
const MAPS_APIKEY = "xxxxxx";

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
      coordinates: [...this.state.coordinates, e.nativeEvent.coordinate],
    });
  };

  render() {
    const { coordinates } = this.state;
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
          ref={(c) => (this.mapView = c)}
          onPress={this.onMapPress}
        >
          {this.state.coordinates.map((coordinate, index) => (
            <Marker key={`coordinate_${index}`} coordinate={coordinate} />
          ))}
          {this.state.coordinates.length >= 2 && (
            <MapViewDirections
              origin={this.state.coordinates[0]}
              destination={
                this.state.coordinates[this.state.coordinates.length - 1]
              }
              apikey={MAPS_APIKEY}
              mode="BICYCLING"
              strokeWidth={6}
              strokeColor={"#0000FF"}
              resetOnChange={true}
              onStart={(params) => {
                console.log(
                  `Started routing between "${params.origin}" and "${params.destination}"`
                );
              }}
              onReady={(result) => {
                console.log(`Distance: ${result.distance} km`);
                console.log(`Duration: ${result.duration} min.`);
                this.mapView.fitToCoordinates(result.coordinates, {
                  edgePadding: {
                    right: width / 20,
                    bottom: height / 20,
                    left: width / 20,
                    top: height / 20,
                  },
                });
              }}
              onError={(errorMessage) => {
                console.log("GOT AN ERROR");
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

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-maps. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-maps](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-maps.md#link) to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-maps-directions Releases](https://github.com/react-native-oh-library/react-native-maps-directions/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.
>
> 由于渲染在屏幕上的结果是 `MapView.Polyline` 组件，因此也支持 `MapView.Polyline` Properties，`MapView.Polyline`Properties 参见[**react-native-maps**](/en/react-native-maps.md#polyline)。

| Name                     | **Description**                                                                                                                                                                                                                                                                                                                                                                                           | Type                   | Required | **Default** | Platform    | HarmonyOS Support                                           |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- | -------- | ----------- | ----------- | ----------------------------------------------------------- |
| `origin`                 | The origin location to start routing from.                                                                                                                                                                                                                                                                                                                                                                | LatLng`or`String       | true     |             | iOS/Android | yes                                                         |
| destination              | The destination location to start routing to.                                                                                                                                                                                                                                                                                                                                                             | LatLng`or`String       | true     |             | iOS/Android | yes                                                         |
| apikey                   | Your Google Maps API Key or HUWEI Map API Key. HUWEI Map API Key see [here](https://developer.huawei.com/consumer/cn/doc/HMSCore-Guides/preparations-0000001185174404#section169441820428)                                                                                                                                                                                                                | String                 | true     |             | iOS/Android | yes                                                         |
| waypoints                | Array of waypoints to use between origin and destination.                                                                                                                                                                                                                                                                                                                                                 | [`LatLng` or `String`] | false    | []          | iOS/Android | no                                                          |
| language                 | The language to use when calculating directions. See [here](https://developers.google.com/maps/documentation/javascript/localization) for more info.                                                                                                                                                                                                                                                      | String                 | false    | en          | iOS/Android | no                                                          |
| mode                     | Which transportation mode to use when calculating directions. Allowed values are `"DRIVING"`, `"BICYCLING"`, `"WALKING"`, and `"TRANSIT"`.                                                                                                                                                                                                                                                                | String                 | false    | "DRIVING"   | iOS/Android | partially (Support `"DRIVING"`, `"BICYCLING"`, `"WALKING"`) |
| resetOnChange            | Tweak if the rendered `MapView.Polyline` should reset or not when calculating the route between `origin` and `destionation`. Set to `false` if you see the directions line glitching.                                                                                                                                                                                                                     | boolean                | false    | true        | iOS/Android | yes                                                         |
| optimizeWaypoints        | Set it to true if you would like Google Maps to re-order all the waypoints to optimize the route for the fastest route. Please be aware that if this option is enabled, you will be billed at a higher rate by Google as stated [here](https://developers.google.com/maps/documentation/javascript/directions#Waypoints).                                                                                 | boolean                | false    | false       | iOS/Android | no                                                          |
| splitWaypoints           | Directions API has a [limit](https://developers.google.com/maps/documentation/directions/usage-and-billing#directions-advanced) of 10 or 25 (depends on the billing plan) waypoints per route. When exceeding this limit you will be billed at a higher reate by Google. Set this to `true` if you would like to automatically split waypoints into multiple routes, thus bypassing this waypoints limit. | boolean                | false    | false       | iOS/Android | no                                                          |
| directionsServiceBaseUrl | Base URL of the Directions Service (API) you are using.                                                                                                                                                                                                                                                                                                                                                   | string                 | false    | (Google's)  | iOS/Android | yes                                                         |
| region                   | If you are using strings for **origin** or **destination**, sometimes you will get an incorrect route because Google Maps API needs the region where this places belong to. See [here](https://developers.google.com/maps/documentation/javascript/localization#Region) for more info.                                                                                                                    | String                 | false    |             | iOS/Android | no                                                          |
| precision                | The precision level of detail of the drawn polyline. Allowed values are "high", and "low". Setting to "low" will yield a polyline that is an approximate (smoothed) path of the resulting directions. Setting to "high" may cause a hit in performance in case a complex route is returned.                                                                                                               | String                 | false    | "low"       | iOS/Android | no                                                          |
| timePrecision            | The timePrecision to get Realtime traffic info. Allowed values are "none", and "now". Defaults to "none".                                                                                                                                                                                                                                                                                                 | String                 | false    | "none"      | iOS/Android | no                                                          |
| channel                  | If you include the channel parameter in your requests, you can generate a Successful Requests report that shows a breakdown of your application's API requests across different applications that use the same client ID (such as externally facing access vs. internally facing access).                                                                                                                 | String                 | false    | null        | iOS/Android | no                                                          |

### Event and Returns

| Event Name | **Description**                                                                                                                   | Type     | Required | Platform    | HarmonyOS Support |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| `onStart`  | Callback that is called when the routing has started.                                                                             | Function | false    | iOS/Android | yes               |
| `onReady`  | Callback that is called when the routing has succesfully finished. note: distance returned in kilometers and duration in minutes. | Function | false    | iOS/Android | yes               |
| `onError`  | Callback that is called in case the routing has failed.                                                                           | Function | false    | iOS/Android | yes               |

#### onStart

```
 onStart(params:Object):void
```

| Name   | **Description**                                                                                        | Type   | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------------------------------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| params | 回调函数返回值，包含起点、终点和中间点的经纬度信息。数据格式为：{ origin, destination, waypoints: [] } | Object | True     | iOS/Android | yes               |

#### onReady

```
 onReady(result:Object):void
```

| Name   | **Description**                                                                                                                                                                | Type   | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| result | 回调函数返回值，包含起点到终点的距离、路程时间、和途径路径的经纬度等信息。数据格式：{ distance: Number, duration: Number, coordinates: [], fare: Object, waypointOrder: [[]] } | Object | True     | iOS/Android | yes               |

#### onError

```
 onError(errorMessage:Object):void
```

| Name         | **Description**                                     | Type   | Required | Platform    | HarmonyOS Support |
| ------------ | --------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| errorMessage | 回调函数返回值，访问 directions rest api 的报错信息 | Object | True     | iOS/Android | yes               |

## Known Issues

- [ ] waypointsProperties 不支持，不支持的原因是由于华为侧 Directions API 不支持中间点参数查询：[issue#13](https://github.com/react-native-oh-library/react-native-maps-directions/issues/13)
- [ ] languageProperties 不支持，不支持的原因是由于华为侧 Directions API 只支持文字指引的语种和谷歌地图 api 的语言本地化本地化功能不一样：[issue#14](https://github.com/react-native-oh-library/react-native-maps-directions/issues/14)
- [ ] optimizeWaypointsProperties 不支持，不支持的原因是由于华为侧 Directions API 不支持中间点优化，获取更快路线：[issue#15](https://github.com/react-native-oh-library/react-native-maps-directions/issues/15)
- [ ] splitWaypointsProperties 不支持，不支持的原因是由于华为侧 Directions API 不支持将中间点个数设置，将其分割成多条路线：[issue#16](https://github.com/react-native-oh-library/react-native-maps-directions/issues/16)
- [ ] regionProperties 不支持，不支持的原因是由于华为侧 Directions API 不支持地区代码和地点的映射：[issue#17](https://github.com/react-native-oh-library/react-native-maps-directions/issues/17)
- [ ] precisionProperties 不支持，不支持的原因是由于华为侧 Directions API 不支持更精细的绘画路程线路：[issue#18](https://github.com/react-native-oh-library/react-native-maps-directions/issues/18)
- [ ] timePrecisionProperties 不支持，不支持的原因是由于华为侧 Directions API 不支持实时查询路线：[issue#19](https://github.com/react-native-oh-library/react-native-maps-directions/issues/19)
- [ ] channelProperties 不支持，不支持的原因是由于华为侧 Directions API 不支持渠道查询：[issue#20](https://github.com/react-native-oh-library/react-native-maps-directions/issues/20)

## Others

- 华为地图 apikey 申请参见[获取 API key](https://developer.huawei.com/consumer/cn/doc/HMSCore-Guides/preparations-0000001185174404#section169441820428) ，其中说明的内容请重点关注。

## License

This project is licensed under [The MIT License (MIT)](https://github.com/bramus/react-native-maps-directions/blob/master/LICENSE.md).
