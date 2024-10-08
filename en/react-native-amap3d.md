<!--{%raw%}-->
> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-amap3d)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-amap3d Releases](https://github.com/react-native-oh-library/react-native-amap3d/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-amap3d@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-amap3d@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

目前HarmonyOS暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-amap3d": "file:../../node_modules/@react-native-oh-tpl/react-native-amap3d/harmony/rn_amap3d.har"
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

### 3.配置 CMakeLists 和引入 MapViewPackge

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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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


### 4.在 ArkTs 侧引入 react-native-amap3d 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

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

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

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

### 5.在 ArkTs 侧引入 AMap3DPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：


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

### 6.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-amap3d Releases](https://github.com/react-native-oh-library/react-native-amap3d/releases)


## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
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

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
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

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| initSDK  | 初始化高德SDK         | void  | yes | iOS      | no |
| getVersion  | 获取版本信息         | Promise<string>  | yes | iOS      | no |

## 遗留问题
- [ ] initSDK：hramony暂不支持: [issue#16](https://github.com/react-native-oh-library/react-native-amap3d/issues/16)
- [ ] getVersion：hramony暂不支持: [issue#17](https://github.com/react-native-oh-library/react-native-amap3d/issues/17)
### MapView
- [ ] indoorViewEnabled：高德SDK暂不支持: [issue#6](https://github.com/react-native-oh-library/react-native-amap3d/issues/6)
- [ ] compassEnabled：高德SDK暂不支持: [issue#7](https://github.com/react-native-oh-library/react-native-amap3d/issues/7)
- [ ] buildingsEnabled：高德SDK暂不支持: [issue#33](https://github.com/react-native-oh-library/react-native-amap3d/issues/33)
- [ ] myLocationEnabled：高德SDK暂不支持: [issue#29](https://github.com/react-native-oh-library/react-native-amap3d/issues/29)
- [ ] distanceFilter：高德SDK暂不支持: [issue#11](https://github.com/react-native-oh-library/react-native-amap3d/issues/11)
- [ ] anchor:高德SDK暂不支持: [issue#34](https://github.com/react-native-oh-library/react-native-amap3d/issues/34)
- [ ] centerOffset:高德SDK暂不支持: [issue#35](https://github.com/react-native-oh-library/react-native-amap3d/issues/35)
- [X] zoomControlsEnabled：高德SDK暂不支持: [issue#8](https://github.com/react-native-oh-library/react-native-amap3d/issues/8)
- [X] scaleControlsEnabled：高德SDK暂不支持: [issue#9](https://github.com/react-native-oh-library/react-native-amap3d/issues/9)
- [ ] headingFilter：高德SDK暂不支持: [issue#12](https://github.com/react-native-oh-library/react-native-amap3d/issues/12)
- [ ] geodesic：高德SDK暂不支持: [issue#36](https://github.com/react-native-oh-library/react-native-amap3d/issues/36)
- [ ] onCameraMove: 高德SDK暂不支持： [issue#14](https://github.com/react-native-oh-library/react-native-amap3d/issues/14)
- [ ] onCameraIdle: 高德SDK暂不支持: [issue#15](https://github.com/react-native-oh-library/react-native-amap3d/issues/15)
- [X] onPressPoi：高德SDK暂不支持: [issue#13](https://github.com/react-native-oh-library/react-native-amap3d/issues/13)
- [ ] onLocation：高德SDK暂不支持: [issue#10](https://github.com/react-native-oh-library/react-native-amap3d/issues/10)
- [ ] onCallback：高德SDK部分支持: [issue#21](https://github.com/react-native-oh-library/react-native-amap3d/issues/21)
- [ ] moveCamera：harmony暂不支持: [issue#19](https://github.com/react-native-oh-library/react-native-amap3d/issues/19)
- [ ] call：harmony暂不支持: [issue#5](https://github.com/react-native-oh-library/react-native-amap3d/issues/5)

### Marker
- [ ] icon：高德SDK暂不支持: [issue#20](https://github.com/react-native-oh-library/react-native-amap3d/issues/20)
- [ ] update：harmony暂不支持: [issue#18](https://github.com/react-native-oh-library/react-native-amap3d/issues/18)
### Cluster
- [ ] Cluster：高德SDK暂不支持添加该组件: [issue#2](https://github.com/react-native-oh-library/react-native-amap3d/issues/2)
### HeatMap
- [ ] HeatMap：高德SDK暂不支持添加该组件: [issue#3](https://github.com/react-native-oh-library/react-native-amap3d/issues/3)
### MultiPoint
- [ ] MultiPoint：高德SDK暂不支持添加该组件: [issue#4](https://github.com/react-native-oh-library/react-native-amap3d/issues/4)


## 其他

## 开源协议

本项目基于 [MIT License (MIT)](https://github.com/qiuxiang/react-native-amap3d/blob/main/license) ，请自由地享受和参与开源。
<!--{%endraw%}-->
