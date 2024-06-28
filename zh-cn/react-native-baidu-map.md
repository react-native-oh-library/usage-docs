<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-baidu-map</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lovebing/react-native-baidu-map">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lovebing/react-native-baidu-map/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-baidu-map)

## 安装与使用

请到三方库的 Releases
发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-baidu-map Releases](https://github.com/react-native-oh-library/react-native-baidu-map/releases)
，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-baidu-map@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-baidu-map@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react';
import { Text, ScrollView, View, StyleSheet } from 'react-native';
import { MapApp, Location, BaiduMapManager, MapView, Overlay } from 'react-native-baidu-map';


function App({ }): JSX.Element {

    const _onMapClick = (location: Location) => {
        console.log('baidumap _onMapClick location latitude:' + location.latitude);
        console.log('baidumap _onMapClick location longitude:' + location.longitude);
    }

    const _onMapDoubleClick = () => {
        console.log('baidumap _onMapDoubleClick');
    }

    const _onMapLoaded = () => {
        console.log('baidumap _onMapLoaded');
    }


    function _TestTurboModule() {
        console.log('baidumap _TestTurboModule');
        BaiduMapManager.initSDK('test');
        BaiduMapManager.hasLocationPermission().then((hasPermission: boolean) => {
            console.log('baidumap hasLocationPermission:' + hasPermission);
        })
        MapApp.openDrivingRoute({ latitude: 38.914935, longitude: 115.403119, name: "" }, { latitude: 39.914935, longitude: 116.403119, name: "" });
        MapApp.openTransitRoute({ latitude: 36.914935, longitude: 113.403119, name: "" }, { latitude: 37.914935, longitude: 114.403119, name: "" });
        MapApp.openWalkNavi({ latitude: 34.914935, longitude: 111.403119, name: "" }, { latitude: 35.914935, longitude: 112.403119, name: "" });
    }
    return (
    <View >
        <View style={[styles.button, { marginLeft: 100, marginTop: 40 }]}
            onTouchEnd={() => {
             _TestTurboModule();
            }
    }>
    <Text style={styles.buttonText}>_TestTurboModule</Text>
        </View>
        <MapView
    center={{ latitude: 38.914935, longitude: 115.403119 }}
    zoom={12.0}
    mapType={1}
    trafficEnabled={true}
    zoomGesturesEnabled={true}
    scrollGesturesEnabled={true}
    zoomControlsVisible={true}
    showsUserLocation={true}
    locationData={{ latitude: 38.914935, longitude: 115.403119 }}
    onMapClick={_onMapClick}
    onMapLoaded={_onMapLoaded}
    onMapDoubleClick={_onMapDoubleClick}
    style={{ width: '100%', height: '90%' }}
    >
    <Overlay.Circle
    radius={6000}
    fillColor='0000FF'
    stroke={{ width: 12, color: 'AAEEFF11' }}
    center={{ latitude: 38.914935, longitude: 115.403119 }} />
    
        <Overlay.Marker
    location={{ latitude: 39.844935, longitude: 115.603119 }} onClick={() => {
        console.log("baidumap Marker CLICK1")
    }} icon={{ uri: "https://maponline0.bdimg.com/sty/map_icons2x/MapRes/huochezhan.png?udt=20230227" }} />
    
        <Overlay.Marker
    location={{ latitude: 40.044935, longitude: 115.603119 }} onClick={() => {
        console.log("baidumap Marker CLICK2")
    }} icon={{ uri: "https://maponline0.bdimg.com/sty/map_icons2x/MapRes/huochezhan.png?udt=20230227" }} />
    
    
        <Overlay.Polyline
    points={[{ latitude: 38.914935, longitude: 115.403119 }, { latitude: 39.014935, longitude: 115.603119 }, { latitude: 38.814935, longitude: 115.603119 }]}
    stroke={{ width: 5, color: 'AA000000' }} />
    
        <Overlay.Polygon
    points={[{ latitude: 38.914935, longitude: 115.403119 }, { latitude: 38.614935, longitude: 115.203119 }, { latitude: 39.414935, longitude: 115.403119 }]}
    stroke={{ width: 5, color: 'AA000000' }}
    fillColor='0000FF' />
        <Overlay.Text
    location={{ latitude: 38.614935, longitude: 115.403119 }}
    fontColor='0000FF'
    fontSize={32}
    bgColor='888888'
    rotate={10}
    text='overlay Text test' />
        </MapView>
        </View>
    
    )
    }
    
    const styles = StyleSheet.create({
        button: {
            width: 160,
            height: 36,
            backgroundColor: 'hsl(190, 50%, 70%)',
            paddingHorizontal: 16,
            paddingVertical: 8,
            borderRadius: 8,
        },
        buttonText: {
            width: '100%',
            height: '100%',
            fontWeight: 'bold',
        },
    });

export default App;
```

## Link

目前harmonyOS暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的harmonyOS工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony": "./react_native_openharmony"
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
"@react-native-oh-tpl/react-native-baidu-map": "file:../../node_modules/@react-native-oh-tpl/react-native-baidu-map/harmony/baidu_map.har"
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

### 配置 CMakeLists 和引入 BaiduMapPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-baidu-map/src/main/cpp" ./baidu-map)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_baidu_map)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "BaiduMapPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<BaiduMapPackage>(ctx),
    };
}
```

### 在 ArkTs 侧引入 BaiduMapPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {BaiduMapPackage} from '@react-native-oh-tpl/react-native-baidu-map/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new BaiduMapPackage(ctx)
  ];
}
```

### 在 ArkTs 侧引入 react-native-baidu-map 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets`
或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import {
+  BAIDU_MAP_OVERLAY_CIRCLE_TYPE,
+  BAIDU_MAP_OVERLAY_MARKER_TYPE,
+  BAIDU_MAP_OVERLAY_POLYGON_TYPE,
+  BAIDU_MAP_OVERLAY_POLYLINE_TYPE,
+  BAIDU_MAP_OVERLAY_TEXT_TYPE,
+  BAIDU_MAP_VIEW_TYPE,
+  BaiduMapOverlayCircle,
+  BaiduMapOverlayPolygon,
+  BaiduMapOverlayPolyline,
+  BaiduMapOverlayText,
+  BaiduMapView
+} from '@react-native-oh-tpl/react-native-baidu-map';

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
...
+ if (ctx.componentName === BAIDU_MAP_VIEW_TYPE) {
+      BaiduMapView({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === BAIDU_MAP_OVERLAY_CIRCLE_TYPE) {
+      BaiduMapOverlayCircle({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === BAIDU_MAP_OVERLAY_MARKER_TYPE) {
+      BaiduMapOverlayMarkerS({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === BAIDU_MAP_OVERLAY_POLYGON_TYPE) {
+      BaiduMapOverlayPolygon({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === BAIDU_MAP_OVERLAY_POLYLINE_TYPE) {
+      BaiduMapOverlayPolyline({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === BAIDU_MAP_OVERLAY_TEXT_TYPE) {
+      BaiduMapOverlayText({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames`
在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ BAIDU_MAP_VIEW_TYPE,
+ BAIDU_MAP_OVERLAY_CIRCLE_TYPE,
+ BAIDU_MAP_OVERLAY_MARKER_TYPE,
+ BAIDU_MAP_OVERLAY_POLYGON_TYPE,
+ BAIDU_MAP_OVERLAY_POLYLINE_TYPE,
+ BAIDU_MAP_OVERLAY_TEXT_TYPE
  ];
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

请到三方库相应的 Releases 发布地址查看 Release
配套的版本信息：[@react-native-oh-tpl/react-native-baidu-map Releases](https://github.com/react-native-oh-library/react-native-baidu-map/releases)

### 权限要求

#### 在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

```diff
...
"requestPermissions": [
+      {
+        "name": "ohos.permission.WRITE_USER_STORAGE"
+      },
+      {
+        "name": "ohos.permission.READ_USER_STORAGE"
+      },
+      {
+        "name": "ohos.permission.INTERNET"
+      },
+      {
+        "name": "ohos.permission.GET_BUNDLE_INFO"
+      },
+      {
+        "name": "ohos.permission.LOCATION",
+        "reason": "$string:EntryAbility_desc",
+        "usedScene": {
+          "abilities": [
+            "MainAbility"
+          ],
+          "when": "inuse"
+        }
+      },
+      {
+        "name": "ohos.permission.LOCATION_IN_BACKGROUND",
+        "reason": "$string:EntryAbility_desc",
+        "usedScene": {
+          "abilities": [
+            "MainAbility"
+          ],
+          "when": "inuse"
+        }
+      },
+      {
+        "name": "ohos.permission.APPROXIMATELY_LOCATION",
+        "reason": "$string:EntryAbility_desc",
+        "usedScene": {
+          "abilities": [
+            "MainAbility"
+          ],
+          "when": "inuse"
+        }
+      }
    ]
```

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标
> iOS 或 Android 的效果。

#### MapView Props 属性

| Name                    | Description                      | Type     | Required | Platform | HarmonyOS Support |
|-------------------------|----------------------------------|----------|----------|----------|-------------------|
| zoomControlsVisible     | 显示或隐藏缩放控件，仅 Android              | Boolean  | no      | Android  | yes               |
| trafficEnabled          | 是否启用交通图层                         | Boolean  | no      | All      | yes                |
| baiduHeatMapEnabled     | 是否启用百度热力图                        | Boolean  | no      | All      | yes                |
| zoomGesturesEnabled     | 允许手势缩放                           | Boolean  | no      | All      | yes                |
| scrollGesturesEnabled   | 允许拖动                             | Boolean  | no      | All      | yes                |
| mapType                 | 地图类型                             | Number   | no      | All      | partially                |
| zoom                    | 地图的缩放级别                          | Number   | no      | All      | yes                |
| showsUserLocation       | 是否显示定位                           | Boolean  | no      | All      | yes                |
| locationData            | 定位信息 {latitude: 0, longitude: 0} | Object   | no      | All      | yes                |
| center                  | {latitude: 0, longitude: 0}      | Object   | no      | All      | yes                |
| onMapStatusChangeStart  | 地图状态开始变化时的回调函数，仅 Android         | Function | no      | Android  | no                |
| onMapStatusChange       | 地图状态变化时的回调函数                     | Function | no      | All      | no                |
| onMapStatusChangeFinish | 地图状态变化完成时的回调函数，仅 Android         | Function | no      | Android  | no                |
| onMapLoaded             | 地图加载完成时的回调函数                     | Function | no      | All      | yes                |
| onMapClick              | 地图被点击时的回调函数                      | Function | no      | All      | yes                |
| onMapDoubleClick        | 地图被双击时的回调函数                      | Function | no      | All      | yes                |
| onMarkerClick           | 地图上的标记被点击时的回调函数                  | Function | no      | All      | no                |
| onMapPoiClick           | 地图上的兴趣点（POI）被点击时的回调函数            | Function | no      | All      | no                |

#### Marker Props 属性

| Name         | Description                              | Type     | Required | Platform | HarmonyOS Support |
|--------------|------------------------------------------|----------|----------|----------|-------------------|
| title        | 如果没有 InfoWindow，将会根据 title 生成 InfoWindow | String   | no       | All      | no                |
| titleOffsetY | title 作为 InfoWindow 展示的 y 轴偏移量，仅 Android | Number   | no       | Android  | no                |
| location     | 标记的经纬度坐标位置                               | Object   | yes      | All      | yes               |
| perspective  | 是否启用标记的透视效果，仅 Android                    | Boolean  | no       | Android  | yes               |
| flat         | 是否使标记扁平化，仅 Android                       | Boolean  | no       | Android  | yes               |
| rotate       | 旋转角度，仅 Android                           | Number   | no       | Android  | yes               |
| icon         | icon图片，同  的 source 属性                    | Object   | no       | All      | yes               |
| alpha        | 透明度，仅 Android                            | Number   | no       | Android  | yes               |
| animateType  | 动画效果：drop/grow/jump (iOS 仅支持 drop)       | String   | no       | All      | yes               |
| pinColor     | red/green/purple，大头针颜色，仅 iOS             | String   | no       | IOS      | no                |
| onClick      | 当标记被点击时触发的回调函数                           | Function | no       | All      | yes               |

#### Cluster 点聚合

#### Arc Props 属性

| Name   | Description    | Type    | Required | Platform | HarmonyOS Support |
|--------|----------------|---------|----------|----------|-------------------|
| stroke | 当标记被点击时触发的回调函数 | Object  | yes      | All      | no                |
| points | 数值长度必须为        | Object  | yes      | All      | no                |
| dash   | 是否为虚线，仅 iOS    | Boolean | yes      | iOS      | no                |

#### Circle Props 属性

| Name      | Description       | Type   | Required | Platform | HarmonyOS Support |
|-----------|-------------------|--------|----------|----------|-------------------|
| radius    | 圆的半径              | Number | yes      | All      | yes               |
| fillColor | 圆的填充颜色（十六进制，带透明度） | String | yes       | All      | yes               |
| stroke    | 圆的描边样式            | Object | yes       | All      | yes               |
| center    | 圆的中心点坐标           | Object | yes       | All      | yes               |

#### Polyline Props 属性

| Name   | Description | Type   | Required | Platform | HarmonyOS Support |
|--------|-------------|--------|----------|----------|-------------------|
| points | 折线的顶点坐标数组   | Object | yes      | All      | yes               |
| stroke | 折线的描边样式     | Object | yes      | All      | yes               |

#### Polygon Props 属性

| Name      | Description          | Type   | Required | Platform | HarmonyOS Support |
|-----------|----------------------|--------|----------|----------|-------------------|
| points    | 多边形的顶点坐标数组           | Object | yes      | All      | yes               |
| fillColor | 多边形的填充颜色（十六进制，带透明度）	 | String | no      | All      | yes               |
| stroke    | 多边形的描边样式             | Object | no      | All      | yes               |

#### Text Props 属性

| Name      | Description   | Type   | Required | Platform | HarmonyOS Support |
|-----------|---------------|--------|----------|----------|-------------------|
| text      | 要显示的文本        | String | yes      | All      | yes               |
| fontSize  | 文本的字体大小       | Number | no       | All      | yes               |
| fontColor | 文本的字体颜色（十六进制） | String | no       | All      | yes               |
| bgColor   | 文本的背景颜色（十六进制） | String | no       | All      | yes               |
| rotate    | 文本旋转的角度       | Number | no       | All      | yes               |
| location  | 文本在地图上的位置坐标	  | Object | yes      | All      | yes               |

#### MarkerIcon 使用 View 作为 marker 的 icon

#### InfoWindow Props 属性

#### 必须作为 Marker 的子组件

| Name    | Description                    | Type   | Required | Platform | HarmonyOS Support |
|---------|--------------------------------|--------|----------|----------|-------------------|
| offsetY | 相对于 point 在 y 轴的偏移量，仅 Android	 | Object | yes      | Android  | no                |

#### HeatMap Props 属性

| Name     | Description | Type   | Required | Platform | HarmonyOS Support |
|----------|-------------|--------|----------|----------|-------------------|
| points   | 绘制热度图的点     | array  | yes      | All      | no                |
| gradient | 颜色渐变对象      | object | yes      | All      | no                |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标
> iOS 或 Android 的效果。

#### BaiduMapManager

| Name                          | Description | Type | Required | Platform | HarmonyOS Support |
|-------------------------------|-------------|------|----------|----------|-------------------|
| initSDK                       | iOS 初始化 SDK | void | no      | All      | yes               |
| Promise hasLocationPermission | 是否有定位权限     | void | no       | All      | yes               |

#### Geolocation Methods

| Name                                              | Description                          | Type | Required | Platform | HarmonyOS Support |
|---------------------------------------------------|--------------------------------------|------|----------|----------|-------------------|
| Promise reverseGeoCode                            | 根据给定的经纬度坐标获取相应的地址信息                  | void | no      | All      | no                |
| Promise reverseGeoCodeGPS                         | 通过给定的经纬度进行反向地理编码，从而获取与该经纬度对应的地理位置信息。 | void | no       | All      | no                |
| Promise geocode                                   | 调用一个提供地理编码服务的API                     | void | no       | All      | no                |
| Promise getCurrentPosition                        | 获取当前定位信息，coorType 可为 bd09ll 或 gcj02，默认 bd09ll | void | no       | All      | no                |
| startLocating(function listener, String coorType) | 开始持续定位                               | void | no       | All      | no                |
| stopLocating                                      | 停止持续定位                               | void | no       | All      | no                |

#### GetDistance Methods

| Name                        | Description   | Type | Required | Platform | HarmonyOS Support |
|-----------------------------|---------------|------|----------|----------|-------------------|
| Promise getLocationDistance | 计算两个地理位置之间的距离 | no   | no      | All      | no                |

#### MapApp Methods 调起百度地图客户端

| Name             | Description | Type | Required | Platform | HarmonyOS Support |
|------------------|-------------|------|----------|----------|-------------------|
| openDrivingRoute | 调起百度地图驾车规划  | void | no       | All      | yes               |
| openTransitRoute | 调起百度地图公交路线  | void | no       | All      | yes               |
| openWalkNavi     | 调起百度地图步行路线  | void | no       | All      | yes               |

## 遗留问题
- [ ] Arc覆盖物未实现 [#15](https://github.com/react-native-oh-library/react-native-baidu-map/issues/15)
- [ ] infoWindow覆盖物未实现 [#16](https://github.com/react-native-oh-library/react-native-baidu-map/issues/16)
- [ ] HeatMap覆盖物未实现 [#17](https://github.com/react-native-oh-library/react-native-baidu-map/issues/17)
- [ ] Cluster 覆盖物未实现 [#18](https://github.com/react-native-oh-library/react-native-baidu-map/issues/18)
- [ ] MarkerIcon 覆盖物未实现 [#19](https://github.com/react-native-oh-library/react-native-baidu-map/issues/19)
- [ ] MapView部分事件未实现 [#20](https://github.com/react-native-oh-library/react-native-baidu-map/issues/20)
- [ ] marker的title、pincolor属性未实现 [#21](https://github.com/react-native-oh-library/react-native-baidu-map/issues/21)
- [ ] Geolocation 静态类功能未实现  [#22](https://github.com/react-native-oh-library/react-native-baidu-map/issues/22)
- [ ] GetDistance静态类功能未实现 [#23](https://github.com/react-native-oh-library/react-native-baidu-map/issues/23)


## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/lovebing/react-native-baidu-map/blob/master/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->