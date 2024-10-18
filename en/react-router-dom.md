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

> [!Tip] [Github 地址](https://github.com/remix-run/react-router/tree/main/packages/react-router-dom)

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

```js
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

1. RNOH: 0.72.28; SDK:HarmonyOS-Next-DB6 5.0.0.61 SDK; IDE: DevEco Studio 5.0.3.706; ROM: 3.0.0.61;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Component

| Name        | Description       | Type     | Required | Platform | HarmonyOS Support |
| ----------- | ----------------- | -------- | -------- | -------- | ----------------- |
| Route   | Routes are perhaps the most important part of a React Router app. They couple URL segments to components, data loading and data mutations. Through route nesting, complex application layouts and data dependencies become simple and declarative. | Component | no       |All      | yes               |
| Routes   | Rendered anywhere in the app, <Routes> will match a set of child routes from the current location. | Component | no       |All  | yes               |
| Navigate   | A <Navigate> element changes the current location when it is rendered. It's a component wrapper around useNavigate, and accepts all the same arguments as props.<docs-info>Having a component-based version of the useNavigate hook makes it easier to use this feature in a React.Component subclass where hooks are not able to be used.</docs-info> | Component | no       |All     | yes               |
| Outlet   | An <Outlet> should be used in parent route elements to render their child route elements. This allows nested UI to show up when child routes are rendered. If the parent route matched exactly, it will render a child index route or nothing if there is no index route. | Component | no       |All      | yes               |
| MemoryRouter   | A <MemoryRouter> stores its locations internally in an array. Unlike <BrowserHistory> and <HashHistory>, it isn't tied to an external source, like the history stack in a browser. This makes it ideal for scenarios where you need complete control over the history stack, like testing. | Component | no       |All     | yes               |
| BrowserRouter   |  A <BrowserRouter> stores the current location in the browser's address bar using clean URLs and navigates using the browser's built-in history stack.    | Component | no       | web   | no        |
| Form   |   The Form component is a wrapper around a plain HTML form that emulates the browser for client side routing and data mutations. It is not a form validation/state management library like you might be used to in the React ecosystem (for that, we recommend the browser's built in HTML Form Validation and data validation on your backend server).   | Component | no       | web   | no        |
| HashRouter   |   <HashRouter> is for use in web browsers when the URL should not (or cannot) be sent to the server for some reason.    | Component | no       | web   | no        |
| Link   |   A <Link> is an element that lets the user navigate to another page by clicking or tapping on it.   | Component | no       | web   | no        |
| NavLink   |  A <NavLink> is a special kind of <Link> that knows whether or not it is "active", "pending", or "transitioning".     | Component | no       | web   | no        |
| RouterProvider   | All data router objects are passed to this component to render your app and enable the rest of the data APIs.     | Component | no       | web   | no        |
| ScrollRestoration   |     This component will emulate the browser's scroll restoration on location changes after loaders have completed to ensure the scroll position is restored to the right spot, even across domains. | Component | no       | web   | no        |

### Hooks
| Name                            | Description       | Type     | Required | Platform | HarmonyOS Support |
|---------------------------------| ----------------- |----------|----------|----------|-------------------|
| useLocation                     | This hook returns the current [`location`](https://reactrouter.com/en/main/utils/location) object. This can be useful if you'd like to perform some side effect whenever the current location changes. | Function | no       | All      | yes               |
| useNavigate                     | The `useNavigate` hook returns a function that lets you navigate programmatically, for example in an effect:  | Function | no       | All      | yes               |
| useOutlet                       | Returns the element for the child route at this level of the route hierarchy. This hook is used internally by < Outlet > to render child routes.   | Function | no       | All      | yes               |
| useRoutes                       | The useRoutes hook is the functional equivalent of < Routes >, but it uses JavaScript objects instead of < Route > elements to define your routes. These objects have the same properties as normal < Route > elements, but they don't require JSX. | Function | no       | All      | yes               |
| createBrowserRouter             |  This is the recommended router for all React Router web projects. It uses the DOM History API to update the URL and manage the history stack.    | Function | no       | web      | no                |
| createHashRouter                |     This router is useful if you are unable to configure your web server to direct all traffic to your React Router application. Instead of using normal URLs, it will use the hash (#) portion of the URL to manage the "application URL". | Function | no       | web      | no                |
| createSearchParams              |   createSearchParams is a thin wrapper around new URLSearchParams(init) that adds support for using objects with array values.    | Function | no       | web      | no                |
| unstable_useprompt              |   The unstable_usePrompt hook allows you to prompt the user for confirmation via window.confirm prior to navigating away from the current location.   | Function | no       | web      | no                |
| unstable_useViewTransitionState |    This hook returns true when there is an active View Transition to the specified location. This can be used to apply finer-grained styles to elements to further customize the view transition. This requires that view transitions have been enabled for the given navigation via the unstable_viewTransition prop on the Link (or the Form, navigate, or submit call). | Function | no       | web      | no                |
| useBeforeUnload                 |  This hook is just a helper around window.onbeforeunload. It can be useful to save important application state on the page (to something like the browser's local storage), before the user navigates away from your page. That way if they come back you can restore any stateful information (restore form input values, etc.) | Function | no       | web      | no                |
| useFetcher                      |   In HTML/HTTP, data mutations and loads are modeled with navigation: <a href> and <form action>. Both cause a navigation in the browser. The React Router equivalents are <Link> and <Form>.   | Function | no       | web      | no                |
| useFetchers                     |  Returns an array of all inflight fetchers without their load, submit, or Form properties (can't have parent components trying to control the behavior of their children! We know from IRL experience that this is a fool's errand.) | Function | no       | web      | no                |
| useFormAction                   |  This hook is used internally in <Form> to automatically resolve default and relative actions to the current route in context.     | Function | no       | web      | no                |
| useLinkClickHandler             | The useLinkClickHandler hook returns a click event handler for navigation when building a custom <Link> in react-router-dom.     | Function | no       | web      | no                |
| useSearchParams                 | The useSearchParams hook is used to read and modify the query string in the URL for the current location. Like React's own useState hook, useSearchParams returns an array of two values: the current location's search params and a function that may be used to update them. Just as React's useState hook, setSearchParams also supports functional updates. | Function | no       | web      | no                |
| useSubmit                       |   The imperative version of <Form> that lets you, the programmer, submit a form instead of the user.   | Function | no       | web      | no                |
| useNavigation                   |  This hook tells you everything you need to know about a page navigation to build pending navigation indicators and optimistic UI on data mutations.  | Function | no       | web      | no                |
| useParams                       | The useParams hook returns an object of key/value pairs of the dynamic params from the current URL that were matched by the <Route path>. Child routes inherit all params from their parent routes. | Function | no       | All      | yes               |
| useRouteError                   |Inside of an errorElement, this hook returns anything thrown during an action, loader, or rendering. Note that thrown responses have special treatment, see isRouteErrorResponse for more information.| Function | no       | web      | no                |
| useAsyncError                   |Returns the rejection value from the nearest `<Await>` component.                                                                                                                                | Function | no       | All      | yes               |
| useAsyncValue                   |Returns the resolved data from the nearest `<Await>` ancestor component.                                                                                                                         | Function | no       | All      | yes               |
| useBlocker                      | The useBlocker hook allows you to prevent the user from navigating away from the current location, and present them with a custom UI to allow them to confirm the navigation.                   | Function | no       | web      | no                |
| useHref                         | The `useHref` hook returns a URL that may be used to link to the given `to` location, even outside of React Router.                                                                             | Function | no       | All      | yes               |
| useInRouterContext              | The `useInRouterContext` hooks returns `true` if the component is being rendered in the context of a `<Router>`, `false` otherwise. This can be useful for some 3rd-party extensions that need to know if they are being rendered in the context of a React Router app. | Function | no       | All      | yes               |
| useLoaderData                   | This hook provides the value returned from your route loader.                                                                                                                                   | Function | no       | web      | no                |
| useMatches                      | Returns the current route matches on the page. This is most useful for creating abstractions in parent layouts to get access to their child route's data.                                       | Function | no       | web      | no                |
| useNavigationType               | This hook returns the current type of navigation or how the user came to the current page; either via a pop, push, or replace action on the history stack.                                      | Function | no       | All      | yes               |
| useOutletContext                | parent routes manage state or other values you want shared with child routes.                                                                                                                   | Function | no       | All      | yes               |
| useResolvedPath                 | This hook resolves the `pathname` of the location in the given `to` value against the pathname of the current location.                                                                         | Function | no       | web      | no                |
| useRevalidator                  | This hook allows you to revalidate the data for any reason. React Router automatically revalidates the data after actions are called, but you may want to revalidate for other reasons like when focus returns to the window. | Function | no       | web      | no                |
| useRouteLoaderData              | This hook makes the data at any currently rendered route available anywhere in the tree. This is useful for components deep in the tree needing data from routes much farther up, as well as parent routes needing the data of child routes deeper in the tree. | Function | no       | web      | no                |
| useActionData                   | This hook provides the returned value from the previous navigation's `action` result, or `undefined` if there was no submission.                                                                | Function | no       | web      | no                |

### Utilities
| Name               | Description                                                                                                                                                                                                                                                                                               | Type      | Required | Platform | HarmonyOS Support |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|----------|----------|-------------------|
| redirect           | Because you can return or throw responses in loaders and actions, you can use redirect to redirect to another route..                                                                                                                                                                                     | Function  | no       | web      | no                |
| isRouteErrorResponse | This returns true if a route error is a route error response.                                                                                                                                                                                                                                             | Function  | no       | web      | no                |
| matchPath          | `matchPath` matches a route path pattern against a URL pathname and returns information about the match. This is useful whenever you need to manually run the router's matching algorithm to determine if a route path matches or not. It returns `null` if the pattern does not match the given pathname. | Function  | no       | web      | no                |
| matchRoutes        | `matchRoutes` runs the route matching algorithm for a set of routes against a given [`location`][location] to see which routes (if any) match. If it finds a match, an array of `RouteMatch` objects is returned, one for each route that matched.                                                        | Function  | no       | web      | no                |
| parsePath          | Parses a string as a URL                                                                                                                                                                                                                                                                                  | Function  | no       | All      | yes               |
| redirectDocument   | This is a small wrapper around `redirect` that will trigger a document-level redirect to the new location instead of a client-side navigation.                                                                                                                                                            | Function  | no       | web      | no                |
| renderMatches      | `renderMatches` renders the result of `matchRoutes()` into a React element.                                                                                                                                                                                                                               | Function  | no       | web      | no                |
| resolvePath        | `resolvePath` resolves a given `To` value into an actual `Path` object with an absolute `pathname`. This is useful whenever you need to know the exact path for a relative `To` value.                                                                                                                    | Function  | no       | web      | no                |
| generatePath       | `generatePath` interpolates a set of params into a route path string with `:id` and `*` placeholders. This can be useful when you want to eliminate placeholders from a route path so it matches statically instead of using a dynamic parameter.                                                         | Function  | no       | web      | no                |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/remix-run/react-router/blob/main/LICENSE.md) ，请自由地享受和参与开源。

