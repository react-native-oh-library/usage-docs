<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-maps</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-maps/react-native-maps">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-maps/react-native-maps/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-maps)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-maps Releases](https://github.com/react-native-oh-library/react-native-maps/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-maps@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-maps@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { StyleSheet, View, Text, Dimensions } from "react-native";
import MapView, { Circle, Polygon, Polyline, Marker } from "react-native-maps";

const { width, height } = Dimensions.get("window");

const ASPECT_RATIO = width / height;
const LATITUDE = 39.9;
const LONGITUDE = 116.4;
const LATITUDE_DELTA = 0.0922;
const LONGITUDE_DELTA = LATITUDE_DELTA * ASPECT_RATIO;
const SPACE = 0.01;

class Overlays extends React.Component<any, any> {
  constructor(props: any) {
    super(props);

    this.state = {
      marker1: true,
      region: {
        latitude: LATITUDE,
        longitude: LONGITUDE,
        latitudeDelta: LATITUDE_DELTA,
        longitudeDelta: LONGITUDE_DELTA,
      },
      circle: {
        center: {
          latitude: LATITUDE + SPACE,
          longitude: LONGITUDE + SPACE,
        },
        radius: 700,
      },
      polygon: [
        {
          latitude: LATITUDE + SPACE,
          longitude: LONGITUDE + SPACE,
        },
        {
          latitude: LATITUDE - SPACE,
          longitude: LONGITUDE - SPACE,
        },
        {
          latitude: LATITUDE - SPACE,
          longitude: LONGITUDE + SPACE,
        },
      ],
      polyline: [
        {
          latitude: LATITUDE + SPACE,
          longitude: LONGITUDE - SPACE,
        },
        {
          latitude: LATITUDE - 2 * SPACE,
          longitude: LONGITUDE + 2 * SPACE,
        },
        {
          latitude: LATITUDE - SPACE,
          longitude: LONGITUDE - SPACE,
        },
        {
          latitude: LATITUDE - 2 * SPACE,
          longitude: LONGITUDE - SPACE,
        },
      ],
    };
  }

  render() {
    const { region, circle, polygon, polyline } = this.state;
    return (
      <View style={styles.container}>
        <MapView
          provider={this.props.provider}
          style={styles.map}
          initialRegion={region}
        >
          <Marker
            onPress={() => this.setState({ marker1: !this.state.marker1 })}
            coordinate={{
              latitude: LATITUDE + SPACE,
              longitude: LONGITUDE - SPACE,
            }}
            centerOffset={{ x: -42, y: -60 }}
            anchor={{ x: 0.84, y: 1 }}
            opacity={0.6}
          />
          <Circle
            center={circle.center}
            radius={circle.radius}
            fillColor="rgba(255, 255, 255, 1)"
            strokeColor="rgba(0,0,0, 1)"
            zIndex={2}
            strokeWidth={10}
          />
          <Polygon
            coordinates={polygon}
            fillColor="rgba(0, 200, 0, 1)"
            strokeColor="rgba(0,0,0, 1)"
            strokeWidth={10}
          />
          <Polyline
            coordinates={polyline}
            strokeColor="rgba(0,0,200, 1)"
            strokeWidth={10}
            lineDashPattern={[5, 2, 3, 2]}
          />
        </MapView>
        <View style={styles.buttonContainer}>
          <View style={styles.bubble}>
            <Text>Render circles, polygons, and polylines</Text>
          </View>
        </View>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    ...StyleSheet.absoluteFillObject,
    justifyContent: "flex-end",
    alignItems: "center",
  },
  map: {
    ...StyleSheet.absoluteFillObject,
  },
  bubble: {
    flex: 1,
    backgroundColor: "rgba(255,255,255,0.7)",
    paddingHorizontal: 18,
    paddingVertical: 12,
    borderRadius: 20,
  },
  latlng: {
    width: 200,
    alignItems: "stretch",
  },
  button: {
    width: 80,
    paddingHorizontal: 12,
    alignItems: "center",
    marginHorizontal: 10,
  },
  buttonContainer: {
    flexDirection: "row",
    marginVertical: 20,
    backgroundColor: "transparent",
  },
});
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-maps": "file:../../node_modules/@react-native-oh-tpl/react-native-maps/harmony/maps.har"
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

### 配置 CMakeLists 和引入 MapsPackge

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-maps/src/main/cpp" ./maps)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_maps)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "MapsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<MapsPackage>(ctx)
    };
}
```


### 在 ArkTs 侧引入 AIRMap 等组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import { AIRMap, AIR_MAP_TYPE, AIRMapMarker, AIR_MAP_MARKER_TYPE, AIRMapPolyline, AIR_MAP_POLYLINE_TYPE, AIRMapPolygon,
+  AIR_MAP_POLYGON_TYPE, AIRMapCircle, AIR_MAP_CIRCLE_TYPE, AIR_MAP_CALLOUT_SUBVIEW_TYPE, AIR_MAP_CALLOUT_TYPE,
+  AIRMapCallout,
+  AIRMapCalloutSubview,
+  Geojson,
+  AIR_GEOJSON_TYPE,
+  AIRMapUrlTile,
+  AIR_URLTILE_TYPE,
+  AIRMapWMSTile,
+  AIR_WMSTILE_TYPE,
+  AIR_OVERLAY_TYPE,
+  AIRMapOverlay
+ } from "@react-native-oh-tpl/react-native-maps"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
...
+  if (ctx.componentName === AIR_MAP_TYPE) {
+    AIRMap({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }else if (ctx.componentName === AIR_MAP_MARKER_TYPE) {
+    AIRMapMarker({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }else if (ctx.componentName === AIR_MAP_POLYLINE_TYPE) {
+    AIRMapPolyline({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }else if (ctx.componentName === AIR_MAP_POLYGON_TYPE) {
+    AIRMapPolygon({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }else if (ctx.componentName === AIR_MAP_CIRCLE_TYPE) {
+    AIRMapCircle({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }else if (ctx.componentName === AIR_MAP_CALLOUT_TYPE) {
+    AIRMapCallout({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }else if (ctx.componentName === AIR_MAP_CALLOUT_SUBVIEW_TYPE) {
+    AIRMapCalloutSubview({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }else if (ctx.componentName === AIR_MAP_CALLOUT_SUBVIEW_TYPE) {
+    AIRMapCalloutSubview({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }else if (ctx.componentName === AIR_GEOJSON_TYPE) {
+    Geojson({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }else if (ctx.componentName === AIR_URLTILE_TYPE) {
+    AIRMapUrlTile({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }else if (ctx.componentName === AIR_WMSTILE_TYPE) {
+    AIRMapWMSTile({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }else if (ctx.componentName === AIR_OVERLAY_TYPE) {
+    AIRMapOverlay({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag,
+    })
+  }
...
}
...
```
[!TIP] 本库使用了混合方案，需要添加组件名。

