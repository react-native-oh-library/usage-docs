> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@th3rdwave/react-navigation-bottom-sheet</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/th3rdwave/react-navigation-bottom-sheet">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/th3rdwave/react-navigation-bottom-sheet/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/th3rdwave/react-navigation-bottom-sheet)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @th3rdwave/react-navigation-bottom-sheet@0.3.2
```

#### **yarn**

```bash
yarn add @th3rdwave/react-navigation-bottom-sheet@0.3.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!TIP] 本示例依赖 react-native-gesture-handler 库，参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)进行引入。

```js
import * as React from 'react';
import { StyleSheet, Dimensions, View, Button, Text } from 'react-native';
import { GestureHandlerRootView } from 'react-native-gesture-handler';
import {
  BottomSheetBackdrop,
  BottomSheetBackdropProps,
} from '@gorhom/bottom-sheet';
import { NavigationContainer } from '@react-navigation/native';
import {
  BottomSheetScreenProps,
  createBottomSheetNavigator,
} from '@th3rdwave/react-navigation-bottom-sheet';


type BottomSheetParams = {
  Home: undefined;
  Sheet: { id: number };
  BigSheet: { id: number };
};

const BottomSheet = createBottomSheetNavigator<BottomSheetParams>();

function HomeScreen({
  navigation,
}: BottomSheetScreenProps<BottomSheetParams, 'Home'>) {
  return (
    <View style={styles.container}>
      <Text style={{ color: 'black' }}>Home Screen</Text>
      <View style={styles.spacer} />
      <Button
        title="Open sheet"
        onPress={() => {
          navigation.navigate('Sheet', { id: 1 });
        }}
      />
      <View style={styles.spacer} />
      <Button
        title="Open a big sheet"
        onPress={() => {
          navigation.navigate('BigSheet', { id: 1 });
        }}
      />
    </View>
  );
}

function SheetScreen({
  route,
  navigation,
}: BottomSheetScreenProps<BottomSheetParams, 'Sheet'>) {
  let timer: any = null

  React.useEffect(() => {
    return () => {
      clearTimeout(timer)
    }
  })

  return (
    <View style={[styles.container, styles.content]}>
      <Text>Sheet Screen {route.params.id}</Text>
      <View style={styles.spacer} />
      <Button
        title="Open new sheet"
        onPress={() => {
          navigation.navigate('Sheet', { id: route.params.id + 1 });
        }}
      />
      <View style={styles.spacer} />
      <Button
        title="Open new big sheet"
        onPress={() => {
          navigation.navigate('BigSheet', { id: route.params.id + 1 });
        }}
      />
      <View style={styles.spacer} />
      <Button
        title="Close this sheet"
        onPress={() => {
          navigation.goBack();
        }}
      />
      <View style={styles.spacer} />
      {route.name === ('BigSheet' as unknown) && (
        <>
          <Button
            title="Snap to top"
            onPress={() => {
              timer = setTimeout(() => {
                navigation.snapTo(1);
              })
            }}
          />
        </>
      )}
    </View>
  );
}

const renderBackdrop = (props: BottomSheetBackdropProps) => (
  <BottomSheetBackdrop {...props} appearsOnIndex={0} disappearsOnIndex={-1} />
);

function SimpleExample() {
  return (
    <NavigationContainer>
      <BottomSheet.Navigator
        screenOptions={{
          backdropComponent: renderBackdrop,
        }}
      >
        <BottomSheet.Screen name="Home" component={HomeScreen} />
        <BottomSheet.Screen
          name="Sheet"
          component={SheetScreen}
          getId={({ params }) => `sheet-${params.id}`}
        />
        <BottomSheet.Screen
          name="BigSheet"
          component={SheetScreen}
          options={{
            snapPoints: ['70%', '90%'],
          }}
          getId={({ params }) => `sheet-${params.id}`}
        />
      </BottomSheet.Navigator>
    </NavigationContainer>
  );
}

export function BottomExample() {
  return (
    <GestureHandlerRootView style={styles.container1}>
        <SimpleExample />
    </GestureHandlerRootView>
  );
}

const styles = StyleSheet.create({
  container1: {
    flex: 1,
  },
  container: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
  },
  content: {
    marginVertical: 20,
  },
  spacer: {
    margin: 5,
  },
  bottom: {
    display: 'flex',
    flexDirection: 'row'
  }
});

```
## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-gesture-handler、@react-native-oh-tpl/react-native-reanimated、@react-native-oh-tpl/bottom-sheet的原生端代码，如已在鸿蒙工程中引入过这三个库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)、[@react-native-oh-tpl/react-native-reanimated 文档](/zh-cn/react-native-reanimated.md)、[@react-native-oh-tpl/bottom-sheet 文档](/zh-cn/gorhom-bottom-sheet.md)进行引入

