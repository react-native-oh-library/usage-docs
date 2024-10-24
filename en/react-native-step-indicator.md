> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-step-indicator</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/24ark/react-native-step-indicator">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/24ark/react-native-step-indicator/blob/master/LICENSE">
        <!-- <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" /> -->
        <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/24ark/react-native-step-indicator)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-step-indicator@1.0.3 --save
```

#### **yarn**

```bash
yarn add react-native-step-indicator@1.0.3
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

#### Using a Component

```js
import * as React from 'react';
import { StyleSheet, View, Text } from 'react-native';
import StepIndicator from 'react-native-step-indicator';

const firstIndicatorStyles = {
  stepIndicatorSize: 30,
  currentStepIndicatorSize: 40,
  separatorStrokeWidth: 3,
  currentStepStrokeWidth: 5,
  separatorFinishedColor: '#4aae4f',
  separatorUnFinishedColor: '#a4d4a5',
  stepIndicatorFinishedColor: '#4aae4f',
  stepIndicatorUnFinishedColor: '#a4d4a5',
  stepIndicatorCurrentColor: '#ffffff',
  stepIndicatorLabelFontSize: 15,
  currentStepIndicatorLabelFontSize: 15,
  stepIndicatorLabelCurrentColor: '#000000',
  stepIndicatorLabelFinishedColor: '#ffffff',
  stepIndicatorLabelUnFinishedColor: 'rgba(255,255,255,0.5)',
  labelColor: '#666666',
  labelSize: 12,
  currentStepLabelColor: '#4aae4f',
};

const secondIndicatorStyles = {
  stepIndicatorSize: 30,
  currentStepIndicatorSize: 40,
  separatorStrokeWidth: 2,
  currentStepStrokeWidth: 3,
  stepStrokeCurrentColor: '#fe7013',
  stepStrokeWidth: 3,
  separatorStrokeFinishedWidth: 4,
  stepStrokeFinishedColor: '#fe7013',
  stepStrokeUnFinishedColor: '#aaaaaa',
  separatorFinishedColor: '#fe7013',
  separatorUnFinishedColor: '#aaaaaa',
  stepIndicatorFinishedColor: '#fe7013',
  stepIndicatorUnFinishedColor: '#ffffff',
  stepIndicatorCurrentColor: '#ffffff',
  stepIndicatorLabelFontSize: 13,
  currentStepIndicatorLabelFontSize: 13,
  stepIndicatorLabelCurrentColor: '#fe7013',
  stepIndicatorLabelFinishedColor: '#ffffff',
  stepIndicatorLabelUnFinishedColor: '#aaaaaa',
  labelColor: '#999999',
  labelSize: 13,
  currentStepLabelColor: '#fe7013',
};

const thirdIndicatorStyles = {
  stepIndicatorSize: 25,
  currentStepIndicatorSize: 30,
  separatorStrokeWidth: 2,
  currentStepStrokeWidth: 3,
  stepStrokeCurrentColor: '#7eaec4',
  stepStrokeWidth: 3,
  stepStrokeFinishedColor: '#7eaec4',
  stepStrokeUnFinishedColor: '#dedede',
  separatorFinishedColor: '#7eaec4',
  separatorUnFinishedColor: '#dedede',
  stepIndicatorFinishedColor: '#7eaec4',
  stepIndicatorUnFinishedColor: '#ffffff',
  stepIndicatorCurrentColor: '#ffffff',
  stepIndicatorLabelFontSize: 0,
  currentStepIndicatorLabelFontSize: 0,
  stepIndicatorLabelCurrentColor: 'transparent',
  stepIndicatorLabelFinishedColor: 'transparent',
  stepIndicatorLabelUnFinishedColor: 'transparent',
  labelColor: '#999999',
  labelSize: 13,
  currentStepLabelColor: '#7eaec4',
};

export default function App() {
  const [currentPage, setCurrentPage] = React.useState<number>(0);

  const onStepPress = (position: number) => {
    setCurrentPage(position);
  };

  const renderStepIndicator = (params: any) => (
    <Text>good</Text>
  );

  const renderLabel = ({
    position,
    stepStatus,
    label,
    currentPosition,
  }: {
    position: number;
    stepStatus: string;
    label: string;
    currentPosition: number;
  }) => {
    return (      
      <Text
        style={
          position === currentPosition
            ? styles.stepLabelSelected
            : styles.stepLabel
        }
      >
        {label}
      </Text>
    );
  };

  return (
    <View style={styles.container}>
      <View style={styles.stepIndicator}>
        <StepIndicator
          customStyles={firstIndicatorStyles}
          currentPosition={currentPage}
          labels={['Account', 'Profile', 'Band', 'Membership', 'Dashboard']}
          renderLabel={renderLabel}
          onPress={onStepPress}
        />
      </View>
      <View style={styles.stepIndicator}>
        <StepIndicator
          customStyles={secondIndicatorStyles}
          currentPosition={currentPage}
          onPress={onStepPress}
          renderStepIndicator={renderStepIndicator}
          labels={[
            'Cart',
            'Delivery Address',
            'Order Summary',
            'Payment Method',
            'Track',
          ]}
        />
      </View>
      <View style={styles.stepIndicator}>
        <StepIndicator
          stepCount={4}
          customStyles={thirdIndicatorStyles}
          currentPosition={currentPage}
          onPress={onStepPress}
          labels={['Approval', 'Processing', 'Shipping', 'Delivery']}
        />
      </View>
      
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#ffffff',
  },
  stepIndicator: {
    marginVertical: 50,
  },
  page: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  stepLabel: {
    fontSize: 12,
    textAlign: 'center',
    fontWeight: '500',
    color: '#999999',
  },
  stepLabelSelected: {
    fontSize: 12,
    textAlign: 'center',
    fontWeight: '500',
    color: '#4aae4f',
  },
});
```

