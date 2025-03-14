> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-pickers</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/iberHK/react-native-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.isc.org/licenses/">
        <img src="https://img.shields.io/badge/license-ISC-red.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/iberHK/react-native-picker)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-pickers@2.0.0
```

#### **yarn**

```bash
yarn add react-native-pickers@2.0.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { View, Text, TouchableOpacity } from "react-native";
import { BaseComponent, AreaPicker, DatePicker } from "react-native-pickers";

var AreaJson = [
  {
    name: "Hong Kong",
    city: [{ name: "Hong Kong", area: ["中西區", "灣仔區", "東區", "南區"] }],
  },
  {
    name: "Taiwan",
    city: [
      {
        name: "Taiwan",
        area: ["臺北市", "高雄市", "臺北縣", "桃園縣", "新竹縣"],
      },
    ],
  },
  {
    name: "Macao",
    city: [
      {
        name: "Macao",
        area: ["花地瑪堂區", "聖安多尼堂區", "大堂區", "望德堂區"],
      },
    ],
  },
];

export default class MainPage extends BaseComponent {
  constructor(props) {
    super(props);
    this.state = {
      unit: ["Year", "Month ", "Day"],
      startYear: 1900,
      active: false,
      modalVisible: false,
    };
  }

  renderButton(text, callback) {
    return (
      <TouchableOpacity
        onPress={callback.bind(this)}
        style={{
          width: this.getSize(180),
          height: this.getSize(35),
          justifyContent: "center",
          alignItems: "center",
          borderColor: "#999999",
          borderWidth: this.mOnePixel,
          padding: this.getSize(10),
          backgroundColor: "#cccccc",
          borderRadius: this.getSize(4),
          marginBottom: this.getSize(20),
        }}
      >
        <Text>{text}</Text>
      </TouchableOpacity>
    );
  }

  render() {
    return (
      <View
        style={{
          width: this.mScreenWidth,
          height: this.mScreenHeight,
          backgroundColor: "#f9fafb",
          justifyContent: "center",
          alignItems: "center",
        }}
      >
        <View
          style={{
            width: this.mScreenWidth,
            height: 60,
            backgroundColor: 0x00000030,
          }}
        />
        <View
          style={{
            flex: 1,
            width: this.mScreenWidth,
            justifyContent: "center",
            alignItems: "center",
          }}
        >
          {this.renderButton("Administrative region picker", () => {
            this.AreaPicker.show();
          })}
          {this.renderButton("DatePicker", () => {
            this.DatePicker.show();
          })}
          <AreaPicker
            areaJson={AreaJson}
            onPickerCancel={() => {}}
            onPickerConfirm={(value) => {
              alert(JSON.stringify(value));
            }}
            ref={(ref) => (this.AreaPicker = ref)}
          />
          <DatePicker
            unit={this.state.unit}
            startYear={this.state.startYear}
            onPickerConfirm={(value) => {
              alert(JSON.stringify(value));
            }}
            onPickerCancel={() => {
              alert("cancel");
            }}
            ref={(ref) => (this.DatePicker = ref)}
          />
        </View>
      </View>
    );
  }
}
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-svg](/en/react-native-svg-capi.md) to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.26; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.300; ROM: 3.0.0.25;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### AlertDialog

| Name             | Description                                           | Type     | Required | Platform | HarmonyOS Support |
| ---------------- | ----------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| messageText      | 消息文本                                              | string   | no       | All      | yes               |
| messageTextColor | 消息文本字体颜色                                      | string   | no       | All      | yes               |
| messageTextSize  | 消息文本字体大小                                      | number   | no       | All      | yes               |
| negativeText     | 取消文本                                              | string   | no       | All      | yes               |
| negativeColor    | 取消文本颜色                                          | string   | no       | All      | yes               |
| negativeSize     | 取消文本字体大小                                      | number   | no       | All      | yes               |
| positiveText     | 确定文本                                              | string   | no       | All      | yes               |
| positiveColor    | 确定文本颜色                                          | string   | no       | All      | yes               |
| positiveSize     | 确定文本字体大小                                      | number   | no       | All      | yes               |
| onPress          | `positive(确定)返回true` or `negative(取消)返回false` | function | no       | All      | yes               |

### AreaPicker

