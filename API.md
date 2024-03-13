# 一、字符串

## 1.1 字符串的基本操作

### 1.1.1 翻转字符串

```java
StringBuilder sb = new StringBuilder();
sb.reverse();
```

### 1.1.2 删除字符最后一个元素

```java
sb.deleteCharAt(sb.length() - 1);
```
### 1.1.3 将字符串转为字符数组

```java
char[] charArray = s.toCharArray();
```

### 1.1.4 将字符数组转为字符串
```java
char[] charArray = {'h', 'e', 'l', 'l', 'o'};
String str = String.valueOf(charArray);

System.out.println(str); // 输出 "hello"
```

### 1.1.5 将数字转为字符串
```java
int number = 123;
String str1 = String.valueOf(number);
String str2 = Integer.toString(number);

System.out.println(str1); // 输出 "123"
System.out.println(str2); // 输出 "123"

```

### 1.1.6 将字符串转为数字
```java
String str = "123";
int number = Integer.parseInt(str);
System.out.println(number); // 输出 123
```
# 二、HashMap

## 2.1 HashMap初始化

```java
Map<Integer, String> map = new HashMap<>(){{
   put(2, "abc");
   put(3, "def");
   put(4, "ghi");
   put(5, "jkl");
   put(6, "mno");
   put(7, "pqrs");
   put(8, "tuv");
   put(9, "wxyz");
}};
```

# 三、链表
## 3.1 在指定下标插入元素
```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<Integer> linkedList = new LinkedList<>();

        // 添加一些元素到链表中
        linkedList.add(1);
        linkedList.add(2);
        linkedList.add(3);
        linkedList.add(4);

        // 在指定下标处插入元素
        int index = 2; // 指定的下标
        int element = 99; // 要插入的元素
        linkedList.add(index, element);

        // 打印插入元素后的链表
        System.out.println("链表插入元素后： " + linkedList);
    }
}

//链表插入元素后： [1, 2, 99, 3, 4]
```

## 3.1 将链表转为数组

### 3.1.1 将链表转为一维数组
```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        LinkedList<Integer> list = new LinkedList<>();
        list.add(1);
        list.add(2);
        list.add(3);

        Integer[] array = list.toArray(new Integer[list.size()]);

        // 打印转换后的数组
        for (int i = 0; i < array.length; i++) {
            System.out.println(array[i]);
        }
    }
}

```
### 3.1.2 将链表转为二维数组
```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) {
        LinkedList<int[]> que = new LinkedList<>();
        que.add(new int[]{1, 2});
        que.add(new int[]{3, 4});
        que.add(new int[]{5, 6});

        int[][] array = que.toArray(new int[que.size()][]);

        // 打印转换后的二维数组
        for (int i = 0; i < array.length; i++) {
            System.out.println(Arrays.toString(array[i]));
        }
    }
}
```

### 3.1.3 使用mapToInt()方法将链表转为一维数组
```java
import java.util.LinkedList;

public class Main {
    public static void main(String[] args) {
        LinkedList<Integer> list = new LinkedList<>();
        list.add(1);
        list.add(2);
        list.add(3);

//        int[] array = list.stream().mapToInt(Integer::intValue).toArray();
        int[] array = list.stream().mapToInt(x->x).toArray();

        // 打印转换后的数组
        for (int i = 0; i < array.length; i++) {
            System.out.println(array[i]);
        }
    }
}

```
**输出结果：**
```
[1, 2]
[3, 4]
[5, 6]
```
# 四、数组
## 4.1 对数组进行自定义排序
### 4.1.1 样例写法
```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) {
        int[][] array = { {3, 2}, {1, 5}, {4, 7}, {2, 4}, {3, 1}, {3, 3} };
        //第一个元素相同，按照第二个元素升序排序
        //第一个元素不同，按照第一个元素升序排序
        //a - b 是升序排列, b - a 是降序排列
        Arrays.sort(array, (a, b)->{
           if(a[0] == b[0]) return a[1] - b[1];
           return a[0] - b[0];
        });
        // 打印排序后的二维数组
        for (int i = 0; i < array.length; i++) {
            System.out.println(Arrays.toString(array[i]));
        }
    }
}
```
**输出结果：**
```
[1, 5]
[2, 4]
[3, 1]
[3, 2]
[3, 3]
[4, 7]
```
### 4.1.2 完整写法
```java
import java.util.Arrays;
import java.util.Comparator;

public class Main {
    public static void main(String[] args) {
        int[][] array = { {3, 2}, {1, 5}, {4, 7}, {2, 4} };

        // 自定义排序
        Arrays.sort(array, new Comparator<int[]>() {
            @Override
            public int compare(final int[] entry1, final int[] entry2) {
                // 按照每个数组的第一列进行比较
                return Integer.compare(entry1[0], entry2[0]);
            }
        });

        // 打印排序后的二维数组
        for (int i = 0; i < array.length; i++) {
            System.out.println(Arrays.toString(array[i]));
        }
    }
}

```

