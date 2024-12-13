> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-map-linking</code> </h1>
</p>

This project is based on [react-native-map-linking@1.0.1](https://github.com/starlight36/react-native-map-linking).

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-map-linking`, The version correspondence details are as follows:

| Version                   | Package Name                                  | Repository                                                                                | Release                                                                                                     |
| ------------------------- | --------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| <= 1.0.1-0.0.1@deprecated | @react-native-oh-tpl/react-native-map-linking | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-map-linking) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-map-linking/releases) |
| > 1.0.1                   | @react-native-ohos/react-native-map-linking   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-map-linking)                 | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-map-linking/releases)                 |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-map-linking
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-map-linking
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  TouchableOpacity,
} from "react-native";
import MapLinking from "react-native-map-linking";

class MapLinkingDemo extends Component {
  render() {
    return (
      <View style={styles.container}>
        <TouchableOpacity
          onPress={() => {
            MapLinking.markLocation(
              { lat: 39.9901079, lng: 116.1887467 },
              "Xiangshan Park",
              "bbb"
            );
          }}
        >
          <View style={styles.button}>
            <Text style={styles.text}>mark specific locations</Text>
          </View>
        </TouchableOpacity>
        <TouchableOpacity
          onPress={() => {
            MapLinking.planRoute(
              { lat: 39.9901079, lng: 116.1887467, title: "Xiangshan Park" },
              { lat: 40.0382556, lng: 116.3144536, title: "Qinghe Station" },
              "drive"
            );
          }}
        >
          <View style={styles.button}>
            <Text style={styles.text}>route planning</Text>
          </View>
        </TouchableOpacity>
        <TouchableOpacity
          onPress={() => {
            MapLinking.navigate({
              lat: 40.0382556,
              lng: 116.3144536,
              title: "Qinghe Station",
            });
          }}
        >
          <View style={styles.button}>
            <Text style={styles.text}>launch navigation</Text>
          </View>
        </TouchableOpacity>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
  },
  button: {
    padding: 10,
    backgroundColor: "#3B5998",
    marginBottom: 10,
  },
  text: {
    color: "white",
  },
});
export default MapLinkingDemo;
```

## 2. Constraints

### 2.1 Using this third-party library requires configuring querySchemes.

Please configure the `querySchemes` field in `entry/src/module.json5` to support launching Petal Map and Amap.

```
{
  "module": {
    "querySchemes":[
      "maps",
      "amapuri",
    ],
    ...
  }
}
```

### 2.2 Compatibility

Check the release version information in the release address of the third-party library: [@react-native-ohos/react-native-map-linking Releases](https://gitee.com/openharmony-sig/rntpc_react-native-map-linking/releases)

## 3. APIs

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                       | Description                                                        | Optional                                                                                                                                                                                                                                                                                                                                                                                                                         | Required | Platform | HarmonyOS Support |
| ------------------------------------------ | ------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| markLocation(location, title, content)     | Marks a specific location on the map                               | location: Location coordinates, an object that includes: **lat** - Latitude **lng** - Longitude **type** - Coordinate type, supports `gcj02` (China Geodetic Coordinate), `wgs84` (GPS Coordinate) **title** - Location marker name **content** - Location marker description                                                                                                                                                    | no       | all      | partially         |
| planRoute(srcLocation, distLocation, mode) | Plans a route between two locations                                | srcLocation: Starting location coordinates, an object that includes: **lat** - Latitude **lng** - Longitude **title** - Starting location name distLocation: Destination coordinates, an object that includes: **lat** - Latitude **lng** - Longitude **type** - Coordinate type, supports `gcj02`, `wgs84` **title** - Destination name mode: Route mode, options include drive (driving), bus (public transit), walk (walking) | no       | all      | partially         |
| navigate(distLocation)                     | Starts navigation from the current location to the target location | distLocation: Destination coordinates, an object that includes: **lat** - Latitude **lng** - Longitude **type** - Coordinate type, supports `gcj02`, `wgs84` **title** - Destination name                                                                                                                                                                                                                                        | no       | all      | partially         |

## 4. Known Issues

- [ ] Currently, `react-native-map-link` cannot launch Baidu Maps, as the app store URL and specific parameters required for `react-native-map-link` are not provided. [issue#1](https://github.com/react-native-oh-library/react-native-map-linking/issues/1)
- [ ] Currently, `react-native-map-link` only supports route planning with Amap. Other features are not supported yet. [issue#2](https://github.com/react-native-oh-library/react-native-map-linking/issues/2)

## 5. Others

- If there is no available map application installed on the system, the component will recommend downloading Amap.
- Currently, only route planning with Amap is supported. Other features such as launching navigation and marking specific locations are not yet available.

## 6. License

This project is licensed under [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-map-linking/blob/master/LICENSE).
