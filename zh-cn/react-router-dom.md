> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-router-dom</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/remix-run/react-router/tree/main/packages/react-router-dom">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/remix-run/react-router/blob/main/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/remix-run/react-router/tree/main/packages/react-router-dom)

## 安装与使用

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm i react-router-dom@6.22.3
```
#### **yarn**

```bash
yarn add react-router-dom@6.22.3
```
下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React from 'react';
import { Platform, StyleSheet, Text, TextInput, View, Button, ScrollView } from 'react-native';
import {
    Route, Routes, Navigate, Outlet, useLocation,
    useNavigate,
    useOutlet,
    useRoutes,
    MemoryRouter as Router
} from 'react-router-dom';

const Home = () => {
    const navigate = useNavigate();
    const outlet = useOutlet();
    const [messages, setMessages] = React.useState(false);
    const [tasks, setTasks] = React.useState(false);
    return (
        <View>
            <Text>Welcome to the Home page!</Text>
            <Button title={`To Login by navigate("/login")`} onPress={() => {
                navigate("/login");
            }} />
            <Button title={"To Login by navigate(1)"} onPress={() => {
                navigate(1);
            }} />

            <Button title={"To detail by navigate(2)"} onPress={() => {
                navigate(2);
            }} />

            <Button title={"To Index3 by navigate(3) initialEntries下标"} onPress={() => {
                navigate(3);
                // 
            }} />

            <Button title={`To Index3 by navigate("/index3")`} onPress={() => {
                navigate("/index3");
            }} />
            <Button title={"Show messages by Navigate"} onPress={() => {
                setMessages(true)
                setTasks(false)
            }} />
            <Button title={`Show Tasks by navigate("/messages")`} onPress={() => {
                setTasks(true)
                setMessages(false)
                navigate("/messages", {
                    state: {
                    },
                    replace: false,
                    relative: 'route',
                    preventScrollReset: false,
                });
            }} />
            <Button title={`Show Tasks by navigate("/tasks")`} onPress={() => {
                setTasks(true)
                setMessages(false)
                navigate("/tasks", {
                    state: {
                    },
                    replace: false,
                    relative: 'route',
                    preventScrollReset: true,
                });
            }} />

            {messages && (<Navigate to="/messages" replace={false} />)}
            {tasks && (<Text>下面由Outlet生成</Text>)}
            {tasks && (<Outlet />)}
            {messages && (<Text>下面由useOutlet生成</Text>)}
            {messages && (outlet)}
        </View>
    );
};

const HomeMessages = () => {
    return (
        <View style={{ height: 200, backgroundColor: 'yellow' }}>
            <Text>Outlet Demo: HomeMessages page!</Text>
        </View>
    );
};

const HomeTasks = () => {
    return (
        <View style={{ height: 200, backgroundColor: 'red' }}>
            <Text>Outlet Demo: HomeTasks page!</Text>
        </View>
    );
};

const Login = () => {
    const navigate = useNavigate();
    const [login, setLogin] = React.useState(false);
    const [warning, setWarning] = React.useState(false);
    const [username, setUsername] = React.useState('');
    const location = useLocation();

    return (
        <View>
            <Text>Welcome to the Login page!</Text>
            <Text>{location.state?.stateTest} </Text>
            <TextInput placeholder="Input your username" style={{
                color: 'black', height: 40, fontSize: 16, backgroundColor: 'white', borderColor: "blue", borderWidth: 1, borderRadius: 20, paddingLeft: 20
            }}
                onChangeText={(value) => {
                    setUsername(value);
                    setWarning(value.length == 0)
                }} />
            {warning && (<Text style={{ color: 'red' }}>username is empty.</Text>)}
            <Button title={"Login by <Navigate/>"} onPress={() => {
                if (username.length == 0) {
                    setWarning(true)
                    return
                }
                setLogin(true)
            }} />
            {login && (<Navigate to="/detail" state={{ name: username }} replace={false} />)}

            <Button title={`Login by navigate("/detail")`} onPress={() => {
                if (username.length == 0) {
                    setWarning(true)
                    return
                }
                navigate("/detail", {
                    state: {
                        name: username
                    },
                    replace: false,
                    relative: 'route',
                    preventScrollReset: true,
                });

            }} />
            <Button title={"Back Home by navigate(-1)"} onPress={() => {
                navigate(-1);
            }} />
        </View>
    );
};


const LocationTest = () => {
    const location = useLocation();
    return (
        <View>
            <Text>---- {location.key.length == 0 ? "LocationTest page!" : location.key} ----</Text>
            <Text>pathname:{location.pathname} search:{location.search} hash:{location.hash} </Text>
        </View>
    );
};

const UseRoutesTestHome = () => {
    const location = useLocation();
    return (
        <View>
            <Text>---- UseRoutesTestHome home page! ----</Text>
            <Text>pathname:{location.pathname} search:{location.search} hash:{location.hash} </Text>
        </View>
    );
};


const Index3 = () => {
    const navigate = useNavigate();
    const location = useLocation();
    return (
        <View>
            <Text>---- Index3 page! ----</Text>
            <Text>`---- 如果跳转由navigate("/index3") navigate(-1),回返回上一个页面；如果由navigate(3)，则返回initialEntries 下标为2的页面 ----`</Text>
            <Button title={"Back Home by navigate(-1)"} onPress={() => {
                navigate(-1);
            }} />
            <Button title={"Back Home by navigate(-2)"} onPress={() => {
                navigate(-2);
            }} />
            <Button title={"Back Home by navigate(-3)"} onPress={() => {
                navigate(-3);
            }} />
        </View>
    );
};



const Detail = () => {
    const navigate = useNavigate();
    const location = useLocation();
    return (
        <View>
            <Text>{location.state?.name}  logged in successfully! Detail page!</Text>
            <Button title={"Logout"} onPress={() => {
                navigate(-1)
            }} />
            <Button title={"Back Home navigate(-2)"} onPress={() => {
                // seHome(true)
                // 返回上两个  replace={false} 需要
                navigate(-2);
            }} />
        </View>
    );
};

const styles = StyleSheet.create({
    container: {
        flex: 1,
        marginTop: Platform.OS === 'ios' ? 50 : 5, margin: 10,
    },
    root: {
        flex: 1,
    },
    webView: {
        flex: 1,
    },
    link: {
        padding: 10,
        backgroundColor: 'lightblue',
    },
});

function UseRoutesTest() {
    let element = useRoutes([
        {
            path: "/",
            element: <UseRoutesTestHome />,
        },
        { path: "/locationTest", element: <LocationTest /> },
    ]);
    return element;
}

function UseRoutesTest2() {
    const location = {
        pathname: '/locationTest',
        search: '?id=1&name=test',
        hash: '#section1',
        key: "UseRoutesTest2 page",
    };
    let element = useRoutes([
        { path: "/locationTest", element: <LocationTest /> },
    ], location);
    return element;
}

const DomDemo = () => {
    const initialEntries = [
        "/",
        { pathname: "/login", state: { stateTest: "stateTestContent" } },
        { pathname: "/detail", state: { stateTest: "stateTestContent" } },
        "/index3",
    ];
    const location = {
        pathname: '/locationTest',
        search: '?id=1&name=test',
        hash: '#section1',
        key: "locationTest page",
    };
    const initialIndex = 0;
    return (
        <ScrollView style={styles.container}>
            <Router>
                <Routes location={location}>
                    <Route path="/locationTest" element={<LocationTest />} />
                </Routes>
            </Router>

            <Router>
                <UseRoutesTest />
            </Router>
            <Router>
                <UseRoutesTest2 />
            </Router>
            <Router initialEntries={initialEntries} initialIndex={initialIndex} future={{ v7_startTransition: true }}>
                <Routes>
                    <Route path="/" element={<Home />} >
                        <Route path="messages" element={<HomeMessages />} />
                        <Route path="tasks" element={<HomeTasks />} />
                    </Route>
                    <Route path="/login" element={<Login />} />
                    <Route path="/detail" element={<Detail />} />
                    <Route path="/index3" element={<Index3 />} />
                </Routes>
            </Router>
        </ScrollView>
    );
};
export default DomDemo;
```
## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.28; SDK:HarmonyOS-Next-DB5 5.0.0.60 SDK; IDE: DevEco Studio 5.0.3.655; ROM: 3.0.0.60;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，详情见 [react-router-dom源库地址](https://github.com/remix-run/react-router)

