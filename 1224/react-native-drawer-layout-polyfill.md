模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-drawer-layout-polyfill</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/rnc-archive/react-native-drawer-layout-polyfill">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/rnc-archive/react-native-drawer-layout-polyfill)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-drawer-layout-polyfill@2.0.0
```

#### **yarn**

```bash
yarn add react-native-drawer-layout-polyfill@2.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useState, useRef } from "react";
import { Button, Text, StyleSheet, View, TextInput } from "react-native";
import DrawerLayout from 'react-native-drawer-layout-polyfill';

const App = () => {
  const drawerLayoutRef = useRef(null)
  const [drawerPosition, setDrawerPosition] = useState("left");
  const [keyboardDismissMode, setKeyboardDismissMode] = useState("none");
  const [drawerLockMode, setDrawerLockMode] = useState("unlocked ");
  const [isOpen, setIsOpen] = useState("关闭 ");
  const [drawerSlideOutput, setDrawerSlideOutput] = useState("");
  const [drawerStateChangedOutput, setDrawerStateChangedOutput] = useState("");
  const [drawerWidth, setDrawerWidth] = useState(300);
  const [value, onChangeText] = useState("");


  const open = () =>{
    drawerLayoutRef.current.openDrawer()
  }

  const close = () =>{
    drawerLayoutRef.current.closeDrawer()
  }

  const changeDrawerPosition = () => {
    console.log('drawerPosition-修改弹框位置', drawerPosition);
    if (drawerPosition === "left") {
      setDrawerPosition("right");
    } else {
      setDrawerPosition("left");
    }
  };

  const changeDrawerHideKeyboard = () => {
    console.log('keyboardDismissMode-是否隐藏软键盘', keyboardDismissMode);
    if (keyboardDismissMode === "none") {
      setKeyboardDismissMode("on-drag");
    } else {
      setKeyboardDismissMode("none");
    }
  };

  const changeDrawerWidth = () => {
    console.log('drawerWidth-修改弹框宽度', drawerWidth);
    if(value && Number(value) >=  100 ) {
      setDrawerWidth(Number(value))
    }
  }

  const changeDrawerLockMode = (type) => {
    console.log('drawerLockMode-修改弹框锁定模式', type);
    setDrawerLockMode(type)
  };

  const handleDrawerOpen = (e) =>{
    console.log('onDrawerOpen-打开弹框的回调');
    setIsOpen('打开')
  }

  const handleDrawerClose = (e) =>{
    console.log('onDrawerClose-关闭弹框的回调');
    setIsOpen('关闭')
  }

  const handleDrawerSlide = (e) =>{
    console.log('onDrawerSlide-导航视图发生交互时的回调函数');
    setDrawerSlideOutput(JSON.stringify(e.nativeEvent))
  }

  const handleDrawerStateChanged = (e) =>{
    console.log('onDrawerStateChanged-导航视图的状态发生变化时的回调函数');
    setDrawerStateChangedOutput(JSON.stringify(e))
  }


  const navigationView = (
    <View style={styles.navigationContainer}>
      <Text  style={styles.textCommon}>I'm in the Drawer!</Text>
      <Text style={styles.textCommon}>弹框状态:{isOpen}</Text>
      <Text style={styles.textCommon}>弹框打开关闭过程中触发:{drawerSlideOutput}</Text>
      <Text style={styles.textCommon}>弹框状态切换触发:{drawerStateChangedOutput}</Text>
      <Button style={styles.buttonMargin} title="关闭弹框" onPress={() => close()}/>
    </View>
  );

  return (
    <DrawerLayout
      ref={drawerLayoutRef}
      drawerWidth={drawerWidth}
      drawerPosition={drawerPosition}
      renderNavigationView={() => navigationView}
      keyboardDismissMode={keyboardDismissMode}
      drawerLockMode={drawerLockMode}
      drawerBackgroundColor="red"
      statusBarBackgroundColor="blue"
      onDrawerOpen={handleDrawerOpen}
      onDrawerClose={handleDrawerClose}
      onDrawerSlide={handleDrawerSlide}
      onDrawerStateChanged={handleDrawerStateChanged}
    >
      <View style={styles.container}>
        <Text style={styles.textCommon}>设置导航视图的锁定模式:{drawerLockMode}</Text>
        <Text style={styles.textCommon}>是否隐藏软键盘:{keyboardDismissMode}</Text>
        <Text style={styles.textCommon}>弹框状态:{isOpen}</Text>
        <Text style={styles.textCommon}>弹框打开关闭过程中触发:{drawerSlideOutput}</Text>
        <Text style={styles.textCommon}>弹框状态切换触发:{drawerStateChangedOutput}</Text>
        <Button title="打开弹框" onPress={() => open()}/>
        <View style={styles.buttonMargin}></View>
        <Button title="改变弹框位置" onPress={() => changeDrawerPosition()}/>
        <View style={styles.buttonMargin}></View>
        <Button title="弹框动画过程中是否隐藏键盘" onPress={() => changeDrawerHideKeyboard()}/>
        <View style={styles.buttonMargin}></View>
        <Button title="设置导航视图的锁定模式- unlocked " onPress={() => changeDrawerLockMode("unlocked")}/>
        <View style={styles.buttonMargin}></View>
        <Button title="设置导航视图的锁定模式- locked-closed" onPress={() => changeDrawerLockMode("locked-closed")}/>
        <View style={styles.buttonMargin}></View>
        <Button title="设置导航视图的锁定模式- locked-open" onPress={() => changeDrawerLockMode("locked-open")}/>
        <View style={styles.buttonMargin}></View>
        <TextInput
          style={{ height: 40, borderColor: 'gray', borderWidth: 1, width:300 }}
          onChangeText={text => onChangeText(text)}
          value={value}
        />
        <View style={styles.buttonMargin}></View>
        <Button title="修改弹框宽度" onPress={() => changeDrawerWidth()}/>
      </View>
    </DrawerLayout>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
    paddingTop: 50,
    padding: 8
  },
  navigationContainer: {
    flex: 1,
    paddingTop: 50,
    padding: 8
  },
  textCommon: {
    marginBottom:10,
    fontSize:15
  },
  buttonMargin:{
    marginBottom:5,
  },

});

