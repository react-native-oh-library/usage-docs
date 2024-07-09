> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-calendars</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wix/react-native-calendars">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wix/react-native-calendars/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/wix/react-native-calendars)

## 安装与使用

#### **npm**

```bash
npm install --save react-native-calendars@1.1304.1
```

#### **yarn**

```bash
yarn install --save react-native-calendars@1.1304.1
```

下面的代码展示了这个库的基本使用场景：

```js
import React, { useState } from "react";
import { Calendar, CalendarList, Agenda } from "react-native-calendars";
import { View, StyleSheet } from "react-native";

const MySvgComponent = () => {
  const [selected, setSelected] = useState("");
  return (
    <View style={styles.container}>
      <Calendar
        onDayPress={(day) => {
          setSelected(day.dateString);
        }}
        markedDates={{
          [selected]: {
            selected: true,
            disableTouchEvent: true,
            selectedDotColor: "orange",
          },
        }}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    position: "absolute", // 绝对定位
    bottom: 210, // 底部边界与父容器底部对齐
    width: "100%",
    alignItems: "center",
    justifyContent: "center",
    borderWidth: 1,
    backgroundColor: "#CC00FF",
  },
});
export default MySvgComponent;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证：

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                     | Description                                                                                                | Type                 | Required | Platform | HarmonyOS Support |
| ------------------------ | ---------------------------------------------------------------------------------------------------------- | -------------------- | -------- | -------- | ----------------- |
| theme                    | Specify theme properties to override specific styles for calendar parts                                    | Theme                | no       | All      | yes               |
| firstDay                 | If firstDay=1 week starts from Monday. Note that dayNames and dayNamesShort should still start from Sunday | number               | no       | All      | yes               |
| displayLoadingIndicator  | Display loading indicator                                                                                  | boolean              | no       | All      | yes               |
| showWeekNumbers          | Show week numbers                                                                                          | boolean              | no       | All      | yes               |
| style                    | Specify style for calendar container element                                                               | StyleProp<ViewStyle> | no       | All      | yes               |
| current                  | Initially visible month                                                                                    | string               | no       | All      | yes               |
| initialDate              | Initially visible month. If changed will initialize the calendar to this value                             | string               | no       | All      | yes               |
| minDate                  | Minimum date that can be selected, dates before minDate will be grayed out                                 | string               | no       | All      | yes               |
| maxDate                  | Maximum date that can be selected, dates after maxDate will be grayed out                                  | string               | no       | All      | yes               |
| markedDates              | Collection of dates that have to be marked                                                                 | MarkedDates          | no       | All      | yes               |
| hideExtraDays            | Do not show days of other months in month page                                                             | boolean              | no       | All      | yes               |
| showSixWeeks             | Always show six weeks on each month (only when hideExtraDays = false)                                      | boolean              | no       | All      | yes               |
| disableMonthChange       | Disables changing month when click on days of other months (when hideExtraDays is false)                   | boolean              | no       | All      | yes               |
| enableSwipeMonths        | Enable the option to swipe between months                                                                  | boolean              | no       | All      | yes               |
| disabledByDefault        | Disable days by default                                                                                    | boolean              | no       | All      | yes               |
| headerStyle              | Style passed to the header                                                                                 | StyleProp<ViewStyle> | no       | All      | yes               |
| customHeader             | Allow rendering a totally custom header                                                                    | any                  | no       | All      | yes               |
| allowSelectionOutOfRange | Allow selection of dates before minDate or after maxDate                                                   | boolean              | no       | All      | yes               |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                        | Type     | Required | Platform | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| onDayPress            | Handler which gets executed on day press                           | function | no       | All      | yes               |
| onDayLongPress        | Handler which gets executed on day long press                      | function | no       | All      | yes               |
| onMonthChange         | Handler which gets executed when month changes in calendar         | function | no       | All      | yes               |
| onVisibleMonthsChange | Handler which gets executed when visible month changes in calendar | function | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wix/react-native-calendars/blob/master/LICENSE) ，请自由地享受和参与开源。
