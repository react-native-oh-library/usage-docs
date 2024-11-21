> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-offline</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/rgommezz/react-native-offline">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20window%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/rgommezz/react-native-offline/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/rgommezz/react-native-offline)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install  react-native-offline@6.0.2
```

#### **yarn**

```bash
yarn add react-native-offline@6.0.2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import { View, Button } from 'react-native';
import { NetworkProvider, NetworkConsumer, useIsConnected, checkInternetConnection } from 'react-native-offline';

interface Context {
    pingUrl: string;
}

const DummyNetworkContext = React.createContext<Context>({
    pingUrl: 'https://www.huawei.com',
});

export const offlineDemoTest = () => {
    const isConnected = useIsConnected();
    const DEFAULT_TIMEOUT = 3000;
    const DEFAULT_PING_SERVER_URL = 'https://www.huawei.com/';
    const DEFAULT_HTTP_METHOD = 'HEAD';
    const DEFAULT_CUSTOM_HEADERS = {};
    return (
        <View>
            <View>
                {isConnected ? 'isConnected:YES' : 'isConnected:NO'}
            </View>
            <View>
                <DummyNetworkContext.Consumer>
                    {({ pingUrl }) => (
                        <NetworkProvider pingServerUrl={pingUrl}>
                            <NetworkConsumer >
                                {({ isConnected }) => (
                                    <View>
                                        {isConnected ? 'NetworkConsumer: YES' : 'NetworkConsumer :NO'}
                                    </View>
                                )}
                            </NetworkConsumer>
                        </NetworkProvider>
                    )}
                </DummyNetworkContext.Consumer>
            </View>
            <View>
                <Button
                    title='CheckInternetConnection'
                    onPress={async () => {
                        const isConnected = await checkInternetConnection(
                            DEFAULT_PING_SERVER_URL,
                            DEFAULT_TIMEOUT,
                            true,
                            DEFAULT_HTTP_METHOD,
                            DEFAULT_CUSTOM_HEADERS)
                        if (isConnected === true) {
                            <View>
                                CheckInternetConnection: yes
                            </View>
                        }
                    }}
                />
            </View>
        </View>
    );
};
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-community/netinfo. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in @react-native-community/netinfo to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                                  | Type        | Required | Platform              | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ----------- | -------- | --------------------- | ----------------- |
| children              | a React Element. This is the only required prop.             | React.Node  | yes      | Android、iOS、Windows | yes               |
| pingTimeout           | amount of time (in ms) that the component should wait for the ping response. Defaults to 10000 ms. If you want to use a different value, it's recommended to use a higher one. | number      | no       | Android、iOS、Windows | yes               |
| pingServerUrl         | remote server to ping to. Defaults to https://www.google.com/ since it's probably one the most stable servers out there, but you can provide your own if needed. Warning: www.google.com is a blocked domain in China, so if you need your app to be accessible from there, you MUST use another domain. | string      | no       | Android、iOS、Windows | yes               |
| shouldPing            | flag that denotes whether the extra ping check will be performed or not. Defaults to true. | boolean     | no       | Android、iOS、Windows | yes               |
| pingInterval          | the interval (in ms) you want to ping the server at. Defaults to 0, and that means it is not going to check connectivity regularly. If opted in, it's advised not to choose a very small value, because that may drain your battery. Choose wisely. Something around 30000 ms should be fine. | number      | no       | Android、iOS、Windows | yes               |
| pingOnlyIfOffline     | when set to true and pingInterval > 0, it will ping the remote server regularly only if offline. Defaults to false. | boolean     | no       | Android、iOS、Windows | yes               |
| pingInBackground      | whether or not to check connectivity when app isn't in the foreground. Defaults to false. | boolean     | no       | Android、iOS、Windows | yes               |
| httpMethod            | http method used to ping the server. Supports HEAD or OPTIONS. Defaults to HEAD. | HTTPMethod  | no       | Android、iOS、Windows | yes               |
| customHeaders         | optional custom headers to add for ping request.             | HTTPHeaders | no       | Android、iOS、Windows | yes               |
| regexActionType       | regular expression to indicate the action types to be intercepted in offline mode. By default it's configured to intercept actions for fetching data following the Redux convention. That means that it will intercept actions with types such as FETCH_USER_ID_REQUEST, FETCH_PRODUCTS_REQUEST etc. | RegExp      | no       | Android、iOS、Windows | yes               |
| actionTypes           | array with additional action types to intercept that don't fulfil the RegExp criteria. For instance, it's useful for actions that carry along refreshing data, such as REFRESH_LIST. | Arrays      | no       | Android、iOS、Windows | yes               |
| queueReleaseThrottle  | waiting time in ms between dispatches when flushing the offline queue. Useful to reduce the server pressure when coming back online. Defaults to 50ms. | number      | no       | Android、iOS、Windows | yes               |
| shouldDequeueSelector | function that receives the redux application state and returns a boolean. It'll be executed every time an action is dispatched, before it reaches the reducer. This is useful to control if the queue should be released when the connection is regained and there were actions queued up. Returning true (the default behaviour) releases the queue, whereas returning false prevents queue release. For example, you may wanna perform some authentication checks, prior to releasing the queue. Note, if the result of shouldDequeueSelector changes while the queue is being released, the queue will not halt. If you want to halt the queue while is being released, please see relevant FAQ section. | boolean     | no       | Android、iOS、Windows | yes               |
| url                   | remote server to ping to. Defaults to https://www.google.com/ since it's probably one the most stable servers out there, but you can provide your own if needed. Warning: www.google.com is a blocked domain in China, so if you need your app to be accessible from there, you MUST use another domain. | string      | no       | Android、iOS、Windows | yes               |
| method                | http method used to ping the server. Supports HEAD or OPTIONS. Defaults to HEAD. | HTTPMethod  | no       | Android、iOS、Windows | yes               |

## Static Methods 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                    | Description                                                  | Type | Required | Platform              | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | ---- | -------- | --------------------- | ----------------- |
| NetworkProvider         | Provider component that injects the network state to children  components via React Context. Only children prop is required, the rest  are optional. It should be used on top of your components hierarchy, ideally  in (or close to) the entry point. | func | no       | Android、iOS、Windows | yes               |
| NetworkConsumer         | React component that subscribes to connectivity changes. It requires a  function as a child. The function receives the current connectivity status  and returns a React node. This component should be rendered within a  NetworkProvider in order to work properly. | func | no       | Android、iOS、Windows | yes               |
| useIsConnected          | Returns a boolean indicating whether you are connected to the network or not. | func | no       | Android、iOS、Windows | yes               |
| ReduxNetworkProvider    | Uses a provider component mechanism. The same props as for `NetworkProvider` apply. Make sure your component is a descendant of the react-redux `<Provider>` component, so that `ReduxNetworkProvider` has access to the store. | func | no       | Android、iOS、Windows | yes               |
| networkSaga             | Just fork this saga from your root saga. It accepts the same config options as NetworkProvider and ReduxNetworkProvider. Recommended if you are using redux-saga, since it's a very elegant way to deal with global connectivity changes, without having to wrap your components with extra functionality. | func | no       | Android、iOS、Windows | yes               |
| createNetworkMiddleware | Function that returns a Redux middleware which listens to specific actions targeting API calls in online/offline mode. | func | no       | Android、iOS、Windows | yes               |
| OfflineQueue            | A queue system to store actions that failed due to lack of connectivity. It works for both plain object actions and thunks. | func | no       | Android、iOS、Windows | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/rgommezz/react-native-offline/blob/master/LICENSE) ，请自由地享受和参与开源
