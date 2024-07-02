<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-storage</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/sunnylqm/react-native-storage">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/sunnylqm/react-native-storage/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/sunnylqm/react-native-storage)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-storage@1.0.1
```

#### **yarn**

```bash
yarn add react-native-storage@1.0.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import Storage from 'react-native-storage';
import AsyncStorage from '@react-native-async-storage/async-storage';
 class StorageDemo extends Component {
    constructor() {
      super();
      this.listData = [];
      this.state = {
        listData: [],
      };
    }
    updateProgress = (text, resetState) => {
      let listData = [];
      if (!resetState) {
        listData = [...this.listData];
      }
      listData.push(text);
      this.listData = listData;
      this.setState({
        listData,
      });
    };
    componentWillUnmount = () => {
      this.timer && clearTimeout(this.timer);
    };
    saveStorageFun = (type) => {
      console.log("test==== >>>>storage====saveStorageFun");
      this.updateProgress("saveStorage start...");
      storage.save({
        key: 'user', 
        id: type==1?userA.id:userB.id, 
        data: type==1?userA:userB,
        expires: 1000 * 3600 * 24
      }).then(() => {
        console.log("test==== >>>>storage====saveStorage  success");
        this.updateProgress("saveStorage success");
        this.loadStorageFun(type==1?userA:userB)
      });
    
    };
  loadStorageFun = (user) => {
    this.updateProgress("loadStorage start...");
    console.log("test==== >>>>storage====loadStorageFun");
    storage.load({
      key: user.key,
      id:user.id,
    autoSync: false,
    syncInBackground: true,
    }).then(ret => {
      this.updateProgress("data:{"+JSON.stringify(ret)+"}");
      console.log("test==== >>>>storage===="+JSON.stringify(ret));
      this.updateProgress("loadStorage success");
    }).catch(err => {
      console.warn(err.message);
      this.updateProgress("loadStorage fail:"+err.message);
      console.log("test==== >>>>storage====loadStorageFunError   "+err.message);
      switch (err.name) {
          case 'NotFoundError':
              // TODO;
          
              break;
          case 'ExpiredError':
              // TODO
              break;
      }
    })
  }
 removeStorageFun = (type) => {
    this.updateProgress("removeStoreage start...");
    storage.remove({
      key:type==1?userA.key:userB.key,
      id:type==1?userA.id:userB.id
    }).then(() => {
      this.updateProgress("removeStoreage success");
      this.loadStorageFun(type==1?userB:userA)
    }).catch(err => {
      this.updateProgress("removeStorage fail:"+err.message);
      console.log("test==== >>>>storage====removeStorageFunError   "+err.message);
    });
  }
  getIdsForKeyStorageFun = (key) => {
    this.updateProgress("getIdsForKey start...");
    storage.getIdsForKey(key).then(ids => {
      this.updateProgress("getIdsForKey: "+JSON.stringify(ids));
      userids = ids
      console.log(ids);
      console.log("test==== >>>>storage=getIdsForKeyStorageFun==="+JSON.stringify(ids));
      this.updateProgress("getIdsForKey success");
    }).catch(err => {
      this.updateProgress("getIdsForKeyStorage fail:"+err.message);
      console.log("test==== >>>>storage====getIdsForKeyStorageFun===Error   "+err.message);
    });
  }
  getAllDataForKeyStorageFun = (key) => {
    storage.getAllDataForKey(key).then(users => {
      console.log(users);
      console.log("test==== >>>>storage=getAllDataForKeyStorageFun==="+JSON.stringify(users));
    });
  }
  clearMapForKeyStorageFun= (key) =>{
    storage.clearMapForKey(key);
    console.log("test==== >>>>storage=clearMapForKeyStorageFun===");
  }
  clearMapStorageFun = () => {
    console.log("test==== >>>>storage=clearMapStorageFun===");
    this.updateProgress("clearMapStorage start...")
    storage.clearMap().then(() => {
      this.updateProgress("clearMapStorage success")
      this.loadStorageFun(userA)
    });
  }
   getBatchDataStorageFun = () => {
    console.log("test==== >>>>storage=getBatchDataStorageFun===start...");
    storage.getBatchData([
	    { key: 'user'}
    ]).then(results => {
      console.log("test==== >>>>storage=getBatchDataStorageFun==="+JSON.stringify(results));
    })
  }
  getBatchDataWithIdsStorageFun = () => {
    storage.getIdsForKey('user').then(userids => {
      storage.getBatchDataWithIds({
      key: 'user',,
      ids:userids
    }).then(retData => {
      this.updateProgress("storage data: "+JSON.stringify(retData));
      console.log("test==== >>>>storage=getBatchDataWithIdsStorageFun==="+JSON.stringify(retData));
    }).catch(err => {
      console.log("test==== >>>>storage====getBatchDataWithIdsStorageFun===Error   "+err.message);
    });
    }).catch(err => {
      this.updateProgress("getIdsForKeyStorage fail:"+err.message);
      console.log("test==== >>>>storage====getIdsForKeyStorageFun===Error   "+err.message);
    });
  }
 renderProgressEntry = entry => {
    return (
      <View style={listStyles.li}>
        <View>
          <Text style={listStyles.liText}>{entry.name}</Text>
        </View>
      </View>
    );
  };
  render = () => {
    return (
      <View style={styles.mainContainer}>
        <View style={styles.textdata}>
          <Text style = {styles.textkey}>{JSON.stringify(userA)}</Text>
          <Text style = {styles.textkey}>{JSON.stringify(userB)}</Text>
          <Button label='save userA' style={styles.toolbarButton} onPress={() => this.saveStorageFun(1)}/>
          <Button label='save userB' style={styles.toolbarButton} onPress={() =>this.saveStorageFun(2)}/>
          <Button label='get user key all ids' style={styles.toolbarButton} onPress={() =>this.getIdsForKeyStorageFun('user')}/>
          <Button label='remove user key one data' style={styles.toolbarButton} onPress={() =>this.removeStorageFun(1)}/>
          <Button label='clearMapStorage' style={styles.toolbarButton} onPress={() =>this.clearMapStorageFun()}/>
          <Button label='read storage data' style={styles.toolbarButton} onPress={() =>this.getBatchDataWithIdsStorageFun()}/>
        </View>
        <FlatList
          data={this.state.listData}
          renderItem={({item}) => <Item title={item} />}
          keyExtractor={item => item.i}
        />
      </View>
    );
  };
}
  export default StorageDemo;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

