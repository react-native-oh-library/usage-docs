<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-parsed-text</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/taskrabbit/react-native-parsed-text">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/taskrabbit/react-native-parsed-text/blob/master/LICENSE.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/taskrabbit/react-native-parsed-text)


## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-parsed-text@0.0.22
```

#### **yarn**

```bash
yarn add react-native-parsed-text@0.0.22
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import {Tester, Filter} from '@rnoh/testerino';
import React from 'react';
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  useColorScheme,
  View,
  Button,
  Alert,
  Linking
} from 'react-native';
import ParsedText from 'react-native-parsed-text';

export function TestNativeParsedText({ filter }: { filter: Filter }){
  
  const handleUrlPress=(url, matchIndex /*: number*/)=>{
    Linking.openURL(url);
  }

  const handlePhonePress=(phone, matchIndex /*: number*/)=> {
    Alert.alert(`${phone} has been pressed!`);
  }

  const handleNamePress=(name, matchIndex /*: number*/)=> {
    Alert.alert(`Hello ${name}`);
  }

  const handleEmailPress=(email, matchIndex /*: number*/)=> {
    Alert.alert(`send email to ${email}`);
  }
  const handleIDPress=(name, matchIndex /*: number*/)=> {
    Alert.alert(`Hello ${name}`);
  }
  const renderText=(matchingString, matches)=> {
    let pattern = /\[(@[^:]+):([^\]]+)\]/i;
    let match = matchingString.match(pattern);
    return `^^${match[0]}^^`;
  }

    return (
      <View style={{width: '100%', height: '100%'}}>
        <Tester style={{flex: 1}} filter={filter}>
          <View style={styles.container}>
            <ParsedText
              style={styles.text}
              parse={
                [
                  {type: 'url',                       style: styles.url, onPress: handleUrlPress},
                  {type: 'phone',                     style: styles.phone, onPress: handlePhonePress},
                  {type: 'email',                     style: styles.email, onPress: handleEmailPress},
                  {pattern: /Bob|David/,              style: styles.name, onPress: handleNamePress},
                  {pattern: /\[(@[^:]+):([^\]]+)\]/i, style: styles.username, onPress: handleNamePress, renderText: renderText},
                  {pattern: /42/,                     style: styles.magicNumber},
                  {pattern: /#(\w+)/,                 style: styles.hashTag},
                ]
              }
              childrenProps={{allowFontScaling: false}}
            >
                Hello this is an example of the ParsedText, links like http://www.google.com or http://www.facebook.com are clickable and phone number 444-555-6666 can call too.
          But you can also do more with this package, for example Bob will change style and David too. username like [@^^:^^] has been replaced.
          And the magic number is 42!
          #react #react-native
            </ParsedText>
          </View>
        </Tester>
      </View>
    );
  
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  idnumber:{
    color: 'yellow'
  },

  url: {
    color: 'red',
    textDecorationLine: 'underline',
  },

  email: {
    textDecorationLine: 'underline',
  },

  text: {
    color: 'black',
    fontSize: 15,
  },

  phone: {
    color: 'blue',
    textDecorationLine: 'underline',
  },

  name: {
    color: 'red',
  },

  username: {
    color: 'green',
    fontWeight: 'bold'
  },

  magicNumber: {
    fontSize: 42,
    color: 'pink',
  },

  hashTag: {
    fontStyle: 'italic',
    color:'green',
    fontSize:42
  },

});
```

## 约束与限制

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.27; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

ParsedText组件接收所有[React Native Text](https://reactnative.dev/docs/text.html)组件的Props

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| parse  | Array of parsed text.    | array  | yes | IOS/Android   | yes |
| renderText  | Function called to change the displayed children.     | function  | yes | IOS/Android   | yes |
| childrenProps | Properties to pass to the children elements generated by react-native-parsed-text.     | object  | no | IOS/Android   | yes |

eg:

parse: Array of parsed text.
* to use the predefined type: `{type: 'url'}、{type: 'phone'} or {type: 'email'}`.
* to use your own `RegExp`: `{pattern: /something/}`
* to change the style of the matched text your own `RegExp`: `{type: 'phone',style:styles.phoneStyle}`
* to add the onPress event(one of Text Props，and others are supported) of the matched text:`{type: 'url',onPress:this.handlePress}`.
* to add the onLongPress event(one of Text Props，and others are supported) of your own `RegExp` matched text:`{pattern: /something/,onLongPress:this.handleLongPress}`.
* to limit how many matches are found of your own `RegExp` matched text:`{pattern: /something/,nonExhaustiveModeMaxMatchCount:number}`.

renderText: Function called to change the displayed children.

Your str is ```'Mention [@michel:5455345]'``` where 5455345 is ID of this user and @michel the value to display on interface.
Your pattern for ID & username extraction : ```/\[(@[^:]+):([^\]]+)\]/i```
Your renderText method :
```
renderText(matchingString, matches) {
  // matches => ["[@michel:5455345]", "@michel", "5455345"]
  let pattern = /\[(@[^:]+):([^\]]+)\]/i;
  let match = matchingString.match(pattern);
  return `^^${match[1]}^^`;
}
```
Displayed text will be : ```Mention ^^@michel^^```

## 遗留问题

## 其他

## 开源协议

本项目基于 [TTHE MIT License (MIT)](https://github.com/taskrabbit/react-native-parsed-text/blob/master/LICENSE.txt) ，请自由地享受和参与开源。

<!-- {% endraw %} -->