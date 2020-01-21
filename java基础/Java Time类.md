# Java Time 包

> **官方网址：**https://docs.oracle.com/javase/tutorial/datetime/overview/packages.html

Date-Time API由主要包`java.time`和四个子包组成：

- `java.time`

  API的核心，代表日期和时间。它包括日期，时间，组合的日期和时间，时区，瞬间，持续时间和时钟的类。这些类基于ISO-8601中定义的日历系统，并且是不可变的并且是线程安全的。

- `java.time.chrono`

  用于表示默认ISO-8601以外的日历系统的API。您还可以定义自己的日历系统。

- `java.time.format`

  用于格式化和解析日期和时间的类。

- `java.time.temporal`

  扩展的API，主要用于框架和库编写者，允许日期和时间类，查询和调整之间的互操作。字段（`TemporalField`和`ChronoField`）和单位（`TemporalUnit`和`ChronoUnit`）在此包中定义。

- `java.time.zone`

  支持时区，时区偏移量和时区规则的类。如果使用时区，大多数开发人员将仅需要使用`ZonedDateTime`和`ZoneId`或`ZoneOffset`。

# 方法命名约定

Date-Time API在一组丰富的类中提供了一组丰富的方法。使方法名称在类之间尽可能保持一致。例如，许多类都提供了`now`方法，该方法捕获与该类相关的当前时刻的日期或时间值。有`from`方法可以从一个类转换为另一个类。

关于方法名称前缀也存在标准化。由于Date-Time API中的大多数类都是不可变的，因此该API不包含`set`方法。（其创建之后，一个不可变的对象的值不能被改变一个的不可改变的等效。`set`的方法是`with`。）下表列出了常用的前缀：

| 方法前缀 | 方法类型 | 描述                                                         |
| -------- | -------- | ------------------------------------------------------------ |
| of       | 静态工厂 | 创建一个实例，其中工厂主要在验证输入参数，而不转换它们。     |
| from     | 静态工厂 | 将输入参数转换为目标类的实例，这可能涉及从输入中丢失信息。   |
| parse    | 静态工厂 | 解析输入字符串以生成目标类的实例。                           |
| format   | 实例     | 使用指定的格式化程序格式化时间对象中的值以产生字符串。       |
| get      | 实例     | 返回目标对象状态的一部分。                                   |
| is       | 实例     | 查询目标对象的状态。                                         |
| with     | 实例     | 返回更改了一个元素的目标对象的副本；这等效于JavaBean上的set方法。 |
| plus     | 实例     | 返回添加了一定时间的目标对象的副本。                         |
| minus    | 实例     | 返回目标对象的副本，其中减去了一段时间。                     |
| to       | 实例     | 将此对象转换为另一种类型。                                   |
| at       | 实例     | 将此对象与另一个对象合并。                                   |



下表总结了`java.time`包中基于时间的类，这些类存储日期和/或时间信息，或可用于测量时间量。列中的复选标记表示该类使用该特定类型的数据，并且**toString Output**列显示使用`toString`方法打印的实例。