| Name              | Description                        | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ---------------------------------- | -------- | -------- | -------- | ----------------- |
| selectedValue     | 选中                               | Arrays<string\|object>   | no       | All      | yes               |
| areaJson          | 地址数据源                         | json     | no       | All      | yes               |
| confirmText       | 确定选择文本                       | string   | no       | All      | yes               |
| confirmTextSize   | 确定选择文本字体大小               | number   | no       | All      | yes               |
| confirmTextColor  | 确定选择字体颜色                   | string   | no       | All      | yes               |
| cancelText        | 取消选择文本                       | string   | no       | All      | yes               |
| cancelTextSize    | 取消选择文本字体大小               | number   | no       | All      | yes               |
| cancelTextColor   | 取消选择文本字体颜色               | string   | no       | All      | yes               |
| itemTextColor     | item 正常颜色，仅支持 `16进制数字` | string   | no       | All      | yes               |
| itemSelectedColor | item 正常颜色，仅支持 `16进制数字` | string   | no       | All      | yes               |
| itemHeight        | item 高度                          | string   | no       | All      | yes               |
| onPickerCancel    | 取消选择回调                       | function | no       | All      | yes               |
| onPickerConfirm   | 确认选择回调                       | function | no       | All      | yes               |

### DatePicker

| Name              | Description                        | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ---------------------------------- | -------- | -------- | -------- | ----------------- |
| itemTextColor     | item 正常颜色，仅支持 `16进制数字` | string   | no       | All      | yes               |
| itemSelectedColor | item 正常颜色，仅支持 `16进制数字` | string   | no       | All      | yes               |
| onPickerCancel    | 取消选择回调                       | function | no       | All      | yes               |
| onPickerConfirm   | 确认选择回调                       | function | no       | All      | yes               |
| unit              | 单位                               | Arrays<string\|object>   | no       | All      | yes               |
| selectedValue     | 选中                               | string   | no       | All      | yes               |
| startYear         | 起始年份                           | number   | no       | All      | yes               |
| endYear           | 截至年份                           | number   | no       | All      | yes               |
| confirmText       | 确定选择文本                       | string   | no       | All      | yes               |
| confirmTextSize   | 确定选择文本字体大小               | number   | no       | All      | yes               |
| confirmTextColor  | 确定选择文本字体颜色               | string   | no       | All      | yes               |
| cancelText        | 取消选择文本                       | string   | no       | All      | yes               |
| cancelTextSize    | 取消选择文本字体大小               | number   | no       | All      | yes               |
| cancelTextColor   | 取消选择文本字体颜色               | string   | no       | All      | yes               |
| itemHeight        | item 高度                          | number   | no       | All      | yes               |
| HH                | 是否显示小时                       | boolean  | no       | All      | yes               |
| mm                | 是否显示分钟                       | boolean  | no       | All      | yes               |
| ss                | 是否显示秒                         | boolean  | no       | All      | yes               |

### DownloadDialog

| Name           | Description      | Type     | Required | Platform | HarmonyOS Support |
| -------------- | ---------------- | -------- | -------- | -------- | ----------------- |
| title          | 标题文本         | string   | no       | All      | yes               |
| titleColor     | 标题文本字体大小 | string   | no       | All      | yes               |
| titleSize      | 标题文本文本颜色 | number   | no       | All      | yes               |
| active         | 按钮是否可点击   | string   | no       | All      | yes               |
| actionText     | 按钮文本         | string   | no       | All      | yes               |
| onAction       | 点击按钮回调     | function | no       | All      | yes               |
| totalTextColor | 总数文本字体颜色 | string   | no       | All      | yes               |
| totalTextSize  | 总数文本字体大小 | number   | no       | All      | yes               |

### InputDialog

| Name         | Description        | Type     | Required | Platform | HarmonyOS Support |
| ------------ | ------------------ | -------- | -------- | -------- | ----------------- |
| title        | 标题文本           | string   | no       | All      | yes               |
| titleSize    | 标题文本字体大小   | number   | no       | All      | yes               |
| titleColor   | 标题文本文本颜色   | string   | no       | All      | yes               |
| cancelText   | 取消文本           | string   | no       | All      | yes               |
| cancelSize   | 取消文本字体大小   | number   | no       | All      | yes               |
| cancelColor  | 取消文本字体颜色   | string   | no       | All      | yes               |
| btnText      | 提交文本           | string   | no       | All      | yes               |
| btnTextSize  | 提交文本字体大小   | number   | no       | All      | yes               |
| btnTextColor | 提交文本字体颜色   | string   | no       | All      | yes               |
| btnBgColor   | 提交按钮颜色       | string   | no       | All      | yes               |
| placeholder  | 输入框提示语       | string   | no       | All      | yes               |
| onSubmit     | 返回输入的文本内容 | function | no       | All      | yes               |