### 在 ArkTs 侧引入和注册字体文件(非必选配置项)

> [!TIP] 本项非必配项，当使用 customStyles 自定义Properties中的 labelFontFamily Properties指定字体时才需配置

步骤一：
复制字体文件到 `entry/src/main/resources/rawfile/assets/assets/fonts` 目录下(如使用了外部字体文件，需要将\*.ttf 文件复制过来)

步骤二：
打开 `entry/src/main/ets/pages/Index.ets`，添加以下代码

    const fonts: Record<string, Resource> = {
      "Pacifico-Regular": $rawfile("assets/assets/fonts/Pacifico-Regular.ttf")
    }

    @Entry
    @Component
    struct Index {
      //...
      build() {
        Column(){
          //...

          //注册字体文件
          RNApp({
            rnInstanceConfig: {
              //...
              fontResourceByFontFamily: fonts
            },
            //...
          })

        }
        //...
      }
    }

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; OH SDK: HarmonyOS-NEXT-DB1 5.0.0.25; IDE: DevEco Studio: 5.0.3.400; ROM: 3.0.0.25;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Default | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |------------ |
| currentPosition  | Current position in steps         | number  |    no    | 0 |  iOS,Android  |         yes        |
| stepCount  | Number of steps         | number  |    no    | 5 |  iOS,Android  |         yes        |
| direction  | Orientation of the Steps         | 'horizontal' \| 'vertical'  |    no    | 'horizontal' |  iOS,Android  |         yes        |
| customStyles  | Styles for the component         | object  |    no    | {} |  iOS,Android  |         yes        |
| labels  | Labels for each step         | Array\<string\>  |    no    | null |  iOS,Android  |         yes        |
| onPress  | Callback fired when tapping on a step         | Function (position: Number) => void |    no    | null |  iOS,Android  |         yes        |
| renderStepIndicator  | Used to render custom content inside step at specified position         | Function (position: Number, stepStatus: String) => React.ReactNode |    no    | null |  iOS,Android  |         yes        |
| renderLabel  | Use this to render custom label for each step         | Function (position: Number, stepStatus: String, label: String, currentPosition: Number) => React.ReactNode |    no    | null |  iOS,Android  |         yes        |

