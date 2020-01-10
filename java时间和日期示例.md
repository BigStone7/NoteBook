时间和日期的处理在任何程序开发都会经常遇到，但是在java8之前的支持并不好，为了改进这一问题在java8 中推出了java.time包,现在对API进行实践。

### 获取当前时间和日期

* 示例一：`Instant.now()`

  ```java
  Instant now = Instant.now();
  System.out.println("当前时间： "+now);
  
  ----------------输出结果---------------
  当前时间： 2019-09-23T11:22:54.405Z
  ```

  确实输出了一个时间戳，但是，这个时间并不是北京时间，是零时区的，北京位于第八时区，因此将此时间加上8个时区就可以。

  ```java
  Instant now = Instant.now().plusMillis(TimeUnit.HOURS.toMillis(8));
  System.out.println("当前时间： "+now);
  
  ----------------输出结果---------------
  当前时间： 2019-09-23T19:33:03.695Z
  ```

  但是这种方法不常用。

* 示例二：`LocalDateTime.now()`

  ```JAVA
  LocalDateTime now = LocalDateTime.now();
  System.out.println("当前时间： "+now);
  
  ----------------输出结果---------------
  当前时间： 2019-09-23T19:38:01.650
  ```

  这个最常用。

* 示例三：`LocalDate.now()`   `LocalDate.now()`

  ```java
  LocalDate date = LocalDate.now();
  LocalTime time = LocalTime.now();
  System.out.println("当前日期： "+date);
  System.out.println("当前时间： "+time);
  
  ----------------输出结果---------------
  当前日期： 2019-09-23
  当前时间： 19:44:51.366
  ```

  分别读取当前的时间和日期。

### 实例化指定时间和日期

* 示例一：`of()`方法初始化时间实例

  ```java
  LocalDateTime now = LocalDateTime.of(2019,10,1,12,24,23,35);
  LocalDate date = LocalDate.of(2019, 10, 01);
  LocalTime time = LocalTime.of(12,24,23,34);
  System.out.println("指定日期和时间： "+now);
  System.out.println("指定日期： "+date);
  System.out.println("指定时间： "+time);
  
  ----------------------------输出结果-----------------------------
  指定日期和时间： 2019-10-01T12:24:23.000000035
  指定日期： 2019-10-01
  指定时间： 12:24:23.000000034
  ```

* 示例二：`parse()` 方法初始化时间实例

  ```java
  Instant inst = Instant.parse("2019-09-23T11:22:54.405Z");
  LocalDateTime now = LocalDateTime.parse("2019-10-01T12:24:23.000000035");
  LocalDate date = LocalDate.parse("2019-12-01");
  LocalTime time = LocalTime.parse("12:24:23.000000034");
  System.out.println("Instant 指定日期和时间： "+inst);
  System.out.println("指定日期和时间： "+now);
  System.out.println("指定日期： "+date);
  System.out.println("指定时间： "+time);
  
  ---------------------------------输出结果-------------------------------------
  Instant 指定日期和时间： 2019-09-23T11:22:54.405Z
  指定日期和时间： 2019-10-01T12:24:23.000000035
  指定日期： 2019-12-01
  指定时间： 12:24:23.000000034
  ```

### 时间和日期的计算

* 示例一：增加日期

  ```java
  LocalDate now = LocalDate.now();
  LocalDate yesterday = now.minus(1, ChronoUnit.DAYS);
  LocalDate tomorrow  = now.plusDays(1);
  System.out.println("今天： "+now);
  System.out.println("昨天： "+yesterday);
  System.out.println("明天： "+tomorrow);
  
  -----------------输出结果--------------------------------
  今天： 2019-09-23
  昨天： 2019-09-22
  明天： 2019-09-24
  ```

  

>参考网址：
>
>https://docs.oracle.com/en/java/javase/13/docs/api/java.base/java/time/package-summary.html