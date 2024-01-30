> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>react-native-check-box</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/crazycodeboy/react-native-check-box/blob/v2.1.0/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/crazycodeboy/react-native-check-box)
## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-check-box@2.1.0
```
<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, {useEffect, useState} from 'react';
import {StyleSheet, ScrollView, View, Image, Text} from 'react-native';
import CheckBox from 'react-native-check-box';
import keys from './keys.json';
import {Indata} from './CheckBox';
import type {dataType} from './CheckBox';


function example() {
  const [dataArray, setDataArray] = useState<dataType>([]);
  useEffect(() => {
    setDataArray(keys);
  }, []);
  const onClick1 = (data: Indata) => {
    data.checked = !data.checked;
    setDataArray([...dataArray]);
  };
  //基本使用，设置左边文本样式
  const RenderView = () => {
    if (!dataArray || dataArray.length === 0) return; //判断数组中是否为空，如果为空直接返回
    const views = dataArray.map(item => (
      <View key={item.name}>
        <View style={styles.item}>
          <CheckBox
            style={{flex: 1, padding: 10}} //设置复选框的样式
            onClick={() => onClick1(item)} //点击复选框的回调函数
            isChecked={item.checked} //复选框选中的状态
            leftText={item.name} //左侧文本
            leftTextStyle={{fontSize: 20, fontWeight: '700'}} //左侧文本样式
          />
        </View>
        <View style={styles.line}></View>
      </View>
    ));
    return views;
  };
  return (
    <View style={styles.container}>
      <ScrollView>
        <Text style={styles.titleText}>基本使用，设置左边文本样式</Text>
        <RenderView />
      </ScrollView>
    </View>
  );
};

//css样式
const styles = StyleSheet.create({
  titleText: {
    fontSize: 25,
    fontWeight: 'bold',
    marginTop: 20,
    marginBottom: 10,
  },
  container: {
    flex: 1,
    backgroundColor: '#f3f2f2',
    marginTop: 30,
  },
  item: {
    flexDirection: 'row',
  },
  line: {
    flex: 1,
    height: 0.3,
    backgroundColor: 'darkgray',
  },
  });
export default example;

```

## 兼容性

在以下版本验证通过
  1. IDE:4.1.3.500;
     SDK:4.1.5.6;
     测试设备：Mate60 (BRA-AL00);
     Rom: 2.0.0.33(SP34C00E33R4P5log);
     RNOH:0.72.13。

## 属性
详情见[react-native-check-box](https://github.com/crazycodeboy/react-native-check-box)

### React-navite-check-box:

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |
| style|Custom style checkbox |ViewPropTypes.style| No | Android/IOS | Yes |
| leftText |Custom left Text | PropTypes.string | No | Android/IOS | Yes |
| leftTextStyle |Custom left Text style | Text.propTypes.style | No | Android/IOS | Yes |
| rightText |Custom right Text | PropTypes.string | No |  Android/IOS | Yes |
| rightTextView |Custom right TextView | PropTypes.element | No |Android/IOS | Yes |
| rightTextStyle |Custom right Text style | Text.propTypes.style | No | Android/IOS | Yes |
| checkedImage |Custom checked Image | PropTypes.element | No | Android/IOS  | Yes |
| unCheckedImage |Custom unchecked Image | PropTypes.element | No | Android/IOS | Yes |
| isChecked |checkbox checked state | PropTypes.bool | Yes | Android/IOS | Yes |
| onClick |callback function | PropTypes.func.isRequired | Yes | Android/IOS | Yes |
| disabled |Disable the checkbox button | PropTypes.bool | No | Android/IOS | Yes |
| checkBoxColor |Tint color of the checkbox image (this props is for both checked and unchecked state) | PropTypes.string| Yes | Android/IOS | Yes | 
| checkedCheckBoxColor |Tint color of the checked state checkbox image (this prop will override value of checkBoxColor for checked state) | PropTypes.string | No | Android/IOS | Yes |
| uncheckedCheckBoxColor |Tint color of the unchecked state checkbox image (this prop will override value of checkBoxColor for unchecked state) | PropTypes.string| No | Android/IOS | Yes |   

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/crazycodeboy/react-native-check-box/blob/master/LICENSE) ，请自由地享受和参与开源。
