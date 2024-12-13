> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-map-linking</code> </h1>
</p>

本项目基于 [react-native-map-linking@1.0.1](https://github.com/starlight36/react-native-map-linking) 开发。

该第三方库的仓库已迁移至 Gitee，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-map-linking`，具体版本所属关系如下：

| Version                   | Package Name                                  | Repository                                                                                | Release                                                                                                     |
| ------------------------- | --------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| <= 1.0.1-0.0.1@deprecated | @react-native-oh-tpl/react-native-map-linking | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-map-linking) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-map-linking/releases) |
| > 1.0.1                   | @react-native-ohos/react-native-map-linking   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-map-linking)                 | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-map-linking/releases)                 |

## 1. 安装与使用

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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
              "香山公园",
              "bbb"
            );
          }}
        >
          <View style={styles.button}>
            <Text style={styles.text}>在地图上标记位置</Text>
          </View>
        </TouchableOpacity>
        <TouchableOpacity
          onPress={() => {
            MapLinking.planRoute(
              { lat: 39.9901079, lng: 116.1887467, title: "香山公园" },
              { lat: 40.0382556, lng: 116.3144536, title: "清河站" },
              "drive"
            );
          }}
        >
          <View style={styles.button}>
            <Text style={styles.text}>规划线路</Text>
          </View>
        </TouchableOpacity>
        <TouchableOpacity
          onPress={() => {
            MapLinking.navigate({
              lat: 40.0382556,
              lng: 116.3144536,
              title: "清河站",
            });
          }}
        >
          <View style={styles.button}>
            <Text style={styles.text}>导航</Text>
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

## 2. 约束与限制

### 2.1 使用该三方库需要配置 querySchemes 

请在 `entry/src/module.json5` 中配置 `querySchemes` 字段，这样才能支持唤起花瓣地图和高德地图。

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

### 2.2 兼容性

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/react-native-map-linking Releases](https://gitee.com/openharmony-sig/rntpc_react-native-map-linking/releases)

## 3. APIs

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                       | Description                  | Optional                                                                                                                                                                                                                                                                                                                 | Required | Platform | HarmonyOS Support |
| ------------------------------------------ | ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| markLocation(location, title, content)     | 在地图上标记一个点的位置     | location 位置坐标, 是一个对象, 包括: **lat** - 经度**lng** - 纬度 **type** - 坐标类型, 支持`gcj02`(国测局坐标), `wgs84`(GPS 坐标) **title** 地点标记名称 **content** 地点标记说明                                                                                                                                        | no       | all      | partially               |
| planRoute(srcLocation, distLocation, mode) | 规划两点之间的线路           | srcLocation 起始位置坐标, 是一个对象, 包括: **lat** - 经度 **lng** - 纬度 **title** - 起始位置名称 distLocation 结束位置坐标, 是一个对象, 包括: **lat** - 经度 **lng** - 纬度 **type** - 坐标类型, 支持`gcj02`(国测局坐标), `wgs84`(GPS 坐标) **title** - 结束位置名称 mode 路线模式 drive - 驾车 bus - 公交 walk - 步行 | no       | all      | partially               |
| navigate(distLocation)                     | 启动当前位置到目标位置的导航 | distLocation 结束位置坐标, 是一个对象, 包括: **lat** - 经度 **lng** - 纬度 **type** - 坐标类型, 支持`gcj02`(国测局坐标), `wgs84`(GPS 坐标) **title** - 结束位置名称                                                                                                                                                      | no       | all      | partially               |

## 4. 遗留问题

- [ ] react-native-map-link 目前无法唤起百度地图，未提供应用市场地址和具体参数供 react-native-map-link 调用 [issue#1](https://github.com/react-native-oh-library/react-native-map-linking/issues/1)
- [ ] react-native-map-link 目前仅支持高德地图使用路径规划，其他功能暂不支持 [issue#2](https://github.com/react-native-oh-library/react-native-map-linking/issues/2)

## 5. 其他

- 如果系统内没有可用的地图, 组件会推荐下载高德地图。

- 目前仅支持使用高德地图做路线规划，启动导航、标注指定位置等功能暂不支持。

## 6. 开源协议

本项目基于 [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-map-linking/blob/master/LICENSE) ，请自由地享受和参与开源。
