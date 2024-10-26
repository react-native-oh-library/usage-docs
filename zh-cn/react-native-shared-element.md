> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-shared-element</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/IjzerenHein/react-native-shared-element">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/IjzerenHein/react-native-shared-element/blob/main/LICENSE.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-shared-element)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-shared-element Releases](https://github.com/react-native-oh-library/react-native-shared-element/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-shared-element@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-shared-element@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import {
  View,
  StyleSheet,
  Animated,
  Dimensions,
  TouchableOpacity,
  Image,
} from 'react-native';
import {
  SharedElement,
  SharedElementTransition,
  nodeFromRef,
} from 'react-native-shared-element';

export default class App extends React.Component {
  state = {
    progress: new Animated.Value(0),
    isScene2Visible: false,
    isInProgress: false,
    scene1Ancestor: null,
    scene1Node: null,
    scene2Ancestor: null,
    scene2Node: null,
  };

  onPressNavigate = () => {
    this.setState({isScene2Visible: true, isInProgress: true});
    Animated.timing(this.state.progress, {
      toValue: 1,
      duration: 1000,
      useNativeDriver: true,
    }).start(() => this.setState({isInProgress: false}));
  };

  onPressBack = () => {
    this.setState({isInProgress: true});
    Animated.timing(this.state.progress, {
      toValue: 0,
      duration: 1000,
      useNativeDriver: true,
    }).start(() =>
      this.setState({isScene2Visible: false, isInProgress: false}),
    );
  };

  onSetScene1Ref = (ref: View | null) => {
    this.setState({scene1Ancestor: nodeFromRef(ref)});
  };

  onSetScene2Ref = (ref: View | null) => {
    this.setState({scene2Ancestor: nodeFromRef(ref)});
  };

  render() {
    const {state} = this;
    const {width} = Dimensions.get('window');
    return (
      <>
        <TouchableOpacity
          style={styles.container}
          activeOpacity={0.5}
          onPress={
            state.isScene2Visible ? this.onPressBack : this.onPressNavigate
          }>
          {/* Scene 1 */}
          <Animated.View
            style={{
              ...StyleSheet.absoluteFillObject,
              transform: [
                {translateX: Animated.multiply(-200, state.progress)},
              ],
            }}>
            <View style={styles.scene} ref={this.onSetScene1Ref}>
              <SharedElement onNode={node => this.setState({scene1Node: node})}>
                <Image
                  style={styles.image1}
                  source={require('本地图片路径')}
                />
              </SharedElement>
            </View>
          </Animated.View>

          {/* Scene 2 */}
          {state.isScene2Visible ? (
            <Animated.View
              style={{
                ...StyleSheet.absoluteFillObject,
                transform: [
                  {
                    translateX: Animated.multiply(
                      -width,
                      Animated.add(state.progress, -1),
                    ),
                  },
                ],
              }}>
              <View style={styles.scene2} ref={this.onSetScene2Ref}>
                <SharedElement
                  onNode={node => this.setState({scene2Node: node})}>
                  <Image
                    style={styles.image2}
                    source={require('本地图片路径')}
                  />
                </SharedElement>
              </View>
            </Animated.View>
          ) : undefined}
        </TouchableOpacity>

        {/* Transition overlay */}
        {state.isInProgress ? (
          <View style={styles.sharedElementOverlay}>
            <SharedElementTransition
              start={{
                node: state.scene1Node,
                ancestor: state.scene1Ancestor,
              }}
              end={{
                node: state.scene2Node,
                ancestor: state.scene2Ancestor,
              }}
              position={state.progress}
              animation="move"
              resize="auto"
              align="auto"
            />
          </View>
        ) : undefined}
      </>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#ecf0f1',
  },
  scene: {
    ...StyleSheet.absoluteFillObject,
    backgroundColor: 'white',
    justifyContent: 'center',
    alignItems: 'center',
  },
  scene2: {
    ...StyleSheet.absoluteFillObject,
    backgroundColor: '#00d8ff',
    justifyContent: 'center',
    alignItems: 'center',
  },
  image1: {
    width: 160,
    height: 160,
  },
  image2: {
    width: 300,
    height: 300,
  },
  sharedElementOverlay: {
    ...StyleSheet.absoluteFillObject,
  },
});

```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

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

1. 通过 har 包引入
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-shared-element": "file:../../node_modules/@react-native-oh-tpl/react-native-shared-element/harmony/shared-element.har"
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

### 3.配置 CMakeLists 和引入 SharedElementPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-shared-element/src/main/cpp" ./shared-element)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_shared_element)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SharedElementPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SharedElementPackage>(ctx),
    };
}
```

