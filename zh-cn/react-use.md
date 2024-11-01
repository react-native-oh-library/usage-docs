> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-use</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/streamich/react-use">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/streamich/react-use/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/streamich/react-use)

## 安装与使用
进入到工程目录并输入以下命令：
<!-- tabs:start -->
#### **npm**
```bash
npm install react-use@17.5.0
```
#### **yarn**
```bash
yarn add react-use@17.5.0
```
> [!TIP] 如果依赖安装报错，请执行：
```bash
npm install react-use@17.5.0 --legacy-peer-deps
```
> [!TIP] 如果要体验全部demo效果，还需要安装以下依赖：
```bash
npm install @types/lodash --legacy-peer-deps
npm install rxjs --legacy-peer-deps
npm install rebound --legacy-peer-deps
```
<!-- tabs:end -->
## 兼容性
在以下版本验证通过
1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.29; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API
>[!tip] "Platform"列表示该属性在原三方库上支持的平台。

>[!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请查看[react-use 官方文档](https://github.com/streamich/react-use/blob/master/README.md)

### Sensors
| Name                                                     | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| :------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| useMotion                                                | tracks state of device's motion sensor                       | Function | NO       | Android/ios | YES               |
| useBattery                                               | tracks device battery state                                  | Function | NO       | web         | NO                |
| useGeolocation                                           | tracks geo location state of user's device                   | Function | NO       | web         | NO                |
| useHover and useHoverDirty                               | tracks mouse hover state of some element                     | Function | NO       | web         | NO                |
| useHash                                                  | tracks location hash value                                   | Function | NO       | web         | NO                |
| useIdle                                                  | tracks whether user is being inactive                        | Function | NO       | web         | NO                |
| useIntersection                                          | tracks an HTML element's intersection                        | Function | NO       | web         | NO                |
| useKey, useKeyPress, useKeyboardJs, and useKeyPressEvent | track keys                                                   | Function | NO       | web         | NO                |
| useLocation and useSearchParam                           | tracks page navigation bar location state                    | Function | NO       | web         | NO                |
| useLongPress                                             | tracks long press gesture of some element                    | Function | NO       | web         | NO                |
| useMedia                                                 | tracks state of a CSS media query                            | Function | NO       | web         | NO                |
| useMediaDevices                                          | tracks state of connected hardware devices                   | Function | NO       | web         | NO                |
| useMouse and useMouseHovered                             | tracks state of mouse position                               | Function | NO       | web         | NO                |
| useMouseWheel                                            | tracks deltaY of scrolled mouse wheel                        | Function | NO       | web         | NO                |
| useNetworkState                                          | tracks the state of browser's network connection             | Function | NO       | web         | NO                |
| useOrientation                                           | tracks state of device's screen orientation                  | Function | NO       | web         | NO                |
| usePageLeave                                             | triggers when mouse leaves page boundaries                   | Function | NO       | web         | NO                |
| useScratch                                               | tracks mouse click-and-scrub state                           | Function | NO       | web         | NO                |
| useScroll                                                | tracks an HTML element's scroll position                     | Function | NO       | web         | NO                |
| useScrolling                                             | tracks whether HTML element is scrolling                     | Function | NO       | web         | NO                |
| useStartTyping                                           | detects when user starts typing                              | Function | NO       | web         | NO                |
| useWindowScroll                                          | tracks `Window` scroll position                              | Function | NO       | web         | NO                |
| useWindowSize                                            | tracks `Window` dimensions                                   | Function | NO       | web         | NO                |
| useMeasure and useSize                                   | tracks an HTML element's dimensions                          | Function | NO       | web         | NO                |
| createBreakpoint                                         | tracks `innerWidth`                                          | Function | NO       | web         | NO                |
| useScrollbarWidth                                        | detects browser's native scrollbars width                    | Function | NO       | web         | NO                |
| usePinchZoom                                             | tracks pointer events to detect pinch zoom in and out status | Function | NO       | web         | NO                |


### UI
| Name                                                     | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| :------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| useAudio                                                 | plays audio and exposes its controls                         | Function | NO       | web         | NO                |
| useClickAway                                             | triggers callback when user clicks outside target area       | Function | NO       | web         | NO                |
| useCss                                                   | dynamically adjusts CSS                                      | Function | NO       | web         | NO                |
| useDrop and useDropArea                                  | tracks file, link and copy-paste drops                       | Function | NO       | web         | NO                |
| useFullscreen                                            | display an element or video full-screen                      | Function | NO       | web         | NO                |
| useSlider                                                | provides slide behavior over any HTML element                | Function | NO       | web         | NO                |
| useSpeech                                                | synthesizes speech from a text string                        | Function | NO       | web         | NO                |
| useVibrate                                               | provide physical feedback using the [Vibration API](https://developer.mozilla.org/en-US/docs/Web/API/Vibration_API) | Function | NO       | web         | NO                |
| useVideo                                                 | plays video, tracks its state, and exposes playback controls | Function | NO       | web         | NO                |

### Animations
| Name                                                     | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| :------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| useRaf                                                   | re-renders component on each `requestAnimationFrame`         | Function | NO       | Android/ios | YES               |
| useInterval and useHarmonicIntervalFn                    | re-renders component on a set interval using `setInterval`   | Function | NO       | Android/ios | YES               |
| useSpring                                                | interpolates number over time according to spring dynamics   | Function | NO       | Android/ios | YES               |
| useTimeout                                               | re-renders component after a timeout                         | Function | NO       | Android/ios | YES               |
| useTimeoutFn                                             | calls given function after a timeout                         | Function | NO       | Android/ios | YES               |
| useTween                                                 | re-renders component, while tweening a number from 0 to 1    | Function | NO       | Android/ios | YES               |
| useUpdate                                                | returns a callback, which re-renders component when called.  | Function | NO       | Android/ios | YES               |


### Side-effects
| Name                                                     | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| :------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| useAsync useAsyncFn and useAsyncRetry                    | resolves an `async` function                                 | Function | NO       | Android/ios | YES               |
| useBeforeUnload                                          | shows browser alert when user try to reload or close the page | Function | NO       | Android/ios | YES               |
| useCookie                                                | provides way to read, update and delete a cookie             | Function | NO       | Android/ios | YES               |
| useDebounce                                              | debounces a function                                         | Function | NO       | Android/ios | YES               |
| useError                                                 | error dispatcher                                             | Function | NO       | Android/ios | YES               |
| useRafLoop                                               | calls given function inside the RAF loop                     | Function | NO       | Android/ios | YES               |
| useThrottle`and`useThrottleFn                            | throttles a function                                         | Function | NO       | Android/ios | YES               |
| useCopyToClipboard                                       | copies text to clipboard                                     | Function | NO       | web         | NO                |
| useFavicon                                               | sets favicon of the page                                     | Function | NO       | web         | NO                |
| useLocalStorage                                          | manages a value in `localStorage`                            | Function | NO       | web         | NO                |
| useLockBodyScroll                                        | lock scrolling of the body element                           | Function | NO       | web         | NO                |
| useSessionStorage                                        | manages a value in `sessionStorage`                          | Function | NO       | web         | NO                |
| useTitle                                                 | sets title of the page                                       | Function | NO       | web         | NO                |
| usePermission                                            | query permission status for browser APIs                     | Function | NO       | web         | NO                |

### Lifecycles
| Name                                                     | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| :------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| useEffectOnce                                            | a modified [`useEffect`](https://reactjs.org/docs/hooks-reference.html#useeffect) hook that only runs once | Function | NO       | Android/ios | YES               |
| useLifecycles                                            | calls `mount` and `unmount` callbacks                        | Function | NO       | Android/ios | YES               |
| useMountedState and useUnmountPromise                    | track if component is mounted                                | Function | NO       | Android/ios | YES               |
| useLogger                                                | logs in console as component goes through life-cycles        | Function | NO       | Android/ios | YES               |
| useMount                                                 | calls `mount` callbacks                                      | Function | NO       | Android/ios | YES               |
| useUnmount                                               | calls `unmount` callbacks                                    | Function | NO       | Android/ios | YES               |
| useUpdateEffect                                          | run an `effect` only on updates                              | Function | NO       | Android/ios | YES               |
| useIsomorphicLayoutEffect                                | `useLayoutEffect` that that works on server                  | Function | NO       | Android/ios | YES               |
| usePromise                                               | resolves promise only while component is mounted             | Function | NO       | web         | NO                |
| useEvent                                                 | subscribe to events                                          | Function | NO       | web         | NO                |
| useDeepCompareEffect and useCustomCompareEffect          | run an `effect` depending on deep comparison of its dependencies | Function | NO       | Android/ios | YES               |

### State 
| Name                                                     | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| :------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| createMemo                                               | factory of memoized hooks                                    | Function | NO       | Android/ios | YES               |
| createReducerContext and createStateContext              | factory of hooks for a sharing state between components      | Function | NO       | Android/ios | YES               |
| useDefault                                               | returns the default value when state is `null` or `undefined` | Function | NO       | Android/ios | YES               |
| useGetSet                                                | as if [`useGetSet`](https://github.com/streamich/react-use/blob/master/docs/useGetSet.md) and [`useSetState`](https://github.com/streamich/react-use/blob/master/docs/useSetState.md) had a baby | Function | NO       | Android/ios | YES               |
| useGetSetState                                           | as if [`useGetSet`](https://github.com/streamich/react-use/blob/master/docs/useGetSet.md) and [`useSetState`](https://github.com/streamich/react-use/blob/master/docs/useSetState.md) had a baby. | Function | NO       | Android/ios | YES               |
| useLatest                                                | returns the latest state or props                            | Function | NO       | Android/ios | YES               |
| usePrevious                                              | returns the previous state or props                          | Function | NO       | Android/ios | YES               |
| usePreviousDistinct                                      | like `usePrevious` but with a predicate to determine if `previous` should update | Function | NO       | Android/ios | YES               |
| useObservable                                            | tracks latest value of an `Observable`                       | Function | NO       | Android/ios | YES               |
| useRafState                                              | creates `setState` method which only updates after `requestAnimationFrame` | Function | NO       | Android/ios | YES               |
| useSetState                                              | creates `setState` method which works like `this.setState`   | Function | NO       | Android/ios | YES               |
| useStateList                                             | circularly iterates over an array                            | Function | NO       | Android/ios | YES               |
| useToggle                                                | tracks state of a boolean                                    | Function | NO       | Android/ios | YES               |
| useCounter                                               | tracks state of a number                                     | Function | NO       | Android/ios | YES               |
| useList                                                  | tracks state of an array                                     | Function | NO       | Android/ios | YES               |
| useMap                                                   | tracks state of an object                                    | Function | NO       | Android/ios | YES               |
| useSet                                                   | tracks state of a Set                                        | Function | NO       | Android/ios | YES               |
| useQueue                                                 | implements simple queue                                      | Function | NO       | Android/ios | YES               |
| useStateValidator                                        | tracks state of an object                                    | Function | NO       | Android/ios | YES               |
| useStateWithHistory                                      | stores previous state values and provides handles to travel through them | Function | NO       | Android/ios | YES               |
| useMultiStateValidator                                   | alike the `useStateValidator`, but tracks multiple states at a time | Function | NO       | Android/ios | YES               |
| useMediatedState                                         | like the regular `useState` but with mediation by custom function | Function | NO       | Android/ios | YES               |
| useFirstMountState                                       | check if current render is first                             | Function | NO       | Android/ios | YES               |
| useRendersCount                                          | count component renders                                      | Function | NO       | Android/ios | YES               |
| createGlobalState                                        | cross component shared state                                 | Function | NO       | Android/ios | YES               |
| useMethods                                               | neat alternative to `useReducer`                             | Function | NO       | Android/ios | YES               |
| createReducer                                            | factory of reducer hooks with custom middleware              | Function | NO       | web         | NO                |

### Miscellaneous
| Name                                                     | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| :------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| useEnsuredForwardedRef                                   | use a React.forwardedRef safely                              | Function | NO       | Android/ios | YES               |

## 遗留问题
## 其他
## 开源协议
本项目基于 [The MIT License (MIT)](https://github.com/streamich/react-use/blob/master/LICENSE) ，请自由地享受和参与开源。
