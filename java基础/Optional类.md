# Optional类

Optional是java8中新出现的一个类，最初是源自google gava库。目的是对臭名昭著的NullPointerException的异常做预防性的检查。

>**Tips:**
>
>Optional类的源码比较简单，建议大家在使用前仔细看下。我在下面的会给出简单的使用样例，包括一些代码的使用区别，阅读源码有利理解这些区别存在的本质原因。

### 创建Optionl实例

* **Optional.empty()** 

  ```java
  Optional<User> user = Optional.empty();
  ```

  构建了一个空的Optional。

* **Optional.of()** 

  ```java
  User user = new User("张三","12");
  Optional<User> optionalUser = Optional.of(user);
  ```

  创建一个含有user值的Optional。

* **Optional.ofNullable()** 

  ```java
  User user = new User("张三","12");
  Optional<User> optionalUser = Optional.ofNullable(user);
  ```

  创建一个含有有user值的Optional。

  >**tips:**
  >
  > **of()** 和 **ofNullable()** 方法都可以创建包含值的 Optional，但是，如果你把 null 值作为参数传递进去：
  >*   **of()** 方法会抛出 **NullPointerException**；
  >*   **ofNullable()** 方法会抛出 **java.util.NoSuchElementException: No value present**；

###  获取Optional值

* **Optional.get()** 

### Optional判空

* **Optional.isPersion()** 

  ```java
  Optional.ofNullable(user).isPresent()
  ```

  如果Optional对象不为空，输出为false，否则输出为true；

* **Optional.ifPersion(Consumer<? super T> consumer)** 

  ```java
  Optional.ofNullable(user).ifPresent(u ->  System.out.println(u.getName()));
  ```

  如果Optional对象不为空，则会执行后面的lamda表达式。

  >**Tips:**
  >
  >**IsPresent（）**和**IfPresent（）**都可以判读Optional对象是否为空，但是不同的是**IfPresent（）**接受一个Consumer(消费者) 参数，如果对象不是空的，就对执行传入的 Lambda 表达式。这才是Option类的精髓所在，所以不要轻易使用isPresent。否则你的代码和之前`Object！=null`的语法没有区别；

### Optional默认值设置

* **Optional.orElse()** 

  ```java
  User ua = new User();
  User user = new User("张三","13");
  User re = Optional.ofNullable(ua).orElse(user)
  ```

  如果Optional对象为null，就会生成`orElse(user)`中的user，否则返回原ua

* **Optional.orElseGet()** 

  ```java
  User ua = new User();
  User user = new User("张三","13");
  User result = Optional.ofNullable(ua).orElseGet(user);
  ```

  如果Optional对象为null，就会生成`orElseGet(user)`中的user，否则返回原ua。

  >**Tips:**
  >
  >orElse()，工作方式，如果有值则返回该值，否则返回传递给它的参数值；
  >
  >orElseGet()有值的时候返回值，如果没有值，它会执行作为参数传入的 Supplier(供应者) 函数式接口，并将返回其执行结果
  >
  >**区别：**
  > 原传入的值（ua）为null是这个两个方法没有区别，都生成user；
  >
  >但是如果传入的值（ua）不为null，orElse()依旧会生成user类，但是orElseGet()不会。
  >
  >**在执行较密集的调用时，比如调用 Web 服务或数据查询，这个差异会对性能产生重大影响。**

* **Optional.orElseThrow(Supplier<? extends X> exceptionSupplier)** 

  ```java
  User user = null;
  User result = Optional.ofNullable(user)
      .orElseThrow( () -> new IllegalStateException());
  ```

  如果 *user* 值为 null，会抛出 orElseThrow中定义好的异常，这里抛出的是`IllegalStateException()`。这个方法可以让异常处理变的多样，灵活。

### Optional值过滤

* **Optional.filter(Predicate<? super T> predicate)** 

  ```java
  Optional<User> result = Optional.ofNullable(user)
                  .filter(u -> u.getName().contains("三"));
  ```

  filter()中传入一个`Predicate`对象，根据其结果返回过滤后的实例自身，否则返回一个Optional.empty

### Optional值转换

* **Optional.map(Function<? super T, ? extends U> mapper)** 

  ```
  User user = new User("张三","13");
  Optional<String> result = Optional.ofNullable(user).map(u -> u.getName());
  ```

  map()中传入一个Function（函数式接口）对象，map()方法将Optional中的包装对象用Function函数进行运算，并包装成新的Optional对象（包装对象的类型可能改变）；

  上面的`user`对象经过map后变为了`String`对象

* **Optional.flatMap(Function<? super T, Optional<U>> mapper)** 

  ```java
  User user = new User("张三","13");
  Optional<String> result = Optional.ofNullable(user)
  	.flatMap(u->Optional.of("李四"));
  ```
  
  >**Tips:**
  >
  >flatMap()跟map()方法不同的是，入参Function函数的返回值类型为Optional<U>类型，而不是U类型，这样flatMap()能将一个二维的Optional对象映射成一个一维的对象

### Optional的链式调用

Optional的使用除了解决了空指针异常之外，另外一个就是其链式调用。下面写个简单的例子。

```java
public class User {
    private String name;
    private String age;
    private  House house;
    
    ....
}
```

```java
public class House {
    private String size;
    private String address;
    ...
}
```

```java
User user = new User("张三","13");
        String result = Optional.ofNullable(user)
                .map(u -> u.getHouse())
                .map(h ->h.getAddress())
                .orElse("没有地址");
```

***

END!