### 4.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-shared-element Releases](https://github.com/react-native-oh-library/react-native-shared-element/releases)

## 组件

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### SharedElement

| Name          | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| children      | A single child component, which must map to a real view in the native view hierarchy | element  | yes      | ALL      | yes               |
| onNode        | Event handler that sets or unsets the node-handle            | function | yes      | ALL      | yes               |
| View props... | Other props supported by View                                | NA       | yes      | ALL      | yes               |

### SharedElementTransition

| Name      | Description                                                  | Type                                                         | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| start     | Start node- and ancestor                                     | { node: SharedElementNode, ancestor: SharedElementNode }     | yes      | ALL      | yes               |
| end       | End node- and ancestor                                       | { node: SharedElementNode, ancestor: SharedElementNode }     | yes      | ALL      | yes               |
| position  | Interpolated position (0..1), between the start- and end nodes | number\|Animated.Value\|Reanimated.Value                     | yes      | ALL      | yes               |
| animation | Type of animation, e.g move start element or cross-fade between start- and end elements (default = move) | [SharedElementAnimation](https://github.com/IjzerenHein/react-native-shared-element#SharedElementAnimation) | yes      | ALL      | yes               |
| resize    | Resize behavior (default = auto)                             | [SharedElementResize](https://github.com/IjzerenHein/react-native-shared-element#SharedElementResize) | yes      | ALL      | yes               |
| align     | Alignment behavior (default = auto)                          | [SharedElementAlign](https://github.com/IjzerenHein/react-native-shared-element#SharedElementAlign) | yes      | ALL      | yes               |
| debug     | Renders debug overlays for diagnosing measuring and animations | boolean                                                      | no       | ALL      | yes               |
| onMeasure | Event handler that is called when nodes have been measured and snapshotted | function                                                     | no       | ALL      | yes               |

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### SharedElementAnimation

| Name | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| move      | Moves the start- element to the end position                 | string | no       | ALL      | yes               |
| fade      | Cross-fades between the start- and end elements              | string | no       | ALL      | yes               |
| fade-in   | Fade-in the end element coming from the start position (start-element is not visible) | string | no       | ALL      | yes               |
| fade-out  | Fade-out the start element to the end position (end-element is not visible) | string | no       | ALL      | yes               |

#### SharedElementResize

| Name | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| auto      | Automatically selects the default resize behavior. For images this will perform the best possible transition based on the of the image. For other kinds of views, this will default to .`resizeMode` `stretch` | string | no       | ALL      | yes               |
| stretch   | Stretches the element to the same shape and size of the other element. If the aspect-ratio of the content differs, you may see stretching. In that case consider the or resize options.`clip` `none` | string | no       | ALL      | yes               |
| clip      | Do not resize, but clip the content to the size of the other content. This option is for instance useful in combination with components, where you want to reveal more text.`<Text>` | string | no       | ALL      | yes               |
| none      | Do not resize the content. When combined with , this creates a plain cross-fade effect without any resizing or clipping`fade` | string | no       | ALL      | yes               |

#### SharedElementAlign

| Name          | Description                                                      | Type   | Required | Platform | HarmonyOS Support |
|---------------|------------------------------------------------------------------|--------|----------|----------|-------------------|
| left-center   | Aligns the shared element to the left-center position            | string | no       | ALL      | yes               |
| left-top      | Aligns the shared element to the left-top position               | string | no       | ALL      | yes               |
| left-right    | Aligns the shared element to the left-right position             | string | no       | ALL      | yes               |
| right-center  | Aligns the shared element to the right-center position          | string | no       | ALL      | yes               |
| right-top     | Aligns the shared element to the right-top position              | string | no       | ALL      | yes               |
| right-bottom  | Aligns the shared element to the right-bottom position           | string | no       | ALL      | yes               |
| center-top    | Aligns the shared element to the center-top position             | string | no       | ALL      | yes               |
| center-center | Aligns the shared element to the center-center position         | string | no       | ALL      | yes               |
| center-bottom | Aligns the shared element to the center-bottom position         | string | no       | ALL      | yes               |


## 遗留问题

- [ ] SharedElementTransition中的align属性，鸿蒙侧对标iOS已实现，无法看出效果。当前实现无效果的原因是因为图片占据容器全部位置，无法体现效果。如果扩大容器，在使用时，图片有可能会移出屏幕外，影响使用效果。[issue#3](https://github.com/react-native-oh-library/react-native-shared-element/issues/3)


## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/IjzerenHein/react-native-shared-element/blob/main/LICENSE.txt) ，请自由地享受和参与开源。
