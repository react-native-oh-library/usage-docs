> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>Moment</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/moment/moment/blob/develop/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/moment/moment)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install moment@2.30.1
```

#### **yarn**

```bash
yarn add moment@2.30.1
```

<!-- tabs:end -->

quick use：

```bash
import moment from 'moment';
moment().format();
```

Set the moment area:

```bash
// Import method
import 'moment/locale/zh-cn';
moment.locale('zh-cn');
```

## Constraints

## Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## API

详情请查看[moment官方文档](https://momentjs.com/docs/#/use-it/)

以下moment为moment.js导出的对象，即：

```bash
import moment from 'moment';
```

The following code shows the basic use scenario of the repository:

```js
// 获取今天0时0分0秒
moment().startOf("day");
// 获取当前月第一天0时0分0秒
moment().startOf("month");
// 获取当前月的总天数
moment().daysInMonth();
// 获取时间戳(以秒为单位)
moment().format("X"); // 返回值为字符串类型
moment().unix(); // 返回值为数值型
// 获取时间戳(以毫秒为单位)
moment().format("x"); // 返回值为字符串类型
moment().valueOf(); // 返回值为数值型
// 获取年份
moment().year();
moment().get("year");
// 获取月份
moment().month(); // (0~11, 0: January, 11: December)
moment().get("month");
// 获取一个星期中的某一天
moment().date();
moment().get("date");
// 获取小时
moment().hours();
moment().get("hours");
// 获取分钟
moment().minutes();
moment().get("minutes");
// 获取当前的年月日时分秒
moment().toArray(); // [years, months, date, hours, minutes, seconds, milliseconds]
moment().toObject(); // {years: xxxx, months: x, date: xx ...}

// 设置年份
moment().year(2019);
moment().set("year", 2019);
moment().set({ year: 2019 });
// 设置月份
moment().month(11); // (0~11, 0: January, 11: December)
moment().set("month", 11);
// 设置某个月中的某一天
moment().date(15);
moment().set("date", 15);
// 设置某个星期中的某一天
moment().weekday(0); // 设置日期为本周第一天（周日）
moment().isoWeekday(1); // 设置日期为本周周一
moment().set("weekday", 0);
moment().set("isoWeekday", 1);
// 设置小时
moment().hours(12);
moment().set("hours", 12);
// 年份+1
moment().add(1, "years");
moment().add({ years: 1 });

// 获取两个日期之间的时间差
let start_date = moment().subtract(1, "weeks");
let end_date = moment();
end_date.diff(start_date); // 返回毫秒数
end_date.diff(start_date, "months"); // 0
end_date.diff(start_date, "weeks"); // 1
end_date.diff(start_date, "days"); // 7
start_date.diff(end_date, "days"); // -7
// 转化为JavaScript原生Date对象
moment().toDate();
new Date(moment());