### 4.1.3 Lambda表达式写法
```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[][] array = { {3, 2}, {1, 5}, {4, 7}, {2, 4} };

        // 自定义排序
        Arrays.sort(array, (entry1, entry2) -> Integer.compare(entry1[0], entry2[0]));

        // 打印排序后的二维数组
        for (int i = 0; i < array.length; i++) {
            System.out.println(Arrays.toString(array[i]));
        }
    }
}
```

### 4.1.4 二维数组排序（比较器写法）
```java
import java.util.Arrays;
import java.util.Comparator;

public class Main {
    public static void main(String[] args) {
        int[][] array = { {3, 2}, {1, 5}, {4, 7}, {2, 4}, {3, 1}, {3, 3} };

        // 自定义排序
        Arrays.sort(array, new Comparator<int[]>() {
            @Override
            public int compare(final int[] entry1, final int[] entry2) {
                // 首先按照第一个字段进行比较
                int result = Integer.compare(entry1[0], entry2[0]);
                // 如果第一个字段相同，则按照第二个字段从小到大进行比较
                if (result == 0) {
                    result = Integer.compare(entry1[1], entry2[1]);
                }
                return result;
            }
        });

        // 打印排序后的二维数组
        for (int i = 0; i < array.length; i++) {
            System.out.println(Arrays.toString(array[i]));
        }
    }
}
```

_注意：_

Integer.compare(int x, int y) 是一个静态方法，用于比较两个整数的大小。它返回一个整数值，表示 x 和 y 的相对顺序。

如果 x 小于 y，则返回一个负数。
如果 x 等于 y，则返回 0。
如果 x 大于 y，则返回一个正数。
这个方法的签名如下：

```java
public static int compare(int x, int y)
```
Integer.compare() 方法可以用于对整数进行比较，并且它避免了使用减法来进行比较，因此更加安全。在某些情况下，直接使用减法进行比较可能会导致整数溢出的问题，而 Integer.compare() 方法不会出现这样的问题。

此外，Integer.compare() 方法也是 Comparator 接口的默认方法之一，可以用于比较两个整数的大小，例如在排序算法中使用。

### 4.1.5 二维数组排序（Lambda表达式写法）
```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[][] array = { {3, 2}, {1, 5}, {4, 7}, {2, 4}, {3, 1}, {3, 3} };

        // 自定义排序
        Arrays.sort(array, (entry1, entry2) -> {
            // 首先按照第一个字段进行比较
            int result = Integer.compare(entry1[0], entry2[0]);
            // 如果第一个字段相同，则按照第二个字段从小到大进行比较
            return result == 0 ? Integer.compare(entry1[1], entry2[1]) : result;
        });

        // 打印排序后的二维数组
        for (int i = 0; i < array.length; i++) {
            System.out.println(Arrays.toString(array[i]));
        }
    }
}
```

_注意：_

在这种情况下，使用 Integer.compare() 方法和直接使用 - 运算符进行比较的结果是相同的。两种方法都可以用于比较两个整数的大小，返回值表示两个整数的相对顺序。

Integer.compare() 方法是一种更加规范和明确的方式，它会返回一个整数，表示两个整数的比较结果。如果第一个整数小于第二个整数，返回负值；如果第一个整数等于第二个整数，返回0；如果第一个整数大于第二个整数，返回正值。

使用 - 运算符直接进行比较是一种更加简单的方式，如果 a[1] 大于 b[1]，则会返回一个正数；如果相等，返回0；如果 a[1] 小于 b[1]，则会返回一个负数。

两种方式的选择取决于你的个人偏好和代码的可读性。通常来说，使用 Integer.compare() 方法更容易理解，尤其是对于其他人阅读你的代码时更为友好。

## 4.2 初始化数组元素
```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) {
        int[] hash = new int[27];
        //在java.util.*中，将数组元素全部初始化为0
        Arrays.fill(hash, 0);
        System.out.println(Arrays.toString(hash));
    }
}
```