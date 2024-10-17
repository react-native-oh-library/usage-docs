> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-scrollable-tabview</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/itenl/react-native-scrollable-tabview">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/itenl/react-native-scrollable-tabview/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/itenl/react-native-scrollable-tabview)


## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @itenl/react-native-scrollable-tabview@1.1.7
```

#### **yarn**

```bash
yarn add @itenl/react-native-scrollable-tabview@1.1.7
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useEffect, useRef } from 'react';
import { View, Text, Alert, Button } from 'react-native'
import ScrollableTabView from '@itenl/react-native-scrollable-tabview';

export default function ScrollTabsDemo() {

  let [scrollDate, setScrollDate] = useState(Date.now())
  const myRef = useRef<any>(null);

  //  console.error('test')

  return (
    <View style={{ flex: 1 }}>
      <ScrollableTabView
        ref={myRef}
        stacks={[
          {
            screen: ({ onRefresh }: any) => {
              onRefresh((toggled: (arg0: boolean) => void) => {
                setScrollDate(Date.now())
              });
              return (<View style={{ flex: 1, backgroundColor: 'blue', height: 2000 }}><Text>one{scrollDate}</Text></View>)
            },
          }, {
            screen: () => <View style={{ flex: 1, backgroundColor: 'grey', height: 2000 }}><Text>two{scrollDate}</Text></View>,
          },
          {
            screen: () => {
              return (
                <View
                  style={{
                    flex: 1,
                    backgroundColor: "green",
                    justifyContent: "center",
                    alignItems: "center",
                    height: 2000
                  }}
                >
                  <Text>
                    {Date.now()} {scrollDate}
                  </Text>
                </View>
              );
            },
          }
        ]}
        mappingProps={{}}
        tabsStyle={{ backgroundColor: 'yellow', }}
        tabWrapStyle={{ zIndex: 1 }}
        tabInnerStyle={{ paddingLeft: 5 }}
        tabActiveOpacity={0}
        tabStyle={{ backgroundColor: 'orange', width: 100 }}
        textStyle={{ textAlign: 'center', color: 'green' }}
        textActiveStyle={{ fontSize: 30 }}
        tabUnderlineStyle={{ backgroundcolor: 'red', height: 10 }}
        firstIndex={0}
        syncToSticky={true}
        onEndReachedThreshold={0.4}
        onTabviewChanged={(index: any, tabLabel: any, isFirst: any) => {
          setScrollDate(index + tabLabel + isFirst)
        }}
        screenScrollThrottle={100}
        header={() => {
          return <View style={{ backgroundColor: 'pink', height: 80 }}><Text>header</Text></View>;
        }}
      ></ScrollableTabView>
    </View>
  );
}
```



## Constraints

### Compatibility
To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

This document is verified based on the following versions:

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;
2. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1 B.0.18、HarmonyOS NEXT Developer Preview0 B.0.60、HarmonyOS NEXT Developer Preview2 B.0.73; IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.18;
3. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;


## Properties 

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required |   HarmonyOS Support  |
| ---- | ----------- | ---- | -------- |  ------------------ |
stacks | Page stack < [Read Stack Property](#StackProperty) >| Array | / | yes
mappingProps | Associate mapped data to Stack / Sticky | Object | / | yes
badges | Badge for each tab< [Read Badge Property](#BadgeProperty) >| Array | / | yes
tabsStyle |The entire Tabs style | Object | / | yes
tabWrapStyle | Single Tab wrap style (The function parameters provide item, index, and need to return the style object, eg. **`return index == 1 && {zIndex: 10}`**)| Object   / Function | / | yes
tabInnerStyle | Single Tab inner style | Object | / | yes
tabActiveOpacity | Transparency after Tab button click | Number | / | yes
tabStyle | Single Tab style | Object | / | yes
textStyle | Text style in Tab | Object | / | yes
textActiveStyle | Select the active text style | Object | / | yes
tabUnderlineStyle | Select the active underline style | Object | / | yes
firstIndex | Set the stack of **`firstIndex`** to active (make sure that the number of **`stacks`** is greater than to **`firstIndex`** when setting the **`firstIndex`** value) | Number   / Null | / | yes
syncToSticky | Whether it is synchronized (**`render`** triggered in the Screen **`componentDidUpdate`** will update Sticky) | Boolean | / | yes
onEndReachedThreshold | Bottom callback threshold | Number | / | yes
onBeforeRefresh | Pull down to refresh the pre-functions, execute **`next`** to execute **`onRefresh`** function in Screen, execute **`toggled`** to switch system loading, you can pass true / false to specify (callback contains **`next`**, **`toggled`** two formal parameters) | Function | / | yes
onBeforeEndReached |  Slide up to load more pre-functions, execute next will execute the **`onEndReached`** function in the Screen (callback contains **`next`** formal parameters) | Function | / | yes
onTabviewChanged |Tab switch completion callback (callback contains **`index`**, **`tabLabel`**, **`isFirst`** parameters) | Function | / | yes
screenScrollThrottle | **`Screen`** Throttle parameters during lateral sliding, Unit (ms)| Number | / | yes
header | Top component (if the function needs to return Element)| Function   / JSX Element / Class Component | / | yes
stickyHeader | Top component (if the function needs to return Element) for sticky| Function   / JSX Element / Class Component | / | yes
oneTabHidden | Hide itself when there is only one Tab | Boolean | / | yes
enableCachePage |  Whether the persistent page will not be destroyed after switching | Boolean | / | yes
carouselProps | The remaining attributes passed to Carousel< [Read Carousel](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/PROPS_METHODS_AND_GETTERS.md) >| Object | / | yes
sectionListProps | Remaining attributes passed to SectionList< [Read SectionList](https://reactnative.dev/docs/sectionlist) >| Object | / | yes
toHeaderOnTab | Click to trigger the activated Tab will scroll to Header (high priority) | Boolean | / | yes
toTabsOnTab | Click to trigger the activated Tab will scroll to Tabs| Boolean | / | yes
tabsShown |  Configure Tabs display and hide | Boolean | / | yes
fixedTabs | When **`enableCachePage`** is true, slide to switch Screen to set the minimum height to ensure that the Header and Tabs will not bounce | Boolean | / | yes
fixedHeader | Render together with Tabs, fix the top Header, do not follow the scroll | Boolean | / | yes
useScroll | Does Tabs support horizontal scrolling (it needs to be enabled when there are multiple category Tabs, it is recommended that **`tabStyle`** pass in a fixed width)| Boolean | / | yes
useScrollStyle |Set **`contentContainerStyle`** for scrolling **`Tabs`**, usually add margins to the left and right sides **`paddingLeft`** **`paddingHorizontal`** | Object | / | yes
fillScreen | Fill the entire Screen | Boolean | / | yes
title | Animation title | Function   / JSX Element / Class Component | / | yes
titleArgs | Title parameter configuration < [Read interpolate](https://reactnative.dev/docs/animations#interpolation) >| Object | / | yes
onScroll | Scroll event monitoring | Function | / | yes
onScroll2Horizontal | Scroll event monitoring for orizontal | Function | / | yes
tabsEnableAnimated | Enable sliding effect for Tabs, Need to specify **`width`** for **`tabStyle`** | Boolean for TabStyle | / | yes
tabsEnableAnimatedUnderlineWidth | To set a fixed width for the Tabs Underline and add a jumping animation, you need to enable **`tabsEnableAnimated=true`**. (It is recommended to pass in one third of **`tabStyle.width`** or a fixed 30px) | Number | / | yes
errorToThrow |**`console.error`** will throw an error **`throw new Error()`** | Boolean | / | yes

## stack Properties 
Name | Description | Type | Required | HarmonyOS   Support
-- | -- | -- | -- | --
screen | Screen components | Class   Component | / | yes 
sticky | Ceiling component. The context of the component is returned in the instance. | Class   Component | / | yes 
tabLabel | Tab Nickname                                                 | String | / | yes 
tabLabelRender | Customized tab rendering function, which has a higher priority than tabLabel. | Function | / | yes 
badge | Badge for the current tab, which is mutually exclusive with the badges attribute and has a higher priority than the outermost attribute badges | Array | / | yes 
toProps | toProps is transferred only to the screen and is not associated with data | Object | / | yes 

## Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


Name | Description | Type | Required | HarmonyOS   Support
-- | -- | -- | -- | --
getCurrentRef(index:   number.optional) | Obtains the instance of the current active view. You can transfer the index to obtain the specified instance | Function | / | yes 
toTabView(index:   number.required / label: string.required) | Go to the specified screen.                                  | Function | / | yes 
scrollTo(index:   number.required) | Slide up and down to the specified position (By default, if 0 is input, the tab is located./If a negative number is input, the tab is pinned to the top) | Function | / | yes 
clearStacks(callback:   function.optional) | Clear the stack and related status (Tabs / Badge / Stacks) | Function | / | yes 


## Others

## License

This project is licensed under  [The MIT License (MIT)](https://github.com/itenl/react-native-scrollable-tabview/blob/main/LICENSE) .
