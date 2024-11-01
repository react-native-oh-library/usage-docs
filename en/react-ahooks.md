> Template version: v0.2.0

<p align="center">
  <a href="https://ahooks.js.org">
    <img width="200" src="https://ahooks.js.org/logo.svg">
  </a>
</p>
<p align="center">
    <a href="https://github.com/alibaba/hooks/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [GitHub address](https://github.com/alibaba/hooks)

## 📚 文档

- [English](https://ahooks.js.org/)
- [中文](https://ahooks.js.org/zh-CN/)

## ✨ 特性

- 易学易用
- 支持 SSR
- 对输入输出函数做了特殊处理，避免闭包问题
- 包含大量提炼自业务的高级 Hooks
- 包含丰富的基础 Hooks
- 使用 TypeScript 构建，提供完整的类型定义文件

## 📦 Installation

```bash
$ npm install --save ahooks
# or
$ yarn add ahooks
# or
$ pnpm add ahooks
# or
$ bun add ahooks
# or
$ npm install @types/mockjs  --legacy-peer-deps
# or
$ npm install @ahooksjs/use-url-state --legacy-peer-deps
# or
$ npm install react-json-view@1.21.3
```

## Usage

```tsx
/**
 * title: Default usage
 * desc: Update state or props, you can see the output in the console
 *
 * title.zh-CN: 基础用法
 * desc.zh-CN: 更新 state 或 props，可以在控制台看到输出
 */

import { useWhyDidYouUpdate } from 'ahooks';
import React, { useState } from 'react';
import { View, Text, Button } from 'react-native';

const Demo: React.FC<{ count: number }> = (props) => {
  const [randomNum, setRandomNum] = useState(Math.random());

  useWhyDidYouUpdate('useWhyDidYouUpdateComponent', { ...props, randomNum });

  return (
    <View>
      <View>
        <Text>number: {props.count}</Text>
      </View>
      <View>
        <Text>randomNum: {randomNum}</Text>
        <View style={{ marginLeft: 8, width: 60, height: 40 }}>
          <Button
            title="🎲"
            onPress={() => setRandomNum(Math.random)}
          />
        </View>
      </View>
    </View>
  );
};

export function WhyDidYouUpdate() {
  const [count, setCount] = useState(0);

  return (
    <View>
      <Demo count={count} />
      <View style={{ display: 'flex', flexDirection: 'row' }}>
        <View style={{ marginLeft: 8, width: 100, height: 60 }}>
          <Button title="count -" onPress={() => setCount((prevCount) => prevCount - 1)} />
        </View>

        <View style={{ marginLeft: 8, width: 100, height: 60 }}>
          <Button title="count +" onPress={() => setCount((prevCount) => prevCount + 1)} />
        </View>
      </View>
      <Text style={{ marginTop: 8 }}>Please open the browser console to view the output!</Text>
    </View>
  );
};
```



## Compatibility

This document is verified based on the following versions：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


以下Properties已验证，详情见 [ahooks官方文档](https://ahooks.js.org/zh-CN/)

|            Name            |                                                                                                                        Description                                                                                                                        |   Type   | Platform | HarmonyOS Support |
| :------------------------: | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :------: | :------: | :---------------: |
|          快速上手          |                                                                                      `useRequest` 的第一个参数是一个异步函数，在组件初次加载时，会自动触发该函数执行                                                                                      | Function |   All    |        yes        |
|          基础用法          |                                                                                               同时自动管理该异步函数的 `loading` , `data` , `error` 等状态                                                                                                | Function |   All    |        yes        |
|       Loading Delay        |                                                                                   通过设置 `options.loadingDelay` ，可以延迟 `loading` 变成 `true` 的时间，有效防止闪烁                                                                                   | Function |   All    |        yes        |
|            轮询            |                                                                                  通过设置 `options.pollingInterval`，进入轮询模式，`useRequest` 会定时触发 service 执行                                                                                   | Function |   All    |        yes        |
|           Ready            |                                                                                  通过设置 `options.ready`，可以控制请求是否发出，当其值为 `false` 时，请求永远都不会发出                                                                                  | Function |   All    |        yes        |
|          依赖刷新          | 通过设置 `options.refreshDeps`，在依赖变化时， `useRequest` 会自动调用 [refresh](https://ahooks.js.org/zh-CN/hooks/use-request/basic/#result) 方法，实现[刷新（重复上一次请求）](https://ahooks.js.org/zh-CN/hooks/use-request/basic/#刷新重复上一次请求) | Function |   All    |        yes        |
|      屏幕聚焦重新请求      |                                                                             通过设置 `options.refreshOnWindowFocus`，在浏览器窗口 `refocus` 和 `revisible` 时，会重新发起请求                                                                             | Function |   All    |        yes        |
|            防抖            |                                                                       通过设置 `options.debounceWait`，进入防抖模式，此时如果频繁触发 `run` 或者 `runAsync`，则会以防抖策略进行请求                                                                       | Function |   All    |        yes        |
|            节流            |                                                                       通过设置 `options.throttleWait`，进入节流模式，此时如果频繁触发 `run` 或者 `runAsync`，则会以节流策略进行请求                                                                       | Function |   All    |        yes        |
|         缓存 & SWR         |                                                                             通过 `options.staleTime` 设置数据保持新鲜时间，在该时间内，我们认为数据是新鲜的，不会重新发起请求                                                                             | Function |   All    |        yes        |
|          错误重试          |                                                                                     通过设置 `options.retryCount`，指定错误重试次数，则 useRequest 在失败后会进行重试                                                                                     | Function |   All    |        yes        |
|      useHistoryTravel      |                                                                                                     管理状态历史变化记录，方便在历史记录中前进与后退                                                                                                      | Function |   All    |        yes        |
|        useCountDown        |                                                                                                                 一个用于管理倒计时的 Hook                                                                                                                 | Function |   All    |        yes        |
|         useCounter         |                                                                                                                     管理计数器的 Hook                                                                                                                     | Function |   All    |        yes        |
|        useWebSocket        |                                                                                                                用于处理 WebSocket 的 Hook                                                                                                                 | Function |   All    |        yes        |
|          useMount          |                                                                                                                只在组件初始化时执行的 Hook                                                                                                                | Function |   All    |        yes        |
|         useUnmount         |                                                                                                            在组件卸载（unmount）时执行的 Hook                                                                                                             | Function |   All    |        yes        |
|      useUnmountedRef       |                                                                                                              获取当前组件是否已经卸载的 Hook                                                                                                              | Function |   All    |        yes        |
|        useSetState         |                                                                                       管理 object 类型 state 的 Hooks，用法与 class 组件的 `this.setState` 基本一致                                                                                       | Function |   All    |        yes        |
|         useBoolean         |                                                                                                              优雅的管理 boolean 状态的 Hook                                                                                                               | Function |   All    |        yes        |
|         useToggle          |                                                                                                               用于在两个状态值间切换的 Hook                                                                                                               | Function |   All    |        yes        |
|       useCookieState       |                                                                                                           一个可以将状态存储在 Cookie 中的 Hook                                                                                                           | Function |   All    |        yes        |
|   useSessionStorageState   |                                                                                                           将状态存储在 sessionStorage 中的 Hook                                                                                                           | Function |   All    |        yes        |
|        useDebounce         |                                                                                                                   用来处理防抖值的 Hook                                                                                                                   | Function |   All    |        yes        |
|        useThrottle         |                                                                                                                   用来处理节流值的 Hook                                                                                                                   | Function |   All    |        yes        |
|           useMap           |                                                                                                                 管理 Map 类型状态的 Hook                                                                                                                  | Function |   All    |        yes        |
|           useSet           |                                                                                                                 管理 Set 类型状态的 Hook                                                                                                                  | Function |   All    |        yes        |
|        usePrevious         |                                                                                                                   保存上一次状态的 Hook                                                                                                                   | Function |   All    |        yes        |
|        useRafState         |                                                    只在 [requestAnimationFrame](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame) callback 时更新 state，一般用于性能优化                                                    | Function |   All    |        yes        |
|        useSafeState        |                                                               用法与 `React.useState` 完全一样，但是在组件卸载后异步回调内的 `setState` 不再执行，避免因组件卸载后更新状态而导致的内存泄漏                                                                | Function |   All    |        yes        |
|        useGetState         |                                                                                               给 `React.useState` 增加了一个 getter 方法，以获取当前最新值                                                                                                | Function |   All    |        yes        |
|       useResetState        |                                                                                               提供重置 state 方法的 Hooks，用法与 `React.useState` 基本一致                                                                                               | Function |   All    |        yes        |
|      useUpdateEffect       |                                                                                      `useUpdateEffect` 用法等同于 `useEffect`，但是会忽略首次行，只在依赖更新时执行                                                                                       | Function |   All    |        yes        |
|   useUpdateLayoutEffect    |                                                                               `useUpdateLayoutEffect` 用法等同于 `useLayoutEffect`，但是会忽略首次执行，只在依赖更新时执行                                                                                | Function |   All    |        yes        |
|       useAsyncEffect       |                                                                                                                  useEffect 支持异步函数                                                                                                                   | Function |   All    |        yes        |
|     useDebounceEffect      |                                                                                                               为 `useEffect` 增加防抖的能力                                                                                                               | Function |   All    |        yes        |
|       useDebounceFn        |                                                                                                                  用来处理防抖函数的 Hook                                                                                                                  | Function |   All    |        yes        |
|       useThrottleFn        |                                                                                                                  用来处理函数节流的 Hook                                                                                                                  | Function |   All    |        yes        |
|     useThrottleEffect      |                                                                                                               为 `useEffect` 增加节流的能力                                                                                                               | Function |   All    |        yes        |
|    useDeepCompareEffect    |                                                                         用法与 useEffect 一致，但 deps 通过 [lodash isEqual](https://lodash.com/docs/4.17.15#isEqual) 进行深比较                                                                          | Function |   All    |        yes        |
| useDeepCompareLayoutEffect |                                                                      用法与 useLayoutEffect 一致，但 deps 通过 [lodash isEqual](https://lodash.com/docs/4.17.15#isEqual) 进行深比较                                                                       | Function |   All    |        yes        |
|        useInterval         |                                                                                                             一个可以处理 setInterval 的 Hook                                                                                                              | Function |   All    |        yes        |
|       useRafInterval       |                                                   用 `requestAnimationFrame` 模拟实现 `setInterval`，API 和 `useInterval` 保持一致，好处是可以在页面不渲染的时候停止执行定时器，比如页面隐藏或最小化等                                                    | Function |   All    |        yes        |
|         useTimeout         |                                                                                                         一个可以处理 setTimeout 计时器函数的 Hook                                                                                                         | Function |   All    |        yes        |
|       useRafTimeout        |                                                    用 `requestAnimationFrame` 模拟实现 `setTimeout`，API 和 `useTimeout` 保持一致，好处是可以在页面不渲染的时候不触发函数执行，比如页面隐藏或最小化等                                                     | Function |   All    |        yes        |
|         useLockFn          |                                                                                                        用于给一个异步函数增加竞态锁，防止并发执行                                                                                                         | Function |   All    |        yes        |
|         useUpdate          |                                                                                                  useUpdate 会返回一个函数，调用该函数会强制组件重新渲染                                                                                                   | Function |   All    |        yes        |
|   useControllableValuet    |                                                                 在某些组件开发时，我们需要组件的状态既可以自己管理，也可以被外部控制，`useControllableValue` 就是帮你管理这种状态的 Hook                                                                  | Function |   All    |        yes        |
|        useCreation         |                                                          `useCreation` 是 `useMemo` 或 `useRef` 的替代品，因为 `useMemo` 不能保证被 memo 的值一定不会被重新计算，而 `useCreation` 可以保证这一点                                                          | Function |   All    |        yes        |
|      useEventEmitter       |                                                                                                在组件中调用 `useEventEmitter` 可以获得一个 `EventEmitter`                                                                                                 | Function |   All    |        yes        |
|         useLatest          |                                                                                                          返回当前最新值的 Hook，可以避免闭包问题                                                                                                          | Function |   All    |        yes        |
|       useMemoizedFn        |                                                 持久化 function 的 Hook，一般情况下，可以使用 useMemoizedFn 完全代替 useCallback，特殊情况见 [FAQ](https://ahooks.js.org/zh-CN/hooks/use-memoized-fn#faq)                                                 | Function |   All    |        yes        |
|        useReactive         |                                                                                  提供一种数据响应式的操作体验，定义数据状态不需要写`useState`，直接修改Properties即可刷新视图                                                                                   | Function |   All    |        yes        |
|      useTrackedEffect      |                                                                                                        追踪是哪个依赖变化触发了 `useEffect` 的执行                                                                                                        | Function |   All    |        yes        |
|     useWhyDidYouUpdate     |                                                                                                     帮助开发者排查是哪个Properties改变导致了组件的 rerender                                                                                                     | Function |   All    |        yes        |

## 手机端不支持方法澄清

| title    | hook-name             | 解释                                                                                                    | 问题描述                                                                                                                                                          | HarmonyOS Support |
| -------- | --------------------- | ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | :---------------: |
| Dom      | useDrop & useDrag     | 处理元素拖拽的 Hook                                                                                     | Property 'document' doesn't exist Properties“document”不存在                                                                                                            |        NO         |
| Dom      | useEventListener      | 优雅的使用 addEventListener                                                                             | 基础用法：无报错 监听 keydown 事件：无物理键盘                                                                                                                    |        NO         |
| Dom      | useEventListener      | 优雅的使用 addEventListener                                                                             | 报错，无物理键盘                                                                                                                                                  |        NO         |
| Dom      | useClickAway          | 监听目标元素外的点击事件                                                                                | Property 'document' doesn't exist Properties“document”不存在                                                                                                            |        NO         |
| Dom      | useDocumentVisibility | 监听页面是否可见                                                                                        | 无报错，无法监听到state状态变化，获取不到手机窗口                                                                                                                 |        NO         |
| Dom      | useEventTarget        | 常见表单控件(通过 e.target.value 获取表单值) 的 onChange 跟 value 逻辑封装，支持自定义值转换和重置功能  | Cannot read property ‘value’of undefined                                                                                                                          |        NO         |
| Dom      | useExternal           | 动态注入 JS 或 CSS 资源，useExternal 可以保证资源全局唯一                                               | Property 'document' doesn't exist Properties“document”不存在                                                                                                            |        NO         |
| Dom      | useTitle              | 用于设置页面标题                                                                                        | Property 'document' doesn't exist Properties“document”不存在                                                                                                            |        NO         |
| Dom      | useFavicon            | 设置页面的 favicon                                                                                      | Property 'document' doesn't exist Properties“document”不存在                                                                                                            |        NO         |
| Dom      | useFullscreen         | 管理 DOM 全屏的 Hook                                                                                    | Property 'document' doesn't exist Properties“document”不存在                                                                                                            |        NO         |
| Dom      | useHover              | 监听 DOM 元素是否有鼠标悬停                                                                             | 无报错，点击按钮无反应，监听不到Properties变化                                                                                                                          |        NO         |
| Dom      | useInViewport         | 观察元素是否在可见区域，以及元素可见比例                                                                | Property 'document' doesn't exist Properties“document”不存在                                                                                                            |        NO         |
| Dom      | useKeyPress           | 监听键盘按键，支持组合键，支持按键别名                                                                  | 无报错，没有物理键盘，无法操作Properties                                                                                                                                |        NO         |
| Dom      | useLongPress          | 监听目标元素的长按事件                                                                                  | Property 'document' doesn't exist Properties“document”不存在                                                                                                            |        NO         |
| Dom      | useMouse              | 监听鼠标位置                                                                                            | 无报错，点击按钮无反应，监听不到Properties变化                                                                                                                          |        NO         |
| Dom      | useResponsive         | 获取响应式信息                                                                                          | Cannot convert undefined value to object                                                                                                                          |        NO         |
| Dom      | useScroll             | 监听元素的滚动位置                                                                                      | Property 'document' doesn't exist Properties“document”不存在                                                                                                            |        NO         |
| Dom      | useSize               | 监听 DOM 节点尺寸变化的 Hook                                                                            | 无报错，无法获取到document                                                                                                                                        |        NO         |
| Dom      | useFocusWithin        | 监听当前焦点是否在某个区域之内                                                                          | 无报错，无法监听到state变化                                                                                                                                       |        NO         |
| Advanced | useReactive           | 提供一种数据响应式的操作体验，定义数据状态不需要写useState，直接修改Properties即可刷新视图                    | input输入框中无法输入文字，只能输入数字 Cannot read property 'map' of undefined                                                                                   |        NO         |
| State    | useUrlState           | 通过 url query 来管理 state 的 Hook                                                                     | 无报错，不生效                                                                                                                                                    |        NO         |
| State    | useLocalStorageState  | 将状态存储在 localStorage 中的 Hook                                                                     | 无报错，不生效                                                                                                                                                    |        NO         |
| Scene    | useAntdTable          | useAntdTable 会自动管理 Table 分页数据，你只需要把返回的 tableProps 传递给 Table 组件                   | ui组件无法使用，document”不存在                                                                                                                                   |        NO         |
| Scene    | useFusionTable        | useFusionTable 会自动管理 Table 分页数据，你只需要把返回的 tableProps 与 paginationProps 传递给相应组件 | ui组件无法使用，document”不存在                                                                                                                                   |        NO         |
| Scene    | useInfiniteScroll     | useInfiniteScroll 封装了常见的无限滚动逻辑                                                              | 滚动自动加载:在无限滚动场景中数据加载变多Scroll无响应                                                                                                             |        NO         |
| Scene    | usePagination         | 用法与 useRequest 一致，但会多返回一个 pagination 参数，包含所有分页信息，及操作分页的函数              | 报错，不支持mockjs                                                                                                                                                |        NO         |
| Scene    | useDynamicList        | 一个帮助你管理动态列表状态，并能生成唯一 key 的 Hook                                                    | 报错，Render ErrorView config getter callback for component path mustbe a function (recelved undefined). Make sure to startcomponent names with a capital letter. |        NO         |
| Scene    | useVirtualList        | 提供虚拟化列表能力的 Hook，用于解决展示海量数据渲染时首屏渲染缓慢和滚动卡顿问题                         | 无报错，不生效                                                                                                                                                    |        NO         |
| Scene    | useNetwork            | 管理网络连接状态的 Hook                                                                                 | 报错,window.addEventListener is not a function                                                                                                                    |        NO         |
| Scene    | useSelections         | 常见联动 Checkbox 逻辑封装，支持多选，单选，全选逻辑，还提供了是否选择，是否全选，是否半选的状态        | Property 'document' doesn't exist Properties“document”不存在                                                                                                            |        NO         |
| Scene    | useTextSelection      | 实时获取用户当前鼠标选取的文本内容及位置                                                                | 无报错，没有鼠标，无法操作Properties                                                                                                                                    |        NO         |

## Others

## License

This project is licensed under [MIT License](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Foblador%2Freact-native-progress%2Fblob%2Fmaster%2FLICENSE).
