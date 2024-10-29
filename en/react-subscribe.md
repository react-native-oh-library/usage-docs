> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-subscribe</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/tdzl2003/react-subscribe">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.isc.org/licenses/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/tdzl2003/react-subscribe)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install react-subscribe@1.3.2
```

#### **yarn**

```bash
yarn add react-subscribe@1.3.2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React from 'react';
import { Timer } from 'react-subscribe';
import { Text, View,Button} from 'react-native'

export class ReactSubscribeTimerTest extends React.Component {
  state = {
    cd: this.props.cd,
    listening:false
  };
  onTimer = () => {
    this.setState({ cd: this.state.cd - this.props.interval/1000,listening:true });
  };
  timeClick = () => {
    this.setState({cd: this.props.cd,listening: true});
  };
  render() {
    if (this.state.cd <= 0) {
      return (
        <View>
          <Button title='click' onPress={() => this.timeClick()}>click</Button>
          <Text>Cooldown is over and onTimer will not be called again!</Text>
        </View>
      );
    }
    return (
      <View>
        <Button title='click' onPress={() => this.timeClick()}>click</Button>
        {this.state.listening && <Timer interval={this.props.interval} onTimer={this.onTimer}><Text>There is still {this.state.cd} seconds to go.</Text></Timer>}
        <Text>Click the button to start the countdown</Text>
      </View>
    );
  }
}
```

The following code shows the basic use scenario of the Subscribe component:

> [!WARNING] Generally, the `target` is used together with the fbemitter component.
> 
```js
import React from 'react';
import { Subscribe } from 'react-subscribe';
import { TextInput, Text, View,Button} from 'react-native'

export class ReactSubscribeSubscribeTest extends React.Component {
  state = {
    listening : true
  }

  eventName='test1';
  message = '';
  eventType = 1;

  test1Message;
  test2Message;
  test3Message;


  onChangeText(eventName){
    this.eventName = eventName;
  }

  onChangeMessage(message){
    this.message = message;
  }

  eventNameEvent = (ev) => {
    this.setState({
      listening : true
    })
    this.test1Message = ev.message;
  };

  otherEvent = (ev) => {
    this.setState({
      listening : true
    })
    this.test2Message = ev.message;
  };

  sendMessage(){
    if(this.eventName === 'test1'){
      this.props.eventEmitter1.emit(this.eventName, { message: this.message});
    }else{
      this.props.eventEmitter2.emit(this.eventName, { message: this.message});
    }
  }

  render() {
    return (
      <View>
        <TextInput
          placeholder="请输入内容eventName（只有test1和test2输入其他无效）"
          style={{ height: 40, borderColor: 'gray', borderWidth: 1 }}
          onChangeText={text => this.onChangeText(text)}
          value={111}
        />
        <TextInput
          placeholder="Please enter the content to be sent"
          style={{ height: 40, borderColor: 'gray', borderWidth: 1 }}
          onChangeText={text => this.onChangeMessage(text)}
          value={111}
        />
        <Button title='send' onPress={() => this.sendMessage()}>click</Button>
        <Text>'1.监听test1'</Text>
        <Subscribe target={this.props.eventEmitter1} eventName="test1" listener={this.eventNameEvent} />
        {this.test1Message !== null && <Text>test1监听数据:{this.test1Message}</Text>}
        <Text>'2.监听test2'</Text>
        <Subscribe target={this.props.eventEmitter2} eventName="test2" listener={this.otherEvent} >
          <Text>test2监听数据:{this.test2Message}</Text>
        </Subscribe>
      </View>
    );
  }
}
```

Example

``` 
import { EventEmitter } from 'fbemitter';

<ReactSubscribeSubscribeTest eventEmitter1={eventEmitter1} eventEmitter2={eventEmitter1}/>

```

The following code shows the basic use scenario of the Fetch component:

```js
import React from 'react';
import { View,StyleSheet,Text,TouchableOpacity,Button } from 'react-native';
import { Fetch } from 'react-subscribe';
import axios from 'axios';

export class ReactSubscribeFetchTest extends React.Component {

  state = {
    listening:false
  };

  timeClick = () => {
    this.setState({listening: true});
  };

  fetch_option = {
    timeout: 5000,
    method: this.props.method,
    headers: {
      'X-AccessToken': 'some_token',
      "Content-Type":this.props.contentType
    },
    body:this.props.body,
    credentials: 'include', // Default credentials is 'same-origin' in `Fetch`
  };
  