### Custom Styles
| Name | Description | Type | Required | Default | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |------------ |
| stepIndicatorSize  |    Size of step indicator circle    | number  |    no    | 30 |  iOS,Android  |         yes        |
| currentStepIndicatorSize  |    Size of the current step indicator circle    | number  |    no    | 40 |  iOS,Android  |         yes        |
| separatorStrokeWidth  |    Stroke thickness of the separator between steps    | number  |    no    | 2 |  iOS,Android  |         yes        |
| separatorStrokeUnfinishedWidth  |    Stroke thickness of the separator between unifinished steps    | number  |    no    | 0 |  iOS,Android  |         yes        |
| separatorStrokeFinishedWidth  |    Stroke thickness of the separator between finished steps    | number  |    no    | 0 |  iOS,Android  |         yes        |
| stepStrokeWidth  |    Thickness of the stroke around each step    | number  |    no    | 3 |  iOS,Android  |         yes        |
| currentStepStrokeWidth  |    Thickness of the stroke around the current step    | number  |    no    | 3 |  iOS,Android  |         yes        |
| stepStrokeCurrentColor  |    Stroke color for the current step    | string  |    no    | '#fe7013' |  iOS,Android  |         yes        |
| stepStrokeFinishedColor  |    Stroke color for finished steps    | string  |    no    | '#fe7013' |  iOS,Android  |         yes        |
| stepStrokeUnFinishedColor  |    Stroke color for unfinished steps    | string  |    no    | '#aaaaaa' |  iOS,Android  |         yes        |
| separatorFinishedColor  |    Color of separator for finished items    | string  |    no    | '#fe7013' |  iOS,Android  |         yes        |
| separatorUnFinishedColor  |    Color of separator for unfinished items    | string  |    no    | '#aaaaaa' |  iOS,Android  |         yes        |
| stepIndicatorFinishedColor  |    Color of the circle for finished steps    | string  |    no    | '#fe7013' |  iOS,Android  |         yes        |
| stepIndicatorUnFinishedColor  |    Color of the circle for unfinished steps    | string  |    no    | '#ffffff' |  iOS,Android  |         yes        |
| stepIndicatorCurrentColor  |    Color of the circle for the current step    | string  |    no    | '#ffffff' |  iOS,Android  |         yes        |
| stepIndicatorLabelFontSize  |    Font size of the number inside the circle for each step    | number  |    no    | 15 |  iOS,Android  |         yes        |
| currentStepIndicatorLabelFontSize  |    Font size of the number inside the circle for the current step    | number  |    no    | 15 |  iOS,Android  |         yes        |
| stepIndicatorLabelCurrentColor  |    Color of label for the current step    | string  |    no    | '#ffffff' |  iOS,Android  |         yes        |
| stepIndicatorLabelFinishedColor  |    Color of labels that their steps are finished    | string  |    no    | '#ffffff' |  iOS,Android  |         yes        |
| stepIndicatorLabelUnFinishedColor  |    Color of labels that their steps are unfinished    | string  |    no    | 'rgba(255,255,255,0.5)' |  iOS,Android  |         yes        |
| labelColor  |    Color of the label text    | string  |    no    | '#000000' |  iOS,Android  |         yes        |
| currentStepLabelColor  |    Color of the current step label    | string  |    no    | '#4aae4f' |  iOS,Android  |         yes        |
| labelSize  |    Font size for the labels    | number  |    no    | 13 |  iOS,Android  |         yes        |
| labelAlign  |    Label alignment    | 'center' \| 'flex-start' \| 'flex-end' \| 'stretch' \| 'baseline' \| undefined  |    no    | 'center' |  iOS,Android  |         yes        |
| labelFontFamily  |    Label fontFamily for custom fonts    | string  |    no    |   |  iOS,Android  |         yes        |


## Known Issues

## Others

## License

This project is licensed under [Apache License 2.0](https://github.com/24ark/react-native-step-indicator/blob/master/LICENSE).
