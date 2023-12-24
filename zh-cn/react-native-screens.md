> 模板版本：v0.0.1

<p align="center">
  <h1 align="center"> <code>react-native-screens</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-screens">
        <img src="https://img.shields.io/badge/platforms-iOS%20|%20Android%20|%20tvOS%20|%20Windows%20|%20Web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://opensource.org/license/mit/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

### 禁用 `react-native-screens`

因为 ArkUI(Navigation、NavRouter、NavDestination)没有代理任何独特功能，且无法映射到 main_page 通过页面容器优化性能，所以 react-native-screens 禁用鸿蒙原生屏幕使用 react-native views 即可，请在您的入口文件中添加以下代码。 (例如. `App.js`):

```js
import { enableScreens } from "react-native-screens";

enableScreens(false);
```

您还可以通过[`detachInactiveScreens`](https://reactnavigation.org/docs/stack-navigator#detachinactivescreens)在每个导航器中禁用使用原生屏幕。后续待补充各个接口验证情况。

## 属性

[原库接口文档](https://github.com/software-mansion/react-native-screens/blob/main/guides/GUIDE_FOR_LIBRARY_AUTHORS.md) 由于使用 RN 的 view 实现相关功能，理论上接口均支持，若有不可用部分欢迎提交 [issue](https://gitee.com/react-native-oh-library/usage-docs/issues).

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/a7ul/react-native-exception-handler/blob/master/LICENSE) ，请自由地享受和参与开源。