  render (){
    if(this.props.manners === 1){
      return(
        <View>
         <Button title='click' onPress={() => this.timeClick()}>click</Button>
          {this.state.listening && <Fetch doFetch={customRequest} url={this.props.url}>
          <SomeComponent2/>
        </Fetch>}
      </View>
      )
    }
    return(
      <View>
       <Button title='click' onPress={() => this.timeClick()}>click</Button>
        {this.state.listening && <Fetch url={this.props.url} type={this.props.type} options={this.fetch_option}>
        <SomeComponent/>
      </Fetch>}
    </View>
    )
  };
}

function SomeComponent({ data, loading, error, reload, statusCode }) {
  if (loading) {
    return <View><Text>loading...</Text></View>;
  }
  if (error) {
    return (
      <View>
        <Text>error:{error.message}</Text>
        <Button title='点击重新请求' onPress={() => reload()}>click</Button>
      </View>
    );
  }

  return (
    <View>
      <Text>Status Code: {statusCode}</Text>
      <Text>{JSON.stringify(data)}</Text>
    </View>
  );
}

async function customRequest(url) {
  return axios.get(url,{params:{
    value:'自定义组件请求',
  }});
}

function SomeComponent2({ data, loading, error, reload }) {
  if (loading) {
    return <View><Text>loading...</Text></View>;
  }
  if (error) {
    return (
      <View>
        <Text>Error: {error.message}</Text>
        <Button title='点击重新请求' onPress={() => reload}>click</Button>
      </View>
    );
  }
  return (
    <View>
      <Text>Status Code: {data.status}</Text>
      <Text>{JSON.stringify(data.data)}</Text>
    </View>
  );
}
```
## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.26; SDK: HarmonyOS-Next-DB1; IDE: DevEco Studio 5.0.3.300; ROM: 3.0.0.25;
2. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71(API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### react-subscribe:

For details about the Fetch component, see [react-subscribe](https://github.com/tdzl2003/react-subscribe/blob/master/src/Fetch.js)

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| url  | 请求接口url | string  | no | Android/iOS      | yes |
| options  | 请求参数（如果使用doFetch，参数不生效） | object  | no | Android/iOS | yes |
| doFetch  | 自定义的请求服务端方法，方法接收参数为组件url | function  | no | Android/iOS | yes |
| type  | 请求返回数据处理的类型(值只能为'text'或 'json'或'blob')  | string | yes | Android/iOS | yes |
| children| 子组件，接收请求返回数据处理,接收参数有(loading:是否在请求中,statusCode：请求状态码（自定义请求不设置该值）,data:返回业务数据,error:请求错误信息（例：请求超时）,reload:刷新当前请求方法) | element | no | Android/iOS | yes |

For details about the Timer component, see [react-subscribe](https://github.com/tdzl2003/react-subscribe/blob/master/src/Timer.js)

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| interval | 执行间隔时间（毫秒）       | number  | no | Android/iOS | yes |
| onTimer  | 定时执行方法 | function   | no | Android/iOS | yes |
| children | 子组件   | element  | no | Android/iOS  | yes |

For details about the Subscribe component, see [react-subscribe](https://github.com/tdzl2003/react-subscribe/blob/master/src/Subscribe.js)

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| target  | 发射器（一般配合fbemitter组件使用） | object  | no | Android/iOS  | yes |
| eventName | 事件名称 | string  | no | Android/iOS  | yes |
| listener  | 监听方法（当发射器触发当前事件时执行的方法） | function  | no | Android/iOS  | yes |
| children | 子组件 | element  | no | Android/iOS  | yes |

For details about the SubscribeDOM component, see [react-subscribe](https://github.com/tdzl2003/react-subscribe/blob/master/src/SubscribeDOM.js)

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| target  | 发射器（一般配合web中document使用） | object  | no | webOnly  | no |
| eventName | 事件名称 | string  | no | webOnly  | no |
| listener  | 监听方法（当发射器触发当前事件时执行的方法） | function  | no | webOnly  | no |
| children | 子组件 | element  | no | webOnly  | no |

## Known Issues

## Others

## License

This project is licensed under [The ISC License (ISC)](https://www.isc.org/licenses/).