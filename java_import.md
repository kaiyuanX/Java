- [随机数](#随机数)


## 随机数

在 JDK 中提供了一个类叫做 `Random`

```java
// 使用方法跟 Scanner 一样

// 1、导包
import java.util.Random;

public class RandomDemo1 {
    public static void main(String[] args) {

        // 2、创建一个 Random 对象
        Random r = new Random();

        // 3、调用 Random 的方法 nextInt()
        int data = r.nextInt(10); // 得到 [0,9] 的随机数
        System.out.println(data);
    }
}
```
