<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-autocomplete-input</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/byteburgers/react-native-autocomplete-input">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/byteburgers/react-native-autocomplete-input/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/byteburgers/react-native-autocomplete-input)

## 安装与使用
<!-- tabs:start -->
进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install --save react-native-autocomplete-input@5.4.0
```

#### **yarn**

```bash
yarn add react-native-autocomplete-input@5.4.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, { Component } from 'react';
import { View, Text, StyleSheet, TouchableOpacity} from 'react-native';
import AutocompleteInput from 'react-native-autocomplete-input';


const styles = StyleSheet.create({
    containerStyle: {
        borderColor: "#e0494e",
        borderWidth: 5,
        borderRadius: 15,
        width: '100%'
    },
    inputContainerStyle: {
        borderWidth: 3,
        borderColor: "green",

    },
    listContainerStyle: {
        backgroundColor: "yellow"
    },
    itemText: {
        paddingTop: 10,
        paddingBottom: 10,

    },

});

interface AutocompleteItem {
    id: number;
    value: string;
}

const testArray: AutocompleteItem[] = [{ id: 1, value: 'Aabbbbbbb' }, { id: 2, value: 'BBFFFFF' }, { id: 3, value: 'ccccccbbb' }]

function filterData(query: string): AutocompleteItem[] {
    if (query) {
        const filteredItems = testArray.filter(item => item.value.toLowerCase().includes(query.toLowerCase()));
        return filteredItems;
    } else {
        return [];
    }
}

function compare(selectName: string, value: string): boolean {
    return selectName === value;
}

class App extends Component {
    state = {
        query: '', 
        isVisible: true,
        selectName: ''
    };

    render() {
        const { query, isVisible } = this.state;
        const data = filterData(query);
        return (
            <View style={{ backgroundColor: '#d1f8f7', height: '100%' ,paddingTop:100}}>
                <AutocompleteInput
                    containerStyle={styles.containerStyle} 
                    inputContainerStyle={styles.inputContainerStyle} 
                    listContainerStyle={styles.listContainerStyle}
                    data={data.length === 1 && compare(this.state.selectName, data[0].value) ? [] : data} 
                    value={query} 
                    onChangeText={(text) => {

                        if (text.trim() !== this.state.selectName.trim()) {
                            this.setState({
                                isVisible: false,
                                selectName: text
                            });
                        } else {
                            this.setState({
                                isVisible: false,
                                selectName: text
                            });
                        }
                        this.setState({ query: text});
                        console.log("--------onChangeText--++++isVisible:" + isVisible)
                    }} 

                    onShowResults={() => { console.log("--------+++++++++ onShowResults "); }} 
                    
                    hideResults={isVisible} 

                    flatListProps={{
                        keyExtractor: (_, idx) => String(idx),
                        keyboardShouldPersistTaps: 'always', 
                        renderItem: ({ item }) => {
                            return (
                                <TouchableOpacity onPress={() => {
                                    this.setState({ query: item.value, isVisible: true, selectName: item.value });
                                    console.log("--------onPress--++++isVisible:" + isVisible)
                                }}>
                                    <Text style={styles.itemText}>{item.value}</Text>
                                </TouchableOpacity>
                            )
                        },
                    }} 
                />
            </View>
        );
    }
}



export default App;
```
## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;

## 属性
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| containerStyle      | These styles will be applied to the container which surrounds the autocomplete component. | style    | no       | Android/iOS | yes               |
| hideResults         | Set to `true` to hide the suggestion list.                   | bool     | no       | Android/iOS | yes               |
| data                | An array with suggestion items to be rendered in `renderItem({ item, i })`. Any array with length > 0 will open the suggestion list and any array with length < 1 will hide the list. | array    | no       | Android/iOS | yes               |
| inputContainerStyle | These styles will be applied to the container which surrounds the textInput component. | style    | no       | Android/iOS | yes               |
| listContainerStyle  | These styles will be applied to the container which surrounds the result list. | style    | no       | Android/iOS | yes               |
| onShowResults       | will be called when the autocomplete suggestions appear or disappear. | function | no       | Android/iOS | yes               |
| renderTextInput     | render custom TextInput. All props passed to this function.  | function | no       | Android/iOS | yes               |
| flatListProps       | custom props to FlatList.                                    | object   | no       | Android/iOS | yes               |
| renderResultList    | render custom result list. Can be used to replace FlatList. All props passed to this function. | function | no       | Android/iOS | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/byteburgers/react-native-autocomplete-input/blob/main/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->