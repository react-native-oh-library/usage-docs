> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-udp</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/tradle/react-native-udp">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/tradle/react-native-udp/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-udp)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-udp Releases](https://github.com/react-native-oh-library/react-native-udp/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-udp
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-udp
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, {Component} from 'react';
import {ScrollView, StyleSheet, Text, View} from 'react-native';

import dgram from 'react-native-udp';

function randomPort() {
  return (Math.random() * 60536) | (0 + 5000); // 60536-65536
}

function toByteArray(obj) {
  var uint = new Uint8Array(obj.length);
  for (var i = 0, l = obj.length; i < l; i++) {
    uint[i] = obj.charCodeAt(i);
  }

  return new Uint8Array(uint);
}

class App extends Component {
  constructor(props) {
    super(props);

    this.updateChatter = this.updateChatter.bind(this);
    this.state = {chatter: []};
  }

  updateChatter(msg) {
    this.setState({
      chatter: this.state.chatter.concat([msg]),
    });
  }

  componentDidMount() {
    let self = this;

    let a = dgram.createSocket('udp4');
    let aPort = randomPort();
    a.bind(aPort, function(err) {
      if (err) throw err;
      self.updateChatter('a bound to ' + JSON.stringify(a.address()));
    });

    let b = dgram.createSocket('udp4');
    var bPort = randomPort();
    b.bind(bPort, function(err) {
      if (err) throw err;
      self.updateChatter('b bound to ' + JSON.stringify(b.address()));
    });

    a.on('message', function(data, rinfo) {
      var str = String.fromCharCode.apply(null, new Uint8Array(data));
      self.updateChatter(
        'a received echo ' + str + ' ' + JSON.stringify(rinfo),
      );
      a.close();
      b.close();
    });

    b.on('message', function(data, rinfo) {
      var str = String.fromCharCode.apply(null, new Uint8Array(data));
      self.updateChatter('b received ' + str + ' ' + JSON.stringify(rinfo));

      // echo back
      b.send(data, 0, data.length, aPort, '127.0.0.1', function(err) {
        if (err) throw err;
        self.updateChatter('b echoed data');
      });
    });

    b.once('listening', function() {
      var msg = toByteArray('hello');
      a.send(msg, 0, msg.length, bPort, '127.0.0.1', function(err) {
        if (err) throw err;
        self.updateChatter('a sent data');
      });
    });
  }

  render() {
    return (
      <View style={styles.container}>
        <ScrollView>
          {this.state.chatter.map((msg, index) => {
            return (
              <Text key={index} style={styles.welcome}>
                {msg}
              </Text>
            );
          })}
        </ScrollView>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
});

export default App;
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-udp": "file:../../node_modules/@react-native-oh-tpl/react-native-udp/harmony/react_native_udp.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)



### 3.在 ArkTs 侧引入 RNUdpPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...

+ import {RNUdpPackage} from '@react-native-oh-tpl/react-native-udp/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNUdpPackage(ctx)
  ];
}
```

### 4.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-udp Releases](https://github.com/react-native-oh-library/react-native-udp/releases)



## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name           | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| createSocket   | Creates a Socket object.                                     | Function | false    | Android/iOS | yes               |
| close          | Close the underlying socket and stop listening for data on it. If a callback is provided.                                     | Function | false    | Android/iOS | yes               |
| bind           | For UDP sockets, causes the `UdpSocket` to listen for datagram messages on a named `port`. | Function | false    | Android/iOS | yes               |
| send           | Broadcasts a datagram on the socket.                         | Function | false    | Android/iOS | yes               |
| address        | Returns an object containing the address information for a socket. | Function | false    | Android/iOS | yes               |
| setBroadcast   | Sets or clears the `SO_BROADCAST` socket option.             | Function | false    | Android/iOS | yes               |
| addMembership  | Tells the kernel to join a multicast group at the given `multicastAddress` and `multicastInterface` using the `IP_ADD_MEMBERSHIP` socket option. | Function | false    | Android/iOS | yes               |
| dropMembership | Instructs the kernel to leave a multicast group at `multicastAddress` using the `IP_DROP_MEMBERSHIP` socket option. | Function | false    | Android/iOS | yes               |





## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/tradle/react-native-udp/blob/master/LICENSE) ，请自由地享受和参与开源。