**Hooks**

| Name        | Description                                                                                                                                                                                                                                         | Type     | Required | Platform | HarmonyOS Support |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| Route   | Routes are perhaps the most important part of a React Router app. They couple URL segments to components, data loading and data mutations. Through route nesting, complex application layouts and data dependencies become simple and declarative. | Component | NO       | Android、iOS      | YES               |
| Routes   | Rendered anywhere in the app, <Routes> will match a set of child routes from the current location. | Component | NO       | Android、iOS      | YES               |
| Navigate   | A <Navigate> element changes the current location when it is rendered. It's a component wrapper around useNavigate, and accepts all the same arguments as props.<docs-info>Having a component-based version of the useNavigate hook makes it easier to use this feature in a React.Component subclass where hooks are not able to be used.</docs-info> | Component | NO       | Android、iOS     | YES               |
| Outlet   | An <Outlet> should be used in parent route elements to render their child route elements. This allows nested UI to show up when child routes are rendered. If the parent route matched exactly, it will render a child index route or nothing if there is no index route. | Component | NO       | Android、iOS      | YES               |
| MemoryRouter   | A <MemoryRouter> stores its locations internally in an array. Unlike <BrowserHistory> and <HashHistory>, it isn't tied to an external source, like the history stack in a browser. This makes it ideal for scenarios where you need complete control over the history stack, like testing. | Component | NO       | Android、iOS     | YES               |
| useLocation | This hook returns the current [`location`](https://reactrouter.com/en/main/utils/location) object. This can be useful if you'd like to perform some side effect whenever the current location changes.                                              | Function | NO       | Android、iOS      | YES               |
| useNavigate | The `useNavigate` hook returns a function that lets you navigate programmatically, for example in an effect:                                                                                                                                        | Function | NO       | Android、iOS      | YES               |
| useOutlet   | Returns the element for the child route at this level of the route hierarchy. This hook is used internally by < Outlet > to render child routes.                                                                                                    | Function | NO       | Android、iOS      | YES               |
| useRoutes   | The useRoutes hook is the functional equivalent of < Routes >, but it uses JavaScript objects instead of < Route > elements to define your routes. These objects have the same properties as normal < Route > elements, but they don't require JSX. | Function | NO       | Android、iOS      | YES               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/remix-run/react-router/blob/main/LICENSE.md) ，请自由地享受和参与开源。

