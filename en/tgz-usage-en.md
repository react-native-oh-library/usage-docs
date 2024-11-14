# RNOH Third-party Library tgz Package Usage Instructions

## 1. Option 1: Local Installation

### 1.1 Navigate to the corresponding Release page of the third-party library

- Find the desired version.
- Download the tgz package from the attachment to your local machine.
- Place it in the designated path.

### 1.2 Installation

- Run the following command:

    ```bash
    npm install <third-party-library-package-name>@file:<local-tgz-path>
    ```

    Example:

    ```bash
    npm install @react-native-oh-tpl/react-native-svg@file:react-native-oh-tpl-react-native-svg-15.0.0-0.5.8.tgz
    ```

- Or directly specify it in the `package.json`:

    ```json
    "dependencies": {
        "<third-party-library-package-name>": "<local-tgz-path>"
    }
    ```

    Example:

    ```json
    "dependencies": {
        "@react-native-oh-tpl/react-native-svg": "file:react-native-oh-tpl-react-native-svg-15.0.0-0.5.8.tgz"
    }
    ```

## 2. Option 2: Online Installation

### 2.1 Navigate to the corresponding Release page of the third-party library

- Find the desired version.
- Copy the online URL of the tgz package from the attachment.

### 2.2 Installation

- Run the following command:

    ```bash
    npm install <third-party-library-package-name>@file:<online-tgz-url>
    ```

    Example:

    ```bash
    npm install @react-native-oh-tpl/react-native-svg@https://github.com/react-native-oh-library/react-native-harmony-svg/releases/download/15.0.0-0.5.8/react-native-oh-tpl-react-native-svg-15.0.0-0.5.8.tgz
    ```

- Or directly specify it in the `package.json`:

    ```json
    "dependencies": {
        "<third-party-library-package-name>": "<online-tgz-url>"
    }
    ```

    Example:

    ```json
    "dependencies": {
        "@react-native-oh-tpl/react-native-svg": "https://github.com/react-native-oh-library/react-native-harmony-svg/releases/download/15.0.0-0.5.8/react-native-oh-tpl-react-native-svg-15.0.0-0.5.8.tgz"
    }
    ```
