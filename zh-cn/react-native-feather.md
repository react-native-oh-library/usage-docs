> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-feather</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/yigithanyucedag/react-native-feather">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>





> [!TIP] [Github 地址](https://github.com/yigithanyucedag/react-native-feather)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-feather@1.1.2
```

#### **yarn**

```bash
yarn add react-native-feather@1.1.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

此库可以使用的[图标列表](https://feathericons.com/)

>[!WARNING] 使用时 import 的库名不变。且该库强依赖[@react-native-oh-tpl/react-native-svg](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg.md)，请在使用前，安装svg库

```js
import React from 'react';  
import {Text, ScrollView } from 'react-native';   
import * as Icon from "react-native-feather";
//第二种引入方式，可以直接通过组件名称引入
import { Check } from "react-native-feather";


const FeatherExample = () => {  
  return (
  <ScrollView>
  <Text style={{color:"blue"}}>react-native-feather库只是对svg图进行处理的库,以下展示的demo,均只有图片,没有绑定点击事件</Text>
  <Text style={{color:"blue"}}>电池,边线红色,绿色填充,width=150,height=150</Text>
  <Icon.Battery stroke = 'red' width={150} height={150}  fill="green"/>
  <Text style={{color:"blue"}}>菜单栏,边线绿色,宽高默认为25</Text>
  <Icon.Menu stroke = 'green'/>
  <Text style={{color:"blue"}}>播放图标,边线默认为当前颜色,填充色为蓝色,宽高为50</Text>
  <Icon.Video fill="blue" width={50} height={50} />
   
  <Text style={{color:"blue"}}>第二种使用方法：对号,颜色为红色,width和height为32</Text>
  <Check stroke="red" width={32} height={32} />
  </ScrollView>
  );
};  
  
export default FeatherExample;
```
## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](/zh-cn/react-native-svg.md#link)进行引入

## 约束与限制

### 兼容性

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;
2. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1 B.0.18、HarmonyOS NEXT Developer Preview0 B.0.60、HarmonyOS NEXT Developer Preview2 B.0.73; IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.18;

## 属性

所有[SVG属性](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg.md)均可使用

### feather

该库为UI组件库，通过配置属性标签，实现对应的功能。

| Prop        | Description                                                  | Default      | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | ------------ | ----------------- |
| width       | Width of the icon.                                           | 24           | yes               |
| height      | Height of the icon.                                          | 24           | yes               |
| stroke      | The stroke prop refers to the color outline the icon.        | currentColor | yes               |
| strokeWidth | The strokeWidth prop specifies the width of the outline on the icon. | 2            | yes               |
| fill        | The fill prop refers to the color inside the icon.           | none         | yes               |



## 遗留问题

## 其他

以下事项与原库保持一致需注意遵循：

1. 在使用该库前，请保证按照上文"Link"的提示，已经安装 [`react-native-svg`](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg.md)。
2. 此组件包含所有 [`react-native-svg`](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg.md) 兼容的所有 Feather 图标。
3. 基于Feather 图标库版本为V4.28.0。

## 开源协议

本项目基于 [The MIT License (MIT)](https://www.mit-license.org) ，请自由地享受和参与开源。