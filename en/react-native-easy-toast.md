> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-easy-toast</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/crazycodeboy/react-native-easy-toast">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/crazycodeboy/react-native-easy-toast/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/crazycodeboy/react-native-easy-toast)


## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-easy-toast@2.3.0
```

#### **yarn**

```bash
yarn add react-native-easy-toast@2.3.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React, { Component } from "react";
import { Text, View, Button } from "react-native";
import {
  Toast
} from "react-native-easy-toast";

export default class App extends Component {
    constructor(props) {
        super(props);
    }
    render() {
      return (
        <View>
            <Button title={'Press me'} onPress={()=>{
                this.toast.show('hello world!',2000);
            }}/>
            <Toast ref={(toast) => this.toast = toast}/>
        </View>
      )
    }
}


```

More usage scenarios can be viewed [react-native-easy-toast](https://github.com/crazycodeboy/react-native-easy-toast)

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2(B.0.73); IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.58;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;


## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.
>
> For details, see [react-native-easy-toast](https://github.com/crazycodeboy/react-native-easy-toast)

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style  | Custom style toast | View.propTypes.style  | no | All | yes |
| position  | Custom toast position | PropTypes.oneOf(['top','center','bottom',])  | no | All | yes |
| positionValue  | Custom toast position value | React.PropTypes.number | no | All | yes |
| fadeInDuration  | Custom toast show duration | React.PropTypes.number  | no | All | yes |
| fadeOutDuration  | Custom toast close duration | React.PropTypes.number  | no | All | yes |
| opacity  | Custom toast opacity | React.PropTypes.number  | no | All | yes |
| textStyle  | Custom style text | View.propTypes.style  | no | All | yes |

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show  | show a toast,unit is millisecond，and do callback  | (text: string, duration: number, callback: function, onPress: function)  | no | All      | yes |
| close  | start the close timer  | -  | no | All | yes |

## Known Issues

## Others

## License

This project is licensed under [MIT Licensed](https://github.com/crazycodeboy/react-native-easy-toast/blob/master/LICENSE).