### BaseDialog

| Name              | Description                                                     | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | --------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| removeSubviews    | dismiss，是否回收前景控件，拓展出来的子控件，不要动态设置改属性 | boolean  | no       | All      | yes               |
| coverClickable    | 背景点击隐藏                                                    | boolean  | no       | All      | yes               |
| onCoverPress      | 点击背景，dismiss 回调                                          | function | no       | All      | yes               |
| showAnimationType | 入场动画方式 spring timing                                      | function | no       | All      | yes               |

### PickerView

| Name              | Description                        | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ---------------------------------- | -------- | -------- | -------- | ----------------- |
| itemTextColor     | item 正常颜色，仅支持 `16进制数字` | string   | no       | All      | yes               |
| itemSelectedColor | item 正常颜色，仅支持 `16进制数字` | string   | no       | All      | yes               |
| itemHeight        | item 高度                          | number   | no       | All      | yes               |
| onPickerSelected  | 选中时回调                         | function | no       | All      | yes               |
| selectedIndex     | 选中                               | number   | no       | All      | yes               |

### SimpleChooseDialog

| Name              | Description                                                                                                                    | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| items             | 列表数据，可以 string、object (需要指定 itemKey)                                                                               | Arrays<string\|object>   | no       | All      | yes               |
| itemKey           | 当 item 为 object 时，来指定显示的属性 items:[{id:0, value: 'v1'},{id:0, value: 'v1'}]itemKey 设为'value',则等同于['v1', 'v2'] | string   | no       | All      | yes               |
| itemStyle         | 列表文字样式                                                                                                                   | object   | no       | All      | yes               |
| selectColor       | 选中颜色                                                                                                                       | string   | no       | All      | yes               |
| normalColor       | 未选中颜色                                                                                                                     | string   | no       | All      | yes               |
| pointSize         | 左侧选中标识大小                                                                                                               | number   | no       | All      | yes               |
| pointBorderRadius | 左侧选中标识边框弧度                                                                                                           | string   | no       | All      | yes               |
| confirmText       | 确定选择文本                                                                                                                   | string   | no       | All      | yes               |
| confirmBtnColor   | 确定选择按钮颜色                                                                                                               | string   | no       | All      | yes               |
| confirmTextColor  | 确定选择文本颜色                                                                                                               | string   | no       | All      | yes               |
| onPress           | 返回选中 index                                                                                                                 | function | no       | All      | yes               |

### SimpleItemsDialog

| Name            | Description                                                                                                                     | Type     | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| items           | 列表数据，可以 string、object(需要指定 itemKey)                                                                                 | Arrays<string\|object>   | no       | All      | yes               |
| itemKey         | 当 item 为 object 时，来指定显示的属性 items:[{id:0, value: 'v1'},{id:0, value: 'v1'}] itemKey 设为'value',则等同于['v1', 'v2'] | string   | no       | All      | yes               |
| itemStyle       | 列表文字样式                                                                                                                    | object   | no       | All      | yes               |
| onPress         | 返回选中 index                                                                                                                  | function | no       | All      | yes               |
| cancel          | 是否在列表最后 增加 ‘取消’ 项                                                                                                   | string   | no       | All      | yes               |
| cancelText      | 取消项文本                                                                                                                      | string   | no       | All      | yes               |
| cancelTextStyle | 取消文本字体样式                                                                                                                | object   | no       | All      | yes               |

### ToastComponent

| Name            | Description          | Type   | Required | Platform | HarmonyOS Support |
| --------------- | -------------------- | ------ | -------- | -------- | ----------------- |
| duration        | 显示时长（自动隐藏） | number | no       | All      | yes               |
| textColor       | message 字体颜色     | string | no       | All      | yes               |
| fontSize        | message 字体大小     | number | no       | All      | yes               |
| lineHeight      | message 字体行高     | number | no       | All      | yes               |
| paddingH        | 水平 padding         | number | no       | All      | yes               |
| paddingV        | 上下 padding         | number | no       | All      | yes               |
| borderRadius    | 背景圆角             | number | no       | All      | yes               |
| backgroundColor | 背景颜色             | string | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The ISC License (ISC)](https://www.isc.org/licenses/).
