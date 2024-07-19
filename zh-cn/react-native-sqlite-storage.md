<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-sqlite-storage</code> </h1>
</p>  
<p align="center">
    <a href="https://github.com/andpor/react-native-sqlite-storage">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/andpor/react-native-sqlite-storage/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-sqlite-storage)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-sqlite-storage Releases](https://github.com/react-native-oh-library/react-native-sqlite-storage/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-sqlite-storage@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-sqlite-storage@file:#
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
/**
 * @format
 */
import React, {Component} from 'react';
import {AppRegistry, StyleSheet, Text, View, FlatList} from 'react-native';
import {name as appName} from './app.json';
import SQLite from 'react-native-sqlite-storage';
SQLite.DEBUG(true);
SQLite.enablePromise(false);

const database_name = 'Test.db';
const database_version = '1.0';
const database_displayname = 'SQLite Test Database';
const database_size = 200000;
let db;
const Item = ({title}) => (
  <View style={styles.item}>
    <Text style={styles.title}>{title}</Text>
  </View>
);
class SQLiteDemo extends Component {
  constructor() {
    super();
    this.progress = [];
    this.state = {
      progress: [],
    };
  }

  updateProgress = (text, resetState) => {
    let progress = [];
    if (!resetState) {
      progress = [...this.progress];
    }
    progress.push(text);
    this.progress = progress;
    this.setState({
      progress,
    });
  };

  componentWillUnmount = () => {
    this.closeDatabase();
  };

  errorCB = err => {
    console.log('error: ', err);
    this.updateProgress('Error: ' + (err.message || err));
    return false;
  };

  successCB = () => {
    console.log('SQL executed ...');
  };

  openCB = () => {
    this.updateProgress('Database OPEN');
  };

  closeCB = () => {
    this.updateProgress('Database CLOSED');
  };

  deleteCB = () => {
    console.log('Database DELETED');
    this.updateProgress('Database DELETED');
  };

  // eslint-disable-next-line no-shadow
  populateDatabase = db => {
    this.updateProgress('Database integrity check');
    db.executeSql('SELECT 1 FROM Version LIMIT 1',[],() => {
        this.updateProgress('Database is ready ... executing query ...');
        db.transaction(this.queryEmployees, this.errorCB, () => {
          this.updateProgress('Processing completed');
        });
      },
      error => {
        console.log('received version error:', error);
        this.updateProgress('Database not yet ready ... populating data');
        db.transaction(this.populateDB, this.errorCB, () => {
          this.updateProgress('Database populated ... executing query ...');
          db.transaction(this.queryEmployees, this.errorCB, () => {
            console.log('Transaction is now finished');
            this.updateProgress('Processing completed');
          });
        });
      },
    );
  };

   populateDB = tx => {
    this.updateProgress('Executing DROP stmts');

    tx.executeSql('DROP TABLE IF EXISTS Employees;');
    tx.executeSql('DROP TABLE IF EXISTS Offices;');
    tx.executeSql('DROP TABLE IF EXISTS Departments;');

    this.updateProgress('Executing CREATE stmts');

    tx.executeSql('CREATE TABLE IF NOT EXISTS Version( ' +'version_id INTEGER PRIMARY KEY NOT NULL); ',[],this.successCB,this.errorCB,);

    tx.executeSql('CREATE TABLE IF NOT EXISTS Departments( ' +'department_id INTEGER PRIMARY KEY NOT NULL, ' +'name VARCHAR(30) ); ',[],this.successCB,this.errorCB,);

    tx.executeSql('CREATE TABLE IF NOT EXISTS Offices( ' +'office_id INTEGER PRIMARY KEY NOT NULL, ' +'name VARCHAR(20), ' +'longtitude FLOAT, ' +'latitude FLOAT ) ; ',[],this.successCB,this.errorCB,);

    tx.executeSql('CREATE TABLE IF NOT EXISTS Employees( ' +'employe_id INTEGER PRIMARY KEY NOT NULL, ' +'name VARCHAR(55), ' +'office INTEGER, ' +'department INTEGER, ' +'custom_info TEXT DEFAULT "",' +'FOREIGN KEY ( office ) REFERENCES Offices ( office_id ) ' +'FOREIGN KEY ( department ) REFERENCES Departments ( department_id ));',[],);


    this.updateProgress('Executing INSERT stmts');
       
    tx.executeSql('INSERT INTO Departments (name) VALUES ("Client Services");',[],);

    tx.executeSql('INSERT INTO Offices (name, longtitude, latitude) VALUES ("Denver", 59.8,  34.);',[],);

    console.log('all config SQL done');
  };

  queryEmployees = async tx => {
    console.log('Executing JSON1 queries...');

    // 1. JSON_OBJECT
    await tx.executeSql( "SELECT JSON_OBJECT('name', e.name, 'office_id', e.office, 'department_id', e.department) AS data FROM Employees e",[],this.querySuccess,this.errorCB,);

    // 2. JSON_ARRAY
    // Expected: [1,2,"3",4]
    await tx.executeSql("SELECT JSON_ARRAY(1, 2, '3', 4) AS data ",[],this.querySuccess,this.errorCB,);

    // 3. JSON_ARRAY_LENGTH
    // Expected: 4
    await tx.executeSql("SELECT JSON_ARRAY_LENGTH('[1, 2, 3, 4]') AS data",[],this.querySuccess,this.errorCB,);

    // 4. JSON_EXTRACT
    await tx.executeSql( "SELECT JSON_EXTRACT(e.custom_info, '$.known')  AS data FROM Employees e", [],this.querySuccess,this.errorCB,);
      
    // 5. JSON_INSERT
    // Expected: {"a":1,"b":2,"c":3}
    await tx.executeSql('SELECT JSON_INSERT(\'{"a": 1, "b": 2}\', \'$.c\', 3)  AS data',[],this.querySuccess,this.errorCB,);
  };

  querySuccess = (tx, results) => {
    this.updateProgress('Query completed');
    var len = results.rows.length;
    for (let i = 0; i < len; i++) {
      let row = results.rows.item(i);
      this.updateProgress(`${row.data}`);
    }
  };

  loadAndQueryDB = () => {
    this.updateProgress('Opening database ...', true);
    this.updateProgress('Database OPEN');
    db = SQLite.openDatabase(database_name,database_version,database_displayname,database_size,this.openCB,this.errorCB,);
    this.populateDatabase(db);
  };

  deleteDatabase = () => {
    this.updateProgress('Deleting database');
    SQLite.deleteDatabase(database_name, this.deleteCB, this.errorCB);
  };

  closeDatabase = () => {
    if (db) {
      console.log('Closing database ...');
      this.updateProgress('Closing database');
      db.close(this.closeCB, this.errorCB);
    } else {
      this.updateProgress('Database CLOSE callback function error');
    }
  };

  runDemo = () => {
    this.updateProgress('Starting SQLite Callback Demo', true);
    this.loadAndQueryDB();
  };

  renderProgressEntry = entry => {
    return (
      <View style={listStyles.li}>
        <View>
          <Text style={listStyles.liText}>{entry}</Text>
        </View>
      </View>
    );
  };

  render = () => {
    return (
      <View style={styles.mainContainer}>
        <View style={styles.toolbar}>
          <Text style={styles.toolbarButton} onPress={this.runDemo}>Run Demo</Text>
          <Text style={styles.toolbarButton} onPress={this.closeDatabase}>Close DB</Text>
          <Text style={styles.toolbarButton} onPress={this.deleteDatabase}>Delete DB</Text>
        </View>
        <FlatList
          data={this.state.progress}
          renderItem={({item}) => <Item title={item} />}
          keyExtractor={item => item.i}
        />
      </View>
    );
  };
}

var listStyles = StyleSheet.create({
  li: {
    borderBottomColor: '#c8c7cc',
    borderBottomWidth: 0.5,
    paddingTop: 15,
    paddingRight: 15,
    paddingBottom: 15,
  },
  liContainer: {
    backgroundColor: '#fff',
    flex: 1,
    paddingLeft: 15,
  },
  liIndent: {
    flex: 1,
  },
  liText: {
    color: '#333',
    fontSize: 17,
    fontWeight: '400',
    marginBottom: -3.5,
    marginTop: -3.5,
  },
});

var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
  toolbar: {
    backgroundColor: '#51c04d',
    paddingTop: 30,
    paddingBottom: 10,
    flexDirection: 'row',
  },
  toolbarButton: {
    color: 'blue',
    textAlign: 'center',
    flex: 1,
  },
  mainContainer: {
    flex: 1,
  },
});
AppRegistry.registerComponent(appName, () => SQLiteDemo);