在entry/src/main/ets/pages/index.ets 或 entry/src/main/ets/rn/LoadBundle.ets 找到常量 arkTsComponentNames 在其数组里添加组件名
```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ AIR_MAP_TYPE, 
+ AIR_MAP_MARKER_TYPE, 
+ AIR_MAP_POLYLINE_TYPE, 
+ AIR_MAP_POLYGON_TYPE, 
+ AIR_MAP_CIRCLE_TYPE, 
+ AIR_MAP_CALLOUT_TYPE, 
+ AIR_GEOJSON_TYPE, 
+ AIR_URLTILE_TYPE, 
+ AIR_WMSTILE_TYPE, 
+ AIR_OVERLAY_TYPE
  ];
```

### 在 ArkTs 侧引入 MapsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {MapsPackage} from '@react-native-oh-tpl/react-native-maps/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new MapsPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[react-natvie-maps Releases](https://github.com/react-native-oh-library/react-natvie-maps/releases)

本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;

### 权限要求

> [!tip] 如需自建项目使用华为地图可以跳过以下第一步，并前往[华为开发者联盟](https://developer.huawei.com/consumer/cn/wiki/index.php)平台申请对应项目和应用程序

> [!tip] 详细配置参考华为开发者官网[地图服务](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides/appgallery-connect-0000001751989088)

以下是示例项目配置

1.打开 `工程目录/AppScope/app.json5`,修改

```
 bundleName:"com.example.rnmapdemo" //自建项目请与开发者平台上的包名一致
```

2.打开 `entry/src/main/module.json5`，添加相关配置

```
"metadata": [ // 配置如下信息 测试地图功能
    {
        "name": "client_id",
        "value": "110168601"  //配置为从华为开发者平台获取的Client ID，自建项目请与开发者平台上的client id一致
    }
 ],
"requestPermissions": [
      {
        "name": "ohos.permission.APPROXIMATELY_LOCATION",
        "usedScene": {
          "abilities": [
            "EntryAbility"
          ],
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.LOCATION",
        "usedScene": {
          "abilities": [
            "EntryAbility"
          ],
          "when": "always"
        }
      },
      {
        "name": "ohos.permission.INTERNET",
        "usedScene": {
          "abilities": [
            "EntryAbility"
          ],
          "when": "always"
        }
      }
    ]
```

3.打开 `工程目录/build-profile.json5` 在 app 节点下修改

```
 signingConfigs: [
    {
      "name": "default",
      "type": "HarmonyOS",
      "material": {
        "storePassword": "0000001F46D5FEE280574FA23000DE66587FD7FA83EEFEF6D5890B713F4B512621FD3A4F5F6965E94C20441708BCE7", //自建项目配置的指纹证书密码
        "certpath": "E:/aboutKey/rnmapdemo.cer", //自建项目配置的指纹证书
        "keyAlias": "key0",
        "keyPassword": "0000001F2B30EA30206AEBA445E5E69F5A42C4FA4F829039AEBEA0167FF3591ADCAED98732BE405314206771508E5C", //自建项目配置的指纹证书密码
        "profile": "E:/aboutKey/rnmapDebug.p7b",  //自建项目配置的指纹证书
        "signAlg": "SHA256withECDSA",
        "storeFile": "E:/aboutKey/rnmapdemo.p12" //自建项目配置的指纹证书
      }
    }
  ]
```

## MapView

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name                            | Description                                                                                                                                                                                                                                                                                      | Type                                    | Default    | Required | Platform    | HarmonyOS Support |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------------------------- | ---------- | -------- | ----------- | ----------------- |
| provider                        | The map framework to use. Either `"google"` for GoogleMaps, otherwise `null` or `undefined` to use the native map framework (`MapKit` in iOS and `GoogleMaps` in android).                                                                                                                       | string                                  |            | no       | ios/android | no                |
| region                          | The region to be displayed by the map.The region is defined by the center coordinates and the span of coordinates to display.                                                                                                                                                                    | Region                                  |            | no       | ios/android | yes               |
| initialRegion                   | The initial region to be displayed by the map. Use this prop instead of `region` only if you don't want to control the viewport of the map besides the initial region.                                                                                                                           | Region                                  |            | no       | ios/android | yes               |
| camera                          | The camera view the map should display. If you use this, the `region` property is ignored.                                                                                                                                                                                                       | Camera                                  |            | no       | ios/android | yes               |
| initialCamera                   | Like `initialRegion`, use this prop instead of `camera` only if you don't want to control the viewport of the map besides the initial camera setting.                                                                                                                                            | Camera                                  |            | no       | ios/android | yes               |
| mapPadding                      | Adds custom padding to each side of the map. Useful when map elements/markers are obscured.                                                                                                                                                                                                      | EdgePadding                             |            | no       | ios/android | yes               |
| paddingAdjustmentBehavior       | Indicates how/when to affect padding with safe area insets (`GoogleMaps` in iOS only)                                                                                                                                                                                                            | 'always' \ 'automatic' \ 'never'        | 'never'    | no       | ios/android | no                |
| liteMode                        | Enable [lite mode](https://developers.google.com/maps/documentation/android-sdk/lite#overview_of_lite_mode). **Note**: Android only.                                                                                                                                                             | Boolean                                 | false      | no       | android     | no                |
| mapType                         | The map type to be displayed.                                                                                                                                                                                                                                                                    | String                                  | "standard" |          | ios/android | partially         |
| customMapStyle                  | Adds custom styling to the map component.                                                                                                                                                                                                                                                        | Array                                   |            | no       | ios/android | no                |
| userInterfaceStyle              | Sets the map to the style selected. Default is whatever the system settings is. **Note:** iOS Maps only (aka MapKit).                                                                                                                                                                            | 'light'/'dark'                          |            | no       | ios/android | no                |
| showsUserLocation               | If `true` the users location will be shown on the map. **NOTE**: You need runtime location permissions prior to setting this to true, otherwise it is going to _fail silently_! Checkout the excellent [react-native-permissions](https://github.com/zoontek/react-native-permissions) for this. | Boolean                                 | false      | no       | ios/android | yes               |
| userLocationPriority            | Set power priority of user location tracking. See [Google APIs documentation](https://developers.google.com/android/reference/com/google/android/gms/location/LocationRequest.html). **Note:** Android only.                                                                                     | 'balanced' / 'high' / 'low' / 'passive' | 'high'     | no       | android     | no                |
| userLocationUpdateInterval      | Interval of user location updates in milliseconds. See [Google APIs documentation](https://developers.google.com/android/reference/com/google/android/gms/location/LocationRequest.html). **Note:** Android only.                                                                                | Number                                  | 5000       | no       | android     | no                |
| userLocationFastestInterval     | Fastest interval the application will actively acquire locations. See [Google APIs documentation](https://developers.google.com/android/reference/com/google/android/gms/location/LocationRequest.html). **Note:** Android only.                                                                 | Number                                  | 5000       | no       | android     | no                |
| userLocationAnnotationTitle     | The title of the annotation for current user location. This only works if `showsUserLocation` is true. There is a default value `My Location` set by MapView. **Note**: iOS only.                                                                                                                | String                                  |            | no       | ios         | no                |
| followsUserLocation             | If `true` the map will focus on the user's location. This only works if `showsUserLocation` is true and the user has shared their location. **Note**: Apple Maps only.                                                                                                                           | Boolean                                 | false      | no       | ios         | no                |
| userLocationCalloutEnabled      | If `true` clicking user location will show the default callout for userLocation annotation. **Note**: Apple Maps only.                                                                                                                                                                           | Boolean                                 | false      | no       | ios         | no                |
| showsMyLocationButton           | If `false` hide the button to move map to the current user's location.                                                                                                                                                                                                                           | Boolean                                 | true       | no       | ios/android | yes               |
| showsPointsOfInterest           | If `false` points of interest won't be displayed on the map. **Note**: Apple Maps only.                                                                                                                                                                                                          | Boolean                                 | true       | no       | ios         | no                |
| showsCompass                    | If `false` compass won't be displayed on the map.                                                                                                                                                                                                                                                | Boolean                                 | true       | no       | ios/android | yes               |
| showsScale                      | A Boolean indicating whether the map shows scale information. **Note**: Apple Maps only.                                                                                                                                                                                                         | Boolean                                 | true       | no       | ios         | no                |
| showsBuildings                  | A Boolean indicating whether the map displays extruded building information.                                                                                                                                                                                                                     | Boolean                                 | true       | no       | ios/android | no                |
| showsTraffic                    | A Boolean value indicating whether the map displays traffic information.                                                                                                                                                                                                                         | Boolean                                 | false      | no       | ios/android | no                |
| showsIndoors                    | A Boolean indicating whether indoor maps should be enabled.                                                                                                                                                                                                                                      | Boolean                                 | true       | no       | ios/android | no                |
| showsIndoorLevelPicker          | A Boolean indicating whether indoor level picker should be enabled. **Note:** Google Maps only (either Android or iOS with `PROVIDER_GOOGLE`).                                                                                                                                                   | Boolean                                 | false      | no       | ios/android | no                |
| zoomEnabled                     | If `false` the user won't be able to pinch/zoom the map.                                                                                                                                                                                                                                         | Boolean                                 | true       | no       | ios/android | yes               |
| zoomTapEnabled                  | If `false` the user won't be able to double tap to zoom the map. **Note:** But it will greatly decrease delay of tap gesture recognition. **Note:** Google Maps on iOS only                                                                                                                      | Boolean                                 |            | no       | ios/android | yes               |
| zoomControlEnabled              | If `false` the zoom control at the bottom right of the map won't be visible **Note:** Android only.                                                                                                                                                                                              | Boolean                                 | true       | no       | android     | yes               |
| minZoomLevel                    | Minimum zoom value for the map, must be between 0 and 20. **Note:** Deprecated on Apple Maps. Use cameraZoomRange instead.                                                                                                                                                                       | Number                                  | 0          | no       | ios/android | yes               |
| maxZoomLevel                    | Maximum zoom value for the map, must be between 0 and 20. **Note:** Deprecated on Apple Maps. Use cameraZoomRange instead.                                                                                                                                                                       | Number                                  | 20         | no       | ios/android | yes               |
| rotateEnabled                   | If `false` the user won't be able to pinch/rotate the map.                                                                                                                                                                                                                                       | Boolean                                 | true       | no       | ios/android | yes               |
| scrollEnabled                   | If `false` the user won't be able to adjust the camera’s pitch angle.                                                                                                                                                                                                                            | Boolean                                 | true       | no       | ios/android | yes               |
| scrollDuringRotateOrZoomEnabled | If `false` the map will stay centered while rotating or zooming. **Note:** Google Maps only                                                                                                                                                                                                      | Boolean                                 | true       | no       | ios/android | no                |
| pitchEnabled                    | If `false` the user won't be able to adjust the camera’s pitch angle.                                                                                                                                                                                                                            | Boolean                                 | true       | no       | ios/android | no                |
| toolbarEnabled                  | `Android only` If `false` will hide 'Navigate' and 'Open in Maps' buttons on marker press. If you enable the toolbar, make sure to [edit your AndroidManifest.xml](https://github.com/react-native-maps/react-native-maps/issues/4403#issuecomment-1219856534)                                   | Boolean                                 | true       | no       | android     | no                |
| cacheEnabled                    | If `true` map will be cached and displayed as an image instead of being interactable, for performance usage. **Note:** Apple Maps only                                                                                                                                                           | Boolean                                 | false      | no       | ios         | no                |
| loadingEnabled                  | If `true` a loading indicator will show while the map is loading.                                                                                                                                                                                                                                | Boolean                                 | false      | no       | ios/android | no                |
| loadingIndicatorColor           | Sets loading indicator color, default to `#606060`.                                                                                                                                                                                                                                              | Color                                   | \#606060   | no       | ios/android | no                |
| loadingBackgroundColor          | Sets loading background color, default to `#FFFFFF`.                                                                                                                                                                                                                                             | Color                                   | \#FFFFFF   | no       | ios/android | yes               |
| tintColor                       | Sets the tint color of the map. (Changes the color of the position indicator) Defaults to system blue. **Note:** iOS (Apple maps) only.                                                                                                                                                          | Color                                   |            | no       | ios         | no                |
| moveOnMarkerPress               | `Android only` If `false` the map won't move when a marker is pressed.                                                                                                                                                                                                                           | Boolean                                 | true       | no       | android     | no                |
| legalLabelInsets                | If set, changes the position of the "Legal" label link from the OS default. **Note:** iOS only.                                                                                                                                                                                                  | EdgeInsets                              |            | no       | ios         | no                |
| kmlSrc                          | The URL from KML file. **Note:** Google Maps and Markers only (either Android or iOS with `PROVIDER_GOOGLE`).                                                                                                                                                                                    | String                                  |            | no       | ios/android | no                |
| compassOffset                   | If set, changes the position of the compass. **Note:** iOS Maps only.                                                                                                                                                                                                                            | Point                                   |            | no       | ios         | no                |
| isAccessibilityElement          | Determines whether the MapView captures VoiceOver touches or forwards them to children. When `true`, map markers are not visible to VoiceOver. **Note:** iOS Maps only.                                                                                                                          | Boolean                                 | false      | no       | ios         | no                |
| cameraZoomRange                 | Map camera distance limits. `minCenterCoordinateDistance` for minimum distance, `maxCenterCoordinateDistance` for maximum, `animated` for animated zoom range changes. Takes precedence if conflicting with `minZoomLevel`, `maxZoomLevel`. **Note**: iOS 13.0+ only.                            | cameraZoomRange                         |            | no       | ios         | no                |

注：HarmonyOS 侧的 mapType 支持以下字符串值

'none' \ 'standard' \ 'terrain'

### 静态方法

| Name     | Description | Type     | Required | Platform    | HarmonyOS Support |
| -------- | ----------- | -------- | -------- | ----------- | ----------------- |
| Animated | 动画        | Animated | no       | ios/android | no                |

### API

| Name                      | Description                                                                                                                                                       | Arguments                                                                            | Platform    | HarmonyOS Support |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | ----------- | ----------------- |
| getCamera                 | Returns a `Promise<Camera>` structure indicating the current camera configuration.                                                                                |                                                                                      | ios/android | yes               |
| animateCamera             | Animate the camera to a new view. You can pass a partial camera object here; any property not given will remain unmodified.                                       | camera: Camera`, `{ duration: Number }                                               | ios/android | yes               |
| setCamera                 | Like `animateCamera`, but sets the new view instantly, without an animation.                                                                                      | camera: Camera`, `{ duration: Number }                                               | ios/android | yes               |
| animateToRegion           | Like `animateCamera`                                                                                                                                              | region: Region`, `duration: Number                                                   | ios/android | yes               |
| getMapBoundaries          | Promise<{northEast: LatLng, southWest: LatLng}>                                                                                                                   |                                                                                      | ios/android | yes               |
| setMapBoundaries          | The boundary is defined by the map's center coordinates, not the device's viewport itself. **Note:** Google Maps only.                                            | northEast: LatLng`, `southWest: LatLng                                               | ios/android | yes               |
| setIndoorActiveLevelIndex |                                                                                                                                                                   | levelIndex: Number                                                                   | ios/android | no                |
| fitToElements             | **Note** edgePadding is Google Maps only                                                                                                                          | options: { edgePadding: EdgePadding, animated: Boolean }                             | ios/android | no                |
| fitToSuppliedMarkers      | If you need to use this in `ComponentDidMount`, make sure you put it in a timeout or it will cause performance problems. **Note** edgePadding is Google Maps only | markerIDs: String[], options: { edgePadding: EdgePadding, animated: Boolean }        | ios/android | no                |
| fitToCoordinates          | If called in `ComponentDidMount` in android, it will cause an exception. It is recommended to call it from the MapView `onLayout` event.                          | coordinates: Array<LatLng>, options: { edgePadding: EdgePadding, animated: Boolean } | ios/android | yes               |
| addressForCoordinate      | Converts a map coordinate to a address (`Address`). Returns a `Promise<Address>` **Note** Not supported on Google Maps for iOS.                                   | coordinate: LatLng                                                                   | ios/android | yes               |
| pointForCoordinate        | Converts a map coordinate to a view coordinate (`Point`). Returns a `Promise<Point>`.                                                                             | coordinate: LatLng                                                                   | ios/android | yes               |
| coordinateForPoint        | Converts a view coordinate (`Point`) to a map coordinate. Returns a `Promise<Coordinate>`.                                                                        | point: Point                                                                         | ios/android | yes               |
| getMarkersFrames          | Get markers' centers and frames in view coordinates. Returns a `Promise<{ "markerID" : { point: Point, frame: Frame } }>`. **Note**: iOS only.                    | onlyVisible: Boolean                                                                 | ios         | no                |
| takeSnapshot              | Takes a snapshot of the map and saves it to a picture file or returns the image as a base64 encoded string.                                                       | SnapshotOptions                                                                      | ios/android | yes               |

## Marker

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name                    | Description                                                                                                                                                                                                                                                                                                                                                              | Type            | Default  | Required | Platform    | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------- | -------- | -------- | ----------- | ----------------- |
| title                   | The title of the marker. This is only used if the component has no children that are a `<Callout />`, in which case the default callout behavior will be used, which will show both the `title` and the `description`, if provided.                                                                                                                                      | String          |          | no       | ios/android | yes               |
| description             | The description of the marker. This is only used if the component has no children that are a `<Callout />`, in which case the default callout behavior will be used, which will show both the `title` and the `description`, if provided.                                                                                                                                | String          |          | no       | ios/android | yes               |
| image                   | A custom image to be used as the marker's icon. Only local image resources are allowed to be used.                                                                                                                                                                                                                                                                       | `ImageSource`\* |          | no       | ios/android | yes               |
| icon                    | Marker icon to render (equivalent to `icon` property of GMSMarker Class). Only local image resources are allowed to be used. **Note:** Google maps only!                                                                                                                                                                                                                 | `ImageSource`\* |          | no       | ios/android | yes               |
| pinColor                | If no custom marker view or custom image is provided, the platform default pin will be used, which can be customized by this color. Ignored if a custom marker is being used.                                                                                                                                                                                            | Color           |          | no       | ios/android | no                |
| coordinate              | The coordinate for the marker.                                                                                                                                                                                                                                                                                                                                           | LatLng          |          | no       | ios/android | yes               |
| centerOffset            | The offset (in points) at which to display the view.                                                                                                                                                                                                                                                                                                                     | Point           | (0, 0)   | no       | ios/android | no                |
| calloutOffset           | The offset (in points) at which to place the callout bubble.                                                                                                                                                                                                                                                                                                             | Point           | (0, 0)   | no       | ios/android | no                |
| anchor                  | Sets the anchor point for the marker.                                                                                                                                                                                                                                                                                                                                    | Point           | (0.5, 1) | no       | ios/android | yes               |
| calloutAnchor           | Specifies the point in the marker image at which to anchor the callout when it is displayed. This is specified in the same coordinate system as the anchor. See the `anchor` prop for more details.                                                                                                                                                                      | Point           | (0.5, 0) | no       | ios/android | yes               |
| flat                    | Sets whether this marker should be flat against the map true or a billboard facing the camera.                                                                                                                                                                                                                                                                           | Boolean         | false    | no       | ios/android | yes               |
| identifier              | An identifier used to reference this marker at a later date.                                                                                                                                                                                                                                                                                                             | String          |          | no       | ios/android | no                |
| rotation                | A float number indicating marker's rotation angle, in degrees.                                                                                                                                                                                                                                                                                                           | Float           | 0        | no       | ios/android | yes               |
| draggable               | This is a non-value based prop. Adding this allows the marker to be draggable (re-positioned).                                                                                                                                                                                                                                                                           | <null>          |          | no       | ios/android | yes               |
| tappable                | Sets whether marker should be tappable. If set to false, the marker will not have onPress events. **Note**: iOS Google Maps only.                                                                                                                                                                                                                                        | Boolean         | true     | no       | ios/android | yes               |
| tracksViewChanges       | Sets whether this marker should track changes to child views. When using a child view to create a custom marker this option determines if changes to the content will be tracked after the first render pass. This option has a performance impact so when possible it's recommended to disable it and explictly call the `redraw` method if the marker content changes. | Boolean         | true     | no       | ios/android | no                |
| tracksInfoWindowChanges | Sets whether this marker should track view changes in info window. Enabling it will let marker change content of info window after first render pass, but will lead to decreased performance, so it's recommended to disable it whenever you don't need it. **Note**: iOS Google Maps only.                                                                              | Boolean         | false    | no       | ios/android | no                |
| stopPropagation         | Sets whether this marker should propagate `onPress` events. Enabling it will stop the parent `MapView`'s `onPress` from being called. **Note**: iOS only. Android does not propagate `onPress` events. See [#1132](https://github.com/react-community/react-native-maps/issues/1132) for more information.                                                               | Boolean         | false    | no       | ios/android | no                |
| opacity                 | The marker's opacity between 0.0 and 1.0.                                                                                                                                                                                                                                                                                                                                | Float           | 1.0      | no       | ios/android | yes               |
| isPreselected           | When true, the marker will be pre-selected. Setting this to true allows the user to drag the marker without needing to tap on it once to focus on it. **Note**: iOS Apple Maps only.                                                                                                                                                                                     | Boolean         | false    | no       | ios         | no                |
| key                     | If no key or non-unique `key` is specified, the `<Marker />` will be reused, therefore there is an animation when the position is changed. If you want to disable the animation, add a `key` prop with a unique value like `key_${item.longitude}_${item.latitude}`. **Note**: iOS only.                                                                                 |                 |          | no       | ios         | no                |

### 静态方法

| Name     | Description | Type     | Required | Platform    | HarmonyOS Support |
| -------- | ----------- | -------- | -------- | ----------- | ----------------- |
| Animated | 动画        | Animated | no       | ios/android | no                |

### API

| Name                      | Description                                                                                                                            | Arguments | Platform    | HarmonyOS Support |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | --------- | ----------- | ----------------- |
| showCallout               | Shows the callout for this marker                                                                                                      |           | ios/android | yes               |
| hideCallout               | Hides the callout for this marker                                                                                                      |           | ios/android | yes               |
| redrawCallout             | Causes a redraw of the marker's callout. Useful for Google Maps on iOS. **Note**: iOS only.                                            |           | ios         | no                |
| animateMarkerToCoordinate | Animates marker movement. **Note**: Android only                                                                                       |           | android     | no                |
| redraw                    | Causes a redraw of the marker. Useful when there are updates to the marker and `tracksViewChanges` comes with a cost that is too high. |           | ios/android | yes               |

## Polyline

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Type          | Default               | Required | Platform    | HarmonyOS Support |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | --------------------- | -------- | ----------- | ----------------- |
| coordinates     | An array of coordinates to describe the polyline                                                                                                                                                                                                                                                                                                                                                                                                                                  | Array<LatLng> |                       | yes      | ios/android | yes               |
| strokeWidth     | The stroke width to use for the path.                                                                                                                                                                                                                                                                                                                                                                                                                                             | Number        | 1                     | no       | ios/android | yes               |
| strokeColor     | The stroke color to use for the path.                                                                                                                                                                                                                                                                                                                                                                                                                                             | String        | #000, rgba(r,g,b,0.5) | no       | ios/android | yes               |
| strokeColors    | The stroke colors to use for the path (iOS only). Must be the same length as `coordinates`.                                                                                                                                                                                                                                                                                                                                                                                       | Array<String> |                       | no       | ios/android | yes               |
| lineCap         | The line cap style to apply to the open ends of the path. Possible values are `butt`, `round` or `square`. Note: lineCap is not yet supported for GoogleMaps provider on iOS.                                                                                                                                                                                                                                                                                                     | String        | round                 | no       | ios/android | yes               |
| lineJoin        | The line join style to apply to corners of the path. Possible values are `miter`, `round` or `bevel`.                                                                                                                                                                                                                                                                                                                                                                             | String        | round                 | no       | ios/android | partially         |
| miterLimit      | The limiting value that helps avoid spikes at junctions between connected line segments. The miter limit helps you avoid spikes in paths that use the `miter` `lineJoin` style. If the ratio of the miter length—that is, the diagonal length of the miter join—to the line thickness exceeds the miter limit, the joint is converted to a bevel join. The default miter limit is 10, which results in the conversion of miters whose angle at the joint is less than 11 degrees. | Number        |                       | no       | ios/android | no                |
| geodesic        | Boolean to indicate whether to draw each segment of the line as a geodesic as opposed to straight lines on the Mercator projection. A geodesic is the shortest path between two points on the Earth's surface. The geodesic curve is constructed assuming the Earth is a sphere.                                                                                                                                                                                                  | Boolean       |                       | no       | ios/android | yes               |
| lineDashPhase   | (iOS only) The offset (in points) at which to start drawing the dash pattern. Use this property to start drawing a dashed line partway through a segment or gap. For example, a phase value of 6 for the patter 5-2-3-2 would cause drawing to begin in the middle of the first gap.                                                                                                                                                                                              | Number        | 0                     | no       | ios/android | no                |
| lineDashPattern | An array of numbers specifying the dash pattern to use for the path. The array contains one or more numbers that indicate the lengths (measured in points) of the line segments and gaps in the pattern. The values in the array alternate, starting with the first line segment length, followed by the first gap length, followed by the second line segment length, and so on.                                                                                                 | Array<Number> |                       | no       | ios/android | yes               |
| tappable        | Boolean to allow a polyline to be tappable and use the onPress function.                                                                                                                                                                                                                                                                                                                                                                                                          | Bool          |                       | no       | ios/android | yes               |

注：HarmonyOS 侧的 lineJoin 支持以下字符串值

'default' \ 'bevel' \ 'round'

## Polygon

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Type                 | Default                 | Required | Platform    | HarmonyOS Support |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | ----------------------- | -------- | ----------- | ----------------- |
| coordinates     | An array of coordinates to describe the polygon                                                                                                                                                                                                                                                                                                                                                                                                                                   | Array<LatLng>        |                         | yes      | ios/android | yes               |
| holes           | A 2d array of coordinates to describe holes of the polygon where each hole has at least 3 points.                                                                                                                                                                                                                                                                                                                                                                                 | Array<Array<LatLng>> |                         | no       | ios/android | yes               |
| strokeWidth     | The stroke width to use for the path.                                                                                                                                                                                                                                                                                                                                                                                                                                             | Number               | 1                       | no       | ios/android | yes               |
| strokeColor     | The stroke color to use for the path.                                                                                                                                                                                                                                                                                                                                                                                                                                             | String               | #000`, `rgba(r,g,b,0.5) | no       | ios/android | yes               |
| fillColor       | The fill color to use for the path.                                                                                                                                                                                                                                                                                                                                                                                                                                               | String               | #000`, `rgba(r,g,b,0.5) | no       | ios/android | yes               |
| lineCap         | The line cap style to apply to the open ends of the path. Possible values are `butt`, `round` or `square`. Note: lineCap is not yet supported for GoogleMaps provider on iOS.                                                                                                                                                                                                                                                                                                     | String               | round                   | no       | ios/android | no                |
| lineJoin        | The line join style to apply to corners of the path. Possible values are `miter`, `round` or `bevel`.                                                                                                                                                                                                                                                                                                                                                                             | String               | round                   | no       | ios/android | partially         |
| miterLimit      | The limiting value that helps avoid spikes at junctions between connected line segments. The miter limit helps you avoid spikes in paths that use the `miter` `lineJoin` style. If the ratio of the miter length—that is, the diagonal length of the miter join—to the line thickness exceeds the miter limit, the joint is converted to a bevel join. The default miter limit is 10, which results in the conversion of miters whose angle at the joint is less than 11 degrees. | Number               |                         | no       | ios/android | no                |
| geodesic        | Boolean to indicate whether to draw each segment of the line as a geodesic as opposed to straight lines on the Mercator projection. A geodesic is the shortest path between two points on the Earth's surface. The geodesic curve is constructed assuming the Earth is a sphere.                                                                                                                                                                                                  | Boolean              |                         | no       | ios/android | yes               |
| lineDashPhase   | (iOS only) The offset (in points) at which to start drawing the dash pattern. Use this property to start drawing a dashed line partway through a segment or gap. For example, a phase value of 6 for the patter 5-2-3-2 would cause drawing to begin in the middle of the first gap.                                                                                                                                                                                              | Number               | 0                       | no       | ios/android | no                |
| lineDashPattern | (iOS only) An array of numbers specifying the dash pattern to use for the path. The array contains one or more numbers that indicate the lengths (measured in points) of the line segments and gaps in the pattern. The values in the array alternate, starting with the first line segment length, followed by the first gap length, followed by the second line segment length, and so on.                                                                                      | Array<Number>        |                         | no       | ios/android | yes               |
| tappable        | Boolean to allow a polygon to be tappable and use the onPress function.                                                                                                                                                                                                                                                                                                                                                                                                           | Bool                 | false                   | no       | ios/android | yes               |
| zIndex          | (Android Only) The order in which this polygon overlay is drawn with respect to other overlays. An overlay with a larger z-index is drawn over overlays with smaller z-indices. The order of overlays with the same z-index is arbitrary. The default zIndex is 0.                                                                                                                                                                                                                | Number               | 0                       | no       | ios/android | yes               |

注：HarmonyOS 侧的 lineJoin 支持以下字符串值

'default' \ 'bevel' \ 'round'

## Circle

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name            | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Type          | Default                 | Required | Platform    | HarmonyOS Support |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- | ----------------------- | -------- | ----------- | ----------------- |
| center          | The coordinate of the center of the circle                                                                                                                                                                                                                                                                                                                                                                                                                                        | LatLng        |                         | yes      | ios/android | yes               |
| radius          | The radius of the circle to be drawn (in meters)                                                                                                                                                                                                                                                                                                                                                                                                                                  | Number        |                         | yes      | ios/android | yes               |
| strokeWidth     | The stroke width to use for the path.                                                                                                                                                                                                                                                                                                                                                                                                                                             | Number        | 1                       | no       | ios/android | yes               |
| strokeColor     | The stroke color to use for the path.                                                                                                                                                                                                                                                                                                                                                                                                                                             | String        | #000`, `rgba(r,g,b,0.5) | no       | ios/android | yes               |
| fillColor       | The fill color to use for the path.                                                                                                                                                                                                                                                                                                                                                                                                                                               | String        | #000`, `rgba(r,g,b,0.5) | no       | ios/android | yes               |
| zIndex          | The order in which this tile overlay is drawn with respect to other overlays. An overlay with a larger z-index is drawn over overlays with smaller z-indices. The order of overlays with the same z-index is arbitrary. The default zIndex is 0. (Android Only)                                                                                                                                                                                                                   | Number        |                         | no       | ios/android | yes               |
| lineCap         | The line cap style to apply to the open ends of the path. Other values : `butt`, `square`                                                                                                                                                                                                                                                                                                                                                                                         | String        | round                   | no       | ios/android | no                |
| lineJoin        | The line join style to apply to corners of the path. possible value: `miter`, `round`, `bevel`                                                                                                                                                                                                                                                                                                                                                                                    | String        |                         | no       | ios/android | no                |
| miterLimit      | The limiting value that helps avoid spikes at junctions between connected line segments. The miter limit helps you avoid spikes in paths that use the `miter` `lineJoin` style. If the ratio of the miter length—that is, the diagonal length of the miter join—to the line thickness exceeds the miter limit, the joint is converted to a bevel join. The default miter limit is 10, which results in the conversion of miters whose angle at the joint is less than 11 degrees. | Number        |                         | no       | ios/android | no                |
| lineDashPhase   | (iOS only) The offset (in points) at which to start drawing the dash pattern. Use this property to start drawing a dashed line partway through a segment or gap. For example, a phase value of 6 for the patter 5-2-3-2 would cause drawing to begin in the middle of the first gap.                                                                                                                                                                                              | Number        | 0                       | no       | ios/android | no                |
| lineDashPattern | (iOS only) An array of numbers specifying the dash pattern to use for the path. The array contains one or more numbers that indicate the lengths (measured in points) of the line segments and gaps in the pattern. The values in the array alternate, starting with the first line segment length, followed by the first gap length, followed by the second line segment length, and so on.                                                                                      | Array<Number> |                         | no       | ios/android | yes               |

## Overlay

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name     | Description                                                                                                                                      | Type          | Default | Required | Platform    | HarmonyOS Support |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------------- | ------- | -------- | ----------- | ----------------- |
| image    | A custom image to be used as the overlay. Only required local image resources and uri (as for images located in the net) are allowed to be used. | ImageSource   |         | no       | ios/android | no                |
| bounds   | The coordinates for the image (bottom-left corner, top-right corner). ie.`[[lat, long], [lat, long]]`                                            | Array<LatLng> |         | no       | ios/android | no                |
| bearing  | `Google Maps API only` The bearing in degrees clockwise from north. Values outside the range [0, 360) will be normalized.                        | Number        | 0       | no       | ios/android | no                |
| tappable | `Android only` Boolean to allow an overlay to be tappable and use the onPress function.                                                          | Bool          | false   | no       | ios/android | no                |
| opacity  | `Google maps only` The opacity of the overlay.                                                                                                   | Number        | 1.0     | no       | ios/android | no                |

### 静态方法

| Name     | Description | Type     | Required | Platform    | HarmonyOS Support |
| -------- | ----------- | -------- | -------- | ----------- | ----------------- |
| Animated | 动画        | Animated | no       | ios/android | no                |

## UrlTile & WMSTile

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | Type    | Default | Required | Platform    | HarmonyOS Support |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ------- | -------- | ----------- | ----------------- |
| urlTemplate             | The url template of the map tileserver. (URLTile) The patterns {x} {y} {z} will be replaced at runtime. For example, http://c.tile.openstreetmap.org/{z}/{x}/{y}.png. It is also possible to refer to tiles in local filesystem with file:///top-level-directory/sub-directory/{z}/{x}/{y}.png URL-format. (WMSTile) The patterns {minX} {maxX} {minY} {maxY} {width} {height} will be replaced at runtime according to EPSG:900913 specification bounding box. For example, https://demo.geo-solutions.it/geoserver/tiger/wms?service=WMS&version=1.1.0&request=GetMap&layers=tiger:poi&styles=&bbox={minX},{minY},{maxX},{maxY}&width={width}&height={height}&srs=EPSG:900913&format=image/png&transparent=true&format_options=dpi:213. | String  |         | no       | ios/android | no                |
| minimumZ                | The minimum zoom level for this tile overlay.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Number  |         | no       | ios/android | no                |
| maximumZ                | The maximum zoom level for this tile overlay.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Number  |         | no       | ios/android | no                |
| maximumNativeZ          | (Optional) The maximum native zoom level for this tile overlay i.e. the highest zoom level that the tile server provides. Tiles are auto-scaled for higher zoom levels.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | Number  |         | no       | ios/android | no                |
| zIndex                  | (Optional) The order in which this tile overlay is drawn with respect to other overlays. An overlay with a larger z-index is drawn over overlays with smaller z-indices. The order of overlays with the same z-index is arbitrary.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Number  | -1      | no       | ios/android | no                |
| tileSize                | (Optional) Tile size, default size is 256 (for tiles of 256 _ 256 pixels). High-res (aka 'retina') tiles are 512 (tiles of 512 _ 512 pixels).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Number  |         | no       | ios/android | no                |
| doubleTileSize          | (Optional) Doubles tile size from 256 to 512 utilising higher zoom levels i.e loading 4 higher zoom level tiles and combining them for one high-resolution tile. iOS does this automatically, even if it is not desirable always. NB! using this makes text labels smaller than in the original map style.                                                                                                                                                                                                                                                                                                                                                                                                                                | Boolean | false   | no       | ios/android | no                |
| shouldReplaceMapContent | (iOS) Corresponds to MKTileOverlay canReplaceMapContent i.e. if true then underlying iOS basemap is not shown.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Boolean | false   | no       | ios/android | no                |
| flipY                   | (Optional)Allow tiles using the TMS coordinate system (origin bottom left) to be used, and displayed at their correct coordinates.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | Boolean | false   | no       | ios/android | no                |
| tileCachePath           | (Optional) Enable caching of tiles in the specified directory. Directory can be specified either as a normal path or in URL format (`file://`). Tiles are stored in tileCachePath directory as `/{z}/{x}/{y}` i.e. in sub-directories 2-levels deep, filename is tile y-coordinate without any filetype-extension.NB! All cache management needs to be implemented by client e.g. deleting tiles to manage use of storage space etc.                                                                                                                                                                                                                                                                                                      | String  |         | no       | ios/android | no                |
| tileCacheMaxAge         | (Optional) Defines maximum age in seconds for a cached tile before it's refreshed. NB! Refresh logic is "serve-stale-while-refresh" i.e. to ensure map availability a stale (over max age) tile is served while a tile refresh process is started in the background.                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Number  |         | no       | ios/android | no                |
| offlineMode             | (Optional) Sets offline-mode. In offline-mode tiles are not fetched from the tile servers, rather only tiles stored in the cache directory are used. Furthermore automated tile scaling is activated: if tile at a desired zoom level is not found from the cache directory, then lower zoom level tile is used (up to 4 levels lower) and scaled.                                                                                                                                                                                                                                                                                                                                                                                        | Boolean | false   | no       | ios/android | no                |
| opacity                 | (Optional) Map layer opacity. Value between 0 - 1, with 0 meaning fully transparent.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | Number  |         | no       | ios/android | no                |

## Callout

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name         | Description                                                                                                                                                                                     | Type    | Default | Required | Platform    | HarmonyOS Support |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | ------- | -------- | ----------- | ----------------- |
| tooltip      | If `false`, a default "tooltip" bubble window will be drawn around this callouts children. If `true`, the child views can fully customize their appearance, including any "bubble" like styles. | Boolean | false   | no       | ios/android | no                |
| alphaHitTest | If `true`, clicks on transparent areas in callout will be passed to map. **Note**: iOS only.                                                                                                    | Boolean | false   | no       | ios         | no                |

## Geojson

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name              | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | Type                        | Default                                            | Required | Platform    | HarmonyOS Support |
| ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------- | -------------------------------------------------- | -------- | ----------- | ----------------- |
| geojson           | [Geojson](https://geojson.org/) description of object.                                                                                                                                                                                                                                                                                                                                                                                                                            | GeoJSON                     |                                                    | no       | ios/android | yes               |
| strokeColor       | The stroke color to use for polygons and polylines.                                                                                                                                                                                                                                                                                                                                                                                                                               | String                      | stroke`property in GeoJson if present else`#000    | no       | ios/android | yes               |
| fillColor         | The fill color to use for polygons.                                                                                                                                                                                                                                                                                                                                                                                                                                               | String                      | `fill` property in GeoJson                         | no       | ios/android | yes               |
| strokeWidth       | The stroke width to use for polygons and polylines.                                                                                                                                                                                                                                                                                                                                                                                                                               | Number                      | stroke-width`property in Geojson if present else`1 | no       | ios/android | yes               |
| color             | The color to use for points.                                                                                                                                                                                                                                                                                                                                                                                                                                                      | String                      | `marker-color` property in GeoJson                 | no       | ios/android | yes               |
| lineDashPhase     | (iOS only) The offset (in points) at which to start drawing the dash pattern. Use this property to start drawing a dashed line partway through a segment or gap. For example, a phase value of 6 for the patter 5-2-3-2 would cause drawing to begin in the middle of the first gap.                                                                                                                                                                                              | Number                      |                                                    | no       | ios         | no                |
| lineDashPattern   | An array of numbers specifying the dash pattern to use for the path. The array contains one or more numbers that indicate the lengths (measured in points) of the line segments and gaps in the pattern. The values in the array alternate, starting with the first line segment length, followed by the first gap length, followed by the second line segment length, and so on.                                                                                                 | Array<Number>               |                                                    | no       | ios/android | yes               |
| lineCap           | The line cap style to apply to the open ends of the path. Possible values are `butt`, `round` or `square`. Note: lineCap is not yet supported for GoogleMaps provider on iOS.                                                                                                                                                                                                                                                                                                     | 'butt' / 'round' / 'square' |                                                    | no       | ios/android | yes               |
| lineJoin          | The line join style to apply to corners of the path. Possible values are `miter`, `round` or `bevel`.                                                                                                                                                                                                                                                                                                                                                                             | 'miter' / 'round' / 'bevel' |                                                    | no       | ios/android | yes               |
| miterLimit        | The limiting value that helps avoid spikes at junctions between connected line segments. The miter limit helps you avoid spikes in paths that use the `miter` `lineJoin` style. If the ratio of the miter length—that is, the diagonal length of the miter join—to the line thickness exceeds the miter limit, the joint is converted to a bevel join. The default miter limit is 10, which results in the conversion of miters whose angle at the joint is less than 11 degrees. | Number                      |                                                    | no       | ios/android | no                |
| zIndex            | Layer level of the z-index value                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Number                      |                                                    | no       | ios/android | yes               |
| onPress           | returns the selected overlay value with the onPress functionality                                                                                                                                                                                                                                                                                                                                                                                                                 | Function                    |                                                    | no       | ios/android | yes               |
| markerComponent   | Component to render in place of the default marker when the overlay type is a `point`                                                                                                                                                                                                                                                                                                                                                                                             | React Node                  |                                                    | no       | ios/android | no                |
| title             | The title of the marker. This is only used if the component has no children that are a `<Callout />`                                                                                                                                                                                                                                                                                                                                                                              | string                      |                                                    | no       | ios/android | yes               |
| tracksViewChanges | Sets whether this marker should track view changes. It's recommended to turn it off whenever it's possible to improve custom marker performance. This is the default value for all point markers in your geojson data. It can be overriden on a per point basis by adding a `trackViewChanges` property to the `properties` object on the point.                                                                                                                                  | Boolean                     | true                                               | no       | ios/android | no                |

## Heatmap

> **Note**: Supported on Google Maps only.
>
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name     | Description                                                       | Type                  | Default | Required | Platform    | HarmonyOS Support |
| -------- | ----------------------------------------------------------------- | --------------------- | ------- | -------- | ----------- | ----------------- |
| points   | Array of heatmap entries to apply towards density.                | Array<WeightedLatLng> |         | no       | ios/android | no                |
| radius   | The radius of the heatmap points in pixels, between 10 and 50.    | Number                | 20      | no       | ios/android | no                |
| opacity  | The opacity of the heatmap.                                       | Number                | 0.7     | no       | ios/android | no                |
| gradient | Heatmap gradient configuration (See below for _Gradient Config_). | Object                |         | no       | ios/android | no                |

#### Gradient Config

[Android Doc](https://developers.google.com/maps/documentation/android-sdk/utility/heatmap#custom) | [iOS Doc](https://developers.google.com/maps/documentation/ios-sdk/utility/heatmap#customize)

| Name         | Description                                                                                                                           | Type          | Default | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------- | ------------- | ------- | -------- | ----------- | ----------------- |
| colors       | Colors (one or more) to use for gradient.                                                                                             | Array<String> |         | no       | ios/android | no                |
| startPoints  | Array of floating point values from 0 to 1 representing where each color starts. Array length must be equal to `colors` array length. | Array<Number> |         | no       | ios/android | no                |
| colorMapSize | Resolution of color map -- number corresponding to the number of steps colors are interpolated into.                                  | Number        | 256     | no       | ios/android | no                |

## 遗留问题

- [ ] AIRMap 和 AIRMapMarker 中 Animated 未实现 [issues#1](https://github.com/react-native-oh-library/react-native-maps/issues/1)
- [ ] AIRMapOverlay 组件目前华为地图中不支持往地图组件中添加自定义 view [issues#2](https://github.com/react-native-oh-library/react-native-maps/issues/2)
- [ ] AIRMap AIRMapMarker AIRMapPolyline AIRMapPolygon AIRMapCircle 组件在 HarmonyOS 中的不支持属性是因为华为地图没提供对应的属性 [issues#3](https://github.com/react-native-oh-library/react-native-maps/issues/3)
- [ ] AIRMapCallout AIRMapCalloutSubview 组件为 marker 子组件，华为地图中 marker 有自带的，但是目前不支持自定义样式显示 [issues#4](https://github.com/react-native-oh-library/react-native-maps/issues/4)
- [ ] AIRMapUrlTile AIRMapWMSTile 瓦片地图加载方式华为地图不支持 [issues#5](https://github.com/react-native-oh-library/react-native-maps/issues/5)
- [ ] Heatmap 华为地图不支持 [issues#6](https://github.com/react-native-oh-library/react-native-maps/issues/6)

## 开源协议

本项目基于 [MIT License (MIT)](https://github.com/react-native-maps/react-native-maps/blob/master/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->