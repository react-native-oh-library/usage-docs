> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-vconsole</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/bottom-tabs">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/kafudev/react-native-vconsole/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP]
>
>  [Github 地址](https://github.com/kafudev/react-native-vconsole)

## 安装与使用


#### **npm**

```bash
npm i @kafudev/react-native-vconsole@0.1.11
```

#### **yarn**

```bash
yarn add @kafudev/react-native-vconsole@0.1.11
```


下面的代码展示了这个库的基本使用场景：

```js
import VConsole from '@kafudev/react-native-vconsole'
/* INFO is optional */

// in render function
render() {
  return (
    <View>
        <VConsole
            // 使用 'react-native-config-reader' 库获获取额外信息
            appInfo={{
                原生构建类型: ConfigReader.BUILD_TYPE,
                原生版本号: ConfigReader.VERSION_NAME || ConfigReader.CFBundleShortVersionString,
                原生构建时间: ConfigReader.BUILD_TIME,
                热更新版本号: codePushStore.info.label,
                热更新详情: codePushStore.info.desc,
            }}
            // 另外的的面板
            panels={panels}
            // console.time 可辨别是否开启 debug 网页
            console={__DEV__ ? !console.time : true}
        />
    </View>
  )
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证：

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 属性

> [!tip] 
>
> "Platform"列表示该属性在原三方库上支持的平台。

> [!tip]
>
>  "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name    | Description                              | Type    | Required | Platform | HarmonyOS Support |
| ------- | ---------------------------------------- | ------- | -------- | -------- | ----------------- |
| appInfo | Customized Version Info you want to show | json    | no       | All      | yes               |
| panels  | Custom panels                            | json    | no       | All      | yes               |
| console | Whether to show console                  | boolean | no       | All      | yes               |
| showBtn | Whether to show buttons                  | boolean | no       | All      | yes               |

## 遗留问题

- [ ] cppcrash 问题：在 HarmonyOS 测试时，当 network 里有数据时，tab 页从 network 切换到 info 时，会出现 cppcrash 问题，提示/system/lib64/module/application/libapplicationcontext.z.so 包不存在。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-native-slider/blob/main/LICENSE.md) ，请自由地享受和参与开源。
