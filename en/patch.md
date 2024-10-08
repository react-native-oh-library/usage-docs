# RN 三方库补丁化移植

### 简介

因为 `RN` 三方库 `HarmonyOS` 化需保证不影响其他平台上的使用，因此`HarmonyOS` `RN` 三方库使用补丁化实现，项目中会存在**两个独立的包如 `react-native-svg` 和 `@react-native-oh-tpl/react-native-svg`** ,其中 `@react-native-oh-tpl/react-native-svg` 是 `HarmonyOS` 化的库，只能运行在 `HarmonyOS` 平台，两者结合实现了可运行在多平台的 `react-native-svg` , **即在原库的基础上打上适配 `HarmonyOS` 平台的补丁**，其他平台仍走原逻辑不受影响，`HarmnyOS` 侧则使用补丁内代码来实现。

### 如何配置

需要在 `package.json` 添加如下配置：

```diff
{
  "name": "@react-native-oh-tpl/react-native-svg",
+  "harmony": {
+   "alias": "react-native-svg"
+ },
...
}
```

RNOH 会在开发者使用 `import xxx from 原库名` 时，在平台为 `HarmonyOS` 时会重定向到配置了 harmony:alias 字段的三方库里。

比如:

```js
import Svg from "react-native-svg";
```

等于：

```js
import Svg from "@react-native-oh-tpl/react-native-svg";
```

这样开发者就可以不需要更改库名即可使用到我们的补丁内容。

### 影响

对于三方库使用者来说，只需要根据使用文档进行相关配置即可，无其他使用影响，以 [react-native-svg](./react-native-svg-capi.md/) 为例：

1. 安装 `@react-native-oh-tpl/react-native-svg`;
2. 配置相关 Link 操作；

由于该库内部已配置了别名 `react-native-svg`，**因此项目中仍然可以正确识别该库，使用方式也不需要进行特殊修改**。
