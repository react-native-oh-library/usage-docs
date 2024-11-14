# RNOH 三方库 tgz 包使用说明

## 1. 方法一：本地安装

### 1.1 访问对应的三方库 Release 页面

- 查找所需版本。
- 下载附件中的 tgz 包到本地。
- 将 tgz 包放置在指定路径。

### 1.2 安装

- 执行以下命令：

    ```bash
    npm install <三方库包名>@file:<tgz本地路径>
    ```

    示例：

    ```bash
    npm install @react-native-oh-tpl/react-native-svg@file:react-native-oh-tpl-react-native-svg-15.0.0-0.5.8.tgz
    ```

- 或者直接在 `package.json` 中指定路径：

    ```json
    "dependencies": {
        "<三方库包名>": "<tgz本地路径>"
    }
    ```

    示例：

    ```json
    "dependencies": {
        "@react-native-oh-tpl/react-native-svg": "file:react-native-oh-tpl-react-native-svg-15.0.0-0.5.8.tgz"
    }
    ```

## 2. 方法二：在线安装

### 2.1 访问对应的三方库 Release 页面

- 查找所需版本。
- 复制附件中 tgz 包的在线地址。

### 2.2 安装

- 执行以下命令：

    ```bash
    npm install <三方库包名>@file:<tgz在线地址>
    ```

    示例：

    ```bash
    npm install @react-native-oh-tpl/react-native-svg@https://github.com/react-native-oh-library/react-native-harmony-svg/releases/download/15.0.0-0.5.8/react-native-oh-tpl-react-native-svg-15.0.0-0.5.8.tgz
    ```

- 或者直接在 `package.json` 中指定在线地址：

    ```json
    "dependencies": {
        "<三方库包名>": "<tgz在线地址>"
    }
    ```

    示例：

    ```json
    "dependencies": {
        "@react-native-oh-tpl/react-native-svg": "https://github.com/react-native-oh-library/react-native-harmony-svg/releases/download/15.0.0-0.5.8/react-native-oh-tpl-react-native-svg-15.0.0-0.5.8.tgz"
    }
    ```