```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前HarmonyOS暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-sqlite-storage": "file:../../node_modules/@react-native-oh-tpl/react-native-sqlite-storage/platforms/harmony/sqlite_storage.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)


### 在 ArkTs 侧引入 SQLitePluginPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {SQLitePluginPackage} from '@react-native-oh-tpl/react-native-sqlite-storage/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SQLitePluginPackage(ctx)
  ];
}
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-sqlite-storage Releases](https://github.com/react-native-oh-library/react-native-sqlite-storage/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| qid  | 	Unique identifier for the query        | number  | yes | All      | yes |
| sql  | SQL statement to be executed        | string  | yes| All     | yes |
| params  | Parameter list for the SQL statement       |any[]  | yes | All      | yes |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| echoStringValue  | Adapter method    | void  | yes |All     |  yes |
| open  | Opens or initializes        | void  | yes |All     |  yes |
| close  |Closes or releases a previously opened resource      | void  |  yes |All     |  yes |
| delete  |Deletes a resource       |void   |  yes | All   |  yes |
|attach  | Connects or associates with an external resource or database  |  void  |  yes | All   |  yes|
| backgroundExecuteSqlBatch  |Executes a batch of SQL statements in the background without blocking the current thread or process | void   |  yes |All     |  yes |
| execute  |   Bridge execution method   | boolean   |  yes |All     |  yes |
|  startDatabase |   Opens a database    | void   |  yes |All     |  yes |
| closeDatabase  |  Closes a database      | void   |  yes |All     |  yes |
| deleteDatabase  | Deletes a database     | void   |  yes |All     |  yes |
| executeSqlBatchDatabase  | Executes a batch of SQL statements on a database     | void   |  yes |All     |  yes |
| attachDatabase  | Bridges a database  | void   |  yes |All     |  yes |
| INIT | Creates a database sandbox directory and retrieves the database file from the app's rawfile | void   |  yes |All     |  yes |
| saveFileToCache |  Reads the database file from the app's rawfile and saves it to the database sandbox directory  | void   |  yes |All     |  yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/andpor/react-native-sqlite-storage/blob/master/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->