RNOH: 0.72.22; SDK: OpenHarmony(api12) 5.0.0.22; IDE: DevEco Studio 5.0.3.228; ROM: 3.0.0.23;


## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| remove  | 删除单个数据         | function  | yes | iOS/Android      | yes |
| load  | 读取         | function  | yes | iOS/Android      | yes |
| clearAll  | 清空所有数据        | function  | yes | iOS/Android      | yes |
| clearMap  | 清空map,移除所有"key-id"数据（但会保留只有key的数据）         | function  | yes | iOS/Android      | yes |
| clearMapForKey  | 清除某个key下的所有数据(仅key-id数据)         | function  | yes | iOS/Android      | yes |
| getIdsForKey  | 获取某个key下的所有id         | function  | yes | iOS/Android      | yes |
| getBatchData  | 使用和load方法一样的参数读取批量数据，但是参数是以数组的方式提供，会在需要时分别调用相应的sync方法，最后统一返回一个有序数组。        | function  | yes | iOS/Android      | yes |
| getBatchDataWithIds  | 根据key和一个id数组来读取批量数据        | function  | yes | iOS/Android      | yes |
| sync  | 在调用load时，如果本地并没有存储相应的 user，那么会自动触发 storage.sync.user 去远程取回数据并无缝返回        | function  | yes | iOS/Android      | yes |
| save  | 保存数据，这些数据一般是全局独有的，需要谨慎单独处理的数据       | function  | yes | iOS/Android      | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/sunnylqm/react-native-storage/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->