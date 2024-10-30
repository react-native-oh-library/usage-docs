> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>Parse-SDK-JS</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/parse-community/Parse-SDK-JS">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/parse-community/Parse-SDK-JS/blob/alpha/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/parse-community/Parse-SDK-JS)

## Installation and Usage

> [!TIP] 需要配套的服务和三方依赖

Parse JS SDK 兼容以下版本的 Parse Server，Parse Server 服务端搭建可参考[https://github.com/parse-community/parse-server/blob/alpha/README.md](https://github.com/parse-community/parse-server/blob/alpha/README.md)。

|   Parse JS SDK   |   Parse Server   |
| :--------------: | :--------------: |
| >= 4.0.0 < 5.0.0 | >= 6.0.0 < 7.0.0 |
|     >= 5.0.0     |     >= 7.0.0     |

> [!TIP] This library depends on[@react-native-oh-tpl/async-storage](/zh-cn/react-native-async-storage-async-storage.md)、[@react-native-oh-tpl/react-native-get-random-values](/zh-cn/react-native-get-random-values.md)

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install parse@5.3.0
```

#### **yarn**

```bash
yarn add parse@5.3.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```jsx
import React, { useState } from "react";
import { View, Text, Button, Alert, StyleSheet } from "react-native";
import AsyncStorage from "@react-native-async-storage/async-storage";
import Parse from "parse/react-native";

Parse.setAsyncStorage(AsyncStorage);
Parse.initialize("your appId", "your javaScriptKey", "your masterKey");
Parse.serverURL = "your parse server url";
Parse.CoreManager.set("REQUEST_HEADERS", {
  "X-Parse-REST-API-Key": "your RESTAPIKEY",
});

const ParseExample = () => {
  const [data, setData] = useState < any > [];

  async function saveData() {
    const TestObject = Parse.Object.extend("TestObject");
    const testObject = new TestObject();
    testObject.set("name", "Zhang San");
    testObject.set(
      "description",
      "I am Zhang San, created by rn using the parse sdk js library!"
    );

    try {
      const result = await testObject.save();
      if (result) {
        Alert.alert("Added successfully");
      } else {
        Alert.alert("Add failed");
      }
      console.log("Object saved successfully:", result);
    } catch (error) {
      console.error("Error while saving object:", error);
    }
  }
  async function deleteData() {
    const TestObject = Parse.Object.extend("TestObject");
    const query = new Parse.Query(TestObject);
    query.equalTo("name", "Li Si");
    try {
      const results = await query.first();
      if (results) {
        Parse.Object.destroyAll(results).then((res) => {
          Alert.alert("Delete successfully");
        });
      } else {
        Alert.alert("Li Si not found");
      }
    } catch (error) {
      console.error("Error while fetching objects:", error);
    }
  }
  async function updateData() {
    const TestObject = Parse.Object.extend("TestObject");
    const query = new Parse.Query(TestObject);
    try {
      query.equalTo("name", "Zhang San");
      const results = await query.first();
      if (results) {
        console.log(results, 666);
        results.set("name", "Li Si");
        results.set("description", "My name has been changed to Li Si");
        results.save().then((update) => {
          Alert.alert("Modified successfully");
        });
      } else {
        Alert.alert("Modified filed");
      }
    } catch (error) {
      console.error("Error while fetching objects:", error);
    }
  }

  async function fetchData() {
    const TestObject = Parse.Object.extend("TestObject");
    const query = new Parse.Query(TestObject);

    try {
      const results = await query.find();
      const resultJson = results.map((item) => item.toJSON());
      console.log("query was successful:", resultJson);
      setData(resultJson);
    } catch (error) {
      console.error("Error while fetching objects:", error);
    }
  }

  return (
    <View style={style.mainBox}>
      <Text style={{ fontSize: 18, fontWeight: "bold" }}>
        Simulate data for adding, deleting, modifying, and querying
      </Text>
      <Text style={{ fontSize: 16, fontWeight: "bold" }}>
        TestObject Class (Table)
      </Text>
      <View style={{ marginTop: 10, marginBottom: 10 }}>
        <Button
          title="Add one piece of data for Zhang San"
          onPress={saveData}
        />
      </View>
      <View style={{ marginBottom: 10 }}>
        <Button
          title="Delete a data entry with the name Li Si"
          onPress={deleteData}
        />
      </View>
      <View style={{ marginBottom: 10 }}>
        <Button
          title="Modify, change one Zhang San data to Li Si"
          onPress={updateData}
        />
      </View>
      <Button title="Query all data" onPress={fetchData} />
      <View style={style.showBox}>
        {data?.map((item) => {
          return (
            <View style={{ marginTop: 10 }} key={item.objectId}>
              <Text>name: {item?.name}</Text>
              <Text>description: {item?.description}</Text>
            </View>
          );
        })}
      </View>
    </View>
  );
};

const style = StyleSheet.create({
  mainBox: {
    borderWidth: 1,
    borderColor: "#ebebeb",
    padding: 10,
    marginTop: 10,
  },
  showBox: {
    backgroundColor: "#f5f5f5",
    marginTop: 10,
    padding: 10,
    borderWidth: 1,
    borderColor: "#ebebeb",
  },
});

export default ParseExample;
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/async-storage、@react-native-oh-tpl/react-native-get-random-values. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/async-storage docs](/zh-cn/react-native-async-storage-async-storage.md)、[@react-native-oh-tpl/react-native-get-random-values docs](/zh-cn/react-native-get-random-values.md) to add it to your project.

## Constraints

## Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;

## API

不同版本对应的 API 也不同，详情请查看[Parse-SDK-JS 官方文档](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/index.html)。

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**Parse**: Parse 是 Parse-SDK-JS 的核心对象，包含所有 Parse API 类和函数。

| Name            | Description                                                              | Type                                                                        | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------------------------------------ | --------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| initialize      | 初始化 Parse SDK，设置应用程序的 ID 和密钥。通常在应用程序的入口处调用。 | (applicationId: string, javaScriptKey?: string, masterKey?: string) => void | yes      | iOS/Android | yes               |
| setAsyncStorage | 设置 Parse SDK 使用的 AsyncStorage 实例，用于存储会话令牌等信息。        | (storage:AsyncStorage) => void                                              | yes      | iOS/Android | yes               |

**Parse.ACL**: 访问权限对象。

| Name                 | Description                                    | Type                                       | Required | Platform    | HarmonyOS Support |
| -------------------- | ---------------------------------------------- | ------------------------------------------ | -------- | ----------- | ----------------- |
| setPublicReadAccess  | 设置是否允许公共（未认证用户）读取对象。       | (allowed: boolean) => void                 | no       | iOS/Android | yes               |
| setPublicWriteAccess | 设置是否允许公共（未认证用户）写入对象。       | (allowed: boolean) => void                 | no       | iOS/Android | yes               |
| getPublicReadAccess  | 设置是否允许公共（未认证用户）写入对象。       | () => boolean                              | no       | iOS/Android | yes               |
| getPublicWriteAccess | 获取是否允许公共（未认证用户）写入对象的权限。 | () => boolean                              | no       | iOS/Android | yes               |
| setReadAccess        | 设置特定用户是否有读取对象的权限。             | (userId: string, allowed: boolean) => void | no       | iOS/Android | yes               |
| setWriteAccess       | 设置特定用户是否有写入对象的权限。             | (userId: string, allowed: boolean) => void | no       | iOS/Android | yes               |
| getReadAccess        | 获取特定用户是否有读取对象的权限。             | (userId: string) => boolean                | no       | iOS/Android | yes               |
| getWriteAccess       | 获取特定用户是否有写入对象的权限。             | (userId: string) => boolean                | no       | iOS/Android | yes               |

**Parse.Object**: 通常情况下，您不会直接调用此方法。建议您使用 Parse.Object 的子类，通过调用 `extend` 方法创建子类对象。

| Name             | Description                                                         | Type                                                                         | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| set              | 设置数据对象的属性值，其中 `key` 是属性名，`value` 是对应的属性值。 | (key: string\|object, value: string\|object, options: object) => ParseObject | no       | iOS/Android | yes               |
| get              | 获取数据对象的指定属性值，通过 `key` 指定属性名。                   | (attr: string) => any                                                        | no       | iOS/Android | yes               |
| unset            | 移除数据对象的指定属性值，通过 `key` 指定属性名。                   | (attr: string) => ParseObject                                                | no       | iOS/Android | yes               |
| increment        | 增加指定属性的数值类型值，`amount` 是增加的数量。                   | (attr: String, amount: Number) => ParseObject                                | no       | iOS/Android | yes               |
| add              | 添加一个值到数组类型的属性中，`value` 是要添加的值。                | (attr: string, item) => ParseObject                                          | no       | iOS/Android | yes               |
| remove           | 从数组类型的属性中移除一个值，`value` 是要移除的值。                | (attr: string, item) => ParseObject                                          | no       | iOS/Android | yes               |
| save             | 将数据对象保存到 Parse 服务器上，如果对象不存在则创建，存在则更新。 | () => Promise                                                                | no       | iOS/Android | yes               |
| fetch            | 从 Parse 服务器上获取最新的数据对象信息。                           | (options: object) => Promise                                                 | no       | iOS/Android | yes               |
| destroy          | 从 Parse 服务器上删除当前数据对象。                                 | (options: object) => Promise                                                 | no       | iOS/Android | yes               |
| fetchWithInclude | 在获取对象时，包含在查询中指定的关联对象。                          | (keys: string\|Array<string\|Array<string>>, options: object) => Promise     | no       | iOS/Android | yes               |
| saveAll          | 批量保存一组数据对象到 Parse 服务器。                               | (list: Array, options: object) => Array.<Parse.Object>                       | no       | iOS/Android | yes               |
| destroyAll       | 批量删除一组数据对象。                                              | (list: Array, options: object) => Promise                                    | no       | iOS/Android | yes               |

**Parse.Query**: Parse.Query 定义了一个用于获取 Parse.Object 的查询。

|         Name         | Description                                                                                                         | Type                                                                                                                                                    | Required | Platform    | HarmonyOS Support |
| :------------------: | ------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
|       equalTo        | 添加一个相等条件，查询字段 `key` 的值等于 `value`。                                                                 | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
|      notEqualTo      | 添加一个不等条件，查询字段 `key` 的值不等于 `value`。                                                               | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
|       lessThan       | 添加一个小于条件，查询字段 `key` 的值小于 `value`。                                                                 | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
|     greaterThan      | 添加一个大于条件，查询字段 `key` 的值大于 `value`。                                                                 | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
|  lessThanOrEqualTo   | 添加一个小于或等于条件，查询字段 `key` 的值小于或等于 `value`。                                                     | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
| greaterThanOrEqualTo | 添加一个大于或等于条件，查询字段 `key` 的值大于或等于 `value`。                                                     | (key: string, value: any) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                           | no       | iOS/Android | yes               |
|     containedIn      | 添加一个包含于条件，查询字段 `key` 的值包含在 `values` 数组中。                                                     | (key: string, value: any[]) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                         | no       | iOS/Android | yes               |
|    notContainedIn    | 添加一个不包含于条件，查询字段 `key` 的值不包含在 `values` 数组中。                                                 | (key: string, value: any[]) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                         | no       | iOS/Android | yes               |
|        exists        | 添加一个存在条件，查询字段 `key` 的值存在（非 `null` 或 `undefined`）。                                             | (key: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                       | no       | iOS/Android | yes               |
|     doesNotExist     | 添加一个不存在条件，查询字段 `key` 的值不存在（为 `null` 或 `undefined`）。                                         | (key: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                       | no       | iOS/Android | yes               |
|     containsAll      | 添加一个包含所有条件，查询字段 `key` 的值必须包含 `values` 数组中的所有元素。                                       | (key: string, value: any[]) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                         | no       | iOS/Android | yes               |
|      startsWith      | 添加一个以指定前缀开始的条件，查询字段 `key` 的值必须以 `prefix` 字符串开头。                                       | (key: string, prefix: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                       | no       | iOS/Android | yes               |
|       endsWith       | 添加一个以指定后缀结束的条件，查询字段 `key` 的值必须以 `suffix` 字符串结尾。                                       | (key: string, suffix: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                       | no       | iOS/Android | yes               |
|         near         | 添加一个接近条件，查询地理位置字段 `key` 的值接近于指定的地理坐标点 `point`。                                       | (key: string, point: Parse.GeoPoint) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                | no       | iOS/Android | yes               |
|    withinRadians     | 添加一个在指定弧度内的条件，查询地理位置字段 `key` 的值在以 `point` 为中心、半径为 `maxDistance` 的圆形范围内。     | (key: string, point: Parse.GeoPoint, maxDistance: number) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)           | no       | iOS/Android | yes               |
|     withinMiles      | 添加一个在指定英里内的条件，查询地理位置字段 `key` 的值在以 `point` 为中心、半径为 `maxDistance` 英里的圆形范围内。 | (key: string, point: Parse.GeoPoint, maxDistance: number) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)           | no       | iOS/Android | yes               |
|   withinKilometers   | 添加一个在指定公里内的条件，查询地理位置字段 `key` 的值在以 `point` 为中心、半径为 `maxDistance` 公里的圆形范围内。 | (key: string, point: Parse.GeoPoint, maxDistance: number) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)           | no       | iOS/Android | yes               |
|     withinGeoBox     | 添加一个在指定矩形区域内的条件，查询地理位置字段 `key` 的值必须在由 `southwest` 和 `northeast` 定义的矩形内。       | (key: string, southwest: Parse.GeoPoint, northeast: Parse.GeoPoint) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html) | no       | iOS/Android | yes               |
|       include        | 添加一个包含关联对象条件                                                                                            | (key: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                       | no       | iOS/Android | yes               |
|        select        | 仅返回查询结果中指定字段的信息。                                                                                    | (keys: string[]) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                    | no       | iOS/Android | yes               |
|        limit         | 限制返回结果的数量。                                                                                                | (count: number) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                     | no       | iOS/Android | yes               |
|         skip         | 跳过指定数量的查询结果。                                                                                            | (count: number) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                     | no       | iOS/Android | yes               |
|      ascending       | 按照指定字段升序排序查询结果。                                                                                      | (key: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                       | no       | iOS/Android | yes               |
|      descending      | 按照指定字段降序排序查询结果。                                                                                      | (key: string) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                                       | no       | iOS/Android | yes               |
|         find         | 按照指定字段降序排序查询结果。                                                                                      | (options?: Parse.Query.FindOptions) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                 | no       | iOS/Android | yes               |
|        first         | 执行查询并返回符合条件的第一个对象。                                                                                | (options?: Parse.Query.FindOptions) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                 | no       | iOS/Android | yes               |
|        count         | 计算符合条件的对象的数量。                                                                                          | (options?: Parse.Query.CountOptions) => [Parse.Query](https://parseplatform.org/Parse-SDK-JS/api/5.3.0/Parse.Query.html)                                | no       | iOS/Android | yes               |

**Parse.Role**: 表示 Parse 服务器上的角色对象。

| Name           | Description                     | Type                                          | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------- | --------------------------------------------- | -------- | ----------- | ----------------- |
| getName        | 获取角色的名称。                | () => String                                  | no       | iOS/Android | yes               |
| getUsers       | 获取分配给角色的用户列表。      | () => Array<Parse.User>                       | no       | iOS/Android | yes               |
| getRoles       | 获取分配给角色的子角色列表。    | () => Array<Parse.Role>                       | no       | iOS/Android | yes               |
| getRolesByName | 根据角色名称获取角色对象列表。  | (Array<String>) => Promise<Array<Parse.Role>> | no       | iOS/Android | yes               |
| save           | 将角色对象保存到 Parse 服务器。 | (obj: Object) => Promise<Array<Parse.Role>>   | no       | iOS/Android | yes               |
| destroy        | 从 Parse 服务器上删除角色对象。 | (obj: Object) => Promise<Array<Parse.Role>>   | no       | iOS/Android | yes               |

**Parse.User**: 表示 Parse 服务器上的用户对象，可进行注册、登录、登出等操作。

| Name    | Description                                               | Type                                                                         | Required | Platform    | HarmonyOS Support |
| ------- | --------------------------------------------------------- | ---------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| signUp  | 注册新用户到 Parse 服务器。                               | ({username: string, password: string, email: string}) => Promise<Parse.User> | no       | iOS/Android | yes               |
| logIn   | 注册新用户到 Parse 服务器。                               | (username: string, password: string) => Promise<Parse.User>                  | no       | iOS/Android | yes               |
| current | 获取当前已登录的用户对象，如果没有用户登录则返回 `null`。 | () => Parse.User                                                             | no       | iOS/Android | yes               |
| logOut  | 登出当前用户。                                            | () => Promise<void>                                                          | no       | iOS/Android | yes               |
| become  | 通过会话令牌 sessionToken 来认证用户。                    | (sessionToken: string) => Promise<Parse.User>                                | no       | iOS/Android | yes               |
| save    | 将用户对象保存到 Parse 服务器。                           | (user: Object) => Promise<Parse.User>                                        | no       | iOS/Android | yes               |
| destroy | 从 Parse 服务器上删除用户对象。                           | (user: Object) => Promise<void>                                              | no       | iOS/Android | yes               |

**Parse.Cloud**: 可以通过 Cloud API 执行自定义的云代码。以下是支持的主要 Cloud API 及其相关信息:

|     Name     | Description                                                                                                                                                                                      | Type                                                                                                 | Required | Platform    | HarmonyOS Support |
| :----------: | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
|     run      | 调用指定名称的云函数并获取其返回值。`functionName` 是云函数的名称，`data` 是传递给云函数的参数对象，`options` 是一个可选的配置对象，用于设置云函数调用的详细选项，如超时等。                     | (functionName: string, data?: object, options?: Parse.Cloud.HttpOptions) => Promise                  | no       | iOS/Android | yes               |
|  afterSave   | 注册一个在保存对象后触发的云函数。`className` 是对象的类名，`func` 是一个异步函数或返回 void 的函数，接收一个 `Parse.Cloud.AfterSaveRequest` 对象作为参数，可以在保存对象后执行自定义逻辑。      | (className: string, func: (request: Parse.Cloud.AfterSaveRequest) => Promise<void>\|void) => void    | no       | iOS/Android | yes               |
|  beforeSave  | 注册一个在保存对象之前触发的云函数。`className` 是对象的类名，`func` 是一个异步函数或返回 void 的函数，接收一个 `Parse.Cloud.BeforeSaveRequest` 对象作为参数，可以在保存对象前执行自定义逻辑。   | (className: string, func: (request: Parse.Cloud.BeforeSaveRequest) => Promise<void>\|void) => void   | no       | iOS/Android | yes               |
| afterDelete  | 注册一个在删除对象后触发的云函数。`className` 是对象的类名，`func` 是一个异步函数或返回 void 的函数，接收一个 `Parse.Cloud.AfterDeleteRequest` 对象作为参数，可以在删除对象后执行自定义逻辑。    | (className: string, func: (request: Parse.Cloud.AfterDeleteRequest) => Promise<void>\|void) => void  | no       | iOS/Android | yes               |
| beforeDelete | 注册一个在删除对象之前触发的云函数。`className` 是对象的类名，`func` 是一个异步函数或返回 void 的函数，接收一个 `Parse.Cloud.BeforeDeleteRequest` 对象作为参数，可以在删除对象前执行自定义逻辑。 | (className: string, func: (request: Parse.Cloud.BeforeDeleteRequest) => Promise<void>\|void) => void | no       | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The Apache License (Apache)](https://github.com/parse-community/Parse-SDK-JS/blob/alpha/LICENSE).
