> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-iconfont-cli</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/iconfont-cli/react-native-iconfont-cli">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/iconfont-cli/react-native-iconfont-cli/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/iconfont-cli/react-native-iconfont-cli)

## 安装与使用
<!-- tabs:start -->
进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install react-native-iconfont-cli --save-dev
```

#### **yarn**

```bash
yarn add react-native-iconfont-cli --dev
```

生成配置文件
```bash
npx iconfont-init
```

此时项目根目录会生成一个iconfont.json的文件，内容如下：
```json
{
    "symbol_url": "symbol_url和local_svgs可以二选一,也可以都填",
    "use_typescript": false,
    "save_dir": "./src/iconfont",
    "trim_icon_prefix": "icon",
    "default_icon_size": 18,
    "local_svgs": "./localSvgs"
}
```

在配置的"save_dir"下生成React-Native标准组件
```bash
npx iconfont-rn
```

当您在iconfont.cn中的图标有变更时，只需更改配置symbol_url，然后再次执行以下命令即可生成最新的图标组件
```bash
npx iconfont-rn
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import { Component } from 'react';
import { StyleSheet, ScrollView, View, Button } from 'react-native';
import { Tester, TestCase, TestSuite } from '@rnoh/testerino';
import IconFont from '../iconfont';
import IconUser from '../iconfont/IconUser';
import IconTerm from '../iconfont/IconTerm';
import IconSetup from '../iconfont/IconSetup';

const styles = StyleSheet.create({
    container: {
        height: 60,
        width: 80,
        marginBottom: 10,
        display:'flex',
        flexDirection: 'row',
        justifyContent: 'space-between',
        alignItems: 'center',
    },
    minContainer: {
        height: 30,
        width: 40,
        marginBottom: 10,
    },
});

class IconFontSummary extends Component {
    render() {
        return (
            <View>
                <IconFont name="user" size={50}/>
            </View>
        );
    }
}

class IconFontSingle extends Component {
    static title = 'use a single icon';
    render() {
        return (
            <View style={styles.minContainer}>
                <IconTerm/>
            </View>
        );
    }
}

class IconFontSize extends Component {
    static title = 'two types use icon font size attribute';
    render() {
        return (
            <View style={styles.container}>
                <IconFont name="user" size={50}/>
            </View>
        );
    }
}

class IconFontColor extends Component {
    static title = 'use icon font color attribute';
    render() {
        return (
            <View style={styles.minContainer}>
                <IconSetup color="blue" size={30}/>
            </View>
        );
    }
}

class IconFontColorArr extends Component {
    static title = 'use icon font color arr attribute';
    render() {
        return (
            <View style={styles.container}>
                <IconFont name="setup" color={["blue", "orange"]} size={50} />
                <IconFont name="alipay" color={["blue", "orange"]} size={50} />
            </View>
        );
    }
}

const icon = [IconFontSummary, IconFontSingle, IconFontSize, IconFontColor, IconFontColorArr];

export { icon };

export default function () {
    return (
        <ScrollView >
            <Tester style={{
                display: 'flex',
                flexDirection: 'column'
            }}>
                <TestCase itShould="<IconFont name='user'/>">
                    <IconFontSummary />
                </TestCase>
                <TestCase itShould="<IconTerm/>">
                    <IconFontSingle />
                </TestCase>
                <TestCase itShould="<IconFont name='user' size={50}/>">
                    <IconFontSize />
                </TestCase>
                <TestCase itShould="<IconSetup color='blue' size={30}/>">
                    <IconFontColor />
                </TestCase>
                <TestCase itShould="<IconFont name='setup' color={['blue', 'orange']} size={50}/>">
                    <IconFontColorArr />
                </TestCase>
            </Tester>
        </ScrollView>
    )
}
```
## Link

本库在HarmonyOS NEXT侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在HarmonyOS NEXT工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg-capi.md#link)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.22;

## 属性
详细请查看 [react-native-iconfont-cli](https://github.com/iconfont-cli/react-native-iconfont-cli/blob/master/README.md) 的文档介绍

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**IconFont组件属性**

| Name  | Description | Type            | Required | Platform    | HarmonyOS Support |
|-------|-------------|-----------------| -- |-------------| --- |
| color | 图标颜色        | string/string[] | no | Android/IOS | yes |
| size  | 图标尺寸        | number          | no | Android/IOS | yes |

**iconfont.json配置文件属性**

| Name | Description                                               | Type   | Required        | Platform | HarmonyOS Support  |
| ---- |-----------------------------------------------------------|--------|-----------------| -------- | ------------------ |
| symbol_url  | iconfont官网的.js后缀项目链接 | string | 和local_svgs可以二选一也可以都用 | Android/IOS | yes |
| use_typescript  | 项目使用Typescript编写，请设置为true，生成的图标组件是.tsx和.js后缀。当该值为false时，生成.js和.d.ts两种文件 | bool   | yes  | Android/IOS | yes |
| save_dir  | iconfont图标生成的组件存放的位置 | string | yes  | Android/IOS | yes |
| trim_icon_prefix  | 统一去掉图标通用的前缀  | string | no   | Android/IOS | yes |
| default_icon_size  | 图标组件默认的字体大小  | string | no   | Android/IOS | yes |
| local_svgs  | 本地 svg 的路径(暂不支持 color 参数) | string | 和symbol_url可以二选一也可以都用   | Android/IOS | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/iconfont-cli/react-native-iconfont-cli/blob/master/LICENSE) ，请自由地享受和参与开源。