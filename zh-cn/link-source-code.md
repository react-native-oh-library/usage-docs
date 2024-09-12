<!-- {% raw %} -->
### 2.引入原生端代码

#### 直接链接源码情况说明

目前 DevEco Studio 不支持通过源码引入外部 module，我们推荐使用 har 包的方式引入，如需要直接链接源码，请按照以下步骤操作，将源码通过操作改成 harmony 工程的内部模块。

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

把`<RN工程>/node_modules/@react-native-oh-tpl/<Package_Name>/harmony/`目录下的源码`<xxx>`复制到`harmony`工程根目录下

在`harmony`工程根目录的 `build-profile.template.json5`（若存在）和`build-profile.json5` 添加以下模块

```json
modules:[
  ...
  {
    name: '<xxx>',
    srcPath: './<xxx>',
  }
  //提示：{
  //        name: 'safe_area',
  //        srcPath: './safe_area',
  //      } 
]
```

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/<Package_Name>": "file:../<xxx>"
    // 提示: "@react-native-oh-tpl/react-native-safe-area-context": "file:../safe_area"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

<!-- {% endraw %} -->