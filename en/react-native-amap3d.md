> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-amap3d</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/qiuxiang/react-native-amap3d">
        <img src="https://img.shields.io/badge/platforms-android%20|%20iOS%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/qiuxiang/react-native-amap3d/blob/main/license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-amap3d)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-amap3d Releases](https://github.com/react-native-oh-library/react-native-amap3d/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-amap3d
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-amap3d
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import { ScrollView, Text, View,StyleSheet, Alert } from 'react-native';
import {MapView, Circle, Polygon, Polyline, Marker, LatLng,CameraPosition,voidEvent} from 'react-native-amap3d';

import type * as ReactNative from "react-native";

const points = [
  {
    latitude: 39.806901,
    longitude: 116.397972,
  },
  {
    latitude: 39.806901,
    longitude: 116.297972,
  },
  {
    latitude: 39.906901,
    longitude: 116.397972,
  },
];

const points2 = [
  {
    latitude: 39.836901,
    longitude: 116.497972,
  },
  {
    latitude: 39.836901,
    longitude: 116.397972,
  },
  {
    latitude: 39.936901,
    longitude: 116.497972,
  },
];

const line1 = [
  { latitude: 40.006901, longitude: 116.097972 },
  { latitude: 40.006901, longitude: 116.597972 },
];
const line3 = [
  { latitude: 39.806901, longitude: 116.097972 },
  { latitude: 39.806901, longitude: 116.257972 },
  { latitude: 39.806901, longitude: 116.457972 },
  { latitude: 39.806901, longitude: 116.597972 },
];

function AMapDemo() {
  return (
    <View style={styles.container}>
		<MapView 
    mapType={1}
    myLocationEnabled = {true}
    onPress={(event: ReactNative.NativeSyntheticEvent<LatLng>)=>{
      console.info("AMapViewEventType map3d demo " + event.nativeEvent.latitude + "===" + event.nativeEvent.longitude)
    }}
    onLongPress={(event: ReactNative.NativeSyntheticEvent<LatLng>)=>{
      console.info("AMapViewEventType map3d demo longevent===" + event.nativeEvent.latitude + "===" + event.nativeEvent.longitude)
    }}
    onLoad={(event: ReactNative.NativeSyntheticEvent<voidEvent>) => {
      Alert.alert("onLoad successful")
    }}
    > 
    <Circle
      strokeWidth={5}
      strokeColor="rgba(0, 0, 255, 0.5)"
      fillColor="rgba(255, 0, 0, 0.5)"
      radius={500}
      center={{ latitude: 39.906901, longitude: 116.397972 }}
    />
    <Polygon
      strokeWidth={5}
      strokeColor="rgba(0, 0, 255, 0.5)"
      fillColor="rgba(255, 0, 0, 0.5)"
      points={points}
    />
    <Polyline width={100}  color="rgba(0, 255, 0, 0.5)" points={line1} onPress={() => { console.info("AMapViewEventType map3d polyline onPress width 200")}} />
    <Marker
      draggable={true}
      position={{ latitude: 39.806901, longitude: 116.397972 }}
      onPress={() => Alert.alert("onPress")}
      onDragEnd={({ nativeEvent }) =>
        Alert.alert(`onDragEnd: ${nativeEvent.latitude}, ${nativeEvent.longitude}`)}
    />
    </MapView>
	</View>
  );
};

const styles = StyleSheet.create({
  container: {
    backgroundColor: '#fff',
    flex: 1,
    paddingTop: 24,
  }
});
export default AMapDemo;
```

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
    "@react-native-oh-tpl/react-native-amap3d": "file:../../node_modules/@react-native-oh-tpl/react-native-amap3d/harmony/rn_amap3d.har"
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

### 3. Configuring CMakeLists and Introducing MapViewPackge

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-amap3d/src/main/cpp" ./rn_amap3d)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_amap3d)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "MapViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<MapViewPackage>(ctx)
    };
}
```


