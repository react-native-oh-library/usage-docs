

<p align="center">
  <h1 align="center"> <code>react-use</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/zenghongtu/react-use">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/zenghongtu/react-use)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-use@17.2.4
```

#### **yarn**

```bash
yarn add react-use@17.2.4
```

<!-- tabs:end -->

## 兼容性

在以下版本验证通过

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;

## 方法

**Sensors**

- [`useMotion`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseMotion.tsx) — tracks state of device's motion sensor.  

**Animations**

- [`useRaf`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/CreateGlobalState.tsx) — re-renders component on each `requestAnimationFrame`.

- [`useInterval`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseInterval.tsx) and [`useHarmonicIntervalFn`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseHarmonicIntervalFn.tsx) — re-renders component on a set interval using `setInterval`.

- [`useSpring`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseSpring.tsx) — interpolates number over time according to spring dynamics.

- [`useTimeout`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseTimeout.tsx) — re-renders component after a timeout.

- [`useTimeoutFn`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseTimeoutFn.tsx) — calls given function after a timeout.

- [`useTween`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseTween.tsx) — re-renders component, while tweening a number from 0 to 1

- [`useUpdate`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseUpdate.tsx) — returns a callback, which re-renders component when called.

  

**Side-effects**

- [`useAsync`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseAsync.tsx), [`useAsyncFn`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseAsyncFn.tsx), and [`useAsyncRetry`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseAsyncRetry.tsx) — resolves an `async` function.
- [`useBeforeUnload`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseBeforeUnload.tsx) — shows browser alert when user try to reload or close the page.
- [`useCookie`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseCookie.tsx) — provides way to read, update and delete a cookie.
- [`useDebounce`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseDebounce.tsx) — debounces a function. 
- [`useError`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseError.tsx) — error dispatcher. 
- [`useRafLoop`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseRafLoop.tsx) — calls given function inside the RAF loop.
- [`useThrottle` and `useThrottleFn`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseThrottle.tsx) — throttles a function.

**Lifecycles**

- [`useEffectOnce`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseEffectOnce.tsx) — hook that only runs once.
- [`useLifecycles`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseLifecycles.tsx) — calls `mount` and `unmount` callbacks.
- [`useMountedState`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseMountedState.tsx) and [`useUnmountPromise`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseUnmountPromise.tsx) — track if component is mounted.
- [`useLogger`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseLogger.tsx) — logs in console as component goes through life-cycles.
- [`useMount`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseMount.tsx) — calls `mount` callbacks.
- [`useUnmount`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseUnmount.tsx) — calls `unmount` callbacks.
- [`useUpdateEffect`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseUpdateEffect.tsx) — run an `effect` only on updates.
- [`useIsomorphicLayoutEffect`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseIsomorphicLayoutEffect.tsx) — `useLayoutEffect` that does not show warning when server-side rendering.
- [`useDeepCompareEffect`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseDeepCompareEffect.tsx)and [`useCustomCompareEffect`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseCustomCompareEffect.tsx) — run an `effect` depending on deep comparison of its dependencies

**State** 

- [`createMemo`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/CreateMemo.tsx) — factory of memoized hooks.
- [`createReducerContext`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/CreateReducerContext.tsx) and [`createStateContext`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/CreateStateContext.tsx) — factory of hooks for a sharing state between components.
- [`useDefault`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseDefault.tsx) — returns the default value when state is `null` or `undefined`.
- [`useGetSet`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseGetSet.tsx) — returns state getter `get()` instead of raw state.
- [`useGetSetState`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseGetSetState.tsx) — as if [`useGetSet`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseGetSet.tsx) and [`useSetState`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseSetState.tsx) had a baby.
- [`useLatest`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseLatest.tsx) — returns the latest state or props
- [`usePrevious`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UsePrevious.tsx) — returns the previous state or props. 
- [`usePreviousDistinct`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UsePreviousDistinct.tsx) — like `usePrevious` but with a predicate to determine if `previous` should update.
- [`useObservable`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseObservable.tsx) — tracks latest value of an `Observable`.
- [`useRafState`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseRafState.tsx) — creates `setState` method which only updates after `requestAnimationFrame`.
- [`useSetState`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseSetState.tsx) — creates `setState` method which works like `this.setState`.
- [`useStateList`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseStateList.tsx) — circularly iterates over an array.
- [`useToggle` ](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseToggle.tsx) — tracks state of a boolean.
- [`useCounter`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseCounter.tsx) — tracks state of a number. 
- [`useList`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseList.tsx) — tracks state of an array. 
- [`useMap`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseMap.tsx) — tracks state of an object. 
- [`useSet`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseSet.tsx) — tracks state of a Set
- [`useQueue`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseQueue.tsx) — implements simple queue.
- [`useStateValidator`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseStateValidator.tsx) — tracks state of an object.
- [`useStateWithHistory`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseStateWithHistory.tsx) — stores previous state values and provides handles to travel through them.
- [`useMultiStateValidator`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseMultiStateValidator.tsx) — alike the `useStateValidator`, but tracks multiple states at a time
- [`useMediatedState`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseMediatedState.tsx) — like the regular `useState` but with mediation by custom function.
- [`useFirstMountState`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseFirstMountState.tsx) — check if current render is first.
- [`useRendersCount`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseRendersCount.tsx) — count component renders. 
- [`createGlobalState`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/CreateGlobalState.tsx) — cross component shared state
- [`useMethods`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseMethods.tsx) — neat alternative to `useReducer`.

**Miscellaneous**

- [`useEnsuredForwardedRef`](https://github.com/react-native-oh-library/RNOHDCS/blob/main/ReactUseDemo/UseEnsuredForwardedRef.tsx)— use a React.forwardedRef safely.



## 手机端不支持方法澄清

| title        | hook-name                                                | 解释                                        | 问题描述                                                     | HarmonyOS Support |
| ------------ | -------------------------------------------------------- | ------------------------------------------- | ------------------------------------------------------------ | ----------------- |
| Sensors      | useBattery                                               | 跟踪设备电池状态。                          | 无报错，不支持蓄电池传感器                                   | NO                |
| Sensors      | useGeolocation                                           | 跟踪用户设备的地理位置状态。                | Cannot read property 'getCurrentPosition' of undefined没有属性 | NO                |
| Sensors      | useHover and useHoverDirty                               | 跟踪某些元素的鼠标悬停状态。                | 无报错，无反应                                               | NO                |
| Sensors      | useHash                                                  | 跟踪位置哈希值。                            | Hash of undefined                                            | NO                |
| Sensors      | useIdle                                                  | 跟踪用户是否处于非活动状态。                | Property 'document' doesn't exist                            | NO                |
| Sensors      | useIntersection                                          | 跟踪HTML元素的交集                          | 无报错，无反应，状态不对应                                   | NO                |
| Sensors      | useKey, useKeyPress, useKeyboardJs, and useKeyPressEvent | 追踪按键                                    | 无报错，无反应                                               | NO                |
| Sensors      | useLocation and useSearchParam                           | 跟踪页面导航栏的位置状态。                  | Cannot convert undefined value to object                     | NO                |
| Sensors      | useLongPress                                             | 跟踪某些元素的长按手势                      | 无报错，无反应                                               | NO                |
| Sensors      | useMedia                                                 | 跟踪CSS媒体查询的状态                       | window.matchMedia is not a function (it is undefined)        | NO                |
| Sensors      | useMediaDevices                                          | 跟踪连接的硬件设备的状态。                  | 无报错，值为空                                               | NO                |
| Sensors      | useMouse and useMouseHovered                             | 跟踪鼠标位置的状态                          | Property 'document' doesn't exist                            | NO                |
| Sensors      | useMouseWheel                                            | 跟踪滚动鼠标滚轮的deltaY。                  | 无报错，无反应                                               | NO                |
| Sensors      | useNetworkState                                          | 跟踪浏览器的网络连接状态。                  | 无报错，值为空                                               | NO                |
| Sensors      | useOrientation                                           | 跟踪设备屏幕方向的状态。                    | Cannot read property 'orientation' of undefined              | NO                |
| Sensors      | usePageLeave                                             | 当鼠标离开页面边界时触发。                  | Property 'document' doesn't exist 属性“document”不存在       | NO                |
| Sensors      | useScratch                                               | 跟踪鼠标单击和拖动状态。                    | 未报错，无反应                                               | NO                |
| Sensors      | useScroll                                                | 跟踪HTML元素的滚动位置                      | 未报错，无反应                                               | NO                |
| Sensors      | useScrolling                                             | 跟踪HTML元素是否正在滚动。                  | 未报错，无反应                                               | NO                |
| Sensors      | useStartTyping                                           | 检测用户何时开始键入。                      | Property 'document' doesn't exist 属性“document”不存在       | NO                |
| Sensors      | useWindowScroll                                          | 轨迹窗口滚动位置                            | 无报错，值为空                                               | NO                |
| Sensors      | useWindowSize                                            | 跟踪窗口尺寸。                              | 无报错，值为空                                               | NO                |
| Sensors      | useMeasure and useSize                                   | 跟踪HTML元素的维度。                        | 无报错，值为空                                               | NO                |
| Sensors      | createBreakpoint                                         | 宽度                                        | 无报错，返回设备不正确                                       | NO                |
| Sensors      | useScrollbarWidth                                        | 检测浏览器的本地滚动条宽度                  | 无报错，值为0                                                | NO                |
| Sensors      | usePinchZoom                                             | 跟踪指针事件以检测收缩放大和缩小状态。      | Property 'useState' doesn't exist                            | NO                |
| UI           | useAudio                                                 | 播放音频并公开其控件                        | 组件“audio”的 View config getter 回调必须是一个函数          | NO                |
| UI           | useClickAway                                             | 当用户在目标区域外单击时触发回调。          | Property 'document' doesn't exist 属性“document”不存在       | NO                |
| UI           | useCss                                                   | 动态调整CSS。                               | Property 'document' doesn't exist 属性“document”不存在       | NO                |
| UI           | useDrop and useDropArea                                  | 跟踪文件、链接和复制粘贴滴漏。              | Property 'document' doesn't exist 属性“document”不存在       | NO                |
| UI           | useFullscreen                                            | 全屏显示元素或视频                          | 组件“video”的视图配置getter回调必须是一个函数                | NO                |
| UI           | useSlider                                                | 在任何HTML元素上提供幻灯片行为。            | Cannot set property 'userSelect' of undefined                | NO                |
| UI           | useSpeech                                                | 从文本字符串合成语音。                      | Cannot read property 'getVoices' of undefined                | NO                |
| UI           | useVibrate                                               | 使用振动API提供物理反馈。                   | 0, _react.useToggle is not a function (it is undefined)      | NO                |
| UI           | useVideo                                                 | useVideo 播放视频、跟踪其状态并公开播放控件 | 组件“video”的视图配置getter回调必须是一个函数                | NO                |
| Side-effects | useCopyToClipboard                                       | 将文本复制到剪切板。                        | 无报错无反应                                                 | NO                |
| Side-effects | useFavicon                                               | 设置页面的useFavicon。                      | Property 'document' doesn't exist 属性“document”不存在       | NO                |
| Side-effects | useLocalStorage                                          | 管理useLocalStorage中的值。                 | 无报错无反应                                                 | NO                |
| Side-effects | useLockBodyScroll                                        | 锁定body元素的滚动。                        | 无报错无反应                                                 | NO                |
| Side-effects | useSessionStorage                                        | 管理sessionStorage中的值。                  | 无报错无反应                                                 | NO                |
| Side-effects | useTitle                                                 | 设置页面的标题。                            | 无报错无反应                                                 | NO                |
| Side-effects | usePermission                                            | 查询浏览器API的权限状态。                   | Cannot read property 'query' of undefined                    | NO                |
| Lifecycles   | usePromise                                               | 仅在安装组件时解析usePromise                | 无报错无反应                                                 | NO                |
| Lifecycles   | useEvent                                                 | 订阅事件。                                  | 无报错无反应                                                 | NO                |
| State        | createReducer                                            | 带有定制中间件的reducer钩子工厂。           | 无报错无反应                                                 | NO                |

## 遗留问题

## 其他
