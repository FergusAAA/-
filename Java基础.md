Java基础

# java 的访问修饰符

![](https://img2018.cnblogs.com/blog/1151436/201905/1151436-20190503121147370-1645561563.png)

# 包装类

> 基础数据类型和包装类的转换
> 
> 自动装箱和自动拆箱
> 
> （基础数据类型）包装类 和 String 的装换

## 基础数据类型和包装类的转换

- **基础数据类型 -\> 包装类**:
    
    使用构造函数
    
    ```java
    int a = 1;
    Integer i = new Integer(a);
    ```
    
- **包装类 -\> 基础数据类型**：
    
    使用xxx**value（）**
    
    ```java
    int a = i.intValue();
    ```
    

## 自动装箱和自动拆箱

```java
int i = 1;
Integer I = i;

int a = I;
```

## （基础数据类型）包装类 和 String 的装换

### （基础数据类型）包装类 -\> String

- **连接运算**：
    
    ```java
    int num = 10;
    String str = 10 + "";
    ```
    
- **调用String的valueOf函数**：
    
    ```java
    float a = 12.12f;
    String str = String.valueOf(a);
    ```
    

### String -> （基础数据类型）包装类

**调用包装类的parseXxx（）方法**

```java
String str = "123"
int i = Integer.parseInt(str);
```

Java的8种基本类型的包装类(Byte, Short, Integer, Long, Character, Boolean, Float, Double), 除Float和Double以外, 其它六种都实现了常量池, 但是它们只在大于等于-128并且小于等于127时才使用常量池。

* * *

# 抽象（abstract）

> 使用 abstract 关键字修饰
> 
> 可以修饰 类 和 方法

## 抽象类

- 类名使用 abstract 关键字修饰
    
- 不可实例化（有构造函数，每个类都有构造函数）
    
    ```java
    public abstract class xxx {
        
    }
    ```
    

## 抽象方法

- 方法名使用 abstract 修饰
    
- 不能有方法体
    
- 继承带有抽象方法的类，必须重写类中的抽象方法，否则自己必须是个抽象类
    
    ```java
    public abstract void xxx();
    ```
    

## abstract 关键字的一些注意事项

- 不能修饰 属性 和 构造方法
- 不能修饰 私有方法、静态方法、final的方法 和 final的类

## 抽象类的匿名子类

- 抽象类不能实例化，可以通过匿名子类的方法初始化一个子类对象

```java
Employee employee = new Employee() {
    @Override
    public void work() {
    System.out.println("123");
    }
};
```

* * *

# 接口(interface)

> 接口使用 interface 关键字来声明
> 
> 在Java中,接口 和 类是并列的两个结构

## 成员变量的声明(都是public)

- JDK7 之前只能定义: **全局常量** 和 **抽象方法**
    
    - 全局常量 : ==public static final== 的,但书写时可以省略
    - 抽象方法 : ==public abstract== 的,但可以省略
- JKD8 还可以定义 **静态方法** 和 **默认方法**
    
    - 静态方法：==public static==，书写时不可省略（public可以省略）
        
        - 接口中定义的 静态方法 只能通过接口调用
    - 默认方法：==public default==，书写时不可省略（public可以省略）
        
        - 通过实现类的对象，可以调用实现类的 默认方法
            
        - 可以在实现类中 重写 默认方法
            
        - 如果 父类 和 接口 定义类 同名同参数的方法，默认调用 父类的方法
            
        - 实现类中 实现了多个同名同参数的默认方法 ，接口冲突，必须在实现类中 重写方法；
            
            同时可以使用 ==接口名.super.方法名== 的方式调用
            
            ```java
            Test1.super.method1();
            ```
            
- ==接口不能定义构造器==
    
- 通过类来实现(implements)的方法来使用
    
    如果该实现类重写了所有的抽象方法，该实现类可以实例化，否则该实现类仍是一个抽象类
    

## Java类的多实现

```java
public class Test implements Test1,Test2{

}
```

## 接口与接口之间可以==继承==，而且可以==多继承==

## 接口的匿名实现类

```java
public interface Test1 {
    void find();
}

Use use1 = new Use();
use1.use(new Test1() {
    @Override
    public void find() {
                
    }
});
```

* * *

# 内部类

> java中 类A 声明在 类B 中,则 类A 是一个内部类, 类B 称为外部类

- 成员内部类
    
    - 静态成员内部类（作为成员）
        
        ```java
        Animal.Dog dog = new Animal.Dog();
        ```
        
    - 非静态成员内部类（作为成员）
        
        ```java
        Animal animal = new Animal();
        Animal.Cat cat = animal.new Cat();
        ```
        
- 局部内部类
    

* * *

# 异常处理

> error
> 
> 编译时异常
> 
> 运行时异常

## 异常分类

- Error
- Exception
    - 编译时异常
        - IOException
        - ClassNotFoundException
    - 运行时异常
        - NullPointException
        - NumberFormatException

## 异常处理

- try catch finally
    
    “抓”异常
    
- throws
    
    “抛”异常
    
- 子类重写父类的方法，抛出异常类型，不大于父类抛出异常类型
    

```java
class Superclass {
    public void main() throws Exception{
    }
}

class Subclass extends Superclass{
    @Override
    public void main() throws IOException {
    }
}
```

## 手动抛出异常

通过 throw 关键字手动抛出异常

```java
class Student {
    private int id;

    public void regist(int id) {
        try {
            if (id > 0) {
                this.id = id;
            } else {
                throw new Exception("格式不对");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 自定义异常类

- 继承现有异常类
- 提供 静态常亮 ：serialVersionUID
- 提供重载的构造器

```java
class MyException extends RuntimeException {
    static final long serialVersionUID = -23891283L;
    public MyException(){

    }
    public MyException(String msg){
        super(msg);
    }
}
```

* * *

# 多线程

> 线程的创建何使用
> 
> 线程的生命周期
> 
> 线程的同步
> 
> 线程通信

## 线程的创建

- 继承于 Thread 类
    
    1.  创建一个继承于 Thread 类的子类
    2.  重写 Thread 类的 run() 方法
    3.  创建 Thread 类的对象
    4.  通过该对象调用 start() 方法（==一个对象只能创建一个 thread==）
- 实现 Runable 接口
    
    1.  创建一个实现了 Runable 接口的类
    2.  实现 Runable 接口中的 run 方法
    3.  创建实现类的对象
    4.  将此对象作为参数传入 Thread 的构造器
    5.  Thead 类的对象，调用 start 方法
- 实现 Callable 接口
    
    1.  重写 call 方法
    2.  实例化 FutureTask 类
    3.  new 一个新线程，将 FutureTask 作为参数
    4.  使用 FutureTask.get() 方法，取得 call方法 返回值
    
    ```java
    public class NumThread implements Callable {
        @Override
        public Object call() throws Exception {
            int sum = 0;
            for (int i = 0; i <= 100; i++) {
                if (i % 2 == 0) {
                    System.out.println(i);
                    sum += i;
                }
            }
            return sum;
        }
    
        public static void main(String[] args) {
            NumThread numThread = new NumThread();
            FutureTask futureTask = new FutureTask(numThread);
            new Thread(futureTask).start();
            try {
                Object sum = futureTask.get();
                System.out.println("sum: "+sum);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    
    }
    ```
    
- 使用线程池
    
    ```java
    ExecutorService executorService = Executors.newFixedThreadPool(10);
    executorService.execute(Runnable runnable);
    executorService.submit(Callable callable);
    executorService.shutdown();
    ```
    

## 线程的调度

- MAX_PRIORITY
- MIN_PRIORITY
- NORM_PRIORITY
- getpriority获取当前线程优先级
- setPriority设置当前线程优先级

## 线程的生命周期

- 新建：当一个 Thread 类或其子类的对象被声明并创建时，新生的线程对象处于新建的状态
- 就绪：处于新建状态的线程被 start() 后，将进入线程队列等待CPU事件片，此时它已具备了运行的条件，只是没有分配到CPU资源
- 运行：当就绪的线程被调用并获得CPU资源时，便进入运行状态， run() 方法定义了线程的操作和功能
- 阻塞：在某种特殊情况下。被人为挂起或执行输入输出操作时，让出CPU并临时终止自己的执行，进入阻塞状态
- 死亡：线程完成了溻全部工作或线程被提前强制性地中止或出现异常导致结束

## 线程的同步

- 同步代码块

```java
synchronized (object) {
        while (ticket > 0) {
            Thread.sleep(100);
            System.out.println(Thread.currentThread()
                           .getName() + " 余票有: " + (--ticket) + " 张");
        }
}
```

- 同步方法：方法前加 synchronized 关键字
- lock锁：lock锁不存在默认的同步监视器，所以无法使用 wait notify 等方法
- volatile: 用来修饰变量，可以保证变量赋值的原子性和可见性。（不能代替前几种方法）

## 线程的通信

- wait 方法： 阻塞线程，会释放锁（只能使用在同步代码块或同步方法中，lock锁不能用）
- notify/notifyAll 方法: 唤醒线程（只能使用在同步代码块或同步方法中，lock锁不能用）

可以在lock锁中用condition调用 wait 和 notify 方法

```java
Condition condition = lock.newCondition();
condition.wait();
condition.notify();
```

* * *

# Java常用类

> 字符串相关的类
> 
> 日期时间API

## String

- 是声明为 final 的，不可以被继承的
- 实现了 Serializable 接口：表示字符串是支持序列化的
- 实现了 Comparable 接口：表示字符串是可以比较大小的（ compareTo() 方法）
- 内部定义了 ==final char\[\] value== 用于存储字符串数据
- 代表==不可变==的字符串序列
    - 对当前字符串重新赋值时，需要重写指定内存区域赋值，不能使用原有的 value 进行赋值
    - 字符串拼接，也是重写指定内存区域赋值
    - 当使用 replace 方法修改指定字符时，也是重写指定内存区域赋值
- 通过 字面量 的方法给一个字符串赋值，字符串值声明在字符串常量池中
- 字符串常量池中不会存储相同内容的字符串的

### String 的实例化方式

1.  通过字面量的方式：数据声明在方法区的常量池中
2.  通过 new + 构造器的方式：数据声明在堆空间中，char 数组在常量池中

==s.inter() 方法，返回常量池中已经存在的“字符串”==

## StringBuffer 和 StringBuilder

> 可变的字符序列
> 
> 底层也使用 char\[\] 存储
> 
> StringBuffer 是线程安全的，效率低
> 
> StringBuilder 效率高

- StringBuffer 的常用方法
    1.  append(xxx)：用于字符串拼接
    2.  delete(int start , int end)：删除指定位置的内容
    3.  replace( int start ,int end ,String str)：把 \[start,end) 替换为 str
    4.  insert(int offset ，xxx)：在指定位置插入xxx
    5.  reverse()：把当前字符串序列逆转
    6.  setCharAt(int n, char ch)：把指定位置内容替换为 ch

* * *

# 日期和时间API

- System.currentTimeMillis() : 用来返回当前时间与 1970/1/1 0:0:0 之间的以毫秒为单位的时间差
    
- java.util.Date 类
    
    - toString() 方法 : 显示当前的年/月/日 时:分:秒
    - getTime() 方法 : 用来返回当前时间与 1970/1/1 0:0:0 之间的以毫秒为单位的时间差
    - new Date() : 构造当前时间的构造器
    - new Date(long date) : 构造指定时间构造器(与 1970/1/1 0:0:0 之间的以毫秒为单位的时间差)
- java.sql.Date 类
    
    - new Date(long date) : 构造指定时间构造器
        
    - 将 java.util.Date 转换为 java.sql.Date
        
        ```java
        java.util.Date date = new java.util.Date();
        java.sql.Date date2 = new java.sql.Date(date.getTiem));
        ```
        
- java.text.SimpleDateFormat 类(对日期 Date 类的格式化和解析)
    
    - format() 方法 : 格式化(日期 ---> 字符串)
    - parse() 方法 : 解析(字符串 ----> 日期)
    - 用带参构造器实现指定格式的格式化解析 new SimpleFormat("yyyy-MM-dd hh:mm:ss")
- java.util.Calendar 类(抽象类)
    
    - 实例化
        
        - 创建其子类(GregorianCalendar)的对象
        - 调用其静态方法 getInstance() : Calendar.getInstance()
    - 常用方法
        
        - get() :
            
            ```java
            calendar.get(Calendar.DAY_OF_MONTH);	//获取当前这个月的第几天
            calendar.get(Calendar.DAY_OF_YEAR);		//获取当前这一年的第几天
            ```
            
        - set()
            
            ```java
            calendar.set(Calendar.DAY_OF_MONTH);	//设置当前为这个月的第几天
            ```
            
        - add()
            
            ```java
            calendar.add(Calendar.DAY_OF_MONTH,3);	//在当前为这个月的第几天基础上加上3天
            calendar.add(Calendar.DAY_OF_MONTH,-3);	//在当前为这个月的第几天基础上减去3天
            ```
            
        - getTime() :日历类 ---> Data
            
            ```java
            Data date = calendar.getTime();
            ```
            
        - setTime() : Data ---> 日历类
            
            ```java
            Date date = new Date();
            calendar.setTime(date);
            ```
            
- LocalDate、LocalTime、LocalDateTime (不可变性)
    
    - 实例化
        
        - now()
            
            ```java
            LocalDate localDate = LocalDate.now();
            LocalTime localTime = LocalTime.now();
            LocalDateTime localDateTime = LocalDateTime.now();
            ```
            
        - of()
            
            ```java
            LocalDateTime of = LocalDateTime.of(2020, 11, 4, 9, 34);
            ```
            
    - get 方法
        
        - getDayOfMonth() : 这个月的第几天(几号)
        - getDayOfWeek() : 星期几
        - getMonth() : 月份
        - getMonthValue() : 月份(数字)
        - getMinute() : 分钟
- instant (瞬时)
    
    - 实例化
        
        - now() 方法 : (static) 获取一个 instant 的实例(中时区的时间)
            
        - atOffset() 方法 : 设置时区偏移量
            
            ```java
            instant.atOffset(ZoneOffset.ofHours(8));	//设置时区为东八区
            ```
            
        - toEpochMilli() 方法 : 获取自1970年1月1日0时0分0秒 开始的毫秒数
            
- DateTimeFormatter (格式化 或 解析 日期 和 时间)
    
    - 实例化
        
        - 预定义的方式：
            
            ```java
            DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ISO_LOCAL_DATE_TIME;
            ------------------------------
            DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ISO_LOCAL_DATE;
            ------------------------------
            DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ISO_LOCAL_TIME;
            ```
            
        - 本地化格式：
            
            ```java
            DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.SHORT);
            -----------------------------
            DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.MEDIUM);
            -----------------------------
            DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.LONG);
            ```
            
        - 自定义的格式：
            
            ```java
            DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy-MM-dd hh:mm:ss");
            ```
            
    - 格式化 和 解析
        
        ```java
        // 格式化 日期 -> 字符串
        String format = dateTimeFormatter.format(localDateTime);
        
        // 	解析 	字符串 -> 日期
        TemporalAccessor parse = dateTimeFormatter.parse(format);
        ```
        

* * *

# java比较器

> 对象进行 \> 或 < 操作
> 
> Comparable 接口

## 自然排序 实现 Comparable 接口

- 实现 Comparable 接口：自定义类想要排序，需要实现接口
- 重写了 compareTo() 方法：在方法内指明了如何排序
- 大于返回 +
- 小于返回 -
- 等于返回 0

## 定制排序 实现Comparator接口

> 当前元素的类型没有实现 Comparable 接口而又不方便修改代码
> 
> 或者实现了,但是排序规则不适合当前的操作

```java
String[] arr = new String[]{"a", "b", "c", "d"};
Arrays.sort(arr, new Comparator<String>() {
    @Override
    public int compare(String o1, String o2) {
        return -o1.compareTo(o2);
    }
});
System.out.println(Arrays.toString(arr));
```

# 枚举类

> 如何自定义枚举类
> 
> 如何使用关键字 enum 定义枚举类
> 
> Enum 类的主要方法
> 
> 实现接口的枚举类

## 自定义枚举类

- jdk5.0 之前
    
    ```java
    class Season{
        //  声明Season对象的属性（private final）
        private final String seasonName;
        private final String seasonDesc;
    
        // 私有化构造器
        private Season(String seasonName,String seasonDesc){
            this.seasonName = seasonName;
            this.seasonDesc = seasonDesc;
        }
    
        //  提供当前枚举类的多个对象
        public final static Season SPRING = new Season("春天","春暖花开");
        public final static Season SUMMER = new Season("夏天","春暖花开");
        public final static Season AUTUMN = new Season("秋天","春暖花开");
        public final static Season WINTER = new Season("冬天","春暖花开");
    
        //  获取枚举类的属性
        public String getSeasonName() {
            return seasonName;
        }
    
        public String getSeasonDesc() {
            return seasonDesc;
        }
    }
    ```
    
- jdk5.0 之后
    
    ```java
    enum Num{
    //    1.提供枚举类的对象，多个对象中间用逗号隔开，末尾用分号隔开
        ONE(1),
        TWO(2),
        THREE(3);
    
    //    2.声明类的对象：private final
        private final int num;
    
    //    3.私有化构造器
        private Num(int num){
            this.num = num;
        }
    
    //      获取类属性
        public int getNum() {
            return num;
        }
    }
    ```
    
    使用 enum 关键字定义枚举类，默认继承于 java.lang.Enum 类
    

## Enum 类的主要方法

- values() 方法 : 返回一个数组用于存储枚举类对象名
    
    ```java
    Thread.State[] values = Thread.State.values();
    for (int i = 0; i < values.length; i++) {
        System.out.println(values[i]);
    }
    ```
    
- toString() 方法 : 打印枚举类的对象名
    
- valueOf(String objName) 方法 ：返回枚举类中 对象名 是 objname 的对象
    
    ```java
    Num num = Num.valueOf("TWO");
    System.out.println(num.toString());
    ```
    

## 使用 enum 关键字定义的枚举类实现接口的情况

- 情况一 ：实现接口， 在 enum 类中实现抽象方法
    
- 情况二 ：enum 类中每个对象，分别实现抽象方法
    
    ```java
    enum Num implements Info {
        ONE(1){
            @Override
            public String show() {
                return "一";
            }
        },
        TWO(2){
            @Override
            public String show() {
                return "二";
            }
        },
        THREE(3){
            @Override
            public String show() {
                return "三";
            }
        };
        private final int num;
    
        private Num(int num) {
            this.num = num;
        }
    
        @Override
        public String toString() {
            return "Num{" +
                    "num=" + num +
                    '}';
        }
    }
    
    interface Info {
        String show();
    }
    ```
    

* * *

# 注解(Annotation)

> 生成文档的相关注解
> 
> 在编译时进行格式检查（JDK内置的三个基本注解）
> 
> 跟踪代码依赖性，实现替代配置文件功能

## 自定义注解

- 声明为 ： @interface
    
    ```java
    public @interface Myannotation{
        
    }
    ```
    
- 内部定义成员，通常使用value表示
    
    ```java
    String value() default "hello";
    -------------------------------------
    String[] value() default {"hello","a","s"};
    ```
    

## JDK提供的元注解（对现有注解修饰的注解）

- Retention ：指定所修饰的 Annotation 的生命周期：SOURCE / CLASS(默认行为) / RUNTIME
    
    只有声明为 RUNTIME 的注解才能通过反射获取
    
- Target : 指定所修饰的 Annotation 可以使用的位置,默认修饰所有内容
    
- Documented : 用于指定被该元 Annotation 修饰的 Annotation 类将被 javadoc 工具提取成文档;默认情况下
    
    javadoc 是不包括注解的(==Retention 必须为 RUNTIME==)
    
- Inherited : 所修饰的的 Annotation 将具有==继承性==
    

## 通过反射获取注解信息

## JDK8 中注解新特性

- 可重复注解
    - 在 MyAnnotation 上声明 @Repeatable ，成员值为 MyAnnotations.class
    - MyAnnotation 的 Target 和 Retention 和 MyAnnotation 相同
- 类型注解
    - TYPE_PARAMENTER : 表示该注解可以写在类型变量的声明语句中（泛型）
    - TYPE_USE ：表示该注解可以写在使用类型的任何语句中

* * *

# 集合

> 集合 和 数组 都是对多个数据进行存储操作的结构,简称 Java 容器(==内存存储,不涉及持久化存储==)
> 
> 数组 声明后无法修改其 长度；对数组进行 添加 、删除 、插入等操作非常不便，同时效率不高

## Collection: 单列集合，用来存储一个一个的对象

> List ：有序可重复的数据 （动态数组）
> 
> Set ：无序的，不可重复的数据

- Collection 接口中的方法：
    - add(Object e) : 添加元素 e
    - size() : 获取集合元素个数
    - addAll() : 添加另外一个Collection 的元素到 当前Collection
    - clear() : 清空集合元素
    - isEmpty() : 判断当前集合元素是否为空
    - contains(Object obj) : 判断当前集合是否包含 obj ,包含返回 true ,否则返回 false ==(判断的是内容,不是地址,调用equals() 方法)==
    - containsAll(Collection coll) : 判断coll 中的元素是否都在当前集合中 。
    - remove(Object obj) : 从当前集合中移除obj,==调用equals()方法,自定义对象判断需要重写==
    - removeAll(Collection coll) : 从当前集合中移除 coll 中所有元素
    - retainAll(Collection coll) : 求当前集合 和 coll 集合的交集
    - equals(Collection coll) : 比较两个集合是否相等 ,==调用equals()方法,自定义对象判断需要重写==
    - hashCode() : 返回当前集合的哈希值
    - toArray() : 将集合转换为数组
    - iterator() : 返回Iterator接口的实例,用于遍历集合元素

## Iterator : 迭代器接口（遍历Collection）

- next() : 获取集合下一个元素
    
- hasNext() : 判断集合是否有下一个元素
    
    ```java
    while (iterator.hasNext()) {
        System.out.println(iterator.next());
    }
    ```
    
- remove() : 移除集合中的元素
    

## foreach循环 ：增强for循环（遍历集合与数组）

```java
List list = new ArrayList();
list.add(1);
list.add("sdsfs");
list.add(new String[]{"1231", "1231"});

