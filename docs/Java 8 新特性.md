# HashMap

hashmap、concurrentHashMap进行了更新

# 内存结构调整

删除永久区，用元空间替代。

# Lambda表达式

java 8中引入了一个新的操作符“->”，称为箭头操作符或者Lambda操作符。

箭头操作符将Lambda表达式拆分成两部分：

左侧：Lambda表达式的参数列表，也就是接口中的抽象方法的参数列表。

右侧：Lambda表达式中所需要执行的功能，即Lambda体，也是接口中抽象方法的实现。

语法格式一：有一个参数并且无返回值

```java
import org.junit.Test;

/**
 * @author wardseptember
 * @create 2020-07-19 21:06
 */
public class LambdaDemo {

    @Test
    public void test1() {
        Runnable r = new Runnable() {
            @Override
            public void run() {
                System.out.println("hello world");
            }
        };
        r.run();
        Runnable r1 = () -> System.out.println("hello lambda");
        r1.run();
    }
}
```

语法格式二：有两个以上参数，又返回值，并且Lambda体中有多条语句

```java
    @Test
    public void test2() {
        Comparator<Integer> comparator = (x, y) -> {
            System.out.println("函数式接口");
            return Integer.compare(x, y);
        };
    }
    // 只有一条语句，可以省略大括号和return
    @Test
    public void test3() {
        Comparator<Integer> comparator = (x, y) -> Integer.compare(x, y);
    }
```

> Lambda表达式的参数列表的数据类型可以省略不写，因为JVM编译器通过上下文可以推断出数据类型，这个过程即“类型推断”。

Lambda表达式需要“函数式接口”的支持，函数式接口是指接口中只有一个抽象方法。@FunctionalInterface注解修饰的接口必须是函数式接口，相当于做了一个格式检查。

## Java 8内置的四大核心函数式接口

### Consumer<T> 消费型接口

```java
@Test
public void test4() {
    cousumer1(1000d, x -> System.out.println("hello " + x));
}

public void cousumer1(double money, Consumer<Double> con) {
    con.accept(money);
}
```

### Supplier<T> 供给型接口

```java
@Test
public void test5() {
    List<Integer> list = getNumList(10, () -> (int)(Math.random() * 100));
    for (int i : list) {
        System.out.println(i);
    }
}

public List<Integer> getNumList(int num, Supplier<Integer> sup) {
    List<Integer> list = new ArrayList<>();
    for (int i = 0; i < num; i++) {
        Integer n = sup.get();
        list.add(n);
    }
    return list;
}
```

### Fuction<T, R> 函数型接口

```java
@Test
public void test6() {
    String newStr = strHandler(" \t\t\t lambda表达式练习  ", str -> str.trim());
    System.out.println(newStr);
}

public String strHandler(String str, Function<String, String> fun) {
    return fun.apply(str);
}
```

### Predicate<T> 断言型接口

```java
public List<String> filterStr(List<String> list, Predicate<String> predicate) {
    List<String> strList = new ArrayList<>();
    for (String str : list) {
        if (predicate.test(str)) {
            strList.add(str);
        }
    }
    return strList;
}

@Test
public void test7() {
    List<String> list = Arrays.asList("hello", "atguigu", "Lambda", "www");
    List<String> stringList = filterStr(list, s -> s.length() > 3);
    for (String str : stringList) {
        System.out.println(str);
    }
}
```

## 方法引用和构造器引用

若Lambda体中的内容有方法已经实现了，我们可以使用“方法引用”。

主要有三种语法格式：

> Lambda体中调用方法的参数列表与返回值类型，要与函数式接口中抽象方法的函数列表和返回值类型保持一致。

* 对象::实例方法名

```java
@Test
public void test8() {
    Consumer<String> con1 = System.out::println;
    con1.accept("abcdef");

    // 与下面形式等价
    Consumer<String> con2 = x -> System.out.println(x);
    con2.accept("abcdef");
}
```

* 类::静态方法名

```

```



* 类::实例方法名

```java

```

# Stream API