## 约束与限制

### 兼容性


本文档内容基于以下版本验证通过：

1. RNOH: 0.72.29; SDK: HarmonyOS-NEXT-DB6 5.0.0.61 (API Version 12 Beta6); IDE: DevEco Studio 5.0.3.706; ROM: 3.0.0.61;
## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


### Navigation options

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| snapPoints  | Points for the bottom sheet to snap to, points should be sorted from bottom to top. It accepts array of number and string.    | Array<string>  | YES | ALL      | YES |
| backgroundStyle  | View style to be applied to the background component.    | ViewStyle  | NO | ALL      | YES |
| index  | Initial snap index. You also could provide -1 to initiate bottom sheet in closed state.    | number  | NO | ALL      | YES |
| detached  | Defines whether the bottom sheet is attached to the bottom or no.  | boolean  | NO | ALL      | YES |
| overDragResistanceFactor  | Defines how violently sheet has to be stopped while over dragging.  | number  | NO |   ALL    | YES |
| enableOverDrag  | Enable over drag for the sheet.  | boolean  | NO |   ALL    | YES |
| enablePanDownToClose  | Enable pan down gesture to close the sheet.  | boolean  | NO |ALL| YES |
| enableHandlePanningGesture  | Enable handle panning gesture interaction.  | boolean  | NO |ALL| YES |
| enableContentPanningGesture  | Enable content panning gesture interaction. | boolean  | NO |ALL| YES |
| enableDynamicSizing  | Enable dynamic sizing for content view and scrollable content size.  | boolean  | NO | ALL      | YES |
| animateOnMount  | This will initially mount the sheet closed and when it's mounted and calculated the layout, it will snap to initial snap point index.  | boolean  | NO | ALL      | YES |
| style  | View style to be applied at the sheet container, it also could be an AnimatedStyle. This is helpful to add shadow to the sheet.  | ViewStyle  | NO | ALL      | YES |
| handleStyle  | View style to be applied to the handle component. | ViewStyle   | NO | ALL      | YES |
| handleIndicatorStyle  | View style to be applied to the handle indicator component. | ViewStyle  | NO | ALL      | YES |
| handleHeight  | Handle height helps to calculate the internal container and sheet layouts. If handleComponent is provided, the library internally will calculate its layout, unless handleHeight is provided too.| number  | NO | ALL      | NO |
| contentHeight  | Content height helps dynamic snap points calculation.| number  | NO | ALL      | YES |
| topInset  | Top inset to be added to the bottom sheet container, usually it comes from @react-navigation/stack hook useHeaderHeight or from react-native-safe-area-context hook useSafeArea.| number  | NO | ALL      | YES |
| bottomInset  |Bottom inset to be added to the bottom sheet container.| number  | NO | ALL      | YES |
| maxDynamicContentSize  |Max dynamic content size height to limit the bottom sheet height from exceeding a provided size.| number  | NO |    ALL     | YES |
| keyboardBehavior  |Defines the keyboard appearance behavior.| 'extend' or 'fillParent' or 'interactive'  | NO |NO| NO |
| keyboardBlurBehavior  |Defines the keyboard blur behavior.| 'none' or 'restore'  | NO |    NO   | NO |
| animationConfigs  |Animation configs, this could be created by:|function  | NO |   ALL    | YES |
| handleComponent  |Component to be placed as a sheet handle.|React.FC\<BottomSheetHandleProps>  | NO | ALL      | YES |
| backdropComponent  |Component to be placed as a sheet backdrop, by default is set to null, however the library also provide a default implementation BottomSheetBackdrop of a backdrop but you will need to provide it manually.|React.FC\<BottomSheetBackgroundProps>  | NO | ALL      | YES |
| backgroundComponent  |Component to be placed as a sheet background.|React.FC\<BottomSheetBackgroundProps> | NO | ALL      | YES |
| footerComponent  |Component to be placed as a sheet footer.|React.FC\<BottomSheetFooterProps>  | NO | ALL      | YES |


### Navigation helpers

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| snapTo  | Snaps the current sheet to index.    | (index: number) => void  | NO | ALL      | YES |


## 遗留问题

## 其他
- keyboardBehavior属性暂不支持，与iOS表现一致。[issue#24](https://github.com/th3rdwave/react-navigation-bottom-sheet/issues/24)
- keyboardBlurBehavior属性暂不支持，与iOS表现一致。[issue#25](https://github.com/th3rdwave/react-navigation-bottom-sheet/issues/25)
- handleHeight属性暂不支持，与iOS表现一致。[issue#30](https://github.com/th3rdwave/react-navigation-bottom-sheet/issues/30)

## 开源协议

本项目基于 [The MIT License (MIT )](https://github.com/th3rdwave/react-navigation-bottom-sheet/blob/main/LICENSE) ，请自由地享受和参与开源。