for (Object object : list) {
    System.out.println(object);
}
```

## List接口 ：Collection的子接口（动态数组）

- ArrayList ：List接口的主要实现类；线程不安全的，执行效率高；底层使用Object\[\] 存储
    
- LinkList ：对于频繁的插入删除操作，使用LinkList 比 ArrayList效率高；底层使用双向链表存储
    
- Vector ：作为List接口的古老实现类；线程安全的，执行效率低；底层使用Object\[\] 存储
    
- 常用方法
    
    - add(int index,Object obj) : 将当前obj 添加到 index 位置
    - addAll(int index，collection eles)：从index位置开始将eles中的所有元素添加到 当前list中
    - get(int index)：获取指定index位置的元素
    - indexOf(Object obj)：返回obj在当前集合中首次出现的位置
    - lastIndexOf(Object obj)：返回 obj 在当前集合中末次出现的位置
    - remove(int index)：移除指定位置的元素，并返回该元素
    - set(int index，Object obj)：设置指定index位置元素为obj
    - subList(int fromIndex,int toIndex)：返回中 fromIndex 到 toIndex 的子集合

## Set 接口：Collection的子接口（无序、不可重复）

> 无序: 添加元素存储时无序（底层数组+链表），不按数组索引顺序、根据哈希值添加
> 
> 不可重复：保证添加的元素按照 equals() 方法判断时，不能返回true
> 
> 要求：向Set 中添加的元素，其所在类一定要重写 hashCode() 方法 和 equals() 方法

- HashSet：作为 Set 接口的主要实现类：线程安全的：可以存储null
    
    - LinkedHashSet：作为 HashSet 的子类：遍历其内部数据时，可以按照添加的顺序遍历
        
        ==在添加数据的同时，使用双向链表记录添加顺序==
        
- TreeSet：可以按照添加的对象的指定属性，进行排序。
    
    - 向 TreeSet 中添加的数据，要求是相同类的对象
    - 通过 实现 Comparable 接口的 compareTo() 方法实现==自然排序==
        - ==判断两个对象是否相同==的标准为： compareTo() 返回0，不再是qeuals()
    - new TreeSet(com) ,com 为 Comparator 接口的实现类，实现==定制排序==
        - ==判断两个对象是否相同==的标准为： compare() 返回0，不再是qeuals()
    - 使用 红黑树 的数据结构

![](data:image/jpeg;base64,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hpVm168YjibndaOzJyona79XJ/2kX9RqLcE2vV4vVQBERSAiIgCIiAIiIAvHckUTruv09DqdLOS+R3+HCz1nn/b5qG7astCEpyyxV2UDbGntNL5WtmtQ06tG6nVa5jQZQDICMy8P9PJdUHJcst7aXbeq0r3UYGCr0mIzISXbzccThW7Z3a6vrbjBNF1W2OIjLt4PHeDwyqRqwk7Jm3W4fiaMM846FmXq8HNerIaQREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBQ59Y/NTChz6x+aA8REQEyiIgCIiAIiIAiIgCIiAKD2u/Vyf9pF/UapxQe136uT/tIv6jVMdwTa9Xi9VQERFICIiAIiIAiIgPkniuN7R3X6htJekcSOilMDBngGt4cPnzXZcLku12kv0zXZ5twitbf0jH55vPrD+GVr4lNw0OxwOUI4m0t7aGoY4W6XFK5sW+9r8g53iQcDCjTNJWLbELt2aIiRju4jitkXHthZHusIYCGkt4jPNfNLTptXuR0IGnekOHOA9Rva4rR3ksp6Vrl05uq9NTs2m2he06rbALRNE2TB+IBW2sNaBlatFBGMMiYGNHwAwsy6yPBu19AiIhAREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAUOfWPzUwoc+sfmgPEREBMoiIAiIgCIiAIiIAiIgCg9rv1cn/aRf1GqcUHtd+rk/7SL+o1THcE2vV4vVUBERSAiIgCIiAIiIAta9RrahWdXtwslidza4Z+9bK8KEptO6OR65ouj6bt7oegC5bibqTJXkb4O7uj0QCRnichdI0jQaGixblODdJ9aRx3nu+ZPEqm7U7D6fq3lF0PVp7VttnLt3o3gBnRt3m4Hz5rooPBVVOKd0jNUxNapHLOTaPV6vAV6rGAIiIAiIgCIiAIiIAiLzeQHqL53wvQ7KA9REQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBERAEREAREQBQ59Y/NTChz6x+aA8REQEyiIgCIiAIiIAiIgCIiAKD2u/Vyf9pF/UapxQe136uT/tIv6jVMdwTa9Xi9VQERFI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)

* * *

# I/O 流

> I/O 是 input/output 的缩写
> 
> java 中 数据的输入输出操作 都是以"流(stream)"的方式进行
> 
> input : 外部数据 -> 程序
> 
> output : 程序 -> 外部数据

## 流的分类

- 按操作==数据单位==划分：字节流(8 bit)( 非文本数据通常使用 )、字符流(16 bit)
- 按==流向==划分: 输入流、输出流
- 按流的==角色==划分：节点流、处理流(缓冲流、转换流)

## 一、节点流

### 抽象基类（节点流）

| ==抽象基类== | 字节流 | 字符流 |
| --- | --- | --- |
| **输入流** | InputStream | Reader |
| **输出流** | OutputStream | Writer |

### FileReader

```java
try {
    // 1.实例化file对象，指定要操作的文件
    File file = new File("hello.txt");
    //2.用file对象获取 文件输入流
    FileReader fileReader = new FileReader(file);
    //3.数据读入
    //read():返回读入的数据;如果到了文件末尾，返回-1
    int data = fileReader.read();
    while (data != -1) {
        System.out.print(((char) data));
        data = fileReader.read();
    }
    //4.流的关闭操作
    fileReader.close();
} catch (Exception e) {
    e.printStackTrace();
}
```

1.  获取文件路径的方式
    
    - 相对路径：new File("hello.txt") ==相对于整个工程==
    - 绝对路径：new File("D:\\\workspace\\\text\\\hello.txt") ==文件实际所在位置==
2.  在==关闭==之前加 try catch ==保证流一定可以关闭==
    
3.  read() 方法的重载：
    
    - read(char\[\] chars) ==(字符流是 char\[\] ，字节流是 byte\[\])==：返回每次读入数组中字符的个数，如果读到末尾，返回-1
        
        ```java
        char[] chars = new char[2];
        int len = fr.read(chars);	//每次读入的数据量，最多是char[]的length
        while (len != -1) {
            for (int i = 0; i < len; i++) {		//每次读入多少，就循环多少
                System.out.print(chars[i]);
            }
            len = fr.read(chars);
        }
        ```
        

### FileWriter

1.  输出操作 “文件” 是可以不存在的。
    
    - 如果不存在，在输出的过程中会自动创建
        
    - 如果存在：
        
        - new FileWriter(file\_for\_write, true) ：在原有文件基础上追加
        - new FileWriter(file\_for\_write, false)：覆盖原有文件

```java
while (len != -1) {
    fos.write(chars, 0, len);	//直接读入 char数组的 0～len
    len = fis.read(chars);
}
```

## 二、缓冲流

> 提高流的读出，写入的速度

### 抽象基类（缓冲流）

| ==抽象基类== | 字节流 | 字符流 |
| --- | --- | --- |
| **输入流** | BufferedInputStream | BufferedReader |
| **输出流** | BufferedOutputStream | BufferedWriter |

```java
BufferedInputStream bufferedInputStream = null;
BufferedOutputStream bufferedOutputStream = null;