### 4. Introducing react-native-amap3d Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
...
+ import {
+  A_MAP_CIRCLE_VIEW_TYPE,
+  A_MAP_MARKER_TYPE,
+  A_MAP_POLYGON_TYPE,
+  A_MAP_POLYLINE_TYPE,
+  AMapCircle,
+  AMapMarker,
+  AMapPolygon,
+  AMapPolyline,
+  AMapView,
+  GOADE_MAP_VIEW_TYPE
+} from '@react-native-oh-tpl/react-native-amap3d';

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
...
+    if (ctx.componentName === GOADE_MAP_VIEW_TYPE) {
+      AMapView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
+    if (ctx.componentName === A_MAP_CIRCLE_VIEW_TYPE) {
+      AMapCircle({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
+    if (ctx.componentName === A_MAP_MARKER_TYPE) {
+      AMapMarker({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
+    if (ctx.componentName === A_MAP_POLYGON_TYPE) {
+      AMapPolygon({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
+    if (ctx.componentName === A_MAP_POLYLINE_TYPE) {
+      AMapPolyline({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag,
+      })
+    }
...
}
...
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.  

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+  A_MAP_CIRCLE_VIEW_TYPE,
+  A_MAP_MARKER_TYPE,
+  A_MAP_POLYGON_TYPE,
+  A_MAP_POLYLINE_TYPE,
+  GOADE_MAP_VIEW_TYPE
  ];
```

### 5. Introducing AMap3DPackage to ArkTS 

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:


```diff  
  ... 
+ import {AMap3DPackage} from '@react-native-oh-tpl/react-native-amap3d/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new AMap3DPackage(ctx)
  ];
}
```

### 6. Running

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

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-amap3d Releases](https://github.com/react-native-oh-library/react-native-amap3d/releases)


## Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.
### MapView
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| mapType  | 地图类型         | int  | yes | iOS      | yes |
| initialCameraPosition  | 初始状态         | CameraPosition  | yes | iOS      | yes |
| myLocationEnabled  | 是否显示当前定位         | boolean  | yes | iOS      | no |
| indoorViewEnabled  | 是否显示室内地图         | boolean  | yes | iOS      | no |
| buildingsEnabled  | 是否显示3D建筑         | boolean  | yes | iOS      | no |
| labelsEnabled  | 是否显示标注         | boolean  | yes | iOS      | yes |
| compassEnabled  | 是否显示指南针         | boolean  | yes | iOS      | no |
| zoomControlsEnabled  | 是否显示放大缩小按钮         | boolean  | yes | iOS      | yes |
| scaleControlsEnabled  | 是否显示比例尺         | boolean  | yes | iOS      | yes |
| trafficEnabled  | 是否显示路况         | boolean  | yes | iOS      | yes |
| maxZoom  | 最大缩放级别         | float  | yes | iOS      | yes |
| minZoom  | 最小缩放级别         | float  | yes | iOS      | yes |
| zoomGesturesEnabled  | 是否启用缩放手势，用于放大缩小         | boolean  | yes | iOS      | yes |
| scrollGesturesEnabled  | 是否启用滑动手势，用于平移         | boolean  | yes | iOS      | yes |
| rotateGesturesEnabled  | 是否启用旋转手势，用于调整方向         | boolean  | yes | iOS      | yes |
| tiltGesturesEnabled  | 是否启用倾斜手势，用于改变视角         | boolean  | yes | iOS      | yes |
| distanceFilter  | 设定定位的最小更新距离         | float  | yes | iOS      | no|
| headingFilter  | 设定最小更新角度，默认为 1 度         | float  | yes | iOS      | no |

### Circle
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| center  | 圆点坐标         | LatLng  | yes | iOS      | yes |
| radius  | 半径（米）         | Float  | yes | iOS      | yes |
| strokeWidth  | 边线宽度         | Float  | yes | iOS      | yes |
| strokeColor  | 边线颜色         | string  | yes | iOS      | yes |
| fillColor  | 填充颜色         | string  | yes | iOS      | yes |
| zIndex  | 层级         | Float  | yes | iOS      | yes |

### Marker
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| position  | 坐标         | LatLng  | yes | iOS      | yes |
| icon  | 图标         | ImageSourcePropType  | yes | iOS      | no |
| draggable  | 是否可拖拽         | boolean  | yes | iOS      | yes |
| flat  | 是否平贴地图         | boolean  | yes | iOS      | yes |
| zIndex  | 层级         | Float  | yes | iOS      | yes |
| anchor  | 覆盖物锚点比例         | Point  | yes | iOS      | no |
| centerOffset  | 覆盖物偏移位置         | Float  | yes | iOS      | no |

### Polygon
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| points  | 节点坐标         | LatLng[]  | yes | iOS      | yes |
| strokeWidth  | 边线宽度         | Float  | yes | iOS      | yes |
| strokeColor  | 边线颜色         | string  | yes | iOS      | yes |
| fillColor  | 填充颜色         | string  | yes | iOS      | yes |
| zIndex  | 层级         | Float  | yes | iOS      | yes |

### Polyline
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| points  | 节点坐标         | LatLng[]  | yes | iOS      | yes |
| width  | 边线宽度         | Float  | yes | iOS      | yes |
| color  | 线段颜色         | ColorValue  | yes | iOS      | yes |
| zIndex  | 层级         | Float  | yes | iOS      | yes |
| colors  | 多段颜色        | ColorValue[]  | yes | iOS      | yes |
| gradient  | 是否使用颜色渐变        | boolean  | yes | iOS      | yes |
| geodesic  | 是否绘制大地线        | boolean  | yes | iOS      | no |
| dotted  | 是否绘制虚线        | boolean  | yes | iOS      | yes |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.
### MapView
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| onPress  | 点击事件        | LatLng | yes | iOS      | yes |
| onPressPoi  | 标注点击事件        | Poi | yes | iOS      | yes |
| onLongPress  | 长按事件        | LatLng | yes | iOS      | yes |
| onCameraMove  | 地图状态改变事件，随地图状态变化不停地触发        | CameraEvent | yes | iOS      | no |
| onCameraIdle  | 地图状态改变事件，在停止变化后触发        | CameraEvent | yes | iOS      | no |
| onLoad  | 地图初始化完成事件        | void | yes | iOS      | yes |
| onLocation  | 地图定位更新事件        | GeolocationPosition | no | iOS      | no |
| onCallback  | 回调事件        | void | yes | iOS      | no |
| moveCamera  | 移动视角        | void | yes | iOS      | no |
| call  | 调用        | void | yes | iOS      | no |


### Marker
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| onPress  | 点击事件        | void | yes | iOS      | yes |
| onDragStart  | 拖放开始事件        | void | yes | iOS      | yes |
| onDrag  | 拖放进行事件，类似于mousemove，在结束之前会不断调用        | void | yes | iOS      | yes |
| onDragEnd  | 拖放结束事件        | LatLng | yes | iOS      | yes |
| update  | 触发自定义view更新        | void | yes | iOS      | no | 

### Polyline
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| onPress  | 点击事件        | void | yes | iOS      | yes |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| initSDK  | 初始化高德SDK         | void  | yes | iOS      | no |
| getVersion  | 获取版本信息         | Promise<string>  | yes | iOS      | no |

## 遗留问题
- [ ] initSDK: Does not support in hramony: [issue#16](https://github.com/react-native-oh-library/react-native-amap3d/issues/16)
- [ ] getVersion: Does not support in hramony: [issue#17](https://github.com/react-native-oh-library/react-native-amap3d/issues/17)
### MapView
- [ ] indoorViewEnabled: Amap SDK is not supported: [issue#6](https://github.com/react-native-oh-library/react-native-amap3d/issues/6)
- [ ] compassEnabled: Amap SDK is not supported: [issue#7](https://github.com/react-native-oh-library/react-native-amap3d/issues/7)
- [ ] buildingsEnabled: Amap SDK is not supported: [issue#33](https://github.com/react-native-oh-library/react-native-amap3d/issues/33)
- [ ] myLocationEnabled: Amap SDK is not supported: [issue#29](https://github.com/react-native-oh-library/react-native-amap3d/issues/29)
- [ ] distanceFilter: Amap SDK is not supported: [issue#11](https://github.com/react-native-oh-library/react-native-amap3d/issues/11)
- [ ] anchor: Amap SDK is not supported: [issue#34](https://github.com/react-native-oh-library/react-native-amap3d/issues/34)
- [ ] centerOffset: Amap SDK is not supported: [issue#35](https://github.com/react-native-oh-library/react-native-amap3d/issues/35)
- [X] zoomControlsEnabled: Amap SDK is not supported: [issue#8](https://github.com/react-native-oh-library/react-native-amap3d/issues/8)
- [X] scaleControlsEnabled: Amap SDK is not supported: [issue#9](https://github.com/react-native-oh-library/react-native-amap3d/issues/9)
- [ ] headingFilter: Amap SDK is not supported: [issue#12](https://github.com/react-native-oh-library/react-native-amap3d/issues/12)
- [ ] geodesic: Amap SDK is not supported: [issue#36](https://github.com/react-native-oh-library/react-native-amap3d/issues/36)
- [x] onCameraMove: Amap SDK is not supported: [issue#14](https://github.com/react-native-oh-library/react-native-amap3d/issues/14)
- [ ] onCameraIdle: Amap SDK is not supported: [issue#15](https://github.com/react-native-oh-library/react-native-amap3d/issues/15)
- [X] onPressPoi: Amap SDK is not supported: [issue#13](https://github.com/react-native-oh-library/react-native-amap3d/issues/13)
- [ ] onLocation: Amap SDK is not supported: [issue#10](https://github.com/react-native-oh-library/react-native-amap3d/issues/10)
- [ ] onCallback: Amap SDK has partial support: [issue#21](https://github.com/react-native-oh-library/react-native-amap3d/issues/21)
- [x] moveCamera: Does not support in hramony: [issue#19](https://github.com/react-native-oh-library/react-native-amap3d/issues/19)
- [ ] call: Does not support in hramony: [issue#5](https://github.com/react-native-oh-library/react-native-amap3d/issues/5)

### Marker
- [ ] icon: Amap SDK is not supported yet: [issue#20](https://github.com/react-native-oh-library/react-native-amap3d/issues/20)
- [ ] update: Amap SDK is not supported yet: [issue#18](https://github.com/react-native-oh-library/react-native-amap3d/issues/18)
### Cluster
- [ ] Cluster: Amap SDK does not currently support adding this component: [issue#2](https://github.com/react-native-oh-library/react-native-amap3d/issues/2)
### HeatMap
- [ ] HeatMap: Amap SDK does not currently support adding this component: [issue#3](https://github.com/react-native-oh-library/react-native-amap3d/issues/3)
### MultiPoint
- [ ] MultiPoint: Amap SDK does not currently support adding this component: [issue#4](https://github.com/react-native-oh-library/react-native-amap3d/issues/4)


## Others

## License

This project is licensed under [MIT License (MIT)](https://github.com/qiuxiang/react-native-amap3d/blob/main/license).
