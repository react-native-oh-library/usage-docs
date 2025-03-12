
> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-map-clustering</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/venits/react-native-map-clustering">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-map-clustering)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-map-clustering Releases](https://github.com/react-native-oh-library/react-native-map-clustering/releases).

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-map-clustering
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-map-clustering
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import MapView from "react-native-map-clustering";
import { Marker } from "react-native-maps";

function getRandomLatitude(min = 48, max = 56) {
  return Math.random() * (max - min) + min;
}

function getRandomLongitude(min = 14, max = 24) {
  return Math.random() * (max - min) + min;
}

const INITIAL_REGION = {
  latitude: 52.5,
  longitude: 19.2,
  latitudeDelta: 8.5,
  longitudeDelta: 8.5
};

export function MapClusteringExample() {
  const _generateMarkers = (count: number) => {
    const markers = [];

    for (let i = 0; i < count; i++) {
      markers.push(
        <Marker

          title='456'
          key={i}
          coordinate={{
            latitude: getRandomLatitude(),
            longitude: getRandomLongitude()
          }}
        />
      );
    }

    return markers;
  };

  return (
    <MapView initialRegion={INITIAL_REGION}
      style={{ flex: 1 }}
    >
      {_generateMarkers(200)}
    </MapView>
  );
};

```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-maps. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-maps](/en/react-native-maps.md) to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-map-clustering Releases](https://github.com/react-native-oh-library/react-native-map-clustering/releases)


## Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


### MapView

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ----------- |
| clusterColor  | Background color of cluster.      | String  | NO | ALL      | NO |
| clusterTextColor  | 	Color of text in cluster.      | String | NO | ALL      | NO |
| clusterFontFamily  | Font family of text in cluster.       | String  | NO | ALL      | NO |
| onClusterPress(cluster, markers)  | Allows you to control cluster on click event. Function returns information about cluster and its markers.   | Function  | NO | ALL      | YES |
| tracksViewChanges  | Sets whether the cluster markers should track view changes. It's turned off by default to improve cluster markers performance.     | Bool  | NO | NO      | NO |
| width  | map's width.     | Number  | NO |  ALL    | YES |
|height  | map's height.     | Number  | NO | NO      | NO |
| radius  | SuperCluster radius.     | Number  | NO | ALL      | YES |
| extent  | SuperCluster extent.     | Number  | NO | ALL      | YES |
| minZoom  | SuperCluster minZoom.     | Number  | NO | ALL      | YES |
| maxZoom  | SuperCluster maxZoom.     | Number | NO | NO      | NO |
| minPoints  | SuperCluster minPoints.    | Number  | NO | ALL      | YES |
| preserveClusterPressBehavior  | If set to true, after clicking on cluster it will not be zoomed.     | Bool  | NO |  ALL    | YES |
| edgePadding  | Edge padding for react-native-maps's fitToCoordinates method, called in onClusterPress for fitting to pressed cluster children.     | Object  | NO |    NO   | NO |
| animationEnabled  | Animate imploding/exploding of clusters' markers and clusters size change. Works only on iOS.     | Bool  | NO |    iOS   | NO |
| layoutAnimationConf  | LayoutAnimation.Presets.spring     | LayoutAnimationConfig  | NO |    iOS   | NO |
| onRegionChangeComplete(region, markers)  | Called when map's region changes. In return you get current region and markers data.    | Function  | NO |    ALL   | YES |
| onMarkersChange(markers) | CCalled when markers change. In return you get markers data.    | Function  | NO |    ALL   | YES |
| superClusterRef  |Return reference to supercluster library. You can read more about options it has here.    | MutableRefObject  | NO |    ALL   | YES |
| clusteringEnabled  | Set true to enable and false to disable clustering.   | Bool  | NO |    ALL   | YES |
| spiralEnabled  | Set true to enable and false to disable spiral view.   | Bool  | NO |    NO   | NO |
| renderCluster  | Enables you to render custom cluster with custom styles and logic.  | Function  | NO |    ALL   | NO |
| spiderLineColor  | Enables you to set color of spider line which joins spiral location with center location.   | String  | NO |    NO   | NO |


## Known Issues

- [ ] Unsupported property clusterColor [issue#1](https://github.com/react-native-oh-library/react-native-map-clustering/issues/1)
- [ ] Unsupported property clusterTextColor [issue#2](https://github.com/react-native-oh-library/react-native-map-clustering/issues/2)
- [ ] Unsupported property clusterFontFamily [issue#3](https://github.com/react-native-oh-library/react-native-map-clustering/issues/3)
- [ ] Unsupported property tracksViewChanges [issue#4](https://github.com/react-native-oh-library/react-native-map-clustering/issues/4)
- [ ] Unsupported property renderCluster [issue#5](https://github.com/react-native-oh-library/react-native-map-clustering/issues/5)

## Others

- The height property is currently unsupported, consistent with iOS behavior. [issue#273](https://github.com/venits/react-native-map-clustering/issues/273)
- The maxZoom property is currently unsupported, consistent with iOS behavior.[issue#274](https://github.com/venits/react-native-map-clustering/issues/274)
- The edgePadding property is currently unsupported, consistent with iOS behavior.[issue#221](https://github.com/venits/react-native-map-clustering/issues/221)
- The spiralEnabled property is currently unsupported, consistent with iOS behavior.[issue#275](https://github.com/venits/react-native-map-clustering/issues/275)
- The spiderLineColor property is currently unsupported, consistent with iOS behavior.[issue#276](https://github.com/venits/react-native-map-clustering/issues/276)

## License

This project is licensed under [The MIT License (MIT)](https://mit-license.org/).

