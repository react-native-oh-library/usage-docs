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

| title         | hook-name                                       | 描述                                                                                                                                                                                              | 类型     | HarmonyOS Support |
| :------------ | :---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ----------------- |
| Sensors       | useMotion                                       | 跟踪设备运动传感器的状态。                                                                                                                                                                        | Function | YES               |
| Animations    | useRaf                                          | 重新渲染每个请求上的组件AnimationFrame。                                                                                                                                                          | Function | YES               |
| Animations    | useInterval and useHarmonicIntervalFn           | 使用setInterval在设置的间隔上重新渲染组件。                                                                                                                                                       | Function | YES               |
| Animations    | useSpring                                       | 根据弹簧动力学随时间插值数字。                                                                                                                                                                    | Function | YES               |
| Animations    | useTimeout                                      | 超时后重新渲染组件。                                                                                                                                                                              | Function | YES               |
| Animations    | useTimeoutFn                                    | 超时后调用给定的函数。                                                                                                                                                                            | Function | YES               |
| Animations    | useTween                                        | 重新渲染组件，同时推特从0到1的数字。                                                                                                                                                              | Function | YES               |
| Animations    | useUpdate                                       | 返回一个回调，该回调在调用时重新呈现组件。                                                                                                                                                        | Function | YES               |
| Side-effects  | useAsync useAsyncFn and useAsyncRetry           | 解析异步函数。                                                                                                                                                                                    | Function | YES               |
| Side-effects  | useBeforeUnload                                 | 当用户尝试重新加载或关闭页面时，显示浏览器警报。                                                                                                                                                  | Function | YES               |
| Side-effects  | useCookie                                       | 提供了读取、更新和删除cookie的方法。                                                                                                                                                              | Function | YES               |
| Side-effects  | useDebounce                                     | 取消对函数的反弹。                                                                                                                                                                                | Function | YES               |
| Side-effects  | useError                                        | 错误调度器。                                                                                                                                                                                      | Function | YES               |
| Side-effects  | useRafLoop                                      | 调用RAF循环内的给定函数。                                                                                                                                                                         | Function | YES               |
| Side-effects  | useThrottle`and`useThrottleFn                   | 抑制函数。                                                                                                                                                                                        | Function | YES               |
| Lifecycles    | useEffectOnce                                   | 仅运行一次的修改后的[`useEffect`](https://reactjs.org/docs/hooks-reference.html#useeffect)。                                                                                                      | Function | YES               |
| Lifecycles    | useLifecycles                                   | 调用`mount`和`unmount`回调。                                                                                                                                                                      | Function | YES               |
| Lifecycles    | useMountedState and useUnmountPromise           | 跟踪是否安装了组件。                                                                                                                                                                              | Function | YES               |
| Lifecycles    | useLogger                                       | 在组件经历生命周期时登录控制台。                                                                                                                                                                  | Function | YES               |
| Lifecycles    | useMount                                        | 调用`mount`回调。                                                                                                                                                                                 | Function | YES               |
| Lifecycles    | useUnmount                                      | 调用`unmount`回调。                                                                                                                                                                               | Function | YES               |
| Lifecycles    | useUpdateEffect                                 | 仅在更新时运行一个`effect。`                                                                                                                                                                      | Function | YES               |
| Lifecycles    | useIsomorphicLayoutEffect                       | useLayoutEffect在服务器上工作。                                                                                                                                                                   | Function | YES               |
| Lifecycles    | useDeepCompareEffect and useCustomCompareEffect | 运行一个`effect`通过深度比较其依赖项。                                                                                                                                                            | Function | YES               |
| State         | createMemo                                      | 记忆挂钩工厂。                                                                                                                                                                                    | Function | YES               |
| State         | createReducerContext and createStateContext     | 用于组件之间共享状态的挂钩的工厂。                                                                                                                                                                | Function | YES               |
| State         | useDefault                                      | 当state为null或未定义时，返回默认值。                                                                                                                                                             | Function | YES               |
| State         | useGetSet                                       | 返回状态getter get（），而不是原始状态。                                                                                                                                                          | Function | YES               |
| State         | useGetSetState                                  | as if [`useGetSet`](https://github.com/streamich/react-use/blob/master/docs/useGetSet.md) and [`useSetState`](https://github.com/streamich/react-use/blob/master/docs/useSetState.md) had a baby. | Function | YES               |
| State         | useLatest                                       | 返回最新状态或道具。                                                                                                                                                                              | Function | YES               |
| State         | usePrevious                                     | 返回以前的状态或道具。                                                                                                                                                                            | Function | YES               |
| State         | usePreviousDistinct                             | 类似于usePrevious，但有一个谓词来确定是否应该更新previous。                                                                                                                                       | Function | YES               |
| State         | useObservable                                   | 跟踪Observable的最新值。                                                                                                                                                                          | Function | YES               |
| State         | useRafState                                     | 创建setState方法，该方法仅在requestAnimationFrame之后更新。                                                                                                                                       | Function | YES               |
| State         | useSetState                                     | 创建setState方法，其工作方式如下:this.setState。                                                                                                                                                  | Function | YES               |
| State         | useStateList                                    | 在数组上循环迭代。                                                                                                                                                                                | Function | YES               |
| State         | useToggle                                       | 跟踪布尔值的状态。                                                                                                                                                                                | Function | YES               |
| State         | useCounter                                      | 跟踪数字的状态。                                                                                                                                                                                  | Function | YES               |
| State         | useList                                         | 跟踪数组的状态。                                                                                                                                                                                  | Function | YES               |
| State         | useMap                                          | 跟踪对象的状态。                                                                                                                                                                                  | Function | YES               |
| State         | useSet                                          | 跟踪集合的状态。                                                                                                                                                                                  | Function | YES               |
| State         | useQueue                                        | 实现了简单的队列。                                                                                                                                                                                | Function | YES               |
| State         | useStateValidator                               | 跟踪对象的状态。                                                                                                                                                                                  | Function | YES               |
| State         | useStateWithHistory                             | 存储以前的状态值，并提供通过这些值的句柄。                                                                                                                                                        | Function | YES               |
| State         | useMultiStateValidator                          | 类似于useStateValidator，但一次跟踪多个状态。                                                                                                                                                     | Function | YES               |
| State         | useMediatedState                                | 类似于常规的useState，但具有自定义功能的中介。                                                                                                                                                    | Function | YES               |
| State         | useFirstMountState                              | 检查当前渲染是否是第一个。                                                                                                                                                                        | Function | YES               |
| State         | useRendersCount                                 | 计数组件渲染。                                                                                                                                                                                    | Function | YES               |
| State         | createGlobalState                               | 跨组件共享状态。                                                                                                                                                                                  | Function | YES               |
| State         | useMethods                                      | 使用Reducer的整洁替代方案。                                                                                                                                                                       | Function | YES               |
| Miscellaneous | useEnsuredForwardedRef                          | 安全地使用React.forwardedRef。                                                                                                                                                                    | Function | YES               |

## IOS & android 不支持方法澄清

| title        | hook-name                                                | 解释                                   | 问题描述                                                       | HarmonyOS Support |
| ------------ | -------------------------------------------------------- | -------------------------------------- | -------------------------------------------------------------- | ----------------- |
| Sensors      | useBattery                                               | 跟踪设备电池状态。                     | 无报错，不支持蓄电池传感器                                     | NO                |
| Sensors      | useGeolocation                                           | 跟踪用户设备的地理位置状态。           | Cannot read property 'getCurrentPosition' of undefined没有属性 | NO                |
| Sensors      | useHover and useHoverDirty                               | 跟踪某些元素的鼠标悬停状态。           | 无报错，无反应                                                 | NO                |
| Sensors      | useHash                                                  | 跟踪位置哈希值。                       | Hash of undefined                                              | NO                |
| Sensors      | useIdle                                                  | 跟踪用户是否处于非活动状态。           | Property 'document' doesn't exist                              | NO                |
| Sensors      | useIntersection                                          | 跟踪HTML元素的交集。                   | 无报错，无反应，状态不对应                                     | NO                |
| Sensors      | useKey, useKeyPress, useKeyboardJs, and useKeyPressEvent | 追踪按键。                             | 无报错，无反应                                                 | NO                |
| Sensors      | useLocation and useSearchParam                           | 跟踪页面导航栏的位置状态。             | Cannot convert undefined value to object                       | NO                |
| Sensors      | useLongPress                                             | 跟踪某些元素的长按手势。               | 无报错，无反应                                                 | NO                |
| Sensors      | useMedia                                                 | 跟踪CSS媒体查询的状态。                | window.matchMedia is not a function (it is undefined)          | NO                |
| Sensors      | useMediaDevices                                          | 跟踪连接的硬件设备的状态。             | 无报错，值为空                                                 | NO                |
| Sensors      | useMouse and useMouseHovered                             | 跟踪鼠标位置的状态。                   | Property 'document' doesn't exist                              | NO                |
| Sensors      | useMouseWheel                                            | 跟踪滚动鼠标滚轮的deltaY。             | 无报错，无反应                                                 | NO                |
| Sensors      | useNetworkState                                          | 跟踪浏览器的网络连接状态。             | 无报错，值为空                                                 | NO                |
| Sensors      | useOrientation                                           | 跟踪设备屏幕方向的状态。               | Cannot read property 'orientation' of undefined                | NO                |
| Sensors      | usePageLeave                                             | 当鼠标离开页面边界时触发。             | Property 'document' doesn't exist 属性“document”不存在         | NO                |
| Sensors      | useScratch                                               | 跟踪鼠标单击和拖动状态。               | 未报错，无反应                                                 | NO                |
| Sensors      | useScroll                                                | 跟踪HTML元素的滚动位置。               | 未报错，无反应                                                 | NO                |
| Sensors      | useScrolling                                             | 跟踪HTML元素是否正在滚动。             | 未报错，无反应                                                 | NO                |
| Sensors      | useStartTyping                                           | 检测用户何时开始键入。                 | Property 'document' doesn't exist 属性“document”不存在         | NO                |
| Sensors      | useWindowScroll                                          | 轨迹窗口滚动位置。                     | 无报错，值为空                                                 | NO                |
| Sensors      | useWindowSize                                            | 跟踪窗口尺寸。                         | 无报错，值为空                                                 | NO                |
| Sensors      | useMeasure and useSize                                   | 跟踪HTML元素的维度。                   | 无报错，值为空                                                 | NO                |
| Sensors      | createBreakpoint                                         | 跟踪内部宽度。                         | 无报错，返回设备不正确                                         | NO                |
| Sensors      | useScrollbarWidth                                        | 检测浏览器的本地滚动条宽度。           | 无报错，值为0                                                  | NO                |
| Sensors      | usePinchZoom                                             | 跟踪指针事件以检测收缩放大和缩小状态。 | Property 'useState' doesn't exist                              | NO                |
| UI           | useAudio                                                 | 播放音频并公开其控件。                 | 组件“audio”的 View config getter 回调必须是一个函数            | NO                |
| UI           | useClickAway                                             | 当用户在目标区域外单击时触发回调。     | Property 'document' doesn't exist 属性“document”不存在         | NO                |
| UI           | useCss                                                   | 动态调整CSS。                          | Property 'document' doesn't exist 属性“document”不存在         | NO                |
| UI           | useDrop and useDropArea                                  | 跟踪文件、链接和复制粘贴滴漏。         | Property 'document' doesn't exist 属性“document”不存在         | NO                |
| UI           | useFullscreen                                            | 全屏显示元素或视频。                   | 组件“video”的视图配置getter回调必须是一个函数                  | NO                |
| UI           | useSlider                                                | 在任何HTML元素上提供幻灯片行为。       | Cannot set property 'userSelect' of undefined                  | NO                |
| UI           | useSpeech                                                | 从文本字符串合成语音。                 | Cannot read property 'getVoices' of undefined                  | NO                |
| UI           | useVibrate                                               | 使用振动API提供物理反馈。              | 0, \_react.useToggle is not a function (it is undefined)       | NO                |
| UI           | useVideo                                                 | 播放视频、跟踪其状态并公开播放控件。   | 组件“video”的视图配置getter回调必须是一个函数                  | NO                |
| Side-effects | useCopyToClipboard                                       | 将文本复制到剪切板。                   | 无报错无反应                                                   | NO                |
| Side-effects | useFavicon                                               | 设置页面的useFavicon。                 | Property 'document' doesn't exist 属性“document”不存在         | NO                |
| Side-effects | useLocalStorage                                          | 管理useLocalStorage中的值。            | 无报错无反应                                                   | NO                |
| Side-effects | useLockBodyScroll                                        | 锁定body元素的滚动。                   | 无报错无反应                                                   | NO                |
| Side-effects | useSessionStorage                                        | 管理sessionStorage中的值。             | 无报错无反应                                                   | NO                |
| Side-effects | useTitle                                                 | 设置页面的标题。                       | 无报错无反应                                                   | NO                |
| Side-effects | usePermission                                            | 查询浏览器API的权限状态。              | Cannot read property 'query' of undefined                      | NO                |
| Lifecycles   | usePromise                                               | 仅在安装组件时解析promise。            | 无报错无反应                                                   | NO                |
| Lifecycles   | useEvent                                                 | 订阅事件。                             | 无报错无反应                                                   | NO                |
| State        | createReducer                                            | 带有定制中间件的减速器挂钩工厂。       | 无报错无反应                                                   | NO                |

## 遗留问题

## 其他
