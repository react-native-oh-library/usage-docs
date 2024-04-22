> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-router-dom</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/remix-run/react-router">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/remix-run/react-router/blob/main/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/remix-run/react-router)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm i react-router-dom@6.22.1
```

#### **yarn**

```bash
yarn add react-router-dom@6.22.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React from "react";
import { ScrollView } from "react-native";
import { Route, Routes, MemoryRouter as Router } from "react-router-dom";

const DomDemo = () => {
  const initialEntries = [
    "/",
    { pathname: "/login", state: { stateTest: "stateTestContent" } },
    { pathname: "/detail", state: { stateTest: "stateTestContent" } },
    "/index3",
  ];
  return (
    <ScrollView style={styles.container}>
      <Router
        initialEntries={initialEntries}
        initialIndex={initialIndex}
        future={{ v7_startTransition: true }}
      >
        <Routes>
          <Route path="/" element={<Home />}>
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

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，详情见 [react-router-dom源库地址](https://github.com/remix-run/react-router)

**Hooks**

| Name        | Description                                                                                                                                                                                                                                         | Type     | Required | Platform | HarmonyOS Support |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| useLocation | This hook returns the current [`location`](https://reactrouter.com/en/main/utils/location) object. This can be useful if you'd like to perform some side effect whenever the current location changes.                                              | Function | NO       | All      | YES               |
| useNavigate | The `useNavigate` hook returns a function that lets you navigate programmatically, for example in an effect:                                                                                                                                        | Function | NO       | All      | YES               |
| useOutlet   | Returns the element for the child route at this level of the route hierarchy. This hook is used internally by < Outlet > to render child routes.                                                                                                    | Function | NO       | All      | YES               |
| useRoutes   | The useRoutes hook is the functional equivalent of < Routes >, but it uses JavaScript objects instead of < Route > elements to define your routes. These objects have the same properties as normal < Route > elements, but they don't require JSX. | Function | NO       | All      | YES               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/remix-run/react-router/blob/main/LICENSE.md) ，请自由地享受和参与开源。
