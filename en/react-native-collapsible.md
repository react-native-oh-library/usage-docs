> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-collapsible</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/oblador/react-native-collapsible">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/oblador/react-native-collapsible/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/oblador/react-native-collapsible)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-collapsible@1.6.1
```

#### **yarn**

```bash
yarn add react-native-collapsible@1.6.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React, { useState } from 'react';
import { ScrollView, StyleSheet, Text, View, TouchableOpacity,Button } from 'react-native';
import Collapsible from 'react-native-collapsible';
import Accordion from 'react-native-collapsible/Accordion';
export function CollapsibleExample() {
    const [activeSections, setActiveSections] = useState([0]);
    const [isCollapsed, setIsCollapsed] = useState(true);
    function renderHeader(section: any, _: any, isActive: any) {
        return (<Text>{section.title}</Text>);
    };
    function renderContent(section: any, _: any, isActive: any) {
        return (<Text>{section.content}</Text> );
    }
    return(
        <ScrollView>
         <Accordion
            activeSections={activeSections}
            sections={CONTENT}
            touchableComponent={TouchableOpacity}
            renderHeader={renderHeader}
            renderContent={renderContent}
            duration={400}
            onChange={setActiveSections}
            renderAsFlatList={false}
        />
        <Button title = "open" onPress = {() =>{ setIsCollapsed(!isCollapsed) } } />
            <Collapsible 
                collapsed={isCollapsed}
                onAnimationEnd = { ()=>{ console.log("log:动画结束") } }
                duration = { 100 }
                collapsedHeight = { 0 } >
                <Button title = "aaaaa" />
                <Button title = "bbbbb" />
            </Collapsible>
        </ScrollView>
    );
}
const CONTENT = [
    { title: 'First', feet: '1', content: "a", },
    { title: 'Second', feet: '2', content: "b", },
    { title: 'Third', feet: '3', content: "c", },
];
```


## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.
#### Collapsible
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| **`align`**                   | Alignment of the content when transitioning, can be `top`, `center` or `bottom`                           | enum | no | All | yes |                                                                                                                                                                                       
| **`collapsed`**               | Whether to show the child components or not                                                                | boolean | no | All | yes |                                                                                                                                                                                     
| **`collapsedHeight`**         | Which height should the component collapse to                                                           | number | no | All | yes |                                                                                                                                                                                       
| **`enablePointerEvents`**     | Enable pointer events on collapsed view                                                                   | boolean | no | All | yes |                                                                                                                                                                                         
| **`duration`**                | Duration of transition in milliseconds                                                                   | number | no | All | yes |                                                                                                                                                                                        
| **`easing`**                  | Function or function name from [`Easing`](https://github.com/facebook/react-native/blob/master/Libraries/Animated/src/Easing.js) (or [`tween-functions`](https://github.com/chenglou/tween-functions) if < RN 0.8). Collapsible will try to combine `Easing` functions for you if you name them like `tween-functions`. | string \| function | no | All | yes |
| **`renderChildrenCollapsed`** | Render children in collapsible even if not visible.                                                       | boolean | no | All | yes |                                                                                                                                                                                          
| **`style`**                   | Optional styling for the container                                                                       | object | no | All | yes |                                                                                                                                                                                         
| **`onAnimationEnd`**          | Callback when the toggle animation is done. Useful to avoid heavy layouting work during the animation    | function | no | All | yes |

#### Accordion 
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| **`sections`**                                          | An array of sections passed to the render methods                                                              | array | no | All | yes |
| **`renderHeader(content, index, isActive, sections)`**  | A function that should return a renderable representing the header                                             | function | no | All | yes |
| **`renderContent(content, index, isActive, sections)`** | A function that should return a renderable representing the content                                            | function | no | All | yes |
| **`renderFooter(content, index, isActive, sections)`**  | A function that should return a renderable representing the footer                                             | function | no | All | yes |
| **`renderSectionTitle(content, index, isActive)`**      | A function that should return a renderable representing the title of the section outside the touchable element | function | no | All | yes |
| **`onChange(indexes)`**                                 | A function that is called when the currently active section(s) are updated.                                    | function | no | All | yes |
| **`keyExtractor(item, index)`**                         | Used to extract a unique key for a given item at the specified index.                                          | function | no | All | yes |
| **`activeSections`**                                    | Control which indices in the `sections` array are currently open. If empty, closes all sections.               | array | no | All | yes |
| **`underlayColor`**                                     | The color of the underlay that will show through when tapping on headers. Defaults to black.                   | string | no | All | yes |
| **`touchableComponent`**                                | The touchable component used in the Accordion. Defaults to `TouchableHighlight`                                | object | no | All | yes |
| **`touchableProps`**                                    | Properties for the `touchableComponent`                                                                        | object | no | All | yes |
| **`disabled`**                                          | Set whether the user can interact with the Accordion                                                           | boolean | no | All | yes |
| **`align`**                                             | See `Collapsible`                                                                                              | enum | no | All | yes |
| **`duration`**                                          | See `Collapsible`                                                                                              | number | no | All | yes |
| **`easing`**                                            | See `Collapsible`                                                                                              | string \| function | no | All | yes |
| **`onAnimationEnd(key, index)`**                        | See `Collapsible`.                                                                                             | function | no | All | yes |
| **`expandFromBottom`**                                  | Expand content from the bottom instead of the top                                                              | boolean | no | All | yes |
| **`expandMultiple`**                                    | Allow more than one section to be expanded. Defaults to false.                                                 | boolean | no | All | yes |
| **`sectionContainerStyle`**                             | Optional styling for the section container.                                                                    | object | no | All | yes |
| **`containerStyle`**                                    | Optional styling for the Accordion container.                                                                  | object | no | All | yes |
| **`renderAsFlatList`**                                  | Optional rendering as FlatList (defaults to false).                                                            | boolean | no | All | yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/oblador/react-native-collapsible/blob/master/LICENSE).