export default App;
```

## 兼容性

在以下版本验证通过

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;

## 属性

详情见[react-native-drawer-layout-polyfill](https://www.reactnative.cn/docs/drawerlayoutandroid)



| 名称                     | 说明                                                                                                                                                                                                                                                 | 类型     | 是否必填 | 原库平台    | 鸿蒙支持 |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------|-------------|----------|
| renderNavigationView     | 被拉入的导航视图的内容。                                                                                                                                                                                                                              | function | 是      | Android IOS | 是       |
| drawerPosition           | 设置导航视图从屏幕的哪一边拉入。'left' 左侧拉出   'right' 右侧拉出                                                                                                                                                                                     | string   | 否      | Android IOS | 是       |
| drawerWidth              | 设置导航视图从窗口边缘拉入的视图的宽度。                                                                                                                                                                                                               | number   | 否      | Android IOS | 是       |
| keyboardDismissMode      | 设置拖动过程中是否隐藏软键盘。'none' (默认)，拖动时不隐藏软键盘。'on-drag'，拖动时隐藏软键盘。                                                                                                                                                          | string   | 否      | Android IOS | 是       |
| drawerLockMode           | 设置导航视图的锁定模式。有 3 种状态：unlocked (默认)，不锁定，导航视图可以响应打开和关闭操作；locked-closed，导航视图保持关闭，不能用手势打开；locked-open，导航视图保持打开，不能用手势关闭，但仍然可以通过程序打开或关闭。 (`openDrawer`/`closeDrawer`). | string   | 否      | Android IOS | 是       |
| drawerBackgroundColor    | 设置导航视图的背景颜色。默认值为白色。如果你想设置导航视图的不透明度，请使用 rgba。                                                                                                                                                                     | string   | 否      | Android IOS | 是       |
| statusBarBackgroundColor | 使抽屉占满整个屏幕，并设置状态栏颜色(支持 API21+/安卓系统 5.0 以上) 使导航视图占满整个屏幕，并设置状态栏背景，允许他在状态栏上打开。仅在 API 21 及以上版本有效。不支持IOS和harmony。                                                                      | string   | 否      | Android     | 不支持   |
| onDrawerOpen             | 导航视图被打开后的回调函数。                                                                                                                                                                                                                           | function | 否      | Android IOS | 是       |
| onDrawerClose            | 导航视图被关闭后的回调函数。                                                                                                                                                                                                                           | function | 否      | Android IOS | 是       |
| onDrawerSlide            | 导航视图发生交互时的回调函数。                                                                                                                                                                                                                         | function | 否      | Android IOS | 是       |
| onDrawerStateChanged     | 导航视图的状态发生变化时的回调函数。有 3 种状态：idle, 导航视图没有发生任何交互；dragging, 导航视图正在发生交互；settling，导航视图正在发生交互，并且导航视图正在完成其关闭或打开的动画。                                                                 | function | 否      | Android IOS | 是       |



## 方法

| 名称        | 说明          | 是否必填  | 原库平台    | 鸿蒙支持 |
|-------------|---------------|-----------|-------------|---------|
| openDrawer  | 打开导航视图。 | 否       | Android IOS | 是       |
| closeDrawer | 关闭导航视图。 | 否       | Android IOS | 是       |



## 遗留问题

## 其他
