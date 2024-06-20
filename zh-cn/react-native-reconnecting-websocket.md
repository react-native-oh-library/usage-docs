> 模板版本：v0.2.0  

  <p align="center">  
  <h1 align="center"> <code>react-native-reconnecting-websocket</code> </h1>  
  </p >  
  <p align="center">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p> 


> [!TIP] 
>
> [Github 地址](https://github.com/React-Sextant/react-native-reconnecting-websocket)

# 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

```bash
npm install react-native-reconnecting-websocket@^1.0.3
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

<!-- {% raw %} -->
```js
import React, { useEffect, useRef } from 'react';
import { View, Text, Button } from 'react-native';
import ReconnectingWebSocket from 'react-native-reconnecting-websocket';

const WebSocketExample = () => {
  // WebSocket 实例的引用
  const ws = useRef(null);

  // 初始化 WebSocket 连接
  useEffect(() => {
    // WebSocket 连接地址
    const url = 'ws://124.222.224.186:8800';

    // 创建 WebSocket 实例
    ws.current = new ReconnectingWebSocket(url);

    // 监听连接成功事件
    ws.current.onopen = () => {
      console.log('WebSocket 连接已打开');
    };

    // 监听接收到消息事件
    ws.current.onmessage = (event) => {
      console.log('接收到消息:', event.data);
    };

    // 监听连接关闭事件
    ws.current.onclose = () => {
      console.log('WebSocket 连接已关闭');
    };

    // 监听连接发生错误事件
    ws.current.onerror = (error) => {
      console.error('WebSocket 连接发生错误:', error);
    };

    // 组件卸载时关闭 WebSocket 连接
    return () => {
      if (ws.current) {
        ws.current.close();
      }
    };
  }, []);

  // 发送消息
  const sendMessage = () => {
    if (ws.current) {
      const message = 'Hello, WebSocket!';
      ws.current.send(message);
      console.log('发送消息:', message);
    }
  };

  // 关闭连接
  const closeConnection = () => {
    if (ws.current) {
      ws.current.close();
    }
  };

  // 发送 ping
  const sendPing = () => {
    if (ws.current) {
      ws.current.ping();
      console.log('发送 ping');
    }
  };

  return (
    <View>
      <Text>WebSocket Example</Text>
      <Button title="Send Message" onPress={sendMessage} />
      <Button title="Close Connection" onPress={closeConnection} />
      <Button title="Send Ping" onPress={sendPing} />
    </View>
  );
};

export default WebSocketExample;
```
<!-- {% endraw %} -->

# 约束与限制

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

# API

以下是更新后的 API 列表：

| Name                          | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `send(message: string): void` | Sends a message through the WebSocket connection.            | Method | Yes      | All      | Yes               |
| `close(): void`               | Closes the WebSocket connection.                             | Method | No       | All      | Yes               |
| `open(): void`                | Opens the WebSocket connection if it's not already open.     | Method | No       | All      | Yes               |
| `ping(): void`                | Sends a ping frame to the server.                            | Method | No       | All      | Yes               |
| `reconnect(): void`           | Closes the current WebSocket connection and attempts to reconnect using the initial parameters. | Method | No       | All      | Yes               |

以上是 `react-native-reconnecting-websocket` 的主要方法和参数说明。

# 其他

# 开源协议

本项目基于 [MIT License](https://github.com/eranbo/react-native-base64/blob/master/LICENSE) ，请自由地享受和参与开源。