> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-mqtt</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Introvertuous/react-native-mqtt">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Introvertuous/react-native-mqtt/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [GitHub address](https://github.com/Introvertuous/react-native-mqtt)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm i react_native_mqtt@1.3.1
```

#### **yarn**

```bash
yarn add react_native_mqtt@1.3.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.(本组件基于MQTT 3.1.1协议)

```js
import init from 'react_native_mqtt';
import { AsyncStorage } from 'react-native';

//初始化参数
init({
    size: 10000,
    storageBackend: AsyncStorage,
    defaultExpires: 1000 * 3600 * 24,
    enableCache: true,
    reconnect: true,
    sync: {}
});
//MQTT服务器配置
const options = {
    host: 'i1b2c58a.ala.dedicated.aliyun.emqxcloud.cn',
    port: 8083,
    path: '/mqtt',
    userName: 'test1',
    password: '123456',
    keepAliveInterval: 600,
    cleanSession: true,
    clientId: 'mqttTestDemo' + Math.random().toString(16).substring(2, 8)
};
//连接成功
function onConnect() {
    client.subscribe('testTopic', { qos: 0 });
    console.info("Connect Success! ");
}
//连接失败
function onFailure(err) {
    if (err.errorCode !== 0) {
        console.error('Connect Failed! ' + err.errorMessage);
    }
}
//连接丢失
function onConnectionLost(err) {
    if (err.errorCode !== 0) {
        console.error("onConnectionLost:" + err.errorMessage);
    }
}
//接收消息
function onMessageArrived(message) {
    console.info('onMessageArrived: ' + message.payloadString);
}
//连接服务器
const client = new Paho.MQTT.Client(options.host, options.port, options.path, options.clientId);
client.onConnectionLost = onConnectionLost;
client.onMessageArrived = onMessageArrived;
client.connect({
    onSuccess: onConnect,
    onFailure: onFailure,
    useSSL: false,
    userName: options.userName,
    password: options.password,
    keepAliveInterval: options.keepAliveInterval,
    cleanSession: options.cleanSession
});
//取消连接
function disconnect() {
  client.disconnect();
  console.info("DisConnect Success! ");
}
//订阅主题
function subscribe() {
  client.subscribe(onChangeTopic, { qos: 0 });
  console.info("subscribe success! ");
}
//取消订阅
function unSubscribe() {
  client.unsubscribe(onChangeTopic);
  console.info("unsubscribe success! ");
}
//消息发布
function sendMessage() {
  var message = new Paho.MQTT.Message(onChangeMessage);
  message.destinationName = topic;
  client.send(message);
  console.info('send success! ')
}
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400; ROM: 3.0.0.25;
2. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71(API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                                          | Type   | Required | Platform    | HarmonyOS Support |
| ----------------- | ---------------------------------------------------- | ------ | -------- |-------------| ----------------- |
| host              | 服务器地址                                           | string | yes      | Android iOS | yes               |
| port              | 服务器端口                                           | number | yes      | Android iOS | yes               |
| path              | 服务器路径                                           | string | yes      | Android iOS | yes               |
| userName          | 用户名                                               | string | yes      | Android iOS | yes               |
| password          | 密码                                                 | string | yes      | Android iOS | yes               |
| keepAliveInterval | 会话过期时间（秒）                                   | number | no       | Android iOS | yes               |
| cleanSession      | 消息持久化（值为TRUE时，当客户端掉线，清除以前消息） | bool   | no       | Android iOS | yes               |
| clientId          | 客户端ID                                             | string | yes      | Android iOS | yes               |
| useSSL            | SSL/TLS加密通信                                      | bool   | yes      | Android iOS | yes               |
| qos               | 服务级别质量                                         | number | yes      | Android iOS | yes               |

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name             | Description        | Type | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------ | ---- | -------- |-------------| ----------------- |
| client.connect   | 连接MQTT服务器     | func | yes      | Android iOS | yes               |
| onConnect        | 连接成功时的回调   | func | no       | Android iOS | yes               |
| onFailure        | 连接失败时的回调   | func | no       | Android iOS | yes               |
| onConnectionLost | 连接丢失           | func | no       | Android iOS | yes               |
| onMessageArrived | 接收消息           | func | no       | Android iOS | yes               |
| disconnect       | 取消连接MQTT服务器 | func | no       | Android iOS | yes               |
| subscribe        | 订阅主题topic      | func | no       | Android iOS | yes               |
| unSubscribe      | 取消订阅topic      | func | no       | Android iOS | yes               |
| sendMessage      | 发布消息           | func | no       | Android iOS | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/Introvertuous/react-native-mqtt/blob/master/LICENSE).
