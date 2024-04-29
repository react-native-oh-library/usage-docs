> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>DayJs</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/iamkun/dayjs?tab=readme-ov-file">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/iamkun/dayjs?tab=readme-ov-file)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install dayjs --save
```

#### **yarn**

```bash
yarn add dayjs --save
```

<!-- tabs:end -->

快速使用：

```bash
import dayjs from 'dayjs'

dayjs().format()
```

## 约束与限制

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

## API

详情请查看[DayJs官方文档](https://dayjs.gitee.io/zh-CN/)

以下dayjs为day.js导出的对象，即：

```bash
import dayjs from 'dayjs';
```

下面的代码展示了这个库的基本使用示例：

```tsx
import React, { useState, useEffect, useRef } from "react";
import { View, Text, Button, StyleSheet } from "react-native";
import dayjs from "dayjs";
import duration from "dayjs/plugin/duration";

const DayJsDemo = () => {
  dayjs.extend(duration);

  return (
    <View style={styles.container}>
      <Text style={styles.componentTitle}>ValueAssignmentDemo: 取值/赋值</Text>
      <Text style={styles.textCommon}>
        获取或设置毫秒：{dayjs().millisecond()}
      </Text>
      <Text style={styles.textCommon}>获取或设置秒：{dayjs().second()}</Text>
      <Text style={styles.textCommon}>获取或设置分钟：{dayjs().minute()}</Text>
      <Text style={styles.textCommon}>获取或设置小时：{dayjs().hour()}</Text>
      <Text style={styles.textCommon}>
        获取或设置月份里的日期：{dayjs().date()}
      </Text>
      <Text style={styles.textCommon}>获取或设置星期几：{dayjs().day()}</Text>
      <Text style={styles.textCommon}>获取或设置月份：{dayjs().month()}</Text>
      <Text style={styles.textCommon}>获取或设置年份。：{dayjs().year()}</Text>
      <Text style={styles.textCommon}>
        从Dayjs对象中获取相应信息的 getter：年{dayjs().get("year")} 月
        {dayjs().get("month")}
      </Text>
      <Text style={styles.textCommon}>
        格式化{dayjs().format("YYYY-MM-DD")}
      </Text>
      <Text style={styles.textCommon}>时长{dayjs.duration(100)}</Text>
      <Text style={styles.textCommon}>
        时间比较{dayjs().isSame("2011-01-01", "year") ? "相等" : "不相等"}
      </Text>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
    paddingTop: 50,
    padding: 8,
  },
  navigationContainer: {
    flex: 1,
    paddingTop: 50,
    padding: 8,
  },
  textCommon: {
    marginBottom: 10,
    fontSize: 15,
    alignItems: "center",
    justifyContent: "center",
  },
  interval: {
    marginBottom: 10,
  },
  viewBox: {
    width: "100%",
    borderWidth: 1,
    marginBottom: 2,
    padding: 5,
  },
  viewButtonBox: {
    width: "100%",
    flexDirection: "row",
    alignItems: "center",
    marginBottom: 10,
  },
  formatLabel: {
    marginRight: 2,
    fontSize: 16,
    fontWeight: "700",
  },
  flexRowCenter: {
    flexDirection: "row",
    alignItems: "center",
    justifyContent: "center",
  },
  flexColCenter: {
    alignItems: "center",
    justifyContent: "center",
  },
  headerTitle: {
    fontSize: 18,
    fontWeight: "700",
  },
  componentTitle: {
    fontSize: 25,
    fontWeight: "700",
    marginBottom: 20,
  },
  inputStyle: {
    width: 200,
    height: 40,
    borderWidth: 1,
    borderRadius: 10,
  },
});
export default DayJsDemo;
```

如下是已验证接口展示:

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### **Get + Set**

| Name           | Description                                                                                                                                                                            | Type     | Required | HarmonyOS Support | note                                              |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- | ------------------------------------------------- |
| millisecond    | Gets or sets the milliseconds.                                                                                                                                                         | function | no       | yes               |                                                   |
| second         | Gets or sets the seconds.                                                                                                                                                              | function | no       | yes               |                                                   |
| minute         | Gets or sets the minutes.                                                                                                                                                              | function | no       | yes               |                                                   |
| hour           | Gets or sets the hour.                                                                                                                                                                 | function | no       | yes               |                                                   |
| date           | Gets or sets the day of the month                                                                                                                                                      | function | no       | yes               |                                                   |
| day            | Gets or sets the day of the week.                                                                                                                                                      | function | no       | yes               |                                                   |
| weekday        | Gets or sets the day of the week according to the locale.                                                                                                                              | function | no       | yes               | This requires the `Weekday` plugin to work        |
| isoWeekday     | Gets or sets the ISO day of the week with 1 being Monday and 7 being Sunday.                                                                                                           | function | no       | yes               | This requires the `IsoWeek` plugin to work        |
| dayOfYear      | Gets or sets the day of the year.                                                                                                                                                      | function | no       | yes               | This requires the `DayOfYear` plugin to work      |
| week           | Gets or sets the week of the year.                                                                                                                                                     | function | no       | yes               | This requires the `WeekOfYear` plugin to work     |
| isoWeek        | Gets or sets the ISO week of the year.                                                                                                                                                 | function | no       | yes               | This requires the `IsoWeek` plugin to work        |
| month          | Gets or sets the month.                                                                                                                                                                | function | no       | yes               |                                                   |
| quarter        | Gets or sets the quarter.                                                                                                                                                              | function | no       | yes               | This requires the `QuarterOfYear` plugin to work  |
| year           | Gets or sets the year.                                                                                                                                                                 | function | no       | yes               |                                                   |
| weekYear       | Gets the week-year according to the locale.                                                                                                                                            | function | no       | yes               | This requires the `WeekYear` plugin to work       |
| isoWeekYear    | Gets the ISO week-year.                                                                                                                                                                | function | no       | yes               | This requires the `IsoWeek` plugin to work        |
| isoWeeksInYear | Gets the number of weeks in the current year, according to ISO weeks.                                                                                                                  | function | no       | yes               | This requires the `IsoWeeksInYear` plugin to work |
| get            | String getter, returns the corresponding information getting from Day.js object. Units are case insensitive, and support plural and short forms. Note, short forms are case sensitive. | function | no       | yes               |                                                   |
| set            | Generic setter, accepting unit as first argument, and value as second, returns a new instance with the applied changes.                                                                | function | no       | yes               |                                                   |

#### **Manipulate**

| Name      | Description                                                                | Type     | Required | HarmonyOS Support | note                                   |
| --------- | -------------------------------------------------------------------------- | -------- | -------- | ----------------- | -------------------------------------- |
| add       | Returns a cloned Day.js object with a specified amount of time added.      | function | no       | yes               |                                        |
| subtract  | Returns a cloned Day.js object with a specified amount of time subtracted. | function | no       | yes               |                                        |
| startOf   | Returns a cloned Day.js object and set it to the start of a unit of time.  | function | no       | yes               |                                        |
| endOf     | Returns a cloned Day.js object and set it to the end of a unit of time.    | function | no       | yes               |                                        |
| local     | This returns a Day.js object with a flag to use local time.                | function | no       | yes               | This requires the `UTC` plugin to work |
| utc       | This returns a Day.js object with a flag to use UTC time.                  | function | no       | yes               | This requires the `UTC` plugin to work |
| utcOffset | Get the UTC offset in minutes.                                             | function | no       | yes               | This requires the `UTC` plugin to work |

#### **Display**

| Name        | Description                                                                                                                                                                                                                         | Type     | Required | HarmonyOS Support | note                                            |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- | ----------------------------------------------- |
| format      | Get the formatted date according to the string of tokens passed in.                                                                                                                                                                 | function | no       | yes               |                                                 |
| fromNow     | Returns the string of relative time from now.If you pass true, you can get the value without the suffix.                                                                                                                            | function | no       | yes               | This requires the `RelativeTime` plugin to work |
| from        | Returns the string of relative time from X.If you pass true, you can get the value without the suffix.                                                                                                                              | function | no       | yes               | This requires the `RelativeTime` plugin to work |
| toNow       | Returns the string of relative time to now.If you pass true, you can get the value without the suffix.                                                                                                                              | function | no       | yes               | This requires the `RelativeTime` plugin to work |
| to          | Returns the string of relative time to X.If you pass true, you can get the value without the suffix.                                                                                                                                | function | no       | yes               | This requires the `RelativeTime` plugin to work |
| calendar    | Calendar time displays time relative to a given reference time (defaults to now) but does so slightly differently than dayjs#fromNow.                                                                                               | function | no       | yes               | This requires the `Calendar` plugin to work     |
| diff        | This indicates the difference between two date-time in the specified unit.To get the difference in milliseconds, use dayjs#diff.To get the difference in another unit of measurement, pass that measurement as the second argument. | function | no       | yes               |                                                 |
| valueOf     | This returns the number of milliseconds since the Unix Epoch of the Day.js object.                                                                                                                                                  | function | no       | yes               |                                                 |
| unix        | This returns the Unix timestamp (the number of seconds since the Unix Epoch) of the Day.js object.                                                                                                                                  | function | no       | yes               |                                                 |
| daysInMonth | Get the number of days in the current month.                                                                                                                                                                                        | function | no       | yes               |                                                 |
| toDate      | To get a copy of the native Date object parsed from the Day.js object use dayjs#toDate.                                                                                                                                             | function | no       | yes               |                                                 |
| toArray     | Returns an array that mirrors the parameters                                                                                                                                                                                        | function | no       | yes               | This requires the `ToArray` plugin to work      |
| toJSON      | To serialize as an ISO 8601 string.                                                                                                                                                                                                 | function | no       | yes               |                                                 |
| toISOString | To format as an ISO 8601 string.                                                                                                                                                                                                    | function | no       | yes               |                                                 |
| toObject    | Returns an object with the date's properties.                                                                                                                                                                                       | function | no       | yes               | This requires the `ToObject` plugin to work     |
| toString    | Returns a string representation of the date.                                                                                                                                                                                        | function | no       | yes               |                                                 |

#### **Query**

| Name           | Description                                                                                                                                                                                                                                                        | Type     | Required | HarmonyOS Support | note                                              |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------------- | ------------------------------------------------- |
| isBefore       | This indicates whether the Day.js object is before the other supplied date-time.If you want to limit the granularity to a unit other than milliseconds, pass it as the second parameter. In that case, the comparison respects the given unit and the units above. | function | no       | yes               |                                                   |
| isSame         | This indicates whether the Day.js object is the same as the other supplied date-time.If you want to limit the granularity to a unit other than milliseconds, pass it as the second parameter.                                                                      | function | no       | yes               |                                                   |
| isAfter        | This indicates whether the Day.js object is after the other supplied date-time.If you want to limit the granularity to a unit other than milliseconds, pass it as the second parameter. In that case the comparision respects the given unit and the units above.  | function | no       | yes               |                                                   |
| isSameOrBefore | This indicates whether the Day.js object is the same or before another supplied date-time.If you want to limit the granularity to a unit other than milliseconds, pass it as the second parameter.                                                                 | function | no       | yes               | This requires the `IsSameOrBefore` plugin to work |
| isSameOrAfter  | This indicates whether the Day.js object is the same or after another supplied date-time.If you want to limit the granularity to a unit other than milliseconds, pass it as the second parameter.                                                                  | function | no       | yes               | This requires the `IsSameOrAfter` plugin to work  |
| isBetween      | This indicates whether the Day.js object is between two other supplied date-time.If you want to limit the granularity to a unit other than milliseconds, pass it as the third parameter. In that case the comparision respects the given unit and the units above. | function | no       | yes               | This requires the `IsBetween` plugin to work      |
| isDayjs        | This indicates whether a variable is a Day.js object or not.                                                                                                                                                                                                       | function | no       | yes               |                                                   |
| isLeapYear     | This indicates whether the Day.js object's year is a leap year or not.                                                                                                                                                                                             | function | no       | yes               | This requires the `IsLeapYear` plugin to work     |

#### **Durations**

| Name     | Description                                                                          | Type     | Required | HarmonyOS Support | note                                        |
| -------- | ------------------------------------------------------------------------------------ | -------- | -------- | ----------------- | ------------------------------------------- |
| duration | To create a duration, call dayjs.duration() with the length of time in milliseconds. | function | no       | yes               | This requires the `Duration` plugin to work |

#### **Plugins**

加载插件：

```bash
import duration from 'dayjs/plugin/duration'

