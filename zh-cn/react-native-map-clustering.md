> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-map-clustering)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-map-clustering Releases](https://github.com/react-native-oh-library/react-native-map-clustering/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：



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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-maps的原生端代码，如已在鸿蒙工程中引入过这个库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-maps 文档](/zh-cn/react-native-maps.md)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-map-clustering Releases](https://github.com/react-native-oh-library/react-native-map-clustering/releases)


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


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


## 遗留问题
- [ ] 不支持属性clusterColor [issue#1](https://github.com/react-native-oh-library/react-native-map-clustering/issues/1)
- [ ] 不支持属性clusterTextColor [issue#2](https://github.com/react-native-oh-library/react-native-map-clustering/issues/2)
- [ ] 不支持属性clusterFontFamily [issue#3](https://github.com/react-native-oh-library/react-native-map-clustering/issues/3)
- [ ] 不支持属性tracksViewChanges [issue#4](https://github.com/react-native-oh-library/react-native-map-clustering/issues/4)
- [ ] 不支持属性renderCluster [issue#5](https://github.com/react-native-oh-library/react-native-map-clustering/issues/5)

## 其他
- height属性暂不支持，与iOS表现一致。[issue#273](https://github.com/venits/react-native-map-clustering/issues/273)
- maxZoom属性暂不支持，与iOS表现一致。[issue#274](https://github.com/venits/react-native-map-clustering/issues/274)
- edgePadding属性暂不支持，与iOS表现一致。[issue#221](https://github.com/venits/react-native-map-clustering/issues/221)
- spiralEnabled属性暂不支持，与iOS表现一致。[issue#275](https://github.com/venits/react-native-map-clustering/issues/275)
- spiderLineColor属性暂不支持，与iOS表现一致。[issue#276](https://github.com/venits/react-native-map-clustering/issues/276)

## 开源协议

本项目基于 [The MIT License (MIT)](https://mit-license.org/) ，请自由地享受和参与开源。
