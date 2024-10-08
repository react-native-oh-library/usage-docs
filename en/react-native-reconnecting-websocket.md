> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-reconnecting-websocket</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/React-Sextant/react-native-reconnecting-websocket">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://mitlicense.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>





> [!TIP] [Github 地址](https://github.com/React-Sextant/react-native-reconnecting-websocket)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-reconnecting-websocket@^2.0.0
```

#### **yarn**

```bash
yarn add react-native-reconnecting-websocket@^2.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { useEffect, useState } from 'react';
import { Button, View, Text, ScrollView } from 'react-native';
import ReconnectingWebSocket from 'react-native-reconnecting-websocket';

const ws = new ReconnectingWebSocket('ws://121.196.235.57/ws');

const ReconnectingWebsocketDemo = () => {
    const [html, innerHTML] = useState('');

    useEffect(() => {
        return () => {
            ws.close();
        }
    }, [])

    useEffect(() => {
        ws.onopen = e => {
            console.log('onopen:' + JSON.stringify(e));
            innerHTML('onopen:' + JSON.stringify(e) + '\n' + '\n' + html);
        }
        ws.onmessage = e => {
            console.log('onmessage:' + JSON.stringify(e));
            innerHTML('onmessage:' + JSON.stringify(e) + '\n' + '\n' + html);
        }
        ws.onclose = e => {
            console.log('onclose:' + JSON.stringify(e));
            innerHTML('onclose:' + JSON.stringify(e) + '\n' + '\n' + html);
        }
        ws.onerror = e => {
            console.log('onerror:' + JSON.stringify(e));
            innerHTML('onerror:' + JSON.stringify(e) + '\n' + '\n' + html);
        }
        ws.onconnecting = e => {
            console.log("onconnecting:" + JSON.stringify(e));
            innerHTML("onconnecting:" + JSON.stringify(e) + '\n' + '\n' + html);
        }
    }, [html])
    return (
        <>
            <View style={{ height: '100%' }}>
                <Text style={{ lineHeight: 30, textAlign: 'center' }}>进入页面自动连通服务器</Text>
                <Button
                    title='ws.close( )-----关闭连接'
                    onPress={() => {
                        ws.close()
                    }}
                />
                <View style={{ height: 30 }} />
                <Button
                    title='ws.send(可口可乐)-----发送信息'
                    onPress={() => {
                        ws.send('可口可乐')
                    }}
                />
                <View style={{ height: 30 }} />
                <Button
                    title='ws.reconnect( )-----刷新连接'
                    onPress={() => {
                        ws.reconnect()
                    }}
                />
                <ScrollView style={{ flex: 1 }}>
                    <Text>{html}</Text>
                </ScrollView>
            </View>
        </>
    )
}

export default ReconnectingWebsocketDemo;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.29; SDK：HarmonyOS NEXT Developer Beta6; IDE：DevEco Studio 5.0.3.706; ROM：3.0.0.60;

## API

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                          | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `ReconnectingWebSocket()`     | Creating a WebSocket Entity Object for Automatic Reconnection. | Class  | Yes      | All      | Yes               |
| `send(message: string): void` | Sends a message through the WebSocket connection.            | Method | No       | All      | Yes               |
| `close(): void`               | Closes the WebSocket connection.                             | Method | No       | All      | Yes               |
| `ping(): void`                | Sends a ping frame to the server.                            | Method | No       | All      | Yes               |
| `reconnect(): void`           | Closes the current WebSocket connection and attempts to reconnect using the initial parameters. | Method | No       | All      | Yes               |

## 遗留问题
## 其他
## 开源协议

本项目基于 [The MIT License (MIT)](https://mitlicense.org/)，请自由地享受和参与开源。