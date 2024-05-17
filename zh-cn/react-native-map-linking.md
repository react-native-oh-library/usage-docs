> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-map-link</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/starlight36/react-native-map-linking">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/starlight36/react-native-map-linking/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-map-linking)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-map-linking Releases](https://github.com/react-native-oh-library/react-native-map-linking/releases/tag/1.0.1-0.0.1)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-map-linking@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-map-linking@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react';
import {
  AppRegistry,
  StyleSheet,
  Text,
  View,
  TouchableOpacity,
} from 'react-native';
import MapLinking from 'react-native-map-linking';

class MapLinkingDemo extends Component {
  render() {
    return (
      <View style={styles.container}>
        <TouchableOpacity
          onPress={() => {MapLinking.markLocation({lat: 39.9901079, lng:116.1887467},'香山公园','bbb')}}>
          <View style={styles.button}>
            <Text style={styles.text}>在地图上标记位置</Text>
          </View>
        </TouchableOpacity>
        <TouchableOpacity
          onPress={() => {MapLinking.planRoute({lat: 39.9901079, lng:116.1887467, title: '香山公园'}, {lat:40.0382556, lng:116.3144536, title:'清河站'}, 'drive')}}>
          <View style={styles.button}>
            <Text style={styles.text}>规划线路</Text>
          </View>
        </TouchableOpacity>
        <TouchableOpacity
          onPress={() => {MapLinking.navigate({lat:40.0382556, lng:116.3144536, title:'清河站'} )}}>
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
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  button: {
    padding: 10,
    backgroundColor: '#3B5998',
    marginBottom: 10,
  },
  text: {
    color: 'white',
  },
});
export default MapLinkingDemo;  
```



## 约束与限制

### 兼容性
要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 电脑ROM。

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1 B.0.18； IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.18;


## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

Name | Description | Optional | Required | Platform | HarmonyOS   Support
-- | -- | -- | -- | -- | --
markLocation(location, title, content) | 在地图上标记一个点的位置 | location 位置坐标, 是一个对象, 包括: **lat** - 经度**lng** - 纬度 **type** - 坐标类型, 支持`gcj02`(国测局坐标), `wgs84`(GPS坐标) **title** 地点标记名称 **content** 地点标记说明 | / | all | yes
planRoute(srcLocation, distLocation, mode) | 规划两点之间的线路 | srcLocation 起始位置坐标, 是一个对象, 包括:  **lat** - 经度 **lng** - 纬度 **title** - 起始位置名称 distLocation 结束位置坐标, 是一个对象, 包括:  **lat** - 经度 **lng** - 纬度 **type** - 坐标类型, 支持`gcj02`(国测局坐标), `wgs84`(GPS坐标) **title** - 结束位置名称 mode 路线模式  drive - 驾车 bus - 公交 walk - 步行 | / | all | yes
navigate(distLocation) | 启动当前位置到目标位置的导航 | distLocation 结束位置坐标, 是一个对象, 包括:  **lat** - 经度 **lng** - 纬度 **type** - 坐标类型, 支持`gcj02`(国测局坐标), `wgs84`(GPS坐标) **title** - 结束位置名称 | / | all | yes

## 遗留问题

- [ ] 百度地图暂未提供应用市场地址和具体参数（未解决）[#I9OE8Z](https://gitee.com/allisonzhou/usage-docs/issues/I9OE8Z)
- [ ] 高德地图暂未提供具体参数（未解决）[#I9OE7H](https://gitee.com/allisonzhou/usage-docs/issues/I9OE7H)

## 其他

- 如果系统内没有可用的地图, 组件会推荐下载高德地图、百度地图。

- 使用iOS内建地图时, 地图标记和导航功能可能不精确, 推荐使用高德地图

### Harmony配置Schema支持

Harmony系统下需要在module.json5中配置querySchemes支持才能唤起花瓣地图，后续要唤起高德地图和百度地图，也需要将它们的scheme加到这里。
  
```
"querySchemes":[
  "maps"
]
```
  
  
  
### iOS配置Schema支持
  
iOS系统下需要在App的`info.plist`中配置Schema支持才能唤起地图:

 ```
<key>LSApplicationQueriesSchemes</key>
<array>
    <string>baidumap</string>
    <string>iosamap</string>
</array>
 ```

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/starlight36/react-native-map-linking/blob/master/LICENSE) ，请自由地享受和参与开源。

