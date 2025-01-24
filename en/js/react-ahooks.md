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

> [!TIP] [GitHub address](https://github.com/alibaba/hooks)

## 📚 Documents

- [English](https://ahooks.js.org/)
- [Chinese](https://ahooks.js.org/zh-CN/)

## ✨ Features

- Easy to learn and use.
- Supports SSR.
- Special processing for functions to avoid closure problems.
- Contains a large number of advanced Hooks that are extracted from services.
- Contains a comprehensive collection of basic Hooks.
- Written in TypeScript with a complete type definition file provided.

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

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


The following properties have been verified. For details, see [ahooks](https://ahooks.js.org/).

|            Name            |                         Description                          |   Type   | Platform | HarmonyOS Support |
| :------------------------: | :----------------------------------------------------------: | :------: | :------: | :---------------: |
|        Quick Start         | The first parameter of **useRequest** is an asynchronous function, which will be automatically triggered when the component is first loaded. | Function |   All    |        yes        |
|        Basic usage         | Manages the status of **loading**, **data**, **error** of the asynchronous function. | Function |   All    |        yes        |
|       Loading Delay        | Delays the time when **loading** turns to **true** by setting **options.loadingDelay**, effectively preventing UI flashing. | Function |   All    |        yes        |
|          Polling           | Enters the polling mode by setting **options.pollingInterval**. **useRequest** periodically triggers service execution. | Function |   All    |        yes        |
|           Ready            | Controls whether to send a request by setting **options.ready**. If **options.ready** is set to **false**, the request will never be sent. | Function |   All    |        yes        |
|        RefreshDeps         | By setting **options.refreshDeps**, **useRequest** automatically invokes [refresh](https://ahooks.js.org/hooks/use-request/basic/#result) when dependencies change, achieving the effect of [refresh](https://ahooks.js.org/hooks/use-request/basic/#refresh-repeat-the-last-request). | Function |   All    |        yes        |
|    RefreshOnWindowFocus    | Refreshes a request by setting **options.refreshOnWindowFocus** when the browser is **refocus** and **revisible**. | Function |   All    |        yes        |
|          Debounce          | Enters the debounce mode by setting **options.debounceWait**. At this time, if **run** or **runAsync** is triggered frequently, the request will be executed with the debounce strategy. | Function |   All    |        yes        |
|          Throttle          | Enters the throttle mode by setting **options.throttleWait**. At this time, if **run** or **runAsync** is triggered frequently, the request will be executed with the throttle strategy. | Function |   All    |        yes        |
|        Cache & SWR         | Sets the data retention time through **options.staleTime**. During this time, the data is considered to be fresh and the request will not be re-initiated. | Function |   All    |        yes        |
|        Error Retry         | Specifies the number of retry times by setting `options.retryCount`.** useRequest** will retry after a failure. | Function |   All    |        yes        |
|      useHistoryTravel      | Manages state change history to facilitate forward and backward operations in historical records. | Function |   All    |        yes        |
|        useCountDown        |                      Manages countdown.                      | Function |   All    |        yes        |
|         useCounter         |                       Manages counter.                       | Function |   All    |        yes        |
|        useWebSocket        |                      Handles WebSocket.                      | Function |   All    |        yes        |
|          useMount          |   Executes a function only when the component is mounted.    | Function |   All    |        yes        |
|         useUnmount         |     Executes a function when the component is unmounted.     | Function |   All    |        yes        |
|      useUnmountedRef       |         Obtains whether the component is unmounted.          | Function |   All    |        yes        |
|        useSetState         | Manages the state of object type, which is similar to the usage of **this.setState** of the **class** component. | Function |   All    |        yes        |
|         useBoolean         |             Manages the boolean state elegantly.             | Function |   All    |        yes        |
|         useToggle          |                       Toggles states.                        | Function |   All    |        yes        |
|       useCookieState       |                 Stores the state in Cookie.                  | Function |   All    |        yes        |
|   useSessionStorageState   |             Stores the state in sessionStorage.              | Function |   All    |        yes        |
|        useDebounce         |               Deals with the debounced value.                | Function |   All    |        yes        |
|        useThrottle         |            Deals with the value of **Throttle**.             | Function |   All    |        yes        |
|           useMap           |                Manages the state of **Map**.                 | Function |   All    |        yes        |
|           useSet           |                Manages the state of **Set**.                 | Function |   All    |        yes        |
|        usePrevious         |                  Saves the previous state.                   | Function |   All    |        yes        |
|        useRafState         | Updates the state in [requestAnimationFrame](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame), generally used for performance optimization. | Function |   All    |        yes        |
|        useSafeState        | Works in the same way as **React.useState**. However, after the component is unmounted, **setState** in the asynchronous callback is not executed to avoid memory leakage caused by state update. | Function |   All    |        yes        |
|        useGetState         | Adds a **getter** method to the return value of **React.useState** to get the latest value. | Function |   All    |        yes        |
|       useResetState        | Provides a method to reset the state. This hook works similar to **React.useState**. | Function |   All    |        yes        |
|      useUpdateEffect       | Runs the effect when dependencies are updated, but skips running the effect for the first time. This hook works in the same way as **useEffect**. | Function |   All    |        yes        |
|   useUpdateLayoutEffect    | Runs the effect when dependencies are updated, but skips running the effect for the first time. This hook works in the same way as **useLayoutEffect**. | Function |   All    |        yes        |
|       useAsyncEffect       |        Runs the effect using asynchronous functions.         | Function |   All    |        yes        |
|     useDebounceEffect      |                   Debounces **useEffect**.                   | Function |   All    |        yes        |
|       useDebounceFn        |              Deals with the debounce functions.              | Function |   All    |        yes        |
|       useThrottleFn        |              Deals with the throttle functions.              | Function |   All    |        yes        |
|     useThrottleEffect      |                   Throttles **useEffect**.                   | Function |   All    |        yes        |
|    useDeepCompareEffect    | Works in the same way as **useEffect**, but **deps** is compared with [lodash isEqual](https://lodash.com/docs/4.17.15#isEqual). | Function |   All    |        yes        |
| useDeepCompareLayoutEffect | Works in the same way as **useLayoutEffect**, but **deps** is compared with [lodash isEqual](https://lodash.com/docs/4.17.15#isEqual). | Function |   All    |        yes        |
|        useInterval         |         Handles the **setInterval** timer function.          | Function |   All    |        yes        |
|       useRafInterval       | Implements **setInterval** with **requestAnimationFrame**. This hook works in the same way as **useInterval**. The advantage is that the timer can be stopped when the page is not rendered, for example, the page is hidden or minimized. | Function |   All    |        yes        |
|         useTimeout         |          Handles the **setTimeout** timer function.          | Function |   All    |        yes        |
|       useRafTimeout        | Implements **setTimeout** with **requestAnimationFrame**. The API is consistent with **useTimeout**. The advantage is that function execution is not triggered when the page is not rendered, for example, the page is hidden or minimized. | Function |   All    |        yes        |
|         useLockFn          | Adds a lock to an asynchronous function to prevent parallel executions. | Function |   All    |        yes        |
|         useUpdate          | Returns a function which can be used to force the component to re-render. | Function |   All    |        yes        |
|   useControllableValuet    | Manages the states of some components whose states can be managed by themselves or controlled by their parents. | Function |   All    |        yes        |
|        useCreation         | Substitutes for **useMemo** or **useRef** because **useMemo** cannot ensure that the memoized value will not be recalculated, while **useCreation** can ensure that. | Function |   All    |        yes        |
|      useEventEmitter       |    Obtains an instance of **EventEmitter** in components.    | Function |   All    |        yes        |
|         useLatest          |     Returns the latest value to avoid closure problems.      | Function |   All    |        yes        |
|       useMemoizedFn        | Handles persistent functions. In general, **useMemoizedFn** can substitute for **useCallback**. For special cases, see [FAQ](https://ahooks.js.org/hooks/use-memoized-fn/#faq). | Function |   All    |        yes        |
|        useReactive         | Provides data reactivity during operations, in which case **useState** is unnecessary for state definition. Modifying properties will automatically lead to view rerendering. | Function |   All    |        yes        |
|      useTrackedEffect      | Tracks which dependency change triggers the execution of **useEffect**. | Function |   All    |        yes        |
|     useWhyDidYouUpdate     |    Locates the properties that caused component rerender.    | Function |   All    |        yes        |

## Clarification of the Method Not Supported on the Mobile Phone

| title    | hook-name             | Description                                                  | Issue Description                                            | HarmonyOS Support |
| -------- | --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | :---------------: |
| Dom      | useDrop & useDrag     | Manages data transfer between drag and drop.                 | The message "Property 'document' doesn't exist" is displayed. |        NO         |
| Dom      | useEventListener      | Uses **addEventListener** elegantly.                         | No error is reported, but no physical keyboard is available when the keydown event is listened. |        NO         |
| Dom      | useEventListener      | Uses **addEventListener** elegantly.                         | An error is reported, and no physical keyboard is available. |        NO         |
| Dom      | useClickAway          | Listens for click events outside the target element.         | The message "Property 'document' doesn't exist" is displayed. |        NO         |
| Dom      | useDocumentVisibility | Listens for whether the page is visible.                     | No error is reported, but the state change cannot be monitored and the mobile phone window cannot be obtained. |        NO         |
| Dom      | useEventTarget        | Encapsulates **onChange** and **value** logic for form components whose values are obtained through **e.target.value**, and supports custom transformation and reset functionalities. | The error message "Cannot read property 'value' of undefined" is displayed. |        NO         |
| Dom      | useExternal           | Injects JS or CSS resources dynamically. useExternal can ensure that the resources are globally unique. | The message "Property 'document' doesn't exist" is displayed. |        NO         |
| Dom      | useTitle              | Sets the page title.                                         | The message "Property 'document' doesn't exist" is displayed. |        NO         |
| Dom      | useFavicon            | Sets the favicon of the page.                                | The message "Property 'document' doesn't exist" is displayed. |        NO         |
| Dom      | useFullscreen         | Manages DOM full screen.                                     | The message "Property 'document' doesn't exist" is displayed. |        NO         |
| Dom      | useHover              | Listens for whether the element is being hovered.            | No error is reported, but the system does not respond after the button is clicked and the property change cannot be monitored. |        NO         |
| Dom      | useInViewport         | Checks whether the element is in the visible area and the visible area ratio of the element. | The message "Property 'document' doesn't exist" is displayed. |        NO         |
| Dom      | useKeyPress           | Listens for the keyboard press. Composite keys and aliases are supported. | No error is reported, but no physical keyboard is available and properties cannot be operated. |        NO         |
| Dom      | useLongPress          | Listens for the long press event of the target element.      | The message "Property 'document' doesn't exist" is displayed. |        NO         |
| Dom      | useMouse              | Listens for the mouse position.                              | No error is reported, but the system does not respond after the button is clicked and the property change cannot be monitored. |        NO         |
| Dom      | useResponsive         | Obtains responsive information.                              | Cannot convert undefined value to object                     |        NO         |
| Dom      | useScroll             | Listens for the scrolling position of an element.            | The message "Property 'document' doesn't exist" is displayed. |        NO         |
| Dom      | useSize               | Listens for the size change of the DOM node.                 | No error is reported, but the document cannot be obtained.   |        NO         |
| Dom      | useFocusWithin        | Listens for whether the current focus is within a certain area. | No error is reported, but the state change cannot be monitored. |        NO         |
| Advanced | useReactive           | Provides data reactivity during operations, in which case **useState** is unnecessary for state definition. Modifying properties will automatically lead to view rerendering. | Only digits can be entered in the input text box, and the message "Cannot read property 'map' of undefined" is displayed. |        NO         |
| State    | useUrlState           | Manages the state through **url query**.                     | No error is reported and the hook does not take effect.      |        NO         |
| State    | useLocalStorageState  | Stores the state in **localStorage**.                        | No error is reported and the hook does not take effect.      |        NO         |
| Scene    | useAntdTable          | Manages pagination data of **Table**. You only need to pass the returned **tableProps** to the **Table** component. | The UI component cannot be used and document does not exist. |        NO         |
| Scene    | useFusionTable        | Manages the pagination data of **Table**. You only need to pass the returned **tableProps** and **paginationProps** to the corresponding components. | The UI component cannot be used and document does not exist. |        NO         |
| Scene    | useInfiniteScroll     | Encapsulates the common infinite scroll logic.               | In the infinite scrolling scenario, the number of data increases and the scroll does not respond. |        NO         |
| Scene    | usePagination         | Works in the same way as **useRequest**, but returns an additional **pagination** parameter, which contains all pagination information and functions for pagination operations. | An error is reported that **mockjs** is not supported.       |        NO         |
| Scene    | useDynamicList        | Manages dynamic list and generates unique key for each item. | An error is reported and the message "Render ErrorView config getter callback for component path must be a function (received undefined)" is displayed. Make sure to start component names with a capital letter. |        NO         |
| Scene    | useVirtualList        | Allows you to use virtual list to render huge chunks of list data. | No error is reported and the hook does not take effect.      |        NO         |
| Scene    | useNetwork            | Manages the state of network connection.                     | An error is reported and the message "window.addEventListener is not a function" is displayed. |        NO         |
| Scene    | useSelections         | Encapsulates the logic of common Checkbox group. Multiple selection, single selection, select-all, select-none and semi-selected are supported. | The message "Property 'document' doesn't exist" is displayed. |        NO         |
| Scene    | useTextSelection      | Obtains the text content and position selected by the user in real time. | No error is reported, but no mouse is available, and the properties cannot be operated. |        NO         |

## 

## Others

## License

This project is licensed under [MIT License](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Foblador%2Freact-native-progress%2Fblob%2Fmaster%2FLICENSE).