| Class or Enum    | Year                                                         | Month                                                        | Day                                                          | Hours                                                        | Minutes                                                      | Seconds                                                      | Zone Offset                                                  | Zone ID                                                      | toString Output                             |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------- |
| `Instant`        |                                                              |                                                              |                                                              |                                                              |                                                              | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              |                                                              | `2013-08-20T15:16:26.355Z`                  |
| `LocalDate`      | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              |                                                              |                                                              |                                                              |                                                              | `2013-08-20`                                |
| `LocalDateTime`  | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              |                                                              | `2013-08-20T08:16:26.937`                   |
| `ZonedDateTime`  | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | `2013-08-21T00:16:26.941+09:00[Asia/Tokyo]` |
| `LocalTime`      |                                                              |                                                              |                                                              | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              |                                                              | `08:16:26.943`                              |
| `MonthDay`       |                                                              | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              |                                                              |                                                              |                                                              |                                                              | `--08-20`                                   |
| `Year`           | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              | `2013`                                      |
| `YearMonth`      | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              | `2013-08`                                   |
| `Month`          |                                                              | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              |                                                              |                                                              |                                                              |                                                              |                                                              | `AUGUST`                                    |
| `OffsetDateTime` | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              | `2013-08-20T08:16:26.954-07:00`             |
| `OffsetTime`     |                                                              |                                                              |                                                              | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              | `08:16:26.957-07:00`                        |
| `Duration`       |                                                              |                                                              | **                                                           | **                                                           | **                                                           | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              |                                                              | `PT20H` (20 hours)                          |
| `Period`         | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) | ![checked](https://docs.oracle.com/javase/tutorial/images/check.gif) |                                                              |                                                              |                                                              | ***                                                          | ***                                                          | `P10D` (10 days)                            |

*秒被捕获到纳秒精度。**此类不存储此信息，但是具有在这些单位中提供时间的方法。***将`Period`添加到`ZonedDateTime时`，会观察到夏时制或其他本地时间差异。

# DayOfWeek和Month枚举

Date-Time API提供了用于指定星期几和一年中月份的枚举。

## 周日

该 [`DAYOFWEEK`](https://docs.oracle.com/javase/8/docs/api/java/time/DayOfWeek.html)枚举由七个常量形容一周的日子：`MONDAY`至`SUNDAY`。`DayOfWeek`常数的整数值范围是1（星期一）到7（星期日）。使用定义的常量（`DayOfWeek.FRIDAY`）使您的代码更具可读性。

该枚举还提供了许多方法，类似于基于时间的类提供的方法。例如，以下代码将3天添加到“星期一”并打印结果。输出为“ THURSDAY”：

```
System.out.printf（“％s％n”，DayOfWeek.MONDAY.plus（3））;
```

通过使用 [`getDisplayName（TextStyle，Locale）`](https://docs.oracle.com/javase/8/docs/api/java/time/DayOfWeek.html#getDisplayName-java.time.format.TextStyle-java.util.Locale-)方法，您可以检索一个字符串来标识用户语言环境中的星期几。该 TextStyle枚举使您可以指定排序字符串要显示什么：`FULL`，`NARROW`（通常是一个字母），或`SHORT`（缩写）。所述`STANDALONE TextStyle `常量在某些语言中，其中为一个日期时，它被用于通过本身比的一部分使用时的输出是不同的使用。下面的示例为“星期一” 打印`TextStyle`的三种主要形式：

```java
DayOfWeek dow = DayOfWeek.MONDAY;
Locale locale = Locale.getDefault();
System.out.println(dow.getDisplayName(TextStyle.FULL, locale));
System.out.println(dow.getDisplayName(TextStyle.NARROW, locale));
System.out.println(dow.getDisplayName(TextStyle.SHORT, locale));
```

该代码具有用于以下输出`EN`区域：

```
Monday
M
Mon
```

## 月

该 [`月`](https://docs.oracle.com/javase/8/docs/api/java/time/Month.html)枚举包含常数的十二个月内，`一月`至`十二月`。与`DayOfWeek`枚举一样，`Month`枚举也是强类型的，每个常量的整数值对应于从1（一月）到12（十二月）的ISO范围。使用定义的常量（`Month.SEPTEMBER`）可使代码更具可读性。

该`月`枚举还包括了一些方法。下面的代码行使用`maxLength`方法打印2月中的最大可能天数。输出为“ 29”：

```
System.out.printf（“％d％n”，Month.FEBRUARY.maxLength（））;
```

该`月`枚举也实现了 [`getDisplayName（文字样式，语言环境）`](https://docs.oracle.com/javase/8/docs/api/java/time/Month.html#getDisplayName-java.time.format.TextStyle-java.util.Locale-)方法来检索串以识别用户的语言环境的月使用指定的`文字样式`。如果未定义特定的`TextStyle`，则返回表示常量数值的字符串。以下代码使用三种主要的文本样式打印八月：

```java
Month month = Month.AUGUST;
Locale locale = Locale.getDefault();
System.out.println(month.getDisplayName(TextStyle.FULL, locale));
System.out.println(month.getDisplayName(TextStyle.NARROW, locale));
System.out.println(month.getDisplayName(TextStyle.SHORT, locale));
```

该代码具有用于以下输出`EN`区域：

```
August
A
Aug
```

# Date类别

Date-Time API提供了四个类，这些类专门处理日期信息，而不考虑时间或时区。通过类名称建议使用这些类：`LocalDate`，`YearMonth`，`MonthDay`和`Year`。

## LocalDate

一个 [`LOCALDATE的`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html)代表年，月，日的ISO日历，是表示没有时间的日期是有用的。您可以使用`LocalDate`跟踪重要事件，例如出生日期或结婚日期。以下示例使用`of`和`with`方法创建`LocalDate`实例：

```
LocalDate date = LocalDate.of(2000, Month.NOVEMBER, 20);
LocalDate nextWed = date.with(TemporalAdjusters.next(DayOfWeek.WEDNESDAY));
```

有关`TemporalAdjuster`接口的更多信息，请参见 [Temporal Adjuster](https://docs.oracle.com/javase/tutorial/datetime/iso/adjusters.html)。

除了常用的方法外，`LocalDate`类还提供用于获取有关给定日期的信息的getter方法。该 [`getDayOfWeek`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html#getDayOfWeek--)一个特定的日期落在星期方法返回。例如，以下代码行返回“ MONDAY”：

```
DayOfWeek dotw = LocalDate.of（2012，Month.JULY，9）.getDayOfWeek（）;
```

以下示例使用`TemporalAdjuster`检索特定日期之后的第一个星期三。

```
LocalDate date = LocalDate.of(2000, Month.NOVEMBER, 20);
TemporalAdjuster adj = TemporalAdjusters.next(DayOfWeek.WEDNESDAY);
LocalDate nextWed = date.with(adj);
System.out.printf("For the date of %s, the next Wednesday is %s.%n",
                  date, nextWed);
```

运行代码将产生以下结果：

```
对于2000-11-20，下一个星期三是2000-11-22。
```

该 [期和时间](https://docs.oracle.com/javase/tutorial/datetime/iso/period.html)段也有使用的例子`LOCALDATE的`类。

## YearMonth

该 [`YearMonth`](https://docs.oracle.com/javase/8/docs/api/java/time/YearMonth.html)类代表一个特定的一年中的月份。下面的示例使用`YearMonth.lengthOfMonth（）`方法来确定`若干年`和月组合的天数。

```
YearMonth date = YearMonth.now();
System.out.printf("%s: %d%n", date, date.lengthOfMonth());

YearMonth date2 = YearMonth.of(2010, Month.FEBRUARY);
System.out.printf("%s: %d%n", date2, date2.lengthOfMonth());

YearMonth date3 = YearMonth.of(2012, Month.FEBRUARY);
System.out.printf("%s: %d%n", date3, date3.lengthOfMonth());
```

此代码的输出如下所示：

```
2013-06：30
2010-02：28
2012-02：29
```

## MonthDay

该 [`MONTHDAY`](https://docs.oracle.com/javase/8/docs/api/java/time/MonthDay.html)类表示某月的一天，如元旦1月1日。

下面的示例使用 [`MonthDay.isValidYear`](https://docs.oracle.com/javase/8/docs/api/java/time/MonthDay.html#isValidYear-int-)方法确定2月29日对于2010年是否有效。该调用返回`false`，确认2010年不是闰年。

```
MonthDay date = MonthDay.of（Month.FEBRUARY，29）;
boolean validLeapYear = date.isValidYear（2010）;
```

## Year

该 [`年度`](https://docs.oracle.com/javase/8/docs/api/java/time/Year.html)类代表一年。下面的示例使用 [`Year.isLeap`](https://docs.oracle.com/javase/8/docs/api/java/time/Year.html#isLeap--)方法确定给定年份是否为闰年。该返回值`true`，确认2012年是闰年。

```
boolean validLeapYear = Year.of（2012）.isLeap（）;
```

# Date and Time类别

## LocalTime

在 [`本地时间`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalTime.html)类是类似于其他类的名字的前缀为`本地`，但只有一次交易。此类对于表示基于人的时间（例如电影时间或本地图书馆的开放和关闭时间）很有用。它也可以用于创建数字时钟，如以下示例所示：

```
for (;;) {
    thisSec = LocalTime.now();

    // implementation of display code is left to the reader
    display(thisSec.getHour(), thisSec.getMinute(), thisSec.getSecond());
}
```

在`本地时间`类不存储时区或夏令时信息。

## LocalDateTime

处理日期和时间（不带时区）的类是 [`LocalDateTime`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html)，它是Date-Time API的核心类之一。此类用于表示日期（月-日-年）和时间（小时-分钟-秒-纳秒），并且实际上是`LocalDate`和`LocalTime`的组合。此类可以用来表示特定事件，例如，美国杯挑战者系列赛的路易威登杯决赛的第一场比赛于2013年8月17日下午1:10开始。请注意，这意味着下午1:10在当地时间。要包括时区，必须使用`ZonedDateTime`或`OffsetDateTime`，如“ [时区和偏移类”中所述](https://docs.oracle.com/javase/tutorial/datetime/iso/timezones.html)。

除了`now `方法，每一个基于时间的类提供的`LocalDateTime`类有各种`of`（前缀或方法的方法`of`创造的一个实例）`LocalDateTime`。有一个`from`方法可以将实例从另一种时间格式转换为`LocalDateTime`实例。也有加或减小时，分钟，天，周和月的方法。以下示例显示了其中一些方法。日期时间表达式以粗体显示：

```
System.out.printf（“ now：％s％n”，LocalDateTime.now（））;

System.out.printf（“ 1994年4月15日，上午11：30：％s％n”，
                  LocalDateTime.of（1994，Month.APRIL，15，11，30））;

System.out.printf（“立即（来自即时）：％s％n”，
                  LocalDateTime.ofInstant（Instant.now（），ZoneId.systemDefault（）））;

System.out.printf（“距现在6个月：％s％n”，
                  LocalDateTime.now（）。plusMonths（6））;

System.out.printf（“ 6个月前：％s％n”，
                  LocalDateTime.now（）。minusMonths（6））;
```

此代码产生的输出将类似于以下内容：

```
现在：2013-07-24T17：13：59.985
1994年4月15日上午11:30：1994-04-15T11：30
现在（从即时发送）：2013-07-24T17：14：00.479
从现在起的6个月：2014-01-24T17：14：00.480
6个月前：2013-01-24T17：14：00.481
```

# Time Zone and Offset类

阿*时区*是其中使用相同的标准时间上的地球的区域。每个时区都由一个标识符描述，通常具有格式*区域/城市*（`亚洲/东京`）和格林威治/ UTC时间的偏移量。例如，东京的偏移量是`+09：00`。

## ZoneId和ZoneOffset

Date-Time API提供了两个用于指定时区或偏移量的类：

- `ZoneId`指定时区标识符，并提供在`Instant`和`LocalDateTime`之间进行转换的规则。
- `ZoneOffset`指定与格林威治/ UTC时间的时区偏移量。

格林威治时间/ UTC时间的偏移量通常以小时为单位进行定义，但也有例外。[`TimeZoneId`](https://docs.oracle.com/javase/tutorial/datetime/iso/examples/TimeZoneId.java)示例中的以下代码 显示使用格林威治标准时间/ UTC的偏移量（未在整小时内定义）的所有时区的列表。

```
Set<String> allZones = ZoneId.getAvailableZoneIds();
LocalDateTime dt = LocalDateTime.now();

// Create a List using the set of zones and sort it.
List<String> zoneList = new ArrayList<String>(allZones);
Collections.sort(zoneList);

...

for (String s : zoneList) {
    ZoneId zone = ZoneId.of(s);
    ZonedDateTime zdt = dt.atZone(zone);
    ZoneOffset offset = zdt.getOffset();
    int secondsOfHour = offset.getTotalSeconds() % (60 * 60);
    String out = String.format("%35s %10s%n", zone, offset);

    // Write only time zones that do not have a whole hour offset
    // to standard out.
    if (secondsOfHour != 0) {
        System.out.printf(out);
    }
    ...
}
```

本示例将以下列表打印为标准输出：

```
       America/Caracas     -04:30
     America/St_Johns     -02:30
        Asia/Calcutta     +05:30
         Asia/Colombo     +05:30
           Asia/Kabul     +04:30
       Asia/Kathmandu     +05:45
        Asia/Katmandu     +05:45
         Asia/Kolkata     +05:30
         Asia/Rangoon     +06:30
          Asia/Tehran     +04:30
   Australia/Adelaide     +09:30
Australia/Broken_Hill     +09:30
     Australia/Darwin     +09:30
      Australia/Eucla     +08:45
        Australia/LHI     +10:30
  Australia/Lord_Howe     +10:30
      Australia/North     +09:30
      Australia/South     +09:30
 Australia/Yancowinna     +09:30
  Canada/Newfoundland     -02:30
         Indian/Cocos     +06:30
                 Iran     +04:30
              NZ-CHAT     +12:45
      Pacific/Chatham     +12:45
    Pacific/Marquesas     -09:30
      Pacific/Norfolk     +11:30
```

该`TimeZoneId`例子也打印所有时区ID的列表发送到名为文件 [`timeZones`](https://docs.oracle.com/javase/tutorial/datetime/iso/examples/timeZones)。

## The Date-Time 

Date-Time API提供了三个与时区一起使用的基于时间的类：

- `ZonedDateTime`处理具有相应时区的日期和时间，其时区偏离格林威治/ UTC。
- `OffsetDateTime`处理具有与格林威治/ UTC相对应的时区偏移的日期和时间，而没有时区ID。
- `OffsetTime`处理时间与格林威治/ UTC有相应时区偏移的时间，而没有时区ID。

什么时候使用`OffsetDateTime`而不是`ZonedDateTime`？如果要编写复杂的软件，该软件根据地理位置为日期和时间计算建模自己的规则，或者要将时间戳存储在仅跟踪格林威治/ UTC时间的绝对偏移量的数据库中，则可能需要使用`OffsetDateTime`。同样，XML和其他网络格式将日期时间传输定义为`OffsetDateTime`或`OffsetTime`。

虽然所有三类保持从格林尼治/ UTC时间偏移，只有`ZonedDateTime`使用 [`ZoneRules`](https://docs.oracle.com/javase/8/docs/api/java/time/zone/ZoneRules.html)，该部分`java.time.zone`包，以确定如何为特定的时区偏移量发生变化。例如，大多数时区在将时钟向前移动到夏时制时会出现间隔（通常为1小时），而在将时钟向后移动到标准时间和重复转换的最后一个小时时会出现时间重叠。该`ZonedDateTime`类适应这种情况，而`OffsetDateTime`和`OffsetTime`类，它们不具备访问`ZoneRules`，不要。

### ZonedDateTime

该 [ZonedDateTime](https://docs.oracle.com/javase/8/docs/api/java/time/ZonedDateTime.html)类，实际上，结合了 [`LocalDateTime`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html)与类 [`了zoneid`](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneId.html)类。它用于表示带有时区（地区/城市，例如`Europe / Paris`）的完整日期（年，月，日）和时间（小时，分钟，秒，纳秒）。

以下[`Flight`](https://docs.oracle.com/javase/tutorial/datetime/iso/examples/Flight.java)示例中的代码将从 旧金山到东京的航班的起飞时间定义为America / Los Angeles时区中的`ZonedDateTime`。该`withZoneSameInstant`和`plusMinutes`方法用于创建实例`ZonedDateTime`代表在东京的预计到达时间，650分钟的飞行后。该`ZoneRules.isDaylightSavings`方法确定它是否是夏令时的航班在东京抵达。

甲`DateTimeFormatter`对象用于格式化`ZonedDateTime`实例进行打印：

```
DateTimeFormatter format = DateTimeFormatter.ofPattern("MMM d yyyy  hh:mm a");

// Leaving from San Francisco on July 20, 2013, at 7:30 p.m.
LocalDateTime leaving = LocalDateTime.of(2013, Month.JULY, 20, 19, 30);
ZoneId leavingZone = ZoneId.of("America/Los_Angeles"); 
ZonedDateTime departure = ZonedDateTime.of(leaving, leavingZone);

try {
    String out1 = departure.format(format);
    System.out.printf("LEAVING:  %s (%s)%n", out1, leavingZone);
} catch (DateTimeException exc) {
    System.out.printf("%s can't be formatted!%n", departure);
    throw exc;
}

// Flight is 10 hours and 50 minutes, or 650 minutes
ZoneId arrivingZone = ZoneId.of("Asia/Tokyo"); 
ZonedDateTime arrival = departure.withZoneSameInstant(arrivingZone)
                                 .plusMinutes(650);

try {
    String out2 = arrival.format(format);
    System.out.printf("ARRIVING: %s (%s)%n", out2, arrivingZone);
} catch (DateTimeException exc) {
    System.out.printf("%s can't be formatted!%n", arrival);
    throw exc;
}

if (arrivingZone.getRules().isDaylightSavings(arrival.toInstant())) 
    System.out.printf("  (%s daylight saving time will be in effect.)%n",
                      arrivingZone);
else
    System.out.printf("  (%s standard time will be in effect.)%n",
                      arrivingZone);
```

这将产生以下输出：

```
LEAVING:  Jul 20 2013  07:30 PM (America/Los_Angeles)
ARRIVING: Jul 21 2013  10:20 PM (Asia/Tokyo)
  (Asia/Tokyo standard time will be in effect.)
```

### OffsetDateTime

该 [OffsetDateTime](https://docs.oracle.com/javase/8/docs/api/java/time/OffsetDateTime.html)类，实际上，结合了 [`LocalDateTime`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html)与类 [`ZoneOffset`](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneOffset.html)类。它用于表示完整的日期（年，月，日）和时间（小时，分钟，秒，纳秒），与格林威治时间/ UTC时间（+/-小时：分钟，例如`+06：00`或`- 08:00`）。

以下示例将`OffsetDateTime`与`TemporalAdjuster.lastDay`方法`结合`使用，以查找2013年7月的最后一个星期四。

```
//查找2013年7月的最后一个星期四。
LocalDateTime localDate = LocalDateTime.of(2013, Month.JULY, 20, 19, 30);
ZoneOffset offset = ZoneOffset.of("-08:00");

OffsetDateTime offsetDate = OffsetDateTime.of(localDate, offset);
OffsetDateTime lastThursday =
        offsetDate.with(TemporalAdjusters.lastInMonth(DayOfWeek.THURSDAY));
System.out.printf("The last Thursday in July 2013 is the %sth.%n",
                   lastThursday.getDayOfMonth());
```

运行此代码的输出为：

```
The last Thursday in July 2013 is the 25th.
```

### OffsetTime

该 [OffsetTime](https://docs.oracle.com/javase/8/docs/api/java/time/OffsetTime.html)类，实际上，结合 [`本地时间`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalTime.html)与类 [`ZoneOffset`](https://docs.oracle.com/javase/8/docs/api/java/time/ZoneOffset.html)类。它用于表示时间（小时，分钟，秒，纳秒），相对于格林威治时间/ UTC时间（+/-小时：分钟，例如`+06：00`或`-08：00`）。

在与`OffsetDateTime`类相同的情况下使用`OffsetTime`类，但是不需要跟踪日期。

# Instant

Date-Time API的核心类之一是 [`Instant`](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html)类，它表示时间线上十亿分之一秒的开始。此类对于生成表示机器时间的时间戳很有用。

```
import java.time.Instant;

Instant timestamp = Instant.now();
```

从`Instant`类返回的值是从1970年1月1日的第一秒（`1970-01-01T00：00：00Z`）开始的时间，也称为 [`EPOCH`](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html#EPOCH)。在纪元之前发生的瞬间具有负值，在纪元之后发生的瞬间具有正值。

`Instant`类 提供的其他常量是 [`MIN`](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html#MIN)（代表最小的可能（过去）时刻）和 [`MAX`](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html#MAX)（代表最大的（未来）时刻）。

在`Instant`上 调用`toString`会产生如下输出：``

```
2013-05-30T23：38：23.085Z
```

此格式遵循 [ISO-8601](http://www.iso.org/iso/home/standards/iso8601.htm)标准来表示日期和时间。

的`即时`类提供了多种用于操作方法`即时`。有`加`和`减`的增加或减少时间的方法。以下代码将当前时间增加1小时：

```
Instant oneHourLater = Instant.now（）。plusHours（1）;
```

有一些比较瞬间的方法，例如 [`isAfter`](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html#isAfter-java.time.Instant-)和 [`isBefore`](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html#isBefore-java.time.Instant-)。该 [`直到`](https://docs.oracle.com/javase/8/docs/api/java/time/Instant.html#until-java.time.temporal.Temporal-java.time.temporal.TemporalUnit-)两者之间存在着方法返回多少时间`即时`对象。下面的代码行报告自Java时代开始以来已经发生了几秒钟。

```
long secondsFromEpoch = Instant.ofEpochSecond（0L）.until（Instant.now（），
                        ChronoUnit.SECONDS）;
```

在`即时`类不会随着时间的人单位，如年，月，或数天的工作。如果你想在这些单位进行计算，您可以将转换`即时`到另一个类，如`LocalDateTime`或`ZonedDateTime`，通过结合`即时`与一个时区。然后，可以以所需单位访问值。以下代码使用[`ofInstant`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html#ofInstant-java.time.Instant-java.time.ZoneId-)方法和默认时区将`Instant`转换为`LocalDateTime`对象 ，然后以更易读的形式打印出日期和时间：[``](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDateTime.html#ofInstant-java.time.Instant-java.time.ZoneId-)

```
Instant timestamp;
...
LocalDateTime ldt = LocalDateTime.ofInstant（timestamp，ZoneId.systemDefault（））;
System.out.printf（“％s％d％d at％d：％d％n”，ldt.getMonth（），ldt.getDayOfMonth（），
                  ldt.getYear（），ldt.getHour（），ldt.getMinute（））；
```

输出将类似于以下内容：

```
2013年5月30日在18:21
```

可以将`ZonedDateTime`或`OffsetTimeZone`对象转换为`Instant`对象，因为每个对象都映射到时间线上的确切时刻。但是，事实并非如此。要将`Instant`对象转换为`ZonedDateTime`或`OffsetDateTime`对象，需要提供时区或时区偏移信息。

# Parsing and Formatting

Date-Time API中基于时间的类提供了用于解析包含日期和时间信息的字符串的`解析`方法。这些类还提供用于格式化基于时间的对象以供显示的`格式化`方法。在这两种情况下，过程都是相似的：您为`DateTimeFormatter`提供一种模式来创建格式化程序对象。然后将此格式化程序传递给`parse`或`format`方法。

该`DateTimeFormatter`类提供了大量的 [预定义的格式化](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html#predefined)，或者您也可以自己定义。

如果转换过程中发生问题 ，则`parse`和`format`方法将引发异常。因此，您的解析代码应捕获`DateTimeParseException`错误，而格式代码应捕获`DateTimeException`错误。有关异常处理的更多信息，请参见 [捕获和处理异常](https://docs.oracle.com/javase/tutorial/essential/exceptions/handling.html)。

该`DateTimeFormatter`类是不可变的和线程安全的; 在适当的情况下，可以（并且应该）将其分配给静态常量。

------

**版本说明：** 该`java.time`日期时间目标可直接使用`java.util.Formatter中`和`的String.format`通过使用与传统使用熟悉的基于模式的格式化`java.util.Date`和`java.util.Calendar中`类。

------

## Parsing

`LocalDate`类中 的一参数 [`parse（CharSequence）`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html#parse-java.lang.CharSequence-)方法使用`ISO_LOCAL_DATE`格式化程序。若要指定其他格式器，可以使用两个参数的 [`parse（CharSequence，DateTimeFormatter）`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html#parse-java.lang.CharSequence-java.time.format.DateTimeFormatter-)方法。下面的示例使用预定义的`BASIC_ISO_DATE`格式程序，该格式`程序`使用1959年7月9日的格式`19590709`。````[``](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html#parse-java.lang.CharSequence-java.time.format.DateTimeFormatter-)````

```
字符串输入= ...;
LocalDate日期= LocalDate.parse（in，DateTimeFormatter.BASIC_ISO_DATE）;
```

您也可以使用自己的模式定义格式化程序。以下[`Parse`](https://docs.oracle.com/javase/tutorial/datetime/iso/examples/Parse.java)示例中的代码 创建了一个格式为“ MMM d yyyy”的格式程序。此格式指定三个字符代表月份，一位数字代表月份中的日期，四位数字代表年份。使用此模式创建的格式化程序将识别诸如“ Jan 3 2003”或“ Mar 23 1994”之类的字符串。但是，要将格式指定为“ MMM dd yyyy”，每月的两个字符，则必须始终使用两个字符，用一位数字填充零以表示一个数字的日期：“ 2003年6月3日”。

```
String input = ...;
try {
    DateTimeFormatter formatter =
                      DateTimeFormatter.ofPattern("MMM d yyyy");
    LocalDate date = LocalDate.parse(input, formatter);
    System.out.printf("%s%n", date);
}
catch (DateTimeParseException exc) {
    System.out.printf("%s is not parsable!%n", input);
    throw exc;      // Rethrow the exception.
}
//'date'已成功解析
```

`DateTimeFormatter`类 的文档指定了 [完整的符号列表，](https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html#patterns)可用于指定格式或解析的模式。

该`字符串转换`在上例 [非ISO日期转换](https://docs.oracle.com/javase/tutorial/datetime/iso/nonIso.html)页面提供的日期格式的另一个例子。

## Formatting

的 [`格式（DateTimeFormatter）`](https://docs.oracle.com/javase/8/docs/api/java/time/LocalDate.html#format-java.time.format.DateTimeFormatter-)方法转换使用指定的格式的基于时间的对象为字符串表示。以下[`Flight`](https://docs.oracle.com/javase/tutorial/datetime/iso/examples/Flight.java)示例中的代码 使用“ MMM d yyy hh：mm a”格式转换`ZonedDateTime`的实例。日期的定义方式与前面的解析示例所用的方式相同，但是此模式还包括小时，分钟以及上午和下午。

```
ZoneId leavingZone = ...;
ZonedDateTime departure = ...;

try {
    DateTimeFormatter format = DateTimeFormatter.ofPattern("MMM d yyyy  hh:mm a");
    String out = departure.format(format);
    System.out.printf("LEAVING:  %s (%s)%n", out, leavingZone);
}
catch (DateTimeException exc) {
    System.out.printf("%s can't be formatted!%n", departure);
    throw exc;
}
```

此示例的输出同时显示到达和离开时间，如下所示：

```
离开时间：2013年7月20日下午7:30（美国/洛杉矶）
抵达时间：2013年7月21日晚上10:20（亚洲/东京）
```

# Temporal包

该 [`java.time.temporal`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/package-summary.html)包提供的接口，类和枚举的支持日期和时间码，特别是，日期和时间计算的集合。

这些接口旨在用于最低级别。典型的应用程序代码应根据具体类型（例如`LocalDate`或`ZonedDateTime`）而不是`Temporal`接口来声明变量和参数。这与声明`String`类型而不是`CharSequence`类型的变量完全相同。

## Temporal and TemporalAccessor

的 [`时空`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/Temporal.html)接口提供用于访问基于时间的对象的框架，并通过基于时间的类，如实现`即时`，`LocalDateTime`，和`ZonedDateTime`。该接口提供了添加或减少时间单位的方法，从而使基于时间的算术变得容易且在各种日期和时间类中保持一致。该 [`TemporalAccessor`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalAccessor.html)接口提供的只读版本`时空`界面。

两个`颞`和`TemporalAccessor`对象在字段来定义，如在指定 [`TemporalField`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalField.html)接口。所述 [`ChronoField`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/ChronoField.html)枚举是的具体实现`TemporalField`接口，并提供了一套丰富的定义的常量，如`DAY_OF_WEEK`，`MINUTE_OF_HOUR`，和`MONTH_OF_YEAR`。

这些字段的单位由[`TemporalUnit`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalUnit.html)接口指定 。该`ChronoUnit`枚举实现`TemporalUnit`接口。字段`ChronoField.DAY_OF_WEEK`是`ChronoUnit.DAYS`和`ChronoUnit.WEEKS`的组合。的`ChronoField`和`ChronoUnit`枚举在下面的章节中讨论。

`Temporal`接口中 基于算术的方法需要根据[`TemporalAmount`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalAmount.html)值定义的参数 。的`周期`和`持续时间`类（在所讨论的 [时期和疗程](https://docs.oracle.com/javase/tutorial/datetime/iso/period.html)）实现`TemporalAmount`接口。

## ChronoField和IsoFields

的 [`ChronoField`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/ChronoField.html)枚举，它实现了`TemporalField`接口，提供了一套丰富的常量用于访问日期和时间值。一些示例是`CLOCK_HOUR_OF_DAY`，`NANO_OF_DAY`和`DAY_OF_YEAR`。该枚举可用于表达时间的概念方面，例如一年的第三周，一天的第11小时或该月的第一个星期一。当遇到未知类型的`Temporal`时，可以使用 [`TemporalAccessor.isSupported（TemporalField）`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalAccessor.html#isSupported-java.time.temporal.TemporalField-)方法来确定`Temporal是否`支持特定字段。以下代码行返回`false`，指示`LocalDate`不支持`ChronoField.CLOCK_HOUR_OF_DAY`：

```
boolean isSupported = LocalDate.now（）。isSupported（ChronoField.CLOCK_HOUR_OF_DAY）;
```

[`IsoFields`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/IsoFields.html)类 定义了特定于ISO- [`8601日历系统的其他字段`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/IsoFields.html)。以下示例说明如何使用`ChronoField`和`IsoFields`获取字段的值：

```
time.get（ChronoField.MILLI_OF_SECOND）
int qoy = date.get（IsoFields.QUARTER_OF_YEAR）;
```

另外两个类定义了可能有用的其他字段， [`WeekFields`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/WeekFields.html)和 [`JulianFields`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/JulianFields.html)。

## ChronoUnit

所述 [`ChronoUnit`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/ChronoUnit.html)枚举实现`TemporalUnit`接口，并且提供了一组根据日期和时间，从毫秒到几千年标准单元。请注意，并非所有类都支持所有`ChronoUnit`对象。例如，`Instant`类不支持`ChronoUnit.MONTHS`或`ChronoUnit.YEARS`。所述 [`TemporalAccessor.isSupported（TemporalUnit）`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalAccessor.html#isSupported-java.time.temporal.TemporalUnit-)方法可用于验证一个类是否支持特定时间单位。对`isSupported`的以下调用返回`false`，确认`Instant`类不支持`ChronoUnit.DAYS`。

```
boolean isSupported = Instant.isSupported（ChronoUnit.DAYS）;
```

# Temporal Adjuster

`java.time.temporal`包中 的 [`TemporalAdjuster`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalAdjuster.html)接口提供了采用`Temporal`值并返回调整后值的方法。调节器可以与任何基于时间的类型一起使用。````

如果将调节器与`ZonedDateTime`一起使用，则将计算一个保留原始时间和时区值的新日期。

## 预定义调节器

该 [`TemporalAdjusters`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalAdjusters.html)类（注意是复数）提供了查找每月的第一天或最后一天预定义调节器的设定，在今年的第一天或最后一天，每月的最后一个星期三，或特定日期后的第一个星期二，仅举几个例子。预定义的调节器被定义为静态方法，旨在与 [静态import](https://docs.oracle.com/javase/tutorial/java/package/usepkgs.html#staticimport)语句一起使用。

下面的示例将几个`TemporalAdjusters`方法与基于时间的类中定义的`with`方法结合使用，以基于2000年10月15日的原始日期计算新日期：

```
LocalDate日期= LocalDate.of（2000，Month.OCTOBER，15）;
DayOfWeek dotw = date.getDayOfWeek（）;
System.out.printf（“％s在％s％n”上，日期，dotw）；

System.out.printf（“每月的第一天：％s％n”，
                  date.with（TemporalAdjusters.firstDayOfMonth（）））;
System.out.printf（“每月的第一个星期一：％s％n”，
                  date.with（TemporalAdjusters.firstInMonth（DayOfWeek.MONDAY）））;
System.out.printf（“每月的最后一天：％s％n”，
                  date.with（TemporalAdjusters.lastDayOfMonth（）））;
System.out.printf（“下个月的第一天：％s％n”，
                  date.with（TemporalAdjusters.firstDayOfNextMonth（）））;
System.out.printf（“明年的第一天：％s％n”，
                  date.with（TemporalAdjusters.firstDayOfNextYear（）））;
System.out.printf（“一年的第一天：％s％n”，
                  date.with（TemporalAdjusters.firstDayOfYear（）））;
```

这将产生以下输出：

```
2000-10-15在星期日
月的第一天：2000-10-01
月的第一个星期一：2000-10-02
一个月的最后一天：2000-10-31
下个月的第一天：2000-11-01
明年第一天：2001-01-01
一年的第一天：2000-01-01
```

## 定制调节器

您也可以创建自己的自定义调节器。为此，您将创建一个类，该类使用[`adjustInto（Temporal）`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalAdjuster.html#adjustInto-java.time.temporal.Temporal-)方法实现`TemporalAdjuster`接口 。该示例中的 类 是自定义调节器。该`PaydayAdjuster`评估传入的日期并返回下一个发薪日，假设发薪日发生了每月两次：15日，再次在该月的最后一天。如果计算的日期发生在周末，则使用上一个星期五。假定当前日历年。[``](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalAdjuster.html#adjustInto-java.time.temporal.Temporal-)[`PaydayAdjuster`](https://docs.oracle.com/javase/tutorial/datetime/iso/examples/PaydayAdjuster.java)[`NextPayday`](https://docs.oracle.com/javase/tutorial/datetime/iso/examples/NextPayday.java)``

```
/ **
 * AdjustInto方法接受一个Temporal实例 
 *并返回调整后的LocalDate。如果传入
 *参数不是LocalDate，则引发DateTimeException。
 * /
public Temporal AdjustInto（时间输入）{
    LocalDate日期= LocalDate.from（输入）;
    诠释日
    如果（date.getDayOfMonth（）<15）{
        天= 15;
    }其他{
        天= date.with（TemporalAdjusters.lastDayOfMonth（））。getDayOfMonth（）;
    }
    date = date.withDayOfMonth（day）;
    如果（date.getDayOfWeek（）== DayOfWeek.SATURDAY ||
        date.getDayOfWeek（）== DayOfWeek.SUNDAY）{
        日期= date.with（TemporalAdjusters.previous（DayOfWeek.FRIDAY））;
    }

    返回input.with（date）;
}
```

使用`with`方法，以`与`预定义调整器相同的方式调用调整器。下面的代码行来自`NextPayday`示例：

```
LocalDate nextPayday = date.with（new PaydayAdjuster（））;
```

2013年的6月15日和6月30日都是周末。运行分别具有6月3日和6月18日（2013年）的`NextPayday`示例，将得到以下结果：

```
给出的日期：2013年6月3日
下一个发薪日：2013年6月14日

给出的日期：2013年6月18日
下一个发薪日：2013年6月28日
```

# Temporal Query

甲 [`TemporalQuery`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalQuery.html)可用于检索来自基于时间的对象的信息。

## 预定义查询

所述 [`TemporalQueries`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalQueries.html)类（注意复数）提供多个预定义的查询，包括当应用程序不能识别基于时间的对象的类型是有用的方法。与调节器一样，预定义的查询被定义为静态方法，并设计为与 [静态import](https://docs.oracle.com/javase/tutorial/java/package/usepkgs.html#staticimport)语句一起使用。

的 [`精度`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalQueries.html#precision--)的查询，例如，返回最小`ChronoUnit`能够由特定基于时间的对象被返回。以下示例对几种类型的基于时间的对象使用`精度`查询：

```
TemporalQueries查询= TemporalQueries.precision（）;
System.out.printf（“ LocalDate的精度为％s％n”，
                  LocalDate.now（）。query（query））;
System.out.printf（“ LocalDateTime精度为％s％n”，
                  LocalDateTime.now（）。query（query））;
System.out.printf（“年精度为％s％n”，
                  Year.now（）。query（query））;
System.out.printf（“ YearMonth精度为％s％n”，
                  YearMonth.now（）。query（query））;
System.out.printf（“即时精度为％s％n”，
                  Instant.now（）。query（query））;
```

输出如下所示：

```
LocalDate精度是天
LocalDateTime精度为Nanos
年精度为年
YearMonth的精确度是Months
即时精度为Nanos
```

## 自定义查询

您还可以创建自己的自定义查询。一种实现方法是创建一个类，该类使用[`queryFrom（TemporalAccessor）`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalQuery.html#queryFrom-java.time.temporal.TemporalAccessor-)方法实现`TemporalQuery`接口 。该 示例实现了两个自定义查询。可以在实现[`TemporalQuery`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalQuery.html)接口的类中 找到第一个自定义查询 。该`queryFrom`方法比较传入的打击计划休假日期和返回日期`TRUE`如果它落在这些日期范围内。[``](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalQuery.html#queryFrom-java.time.temporal.TemporalAccessor-)[`CheckDate`](https://docs.oracle.com/javase/tutorial/datetime/iso/examples/CheckDate.java)[`FamilyVacations`](https://docs.oracle.com/javase/tutorial/datetime/iso/examples/FamilyVacations.java)[``](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/TemporalQuery.html)````

```
//如果传入的日期发生在其中一个事件中，则返回true
//家庭度假。由于查询仅比较月份和日期，
//即使时间类型不同，检查也会成功。
public Boolean queryFrom（TemporalAccessor date）{
    int month = date.get（ChronoField.MONTH_OF_YEAR）;
    int day = date.get（ChronoField.DAY_OF_MONTH）;

    //春假期间的迪士尼乐园
    如果（（month == Month.APRIL.getValue（））&&（（day> = 3）&&（day <= 8）））
        返回Boolean.TRUE;

    //史密斯一家在索格塔克湖聚会
    如果（（month == Month.AUGUST.getValue（））&&（（day> = 8）&&（day <= 14）））
        返回Boolean.TRUE;

    返回Boolean.FALSE;
}
```

第二个自定义查询在[`FamilyBirthdays`](https://docs.oracle.com/javase/tutorial/datetime/iso/examples/FamilyBirthdays.java)该类中实现 。此类提供了一个`isFamilyBirthday`方法，该方法将传入日期与多个生日进行比较，如果存在匹配项，则返回`TRUE`。

```
//如果传入的日期与其中之一相同，则返回true
//家庭生日。由于查询仅比较月份和日期，
//即使时间类型不同，检查也会成功。
public static Boolean isFamilyBirthday（TemporalAccessor date）{
    int month = date.get（ChronoField.MONTH_OF_YEAR）;
    int day = date.get（ChronoField.DAY_OF_MONTH）;

    // Angie的生日是4月3日。
    如果（（month == Month.APRIL.getValue（））&&（day == 3））
        返回Boolean.TRUE;

    //苏的生日是6月18日。
    如果（（month == Month.JUNE.getValue（））&&（day == 18））
        返回Boolean.TRUE;

    //乔的生日是5月29日。
    如果（（month == Month.MAY.getValue（））&&（day == 29））
        返回Boolean.TRUE;

    返回Boolean.FALSE;
}
```

所述`FamilyBirthday`类不实现`TemporalQuery`接口和可以用作一个的一部分 [lambda表达式](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)。以下来自`CheckDate`示例的代码显示了如何调用这两个自定义查询。

```
//调用查询而不使用lambda表达式。
布尔值isFamilyVacation = date.query（new FamilyVacations（））;

//使用lambda表达式调用查询。
布尔值isFamilyBirthday = date.query（FamilyBirthdays :: isFamilyBirthday）;

如果（isFamilyVacation.booleanValue（）|| isFamilyBirthday.booleanValue（））
    System.out.printf（“％s是重要日期！％n”，日期）;
其他
    System.out.printf（“％s不是重要的日期。％n”，日期）；
```

# Period and Duration

在编写代码以指定时间量时，请使用最能满足您需要的类或方法： [`Duration`](https://docs.oracle.com/javase/8/docs/api/java/time/Duration.html)类， [`Period`](https://docs.oracle.com/javase/8/docs/api/java/time/Period.html)类或 [`ChronoUnit.between`](https://docs.oracle.com/javase/8/docs/api/java/time/temporal/ChronoUnit.html#between-java.time.temporal.Temporal-java.time.temporal.Temporal-)方法。甲`持续时间`测量使用基于时间的值（秒，毫微秒）的时间量。一`期`使用基于日期的值（年，月，日）。

------

**注意：**一天 的`持续时间`*恰好是* 24小时。甲`周期`一天，当加入到`ZonedDateTime`，可根据时区而改变。例如，如果发生在夏令时的第一天或最后一天。

------

## 持续时间

甲`持续时间`是最合适的情况下，该措施机基于时间的，例如使用一个代码`即时`对象。一`时间`对象以秒或纳秒测量，并没有使用基于日期的结构，如年，月和日，虽然类提供的方法进行转换的天数，小时和分钟。如果`持续时间`创建的终点在起点之前，则它可以为负值。

以下代码以纳秒为单位计算两个瞬间之间的持续时间：

```
瞬时t1，t2；
...
long ns = Duration.between（t1，t2）.toNanos（）;
```

以下代码将10秒添加到`Instant`：

```
即时启动；
...
持续时间差距= Duration.ofSeconds（10）;
稍后即时= start.plus（gap）;
```

一`时间`没有连接到时间轴，因为它不跟踪时区或日光节约时间。添加`时间`相当于1天到一个`ZonedDateTime`中添加整整24小时导致，无论夏令时或可能导致其他的时间差。

## 计时单位

[时间包中](https://docs.oracle.com/javase/tutorial/datetime/iso/temporal.html)讨论 的`ChronoUnit`枚举 定义了用于测量时间的单位。当您只想在单个时间单位（例如天或秒）中测量时间量时，`ChronoUnit.between`方法很有用。的`之间`的方法适用于所有基于时间的对象，但它仅在单个单元返回的量。以下代码计算两个时间戳之间的间隔（以毫秒为单位）：````

```
导入java.time.Instant;
导入java.time.temporal.Temporal;
导入java.time.temporal.ChronoUnit;

即时的先前，当前，差距；
...
当前= Instant.now（）;
如果（上一个！= null）{
    差距= ChronoUnit.MILLIS.between（上一个，当前）;
}
...
```

## 期

要使用基于日期的值（年，月，日）定义时间量，请使用 [`Period`](https://docs.oracle.com/javase/8/docs/api/java/time/Period.html)类。该`周期`类提供了多种`获取`方式，比如 [`getMonths`](https://docs.oracle.com/javase/8/docs/api/java/time/Period.html#getMonths--)， [`getDays`](https://docs.oracle.com/javase/8/docs/api/java/time/Period.html#getDays--)和 [`getYears`](https://docs.oracle.com/javase/8/docs/api/java/time/Period.html#getYears--)，这样就可以从周期中提取的时间量。

总时间由三个单位共同表示：月，日和年。要显示以单个时间单位（例如天）衡量的时间量，可以使用`ChronoUnit.between`方法。

下面的代码报告你多大了，假设你出生在1月1日，1960年的`周期`类是用来确定在年，月，日和时间。通过使用`ChronoUnit.between`方法确定同一时期（总计天数），并显示在括号中：

```
今天的LocalDate = LocalDate.now（）;
LocalDate生日= LocalDate.of（1960，Month.JANUARY，1）;

周期p = Period.between（今天的生日）；
长p2 = ChronoUnit.DAYS.between（生日，今天）；
System.out.println（“您是” + p.getYears（）+“年，” + p.getMonths（）+
                   “个月和” + p.getDays（）+
                   “天数。（” + p2 +“总天数”“）；
```

该代码产生类似于以下内容的输出：

```
您今年53岁零4个月零29天。（共19508天）
```

要计算到下一个生日为止的时间，可以使用[`Birthday`](https://docs.oracle.com/javase/tutorial/datetime/iso/examples/Birthday.java)示例中的以下代码 。该`周期`类用于确定月和日值。该`ChronoUnit.between`方法返回总天数的值，并显示在括号中。

```
LocalDate生日= LocalDate.of（1960，Month.JANUARY，1）;

LocalDate nextBDay = Birthday.withYear（today.getYear（））;

//如果您的生日已经在今年发生，请在该年份加1。
如果（nextBDay.isBefore（today）|| nextBDay.isEqual（today））{
    nextBDay = nextBDay.plusYears（1）;
}

周期p = Period.between（today，nextBDay）;
长p2 = ChronoUnit.DAYS.between（today，nextBDay）;
System.out.println（“有” + p.getMonths（）+“月份，和” +
                   p.getDays（）+“直到下一个生日为止的天数。（” +
                   p2 +“总计”））；
```

该代码产生类似于以下内容的输出：

```
距离您的下一个生日还有7个月零2天。（共216）
```

这些计算不考虑时区差异。例如，如果您出生于澳大利亚，但目前居住在班加罗尔，则这会稍微影响您的确切年龄。在这种情况下，`请将``Period`与`ZonedDateTime`类结合使用。将`Period`添加到`ZonedDateTime时`，会观察到时间差异。

# 时钟

大多数基于时间的对象都提供一个无参数的`now（）`方法，该方法使用系统时钟和默认时区提供当前日期和时间。这些基于时间的对象还提供了一个参数`now（Clock）`方法，该方法使您可以传递备用 [`Clock`](https://docs.oracle.com/javase/8/docs/api/java/time/Clock.html)。

当前日期和时间取决于时区，对于全球化的应用程序，必须使用`Clock`来确保使用正确的时区创建日期/时间。因此，尽管使用`Clock`类是可选的，但此功能使您可以测试其他时区的代码，也可以使用时间不变的固定时钟来测试代码。

该`时钟`是一个抽象类，所以不能创建它的一个实例。以下工厂方法对于测试很有用。

- [`Clock.offset（Clock，Duration）`](https://docs.oracle.com/javase/8/docs/api/java/time/Clock.html#offset-java.time.Clock-java.time.Duration-)返回一个由指定` Duration`偏移的时钟。
- [`Clock.systemUTC（）`](https://docs.oracle.com/javase/8/docs/api/java/time/Clock.html#systemUTC--)返回代表格林威治/ UTC时区的时钟。
- [`Clock.fixed（Instant，ZoneId）`](https://docs.oracle.com/javase/8/docs/api/java/time/Clock.html#fixed-java.time.Instant-java.time.ZoneId-)始终返回相同的` Instant`。对于这个时钟，时间静止不动。

# 旧版日期时间代码

此前的Java SE 8发布，Java的日期和时间机制被提供 [`java.util.Date`](https://docs.oracle.com/javase/8/docs/api/java/util/Date.html)， [`java.util.Calendar`](https://docs.oracle.com/javase/8/docs/api/java/util/Calendar.html)以及 [`java.util.TimeZone`](https://docs.oracle.com/javase/8/docs/api/java/util/TimeZone.html)类，以及它们的子类，如 [`java.util.GregorianCalendar中`](https://docs.oracle.com/javase/8/docs/api/java/util/GregorianCalendar.html)。这些类有几个缺点，包括：

- 该`日历`类是不是类型安全的。
- 由于这些类是可变的，因此无法在多线程应用程序中使用它们。
- 由于异常的月份数和缺乏类型安全性，应用程序代码中的错误很常见。

## 与旧版代码的互操作性

也许您有使用`java.util`日期和时间类的遗留代码，并且希望通过对代码进行最少更改来利用`java.time`功能。

JDK 8版本中添加了几种方法，这些方法允许在`java.util`和`java.time`对象之间进行转换：

- [`Calendar.toInstant（）`](https://docs.oracle.com/javase/8/docs/api/java/util/Calendar.html#toInstant--)将` Calendar`对象转换为` Instant`。
- [`GregorianCalendar.toZonedDateTime（）`](https://docs.oracle.com/javase/8/docs/api/java/util/GregorianCalendar.html#toZonedDateTime--)将` GregorianCalendar`实例转换为` ZonedDateTime`。
- [`GregorianCalendar.from（ZonedDateTime）`](https://docs.oracle.com/javase/8/docs/api/java/util/GregorianCalendar.html#from-java.time.ZonedDateTime-)使用来自` ZonedDateTime`实例的默认语言环境创建` GregorianCalendar`对象。``
- [`Date.from（Instant）`](https://docs.oracle.com/javase/8/docs/api/java/util/Date.html#from-java.time.Instant-)从` Instant`创建一个` Date`对象。``
- [`Date.toInstant（）`](https://docs.oracle.com/javase/8/docs/api/java/util/Date.html#toInstant--)将` Date`对象转换为` Instant`。
- [`TimeZone.toZoneId（）`](https://docs.oracle.com/javase/8/docs/api/java/util/TimeZone.html#toZoneId--)将` TimeZone`对象转换为` ZoneId`。

下面的示例将`Calendar`实例转换为`ZonedDateTime`实例。请注意，必须提供一个时区才能将`Instant`转换为`ZonedDateTime`：

```
现在的日历= Calendar.getInstance（）;
ZonedDateTime zdt = ZonedDateTime.ofInstant（now.toInstant（），ZoneId.systemDefault（）））;
```

以下示例显示了`Date`和`Instant`之间的转换：

```
即时inst = date.toInstant（）;

日期newDate = Date.from（inst）;
```

下面的示例从`GregorianCalendar`转换为`ZonedDateTime`，然后从`ZonedDateTime`转换为`GregorianCalendar`。其他基于时间的类是使用`ZonedDateTime`实例创建的：

```
GregorianCalendar cal = ...;

TimeZone tz = cal.getTimeZone（）;
int tzoffset = cal.get（Calendar.ZONE_OFFSET）;

ZonedDateTime zdt = cal.toZonedDateTime（）;

GregorianCalendar newCal = GregorianCalendar.from（zdt）;

LocalDateTime ldt = zdt.toLocalDateTime（）;
LocalDate日期= zdt.toLocalDate（）;
LocalTime时间= zdt.toLocalTime（）;
```

## 将java.util日期和时间功能映射到java.time

由于日期和时间的Java实现已在Java SE 8发行版中进行了完全重新设计，因此您无法将一种方法交换为另一种方法。如果要使用`java.time`包提供的丰富功能，最简单的解决方案是使用上一节中列出的`toInstant`或`toZonedDateTime`方法。但是，如果您不想使用该方法或不足以满足您的需求，则必须重写日期时间代码。

“ [概述”](https://docs.oracle.com/javase/tutorial/datetime/iso/overview.html)页面上介绍的表 是开始评估哪些`java.time`类满足您的需求的好地方。

这两个API之间没有一对一的映射对应关系，但是下表让您大致了解了`java.util`日期和时间类`中`的哪些功能映射到`java.time` API。

| java.util功能                                       | java.time功能                              | 注释                                                         |
| --------------------------------------------------- | ------------------------------------------ | ------------------------------------------------------------ |
| `java.util.Date`                                    | `java.time.Instant`                        | 在`即时`和`日期`类是相似的。每个类： -代表的时间的时间轴（UTC）上的瞬时点 -保存独立的时间段的一个时间 -表示为划时代秒（因为1970-01-01T00：00：00Z）加上纳秒 的`Date.from （即时）`和`Date.toInstant（）`方法允许在这些类之间进行转换。 |
| `java.util.GregorianCalendar`                       | `java.time.ZonedDateTime`                  | 该`ZonedDateTime`类是替代`的GregorianCalendar`。它提供以下类似功能。 人类时间表示如下：  `LocalDate`：年，月，日  `LocalTime`：时，分，秒，纳秒  `ZoneId`：时区  `ZoneOffset`：与GMT 的当前偏移量`GregorianCalendar.from（ZonedDateTime）`和`GregorianCalendar.to（ZonedDateTime）`方法`有助于进行`转换这些类之间。 |
| `java.util.TimeZone`                                | `java.time.ZoneId`或`java.time.ZoneOffset` | 该`了zoneid`类指定的时区标识符和访问规则使用每个时区。该`ZoneOffset`类指定只从格林尼治/ UTC偏移。有关更多信息，请参见 [时区和偏移量类](https://docs.oracle.com/javase/tutorial/datetime/iso/timezones.html)。 |
| ``日历日期设置为`1970-01-01的``GregorianCalendar``` | `java.time.LocalTime`                      | 在`GregorianCalendar`实例中将日期设置为1970-01-01的代码，以便使用时间组件，可以将其替换为`LocalTime`实例。 |
| `GregorianCalendar`，时间设置为`00:00。`            | `java.time.LocalDate`                      | 可以使用`LocalDate`实例替换在`GregorianCalendar`实例中将时间设置为00:00 以便使用日期组件的代码。（这种`GregorianCalendar`方法存在缺陷，因为由于向夏时制的过渡，在某些国家/地区每年一次都不会发生午夜。）```` |

## 日期和时间格式

尽管`java.time.format.DateTimeFormatter`提供了一种用于格式化日期和时间值的强大机制，但是您也可以将`java.time.temporal`基于类的类直接与`java.util.Formatter`和`String.format一起`使用，并且使用基于相同模式的类与`java.util`日期和时间类一起使用的格式。