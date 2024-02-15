# 题目
[28. 找出字符串中第一个匹配项的下标](https://leetcode.cn/problems/find-the-index-of-the-first-occurrence-in-a-string/description/)

给你两个字符串 haystack 和 needle ，请你在 haystack 字符串中找出 needle 字符串的第一个匹配项的下标（下标从 0 开始）。如果 needle 不是 haystack 的一部分，则返回  -1 。

**示例 1：**
``` 
输入：haystack = "sadbutsad", needle = "sad"
输出：0
解释："sad" 在下标 0 和 6 处匹配。
第一个匹配项的下标是 0 ，所以返回 0 。
```
**示例 2：**
``` 
输入：haystack = "leetcode", needle = "leeto"
输出：-1
解释："leeto" 没有在 "leetcode" 中出现，所以返回 -1 。
```
**提示：**
``` 
1 <= haystack.length, needle.length <= 10^4
haystack 和 needle 仅由小写英文字符组成
```

**相似试题**

[831. KMP字符串](https://www.acwing.com/problem/content/submission/833/)

# 思路
KMP算法

# Code1
双指针算法

具体思路：
1. 反转整个字符串
2. 反转0~k-1字符串
3. 反转k~n-1字符串

时间复杂度:
> O(n+m)，其中 n 是字符串 haystack 的长度，m 是字符串 needle 的长度。我们至多需要遍历两字符串一次。

空间复杂度:
> $O(m)$  其中 m 是字符串 needle 的长度。我们只需要保存字符串 needle 的前缀函数。

```java
class Solution {
    public int strStr(String haystack, String needle) {

        int n = haystack.length(), m = needle.length();
        int[] next = new int[m + 1];
        //next
        for(int i = 2, j = 0; i <= m; i ++){
            while(j != 0 && needle.charAt(i - 1) != needle.charAt(j)) j = next[j];
            if(needle.charAt(i - 1) == needle.charAt(j)) j ++;
            next[i] = j;
        }

        //匹配
        for(int i = 1, j = 0; i <= n; i ++){
            while(j != 0 && haystack.charAt(i - 1) != needle.charAt(j)) j = next[j];
            if(haystack.charAt(i - 1) == needle.charAt(j)) j ++;
            if(j == m){
                return i - m;
            }
        }
        
        //没有匹配项
        return -1;
    }
}
```