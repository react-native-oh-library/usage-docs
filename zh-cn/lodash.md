> 模板版本：v0.0.1

<p align="center">
  <h1 align="center"> <code>lodash</code> </h1>
</p>
<p align="center">
    <!-- <a href="https://github.com/lodash/lodash/tree/4.17.21?tab=readme-ov-file">
       <img src="https://img.shields.io/badge/-lightgrey.svg" alt="Supported platforms" />
    </a> -->
    <a href="https://github.com/lodash/lodash/blob/4.17.21/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

## 安装与使用

#### **yarn**

```bash
yarn add lodash
```

#### **npm**
```bash
npm install lodash
```
<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
// findLastIndex 为例
import lodashStable from "lodash";

var users = [
  { 'user': 'barney',  'active': true },
  { 'user': 'fred',    'active': false },
  { 'user': 'pebbles', 'active': false }
];
 
lodashStable.findLastIndex(users, function(o) { return o.user == 'pebbles'; });
// => 2
 
// The `_.matches` iteratee shorthand.
lodashStable.findLastIndex(users, { 'user': 'barney', 'active': true });
// => 0
 
// The `_.matchesProperty` iteratee shorthand.
lodashStable.findLastIndex(users, ['active', false]);
// => 2
 
// The `_.property` iteratee shorthand.
lodashStable.findLastIndex(users, 'active');
// => 0

```
### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

## 静态方法

详情查看[lodash官方文档](https://lodash.com/docs/4.17.15)

如下是已验证接口展示:

| 名称 | 说明 | 类型 | 是否必填 | 鸿蒙支持 | 类别 |
| ---- | ---- | ---- | -------- | -------- | ---- |
| find | Iterates over elements of collection, returning the first element predicate returns truthy for | function | NO | yes | Collection |
| findLast | Iterates over elements of collection from right to left, returning the first element | function | NO | yes | Collection |
| size | Gets the size of collection | function | NO | yes | Collection |
| map | Creates an array of values by running each element in collection thru iteratee | function | NO | yes | Collection |
| includes | Checks if value is in collection. If collection is a string, it's checked for a substring of value, otherwise SameValueZero is used for equality comparisons | function | NO | yes | Collection |
| filter | Iterates over elements of collection, returning an array of all elements predicate returns truthy for | function | NO | yes | Collection |
| uniq | Creates a duplicate-free version of an array, using SameValueZero for equality comparisons, in which only the first occurrence of each element is kept | function | NO | yes | Collection |
| uniqBy | This method is like _.uniq except that it accepts iteratee which is invoked for each element in array to generate the criterion by which uniqueness is computed | function | NO | yes | Collection |
| chunk | Creates an array of elements split into groups the length of size. If array can't be split evenly, the final chunk will be the remaining elements | function | NO | yes | Collection |
| slice | Creates a slice of array from start up to, but not including, end | function | NO | yes | Collection |
| compact | Creates an array with all falsey values removed. The values false, null, 0, "", undefined, and NaN are falsey | function | NO | yes | Collection |
| findIndex | This method is like _.find except that it returns the index of the first element predicate returns truthy for instead of the element itself | function | NO | yes | Array |
| findLastIndex | This method is like _.findIndex except that it iterates over elements of collection from right to left | function | NO | yes | Array |
| head | Gets the first element of array | function | NO | yes | Array |
| flattenDeep | Recursively flattens array | function | NO | yes | Array |
| remove | emoves all elements from array that predicate returns truthy for and returns an array of the removed elements | function | NO | yes | Array |
| nth | Gets the element at index n of array. If n is negative, the nth element from the end is returned | function | NO | yes | Array |
| jion | Converts all elements in array into a string separated by separator | function | NO | yes | Array |
| camelCase | Converts string to camel case | function | NO | yes | String |
| repeat | Repeats the given string n times | function | NO | yes | String |
| truncate |  | function | NO | yes | String |
| toUpper | Converts string, as a whole, to upper case just like String#toUpperCase. | function | NO | yes | String |
| ceil | Computes number rounded up to precision | function | NO | yes | Math |
| divide | Divide two numbers. | function | NO | yes | Math |
| round | Computes number rounded to precision. | function | NO | yes | Math |
| floor | Computes number rounded down to precision | function | NO | yes | Math |
| sum | Computes the sum of the values in array | function | NO | yes | Math |
| findKey | This method is like _.find, returns the key of the first element | function | NO | yes | Object |
| findLastKey | This method is like _.findKey it iterates over elements of a collection in the opposite order | function | NO | yes | Object |
| get | Gets the value at path of object. If the resolved value is undefined, the defaultValue is returned in its place | function | NO | yes | Object |
| values | Creates an array of the own enumerable string keyed property values of object | function | NO | yes | Object |
| keys | Creates an array of the own enumerable property names of object | function | NO | yes | Object |
| merge | This method is like _.assign except that it recursively merges own and inherited enumerable string keyed properties of source objects into the destination object | function | NO | yes | Object |
| range | Creates an array of numbers (positive and/or negative) progressing from start up to, but not including, end | function | NO | yes | Util |
| toPath | Converts value to a property path array | function | NO | yes | Util |
| times | Invokes the iteratee n times, returning an array of the results of each invocation | function | NO | yes | Util |
| isEmpty | Checks if value is an empty object, collection, map, or set | function | NO | yes | Lang |
| isEqual | Performs a deep comparison between two values to determine if they are equivalent | function | NO | yes | Lang |
| isNumber | Checks if value is classified as a Number primitive or object | function | NO | yes | Lang |
| cloneDeep | This method is like _.clone except that it recursively clones value | function | NO | yes | Lang |
| isNaN | Checks if value is NaN | function | NO | yes | Lang |
| isString | Checks if value is classified as a String primitive or object | function | NO | yes | Lang |
| debounce | Creates a debounced function that delays invoking func until after wait milliseconds have elapsed since the last time the debounced function was invoked | function | NO | yes | Function |
| throttle | Creates a throttled function that only invokes func at most once per every wait milliseconds | function | NO | yes | Function |
| clamp | Clamps number within the inclusive lower and upper bounds | function | NO | yes | Number |
| random | Produces a random number between the inclusive lower and upper bounds | function | NO | yes | Number |
| inRange | Checks if n is between start and up to, but not including, end | function | NO | yes | Number |
| chain | Creates a lodash wrapper instance that wraps value with explicit method chain sequences enabled | function | NO | yes | Seq |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/lodash/lodash/blob/4.17.21/LICENSE) ，请自由地享受和参与开源。
