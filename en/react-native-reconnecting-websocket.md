> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/React-Sextant/react-native-reconnecting-websocket)

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

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
                <Text style={{ lineHeight: 30, textAlign: 'center' }}>Automatically connect to the server upon entering the page</Text>
                <Button
                    title='ws.close( )-----Close connection'
                    onPress={() => {
                        ws.close()
                    }}
                />
                <View style={{ height: 30 }} />
                <Button
                    title='ws.send(可口可乐)-----Send a message'
                    onPress={() => {
                        ws.send('可口可乐')
                    }}
                />
                <View style={{ height: 30 }} />
                <Button
                    title='ws.reconnect( )-----Refresh Connection'
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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.29; SDK：HarmonyOS NEXT Developer Beta6; IDE：DevEco Studio 5.0.3.706; ROM：3.0.0.60;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API

> [!Tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!Tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                          | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `ReconnectingWebSocket()`     | Creating a WebSocket Entity Object for Automatic Reconnection. | Class  | Yes      | All      | Yes               |
| `send(message: string): void` | Sends a message through the WebSocket connection.            | Method | No       | All      | Yes               |
| `close(): void`               | Closes the WebSocket connection.                             | Method | No       | All      | Yes               |
| `ping(): void`                | Sends a ping frame to the server.                            | Method | No       | All      | Yes               |
| `reconnect(): void`           | Closes the current WebSocket connection and attempts to reconnect using the initial parameters. | Method | No       | All      | Yes               |

## Known Issues
## Others
## License

This project is licensed under [The MIT License (MIT)](https://mitlicense.org/).