// 格式化年月日： 'xxxx年xx月xx日'
moment().format("YYYY年MM月DD日");
// 格式化年月日： 'xxxx-xx-xx'
moment().format("YYYY-MM-DD");
// 格式化时分秒(24小时制)： 'xx时xx分xx秒'
moment().format("HH时mm分ss秒");
// 格式化时分秒(12小时制)：'xx:xx:xx am/pm'
moment().format("hh:mm:ss a");
```

如下是已验证接口展示:

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### **Get + Set**

| Name          | Description                                                                                                                                                                                                                                                                                 | Type     | Required | HarmonyOS Support |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| millisecond   | Gets or sets the milliseconds.                                                                                                                                                                                                                                                              | function | no       | yes               |
| second        | Gets or sets the seconds.                                                                                                                                                                                                                                                                   | function | no       | yes               |
| minute        | Gets or sets the minutes.                                                                                                                                                                                                                                                                   | function | no       | yes               |
| hour          | Gets or sets the hour.                                                                                                                                                                                                                                                                      | function | no       | yes               |
| date          | Gets or sets the day of the month                                                                                                                                                                                                                                                           | function | no       | yes               |
| day           | Gets or sets the day of the week.                                                                                                                                                                                                                                                           | function | no       | yes               |
| weekday       | Gets or sets the day of the week according to the locale.                                                                                                                                                                                                                                   | function | no       | yes               |
| isoWeekday    | Gets or sets the ISO day of the week with 1 being Monday and 7 being Sunday.                                                                                                                                                                                                                | function | no       | yes               |
| dayOfYear     | Gets or sets the day of the year.                                                                                                                                                                                                                                                           | function | no       | yes               |
| week          | Gets or sets the week of the year.                                                                                                                                                                                                                                                          | function | no       | yes               |
| isoWeek       | Gets or sets the ISO week of the year.                                                                                                                                                                                                                                                      | function | no       | yes               |
| month         | Gets or sets the month.                                                                                                                                                                                                                                                                     | function | no       | yes               |
| quarter       | Gets the quarter (1 to 4).                                                                                                                                                                                                                                                                  | function | no       | yes               |
| year          | Gets or sets the year.                                                                                                                                                                                                                                                                      | function | no       | yes               |
| weekYear      | Gets or sets the week-year according to the locale.                                                                                                                                                                                                                                         | function | no       | yes               |
| isoWeekYear   | Gets or sets the ISO week-year.                                                                                                                                                                                                                                                             | function | no       | yes               |
| weeksInYear   | Gets the number of weeks according to locale in the current moment's year.                                                                                                                                                                                                                  | function | no       | yes               |
| isoWeeksInYea | Gets the number of weeks in the current moment's year, according to ISO weeks.                                                                                                                                                                                                              | function | no       | yes               |
| get           | String getter. In general <br> Units are case insensitive, and support plural and short forms: year (years, y), month (months, M), date (dates, D), hour (hours, h), minute (minutes, m), second (seconds, s), millisecond (milliseconds, ms).                                              | function | no       | yes               |
| set           | Generic setter, accepting unit as first argument, and value as second: <br> Units are case insensitive, and support plural and short forms: year (years, y), month (months, M), date (dates, D), hour (hours, h), minute (minutes, m), second (seconds, s), millisecond (milliseconds, ms). | function | no       | yes               |

#### **Manipulate**

| Name      | Description                                                                                                     | Type     | Required | HarmonyOS Support |
| --------- | --------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| add       | Mutates the original moment by adding time.                                                                     | function | no       | yes               |
| subtract  | Mutates the original moment by subtracting time.                                                                | function | no       | yes               |
| startOf   | Mutates the original moment by setting it to the start of a unit of time.                                       | function | no       | yes               |
| endOf     | Mutates the original moment by setting it to the end of a unit of time.                                         | function | no       | yes               |
| local     | Sets a flag on the original moment to use local time to display a moment instead of the original moment's time. | function | no       | yes               |
| utc       | Sets a flag on the original moment to use UTC to display a moment instead of the original moment's time.        | function | no       | yes               |
| utcOffset | Get or set the UTC offset in minutes.                                                                           | function | no       | yes               |

#### **Display**

| Name        | Description                                                                                                                                                           | Type     | Required | HarmonyOS Support |
| ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| format      | This is the most robust display option. It takes a string of tokens and replaces them with their corresponding values.                                                | function | no       | yes               |
| fromNow     | A common way of displaying time is handled by moment#fromNow. This is sometimes called timeago or relative time.                                                      | function | no       | yes               |
| from        | You may want to display a moment in relation to a time other than now. In that case, you can use moment#from.                                                         | function | no       | yes               |
| toNow       | A common way of displaying time is handled by moment#toNow. This is sometimes called timeago or relative time.                                                        | function | no       | yes               |
| to          | You may want to display a moment in relation to a time other than now. In that case, you can use moment#to.                                                           | function | no       | yes               |
| calendar    | Calendar time displays time relative to a given referenceDay (defaults to the start of today), but does so slightly differently than moment#fromNow.                  | function | no       | yes               |
| diff        | To get the difference in milliseconds, use moment#diff like you would use moment#from.                                                                                | function | no       | yes               |
| valueOf     | moment#valueOf simply outputs the number of milliseconds since the Unix Epoch, just like Date#valueOf.                                                                | function | no       | yes               |
| unix        | moment#unix outputs a Unix timestamp (the number of seconds since the Unix Epoch).                                                                                    | function | no       | yes               |
| daysInMonth | Get the number of days in the current month.                                                                                                                          | function | no       | yes               |
| toDate      | To get a copy of the native Date object that Moment.js wraps, use moment#toDate.                                                                                      | function | no       | yes               |
| toArray     | This returns an array that mirrors the parameters from new Date().                                                                                                    | function | no       | yes               |
| toJSON      | When serializing an object to JSON, if there is a Moment object, it will be represented as an ISO8601 string, adjusted to UTC.                                        | function | no       | yes               |
| toISOString | Formats a string to the ISO8601 standard.                                                                                                                             | function | no       | yes               |
| toObject    | This returns an object containing year, month, day-of-month, hour, minute, seconds, milliseconds.                                                                     | function | no       | yes               |
| toString    | Returns an english string in a similar format to JS Date's .toString().                                                                                               | function | no       | yes               |
| inspect     | Returns a machine readable string, that can be evaluated to produce the same moment. Because of the name it's also used in node interactive shell to display objects. | function | no       | yes               |

#### **Query**

| Name           | Description                                                                                                                  | Type     | Required | HarmonyOS Support |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| isBefore       | Check if a moment is before another moment. The first argument will be parsed as a moment, if not already so.                | function | no       | yes               |
| isSame         | Check if a moment is the same as another moment. The first argument will be parsed as a moment, if not already so.           | function | no       | yes               |
| isAfter        | Check if a moment is after another moment. The first argument will be parsed as a moment, if not already so.                 | function | no       | yes               |
| isSameOrBefore | Check if a moment is before or the same as another moment. The first argument will be parsed as a moment, if not already so. | function | no       | yes               |
| isSameOrAfter  | Check if a moment is after or the same as another moment. The first argument will be parsed as a moment, if not already so.  | function | no       | yes               |
| isBetween      | Check if a moment is between two other moments, optionally looking at unit scale (minutes, hours, days, etc).                | function | no       | yes               |
| isDST          | moment#isDST checks if the current moment is in daylight saving time.                                                        | function | no       | yes               |
| isLeapYear     | moment#isLeapYear returns true if that year is a leap year, and false if it is not.                                          | function | no       | yes               |
| isMoment       | To check if a variable is a moment object, use moment.isMoment().                                                            | function | no       | yes               |
| isDate         | To check if a variable is a native js Date object, use moment.isDate().                                                      | function | no       | yes               |

#### **Durations**

| Name     | Description                                                                           | Type     | Required | HarmonyOS Support |
| -------- | ------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| duration | To create a duration, call moment.duration() with the length of time in milliseconds. | function | no       | yes               |

#### **格式化时间**

| **格式代码** | **说明**                   | **返回值例子**             |
| ------------ | -------------------------- | -------------------------- |
| M            | 数字表示的月份，没有前导零 | 1到12                      |
| MM           | 数字表示的月份，有前导零   | 01到12                     |
| MMM          | 三个字母缩写表示的月份     | Jan到Dec                   |
| MMMM         | 月份，完整的文本格式       | January到December          |
| Q            | 季度                       | 1到4                       |
| D            | 月份中的第几天，没有前导零 | 1到31                      |
| DD           | 月份中的第几天，有前导零   | 01到31                     |
| d            | 星期中的第几天，数字表示   | 0到6，0表示周日，6表示周六 |
| ddd          | 三个字母表示星期中的第几天 | Sun到Sat                   |
| dddd         | 星期几，完整的星期文本     | 从Sunday到Saturday         |
| w            | 年份中的第几周             | 如42：表示第42周           |
| YYYY         | 四位数字完整表示的年份     | 如：2014 或 2000           |
| YY           | 两位数字表示的年份         | 如：14 或 98               |
| A            | 大写的AM PM                | AM PM                      |
| a            | 小写的am pm                | am pm                      |
| HH           | 小时，24小时制，有前导零   | 00到23                     |
| H            | 小时，24小时制，无前导零   | 0到23                      |
| hh           | 小时，12小时制，有前导零   | 00到12                     |
| h            | 小时，12小时制，无前导零   | 0到12                      |
| m            | 没有前导零的分钟数         | 0到59                      |
| mm           | 有前导零的分钟数           | 00到59                     |
| s            | 没有前导零的秒数           | 1到59                      |
| ss           | 有前导零的描述             | 01到59                     |
| X            | Unix时间戳                 | 1411572969                 |

## Others

## License