dayjs.extend(duration)
```

| Name              | Description                                                                                                                                                                                                                     | Required | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ----------------- |
| advancedFormat    | AdvancedFormat extends dayjs().format API to supply more format options.                                                                                                                                                        | no       | yes               |
| arraySupport      | ArraySupport extends dayjs(), dayjs.utc APIs to support array argument.                                                                                                                                                         | no       | yes               |
| bigIntSupport     | BigIntSupport extends dayjs(), dayjs.unix APIs to support BigInt argument.                                                                                                                                                      | no       | yes               |
| buddhistEra       | BuddhistEra extends dayjs().format API to supply Buddhist Era (B.E.) format options.                                                                                                                                            | no       | yes               |
| calendar          | Calendar adds .calendar API to return a string to display calendar time                                                                                                                                                         | no       | yes               |
| customParseFormat | CustomParseFormat extends dayjs() constructor to support custom formats of input strings.                                                                                                                                       | no       | yes               |
| dayOfYear         | DayOfYear adds .dayOfYear() API to returns a number indicating the Dayjs's day of the year, or to set the day of the year.                                                                                                      | no       | yes               |
| devHelper         | DevHelper adds some helper function to give you more hints and warnings while using Day.js.                                                                                                                                     | no       | yes               |
| duration          | Duration adds .duration .isDuration APIs to support duration.                                                                                                                                                                   | no       | yes               |
| isBetween         | IsBetween adds .isBetween() API to returns a boolean indicating if a date is between two other dates.                                                                                                                           | no       | yes               |
| isLeapYear        | IsLeapYear adds .isLeapYear API to returns a boolean indicating whether the Dayjs's year is a leap year or not.                                                                                                                 | no       | yes               |
| isSameOrAfter     | IsSameOrAfter adds .isSameOrAfter() API to return a boolean indicating if a date is the same or after another date.                                                                                                             | no       | yes               |
| isSameOrBefore    | IsSameOrBefore adds .isSameOrBefore() API to returns a boolean indicating if a date is same or before another date.                                                                                                             | no       | yes               |
| isToday           | IsToday adds .isToday() API to indicates whether the Day.js object is today or not.                                                                                                                                             | no       | yes               |
| isTomorrow        | IsTomorrow adds .isTomorrow() API to indicates whether the Day.js object is tomorrow or not.                                                                                                                                    | no       | yes               |
| isYesterday       | IsYesterday adds .isYesterday() API to indicates whether the Day.js object is yesterday or not.                                                                                                                                 | no       | yes               |
| isoWeek           | IsoWeek adds .isoWeek() API to get or set the ISO week of the year. And adds .isoWeekday() to get or set ISO day of the week and .isoWeekYear() to get ISO week-year, and extends .startOf .endOf APIs to support unit isoWeek. | no       | yes               |
| isoWeeksInYear    | IsoWeeksInYear adds .isoWeeksInYear() API to return a number to get the number of weeks in year, according to ISO weeks.                                                                                                        | no       | yes               |
| localeData        | LocaleData extends dayjs().localeData API to supply locale data.                                                                                                                                                                | no       | yes               |
| localizedFormat   | LocalizedFormat extends dayjs().format API to supply localized format options.                                                                                                                                                  | no       | yes               |
| minMax            | MinMax adds .min .max APIs to return a dayjs to compare given dayjs instances. This accepts both multiple arguments and array that contains Day.js instance.                                                                    | no       | yes               |
| objectSupport     | ObjectSupport extends dayjs(), dayjs.utc, dayjs().set, dayjs().add, dayjs().subtract APIs to support object argument.                                                                                                           | no       | yes               |
| pluralGetSet      | PluralGetSet adds plural getter & setter APIs .milliseconds(), .seconds(), .minutes(), .hours(), .days(), .weeks(), .isoWeeks(), .months(), .quarters(), .years(), .dates().                                                    | no       | yes               |
| quarterOfYear     | QuarterOfYear adds .quarter() API to return to which quarter of the year belongs a date, and extends .add .subtract .startOf .endOf APIs to support unit quarter.                                                               | no       | yes               |
| relativeTime      | RelativeTime adds .from .to .fromNow .toNow APIs to formats date to relative time strings (e.g. 3 hours ago).                                                                                                                   | no       | yes               |
| timezone          | Timezone adds dayjs.tz .tz .tz.guess .tz.setDefault APIs to parse or display between time zones.                                                                                                                                | no       | yes               |
| toArray           | ToArray adds .toArray() API to return an array that mirrors the parameters                                                                                                                                                      | no       | yes               |
| toObject          | ToObject adds .toObject() API to return an object with the date's properties.                                                                                                                                                   | no       | yes               |
| updateLocale      | UpdateLocale adds .updateLocale API to update a locale's properties.                                                                                                                                                            | no       | yes               |
| utc               | UTC adds .utc .local .isUTC APIs to parse or display in UTC.                                                                                                                                                                    | no       | yes               |
| weekOfYear        | WeekOfYear adds .week() API to returns a number indicating the Dayjs's week of the year.                                                                                                                                        | no       | yes               |
| weekYear          | WeekYear adds .weekYear() API to get locale aware week of the year.                                                                                                                                                             | no       | yes               |
| weekday           | Weekday adds .weekday() API to get or set locale aware day of the week.                                                                                                                                                         | no       | yes               |

#### **格式化时间**

| **Format** | **Description**                                           | **Output**            |
| ---------- | --------------------------------------------------------- | --------------------- |
| YY         | Two-digit year                                            | 18                    |
| YYYY       | Four-digit year                                           | 2018                  |
| M          | The month, beginning at 1                                 | 1-12                  |
| MM         | The month, 2-digits                                       | 01-12                 |
| MMM        | The abbreviated month name                                | Jan-Dec               |
| MMMM       | The full month name                                       | January-December      |
| D          | The day of the month                                      | 1-31                  |
| DD         | The day of the month, 2-digits                            | 01-31                 |
| d          | The day of the week, with Sunday as 0                     | 0-6                   |
| dd         | The min name of the day of the week                       | Su-Sa                 |
| ddd        | The short name of the day of the week                     | Sun-Sat               |
| dddd       | The name of the day of the week                           | Sunday-Saturday       |
| H          | The hour                                                  | 0-23                  |
| HH         | The hour, 2-digits                                        | 00-23                 |
| h          | The hour, 12-hour clock                                   | 1-12                  |
| hh         | The hour, 12-hour clock, 2-digits                         | 01-12                 |
| m          | The minute                                                | 0-59                  |
| mm         | The minute, 2-digits                                      | 00-59                 |
| s          | The second                                                | 0-59                  |
| ss         | The second, 2-digits                                      | 00-59                 |
| SSS        | The millisecond, 3-digits                                 | 000-999               |
| Z          | The offset from UTC, ±HH:mm                               | +05:00                |
| ZZ         | The offset from UTC, ±HHmm                                | +0500                 |
| A          |                                                           | AM PM                 |
| a          |                                                           | am pm                 |
| Q          | Quarter                                                   | 1-4                   |
| Do         | Day of Month with ordinal                                 | 1st 2nd ... 31st      |
| k          | The hour, beginning at 1                                  | 1-24                  |
| kk         | The hour, 2-digits, beginning at 1                        | 01-24                 |
| X          | Unix Timestamp in second                                  | 1360013296            |
| x          | Unix Timestamp in millisecond                             | 1360013296123         |
| w          | Week of year ( dependent WeekOfYear plugin )              | 1 2 ... 52 53         |
| ww         | Week of year, 2-digits ( dependent WeekOfYear plugin )    | 01 02 ... 52 53       |
| W          | ISO Week of year ( dependent IsoWeek plugin )             | 1 2 ... 52 53         |
| WW         | ISO Week of year, 2-digits ( dependent IsoWeek plugin )   | 01 02 ... 52 53       |
| wo         | Week of year with ordinal ( dependent WeekOfYear plugin ) | 1st 2nd ... 52nd 53rd |
| gggg       | Week Year ( dependent WeekYear plugin )                   | 2017                  |
| GGGG       | ISO Week Year ( dependent IsoWeek plugin )                | 2017                  |
| z          | Abbreviated named offset ( dependent Timezone plugin )    | EST                   |
| zzz        | Unabbreviated named offset ( dependent Timezone plugin )  | Eastern Standard Time |

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/iamkun/dayjs/blob/dev/LICENSE) ，请自由地享受和参与开源。
