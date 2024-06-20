<!-- {% raw %} -->
> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>lodash</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lodash/lodash/blob/4.17.21/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/lodash/lodash/tree/4.17.21)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install lodash@4.17.21
```

#### **yarn**

```bash
yarn add lodash@^4.17.21
```

<!-- tabs:end -->

直接使用：

```js
// findLastIndex 为例
import lodashStable from "lodash";

var users = [
  { user: "barney", active: true },
  { user: "fred", active: false },
  { user: "pebbles", active: false },
];

lodashStable.findLastIndex(users, function (o) {
  return o.user == "pebbles";
});
// => 2

// The `_.matches` iteratee shorthand.
lodashStable.findLastIndex(users, { user: "barney", active: true });
// => 0

// The `_.matchesProperty` iteratee shorthand.
lodashStable.findLastIndex(users, ["active", false]);
// => 2

// The `_.property` iteratee shorthand.
lodashStable.findLastIndex(users, "active");
// => 0
```

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## 静态方法

详情查看[lodash 官方文档](https://lodash.com/docs/4.17.15)

如下是已验证接口展示:

#### **Collection**

| Name     | Description                                                                                                                                                      | Type     | Required | HarmonyOS Support |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| find     | Iterates over elements of collection, returning the first element predicate returns truthy for                                                                   | function | NO       | yes               |
| findLast | Iterates over elements of collection from right to left, returning the first element                                                                             | function | NO       | yes               |
| size     | Gets the size of collection                                                                                                                                      | function | NO       | yes               |
| map      | Creates an array of values by running each element in collection thru iteratee                                                                                   | function | NO       | yes               |
| includes | Checks if value is in collection. If collection is a string, it's checked for a substring of value, otherwise SameValueZero is used for equality comparisons     | function | NO       | yes               |
| filter   | Iterates over elements of collection, returning an array of all elements predicate returns truthy for                                                            | function | NO       | yes               |
| uniq     | Creates a duplicate-free version of an array, using SameValueZero for equality comparisons, in which only the first occurrence of each element is kept           | function | NO       | yes               |
| uniqBy   | This method is like \_.uniq except that it accepts iteratee which is invoked for each element in array to generate the criterion by which uniqueness is computed | function | NO       | yes               |
| chunk    | Creates an array of elements split into groups the length of size. If array can't be split evenly, the final chunk will be the remaining elements                | function | NO       | yes               |
| slice    | Creates a slice of array from start up to, but not including, end                                                                                                | function | NO       | yes               |
| compact  | Creates an array with all falsey values removed. The values false, null, 0, "", undefined, and NaN are falsey                                                    | function | NO       | yes               |

#### **Array**

| Name          | Description                                                                                                                                  | Type     | Required | HarmonyOS Support |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| findIndex     | This method is like \_.find except that it returns the index of the first element predicate returns truthy for instead of the element itself | function | NO       | yes               |
| findLastIndex | This method is like \_.findIndex except that it iterates over elements of collection from right to left                                      | function | NO       | yes               |
| head          | Gets the first element of array                                                                                                              | function | NO       | yes               |
| flattenDeep   | Recursively flattens array                                                                                                                   | function | NO       | yes               |
| remove        | emoves all elements from array that predicate returns truthy for and returns an array of the removed elements                                | function | NO       | yes               |
| nth           | Gets the element at index n of array. If n is negative, the nth element from the end is returned                                             | function | NO       | yes               |
| jion          | Converts all elements in array into a string separated by separator                                                                          | function | NO       | yes               |

#### **String**

| Name      | Description                                                              | Type     | Required | HarmonyOS Support |
| --------- | ------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| camelCase | Converts string to camel case                                            | function | NO       | yes               |
| repeat    | Repeats the given string n times                                         | function | NO       | yes               |
| truncate  | Truncates string if it's longer than the given maximum string length     | function | NO       | yes               |
| toUpper   | Converts string, as a whole, to upper case just like String#toUpperCase. | function | NO       | yes               |

#### **Math**

| Name   | Description                               | Type     | Required | HarmonyOS Support |
| ------ | ----------------------------------------- | -------- | -------- | ----------------- |
| ceil   | Computes number rounded up to precision   | function | NO       | yes               |
| divide | Divide two numbers.                       | function | NO       | yes               |
| round  | Computes number rounded to precision.     | function | NO       | yes               |
| floor  | Computes number rounded down to precision | function | NO       | yes               |
| sum    | Computes the sum of the values in array   | function | NO       | yes               |

#### **Object**

| Name        | Description                                                                                                                                                        | Type     | Required | HarmonyOS Support |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| findKey     | This method is like \_.find, returns the key of the first element                                                                                                  | function | NO       | yes               |
| findLastKey | This method is like \_.findKey it iterates over elements of a collection in the opposite order                                                                     | function | NO       | yes               |
| get         | Gets the value at path of object. If the resolved value is undefined, the defaultValue is returned in its place                                                    | function | NO       | yes               |
| values      | Creates an array of the own enumerable string keyed property values of object                                                                                      | function | NO       | yes               |
| keys        | Creates an array of the own enumerable property names of object                                                                                                    | function | NO       | yes               |
| merge       | This method is like \_.assign except that it recursively merges own and inherited enumerable string keyed properties of source objects into the destination object | function | NO       | yes               |

#### **Util**

| Name   | Description                                                                                                 | Type     | Required | HarmonyOS Support |
| ------ | ----------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| range  | Creates an array of numbers (positive and/or negative) progressing from start up to, but not including, end | function | NO       | yes               |
| toPath | Converts value to a property path array                                                                     | function | NO       | yes               |
| times  | Invokes the iteratee n times, returning an array of the results of each invocation                          | function | NO       | yes               |

#### **Lang**

| Name      | Description                                                                       | Type     | Required | HarmonyOS Support |
| --------- | --------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| isEmpty   | Checks if value is an empty object, collection, map, or set                       | function | NO       | yes               |
| isEqual   | Performs a deep comparison between two values to determine if they are equivalent | function | NO       | yes               |
| isNumber  | Checks if value is classified as a Number primitive or object                     | function | NO       | yes               |
| cloneDeep | This method is like \_.clone except that it recursively clones value              | function | NO       | yes               |
| isNaN     | Checks if value is NaN                                                            | function | NO       | yes               |
| isString  | Checks if value is classified as a String primitive or object                     | function | NO       | yes               |

#### **Function**

| Name     | Description                                                                                                                                              | Type     | Required | HarmonyOS Support |
| -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| debounce | Creates a debounced function that delays invoking func until after wait milliseconds have elapsed since the last time the debounced function was invoked | function | NO       | yes               |
| throttle | Creates a throttled function that only invokes func at most once per every wait milliseconds                                                             | function | NO       | yes               |

#### **Number**

| Name    | Description                                                           | Type     | Required | HarmonyOS Support |
| ------- | --------------------------------------------------------------------- | -------- | -------- | ----------------- |
| clamp   | Clamps number within the inclusive lower and upper bounds             | function | NO       | yes               |
| random  | Produces a random number between the inclusive lower and upper bounds | function | NO       | yes               |
| inRange | Checks if n is between start and up to, but not including, end        | function | NO       | yes               |

#### **Seq**

| Name  | Description                                                                                     | Type     | Required | HarmonyOS Support |
| ----- | ----------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| chain | Creates a lodash wrapper instance that wraps value with explicit method chain sequences enabled | function | NO       | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/lodash/lodash/blob/4.17.21/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->