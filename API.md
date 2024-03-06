# 一、字符串

## 1.1 字符串的基本操作

1.1 翻转字符串

```
StringBuilder sb = new StringBuilder();
sb.reverse();
```

1.2 删除字符最后一个元素

```
sb.deleteCharAt(sb.length() - 1);
```

# 二、HashMap

## 2.1 HashMap初始化

```
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