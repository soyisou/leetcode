# 题目
[337.打家劫舍 III](https://leetcode.cn/problems/house-robber-iii/)

小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为 root 。

除了 root 之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果 两个直接相连的房子在同一天晚上被打劫 ，房屋将自动报警。

给定二叉树的 root 。返回 在不触动警报的情况下 ，小偷能够盗取的最高金额 。



**示例 1:**

![](https://assets.leetcode.com/uploads/2021/03/10/rob1-tree.jpg)

``` 
输入: root = [3,2,3,null,3,null,1]
输出: 7
解释: 小偷一晚能够盗取的最高金额 3 + 3 + 1 = 7
```
**示例 2:**

![](https://assets.leetcode.com/uploads/2021/03/10/rob2-tree.jpg)

``` 
输入: root = [3,4,5,1,3,null,1]
输出: 9
解释: 小偷一晚能够盗取的最高金额 4 + 5 = 9
```


**提示：**

``` 
树的节点数在 [1, 10^4] 范围内
0 <= Node.val <= 10^4
```

# Code1
DP 

动态规划DP五部曲：
1. DP数组及其下标的定义
2. DP数组的初始化
3. 递推公式
4. 遍历顺序
5. 举例推导DP数组

## 代码1
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int rob(TreeNode root) {
        int[] res =  robHandle(root);
        return Math.max(res[0], res[1]);
    }

    public int[] robHandle(TreeNode root){
        if(root == null) return new int[]{0, 0};
        int[] res = new int[2];
        //左边偷或者不偷获取的最大值   
        int[] leftdp = robHandle(root.left);
        //右边偷或者不偷获取的最大值
        int[] rightdp = robHandle(root.right);
        //不偷当前结点
        res[0] = Math.max(leftdp[0], leftdp[1]) + Math.max(rightdp[0], rightdp[1]);
        //偷当前结点
        res[1] = root.val + leftdp[0] + rightdp[0];
        return res;
    }
}
```