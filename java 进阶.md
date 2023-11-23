- [异常](#异常)
  - [异常处理](#异常处理)
  - [自定义异常](#自定义异常)
- [泛型](#泛型)
  - [自定义泛型类](#自定义泛型类)
  - [自定义泛型接口](#自定义泛型接口)
  - [泛型方法](#泛型方法)
  - [泛型限定](#泛型限定)
- [枚举](#枚举)
  - [枚举深入](#枚举深入)
  - [应用场景](#应用场景)
- [可变参数](#可变参数)


---

# 异常

![1667313423356](assets/1667313423356.png)

## 异常处理

IDEA 对异常可能产生的地方 `alt + enter`

- 第一种处理方式是，对异常进行 `try...catch` 捕获处理
  - IDEA `ctrl + alt + t` 生成

```java
try {

    test1();

} catch (FileNotFoundException e) {

    // 一些常用方法
    e.getMessage();
    e.printStackTrace();

} catch (ParseException e) {

    ...

}

// 或者 catch(Exception e)
```

- 第二种处理方式是：在main方法中对异常进行捕获，并尝试修复

```java
public static void test() throws FileNotFoundException {
    InputStream is = new FileInputStream("Path");
}
```

注意：子类不能 `throws` 比父类更大的异常

## 自定义异常

- 先写一个异常类 AgeIllegalException，继承 Exception

```java
public class AgeIllegalException extends Exception{
    public AgeIllegalException() {
    }

    public AgeIllegalException(String message) {
        super(message);
    }
}
```

- 一个测试类

```java

try {
    ...
} catch (AgeIllegalException e) {
    ...
}

public static void saveAge(int age){
    if(...){
        
    }else {
        // throw 抛出去这个异常对象
        throw new AgeIllegalRuntimeException("age is illegal");
    }
}
```


1. 自定义异常类继承 Excpetion，则是编译时异常
	特点：必须在方法上使用 throws 声明，强制调用者处理
	
2. 自定义异常类继承 RuntimeException，则运行时异常
	特点：不需要在方法上用 throws 声明



# 泛型

用一个 `<E>` 表示元素的数据类型

创建对象时，`new ArrayList<String>` 表示 String 类型，`new ArrayList<Integer>` 表示元素为 Integer 类型

泛型只支持引用数据类型，不支持基本数据类型

## 自定义泛型类

格式如下

```java
// 这里的 <T,W> 其实指的就是类型变量，可以是一个，也可以是多个
// T, W 是标识符，随便起名

public class Name<T,W>{
    
}
```

```java
public class MyArrayList<E>{
    private Object[] array = new Object[10];
    //定一个索引，方便对数组进行操作
    private int index;
    
    //添加元素
    public void add(E e){
        array[index]=e;
        index++;
    }
    
    //获取元素
    public E get(int index){
        return (E)array[index];
    }
}
```

## 自定义泛型接口

```java
public interface Name<E>{
    
}
```

```java
// 确定为 String
public class A implements Name<String>{

}

// 不确定
public class B<E> implements Name<E>{

}
```

## 泛型方法

```java
// <T> 表示这是一个泛型方法

public static <T> T test(T t){
    return t;
}
```

## 泛型限定

泛型限定的意思是对泛型的数据类型进行范围的限制

- `<?>` 表示任意类型
- `<? extends className>` 表示指定类型或者指定类型的子类
- `<? super className>` 表示指定类型或者指定类型的父类

```java
// test1 加了 <?> 才能接任何 ArrayList
public static void test1(ArrayList<?> list){
    
}

// 接 Car 和 Car 的子类
public static void test2(ArrayList<? extends Car> list){
    
}
```


# 枚举

格式

```java
public enum Name{
    item1,item2,item3;
}
```

```java
// test

public enum A{
    X,Y,Z;
}

public class Test{
    public static void main(String[] args){
        // 获取枚举 A 类的枚举项
        A a1 = A.X;
        A a2 = A.Y;
        A a3 = A.Z;
    }
}
```

- 枚举类 A 是用 class 定义的，说明枚举确实是一个类，而且 X，Y，Z 都是 A 类的对象
- 每一个枚举项都是被 `public static final` 修饰

## 枚举深入

枚举类中可以定义构造器、成员变量、成员方法

但是一般不会这么写，如果你真要这么干的话，到不如直接写普通类来的直接



## 应用场景

枚举一般表示一组信息，然后作为参数进行传输


```java
public class Constant{
    BOY,GRIL
}
```

```java
public class Test{
    public static void main(String[] args){
        //调用方法，传递男生
        provideInfo(Constant.BOY);
    }
    
    public static void provideInfo(Constant c){
        switch(c){
            case BOY:
                System.out.println("展示一些信息给男生看");
                break;
            case GRIL:
                System.out.println("展示一些信息给女生看");
                break;
        }
    }
}
```

枚举一般表示几个固定的值，然后作为参数进行传输


# 可变参数

形参列表处让方法接收多个同类型的实际参数

可变参数在方法内部，本质上是一个数组

```java
public class ParamTest{
    public static void main(String[] args){
        // 不传递参数，nums 长度则为 0, 打印元素是[]
        test();	
        
        // 传递 3 个参数，nums 长度为 3，打印元素是 [10, 20, 30]
        test(10,20,30); 
        
        // 传递一个数组，下面数组长度为 4，打印元素是 [10,20,30,40] 
        int[] arr = new int[]{10,20,30,40}
        test(arr); 
    }
    
    public static void test(int... nums){
        System.out.println(nums.length);
        System.out.println(Arrays.toString(nums));
    }
}
```

注意：

- 一个形参列表中，只能有一个可变参数
- 一个形参列表中如果多个参数，可变参数需要写在最后

```java
void test(int... nums1, String... nums2);    // wrong
void test(int... nums, int age);             // wrong
```