try {
    //创建文件
    File file_for_read = new File("E:\\学习\\IO流\\【尚硅谷】Java基础全套教程,JAVA零基础入门必备,适合初学者的完整视频 								(宋红康主讲)\\585.583.尚硅谷_IO流-IO流概述与流的分类(Av48144058,P585).mp4");
    File file_for_write = new File("C:\\Users\\17286\\Desktop\\1.mp4");

    //初始化流
    FileInputStream fileInputStream = new FileInputStream(file_for_read);
    FileOutputStream fileOutputStream = new FileOutputStream(file_for_write);

    bufferedInputStream = new BufferedInputStream(fileInputStream);
    bufferedOutputStream = new BufferedOutputStream(fileOutputStream);

    //读写操作
    byte[] bytes = new byte[1024];
    int len = bufferedInputStream.read(bytes);
    while (len != -1) {
        bufferedOutputStream.write(bytes, 0, len);
        len = bufferedInputStream.read(bytes);
    }
} catch (Exception e) {
    e.printStackTrace();
}

    //流的关闭 只需要关闭外层的流，因为关闭外层流 会自动关闭内层的流
if (bufferedInputStream != null) {
    try {
        bufferedInputStream.close();
    } catch (Exception e) {
        e.printStackTrace();
    }
}
if (bufferedOutputStream != null) {
    try {
        bufferedOutputStream.close();
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```

## 三、转换流(属于 字符流)

> 提供了字节流 和 字符流 的转换
> 
> ==inputStreamReader==：将 ==字节的输入流== 转化为 ==字符的输入流==
> 
> ==outputStreamWriter==：将 ==字符的输出流== 转化为 ==字节的输出流==

1.  解码：字节、字节数组——>字符、字符串
    
    编码：字符、字符串——>字节、字节数组
    

```java
FileInputStream fileInputStream = new FileInputStream("helloworld.txt");
//参数二 指明了字符集，具体使用哪个字符集，取决于文件保存时的字符集
InputStreamReader inputStreamReader = new InputStreamReader(fileInputStream, "UTF-8");
```

## 三、标准的输入输出流

- ==System.in==：标准的输入流，默认从键盘输入
- ==System.out==：标准的输出流，默认从控制台输出
- ==System类的 setIn(InputStream is) / setOut(PrintStream ps) 方法==重新指定输入输出的流

## 四、打印流

> printStream
> 
> printWriter
> 
> 都是输出流

## 五、数据流

> DataInputStream
> 
> DataOutputStream
> 
> 作用： 方便操作 JAVA 中的基本数据类型 和 String