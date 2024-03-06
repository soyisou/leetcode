# 题目
[216.组合总和III](https://leetcode.cn/problems/combination-sum-iii/)

找出所有相加之和为 n 的 k 个数的组合，且满足下列条件：

只使用数字1到9
每个数字 最多使用一次
返回 所有可能的有效组合的列表 。该列表不能包含相同的组合两次，组合可以以任何顺序返回。



**示例 1:**

``` 
输入: k = 3, n = 7
输出: [[1,2,4]]
解释:
1 + 2 + 4 = 7
没有其他符合的组合了。
```
**示例 2:**

``` 
输入: k = 3, n = 9
输出: [[1,2,6], [1,3,5], [2,3,4]]
解释:
1 + 2 + 6 = 9
1 + 3 + 5 = 9
2 + 3 + 4 = 9
没有其他符合的组合了。
```
**示例 3:**

``` 
输入: k = 4, n = 1
输出: []
解释: 不存在有效的组合。
在[1,9]范围内使用4个不同的数字，我们可以得到的最小和是1+2+3+4 = 10，因为10 > 1，没有有效的组合。
```

**提示:**

``` 
2 <= k <= 9
1 <= n <= 60
```

# 思路
回溯

# Code1

```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> path = new LinkedList<>();
    public List<List<Integer>> combinationSum3(int k, int n) {
        dfs(k, n, 1);
        return res;
    }
    
    //n表示和，startIdx表示从哪个数字开始选
    void dfs(int k, int n, int startIdx){
        if(path.size() == k){
            if(n == 0){
                res.add(new ArrayList<>(path));
            }
            return;
        }
        for(int i =startIdx; i <= 9; i ++){
            path.add(i);
            //递归
            dfs(k, n - i, i + 1);
            //回溯
            path.removeLast();
        }
    }
}
```

# Code2

```java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    List<Integer> path = new LinkedList<>();
    public List<List<Integer>> combinationSum3(int k, int n) {
        dfs(k, n, 1);
        return res;
    }

    void dfs(int k, int n, int startIdx){
        //剪枝
        if(n < 0) return;
        if(path.size() == k){
            if(n == 0){
                res.add(new ArrayList<>(path));
            }
            return;
        }
        //剪枝
        for(int i =startIdx; i <= 9 - (k - path.size()) + 1; i ++){
            path.add(i);
            dfs(k, n - i, i + 1);
            path.removeLast();
        }
    }
}
```