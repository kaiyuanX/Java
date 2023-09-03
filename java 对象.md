- [面向对象基础](#面向对象基础)
  - [构造](#构造)
  - [封装性](#封装性)
  - [JavaBean 实体类](#javabean-实体类)
- [常用 API](#常用-api)
  - [import PackageName](#import-packagename)
  - [String](#string)
      - [构造](#构造-1)
      - [方法](#方法)
      - [注意事项](#注意事项)
  - [StringBuilder](#stringbuilder)
  - [ArrayList](#arraylist)
      - [方法](#方法-1)

---

# 面向对象基础

对象实质上是一种特殊的数据结构

任何一个对象都可以包含一些数据，数据属于哪个对象，就由哪个对象来处理

在 java 中用 `class` 来设计对象

- 一个代码文件中，可以写多个 `class` 类，但是只能有一个是 `public` 修饰，且 `public` 修饰的类必须和文件名相同

## 构造

在创建对象时，会调用构造器

也就是说 `new Student()` 就是在执行构造器，当构造器执行完了，也就意味着对象创建成功

用来在创建对象时给对象的属性做一些初始化操作

[格式]()

- 方法名与类名相同
- 没有返回值类型，`void` 都没有
- 没 `return`
- 可以有参数

[注意事项]()

- 如果不写构造器，Java 会自动生成一个无参数构造器
- 定义了有参数构造器，Java 就不再提供空参数构造器，此时建议自己加一个无参数构造器

## 封装性

面向对象很重要的特征[封装性]()

| 可以访问的类 | private | (default) | protected | public |
| ------------ | :-----: | :-------: | :-------: | :----: |
| 同一类       |    √    |     √     |     √     |   √    |
| 同一包中的类 |         |     √     |     √     |   √    |
| 子类         |         |           |     √     |   √    |
| 其他包中的类 |         |           |           |   √    |

## JavaBean 实体类

如下的标准：

- 类中成员变量都 `private`，且对外提供 `getXxx()` `setXxx()`
- 提供无参，带参的构造方法
  - 快捷键：`右键 -> Generate -> Constructor/Getter/Setter`
  - `Ptg To JavaBean`

在实际开发中，实体类仅仅只用来封装数据，而对数据的处理交给其他类来完成，以实现数据和数据业务处理相分离，如下

```java
public class Student {
    private String name;
    prevate double score;
}

public class StudentOpt {
    private Student s;
    public StudentOpt(Student ss){
        this.s = ss;
    }
    // 打印成绩等级
    // 等等其他对 Student 数据操作的函数
}
```


# 常用 API

[API](./assets/JDk_API)

Application Program Interface

别人写好的一些程序，给咱们程序员直接拿去调用

## import PackageName

一个包中可以放多个类文件

调包的条件

- 同一个包下的 `class`，互相可以直接调用
- 当前程序要调用其他包下的 `class`，则必须导包
- 调用 `Java.lang` 包下的 `class`，不需要我们导包的

`import PackageName.*;`
`import PackageName.ClassaName;`

## String

不可变的字符序列

在 `java.lang` 包中

#### 构造

```java
// 1、直接双引号得到字符串对象
String name = "666";

// 2、new String() 创建字符串对象，并调用构造器初始化字符串 
new String();
new String(String s);
new String(char[] s);
new String(byte[] s);
```

#### 方法

```java
// 1、获取字符串的长度
s.length();

// 2、提取字符串中某个索引位置处的字符
char c = s.charAt(1);

// 3、把字符串转换成字符数组
char[] chars = s.toCharArray();

// 4、判断字符串内容，内容一样就返回 true
s1 == s2;  // 这个只能比较地址
s1.equals(s2); 

// 5、忽略大小写比较字符串内容
s1.equalsIgnoreCase(s2);

// 6、截取字符串内容 (包前不包后的)
s1 = s2.substring(beginIndex, endIndex)
s1 = s2.substring(beginIndex);

// 8、把字符串中的某个内容替换成新内容
s2 = s1.replace(oldCharSequence, newCharSequence);

// 9、判断字符串中是否包含某个关键字
s.contains(CharSequence)

// 10、把字符串按照某个指定内容分割成多个字符串，放到一个字符串数组中返回给我们
split(String regex, int limit)
- regex : 定界正则表达式
- limit : 控制模式应用的次数
```

#### 注意事项


1. String 类的对象是不可变的对象
   - `s = "fuck"` 实际上是新创建了一个 `String` 再把这个它赋给 `s`
   - 只是 `s` 指向的地址变了，`s` 指向的原地址的内容没变

2. 两种构造的区别
   - 通过 `new` 方式创建字符串对象，每 `new` 一次都会产生一个新的对象放在堆内存中
   - 以 `" "` 方式写出的字符串对象，会在堆内存中的字符串常量池中存储，且相同内容的字符串只存储一份

```java
s1="abc",s2="abc";
s1 == s2 // true
```

## StringBuilder

线程不安全的可变的字符序列，高效地做字符串拼接


在 `java.lang` 中

```java
StringBuilder sb = new StringBuilder()

sb.append(sth);

// 转换
sb.toString();
StringBuilder sb = new StringBuilder(String s)
```

> StringBuffer 线程安全的可变的字符序列


## ArrayList

ArrayList 是大小可变的数组

`java.util`

#### 方法

想要使用 ArrayList 存储数据，并对数据进行操作：

- 创建 ArrayList 容器对象
  - 空参数构造方法 `ArrayList<String> a = new ArrayList()`

- 第二步：调用 ArrayList 类的常用方法对容器中的数据进行操作。常用方法如下：

```java
// 1、创建一个 ArrayList 的集合对象
// ArrayList<String> list = new ArrayList<String>();
// 从 jdk_7 开始支持下面的构造
ArrayList<String> list = new ArrayList<>();

list.add("xxx");

// 2、往集合中的某个索引位置处添加一个数据
list.add(n, "xxx");

// 3、根据索引获取集合中某个索引位置处的值
list.get(n);

// 4、获取集合的大小
list.size();

// 5、根据索引删除集合中的某个元素值，返回被删除的元素值
list.remove(n);

// 6、删除某个元素值，删除成功会返回 true
list.remove("Java");

// 7、修改某个索引位置处的数据，修改后会返回原来的值给我们
list.set(n, "xxx");
```
