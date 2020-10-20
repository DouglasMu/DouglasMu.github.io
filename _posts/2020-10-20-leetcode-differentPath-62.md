---
layout: post
title:  leetcode-62-不同路径
categories: leetcode
tags:  leetcode
author: Keyon
---
* content
{:toc}

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/unique-paths

输入: m = 3, n = 2
输出: 3
解释:
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向右 -> 向下
2. 向右 -> 向下 -> 向右
3. 向下 -> 向右 -> 向右


思路：使用动态规划算法，首先定义一个矩阵d[i][j]来存储初始状态 因为只能向下走或者是向右走，所以d[i][j]=d[i-1][j]+d[i][j-1],d表示可能的路径
初始化为第0行和第0列都为1

```python

class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        dp = [[0] * n for _ in range(m)]
        for i in range(n):
            dp[0][i] = 1
        for i in range(m):
            dp[i][0] = 1
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1]
        return dp[m - 1][n - 1]

    # 优化代码
    # 因为每格的值仅仅和左侧与上一行的值相关，因此我们只要维护一行的值即可，这样可以将空间复杂度降到O(N)
    
    def uniquePaths1(self, m: int, n: int) -> int:
        matrix = [1 for i in range(n)]
        for k in range(1, m):
            for j in range(1, n):
                matrix[j] += matrix[j - 1]
        return matrix[-1]

    # 使用排列组合进行求解
    # 机器人一定会走m+n-2步，即从m+n-2中挑出m-1步向下走就行
    # 注意到这是一个组合问题，直接计算C(m+n-2,m-1)即可。时间复杂度为O(n)，空间复杂度O(1)
    
    def uniquePaths2(self, m: int, n: int) -> int:
        def factor(num):
            if num < 2:
                return 1
            res = 1
            for i in range(1, num + 1):
                res *= i
            return res

        ans = factor(m + n - 2) // (factor(m - 1) * factor(n - 1))
        return ans


if __name__ == '__main__':
    solution = Solution()
    print(solution.uniquePaths(3, 2))
    print(solution.uniquePaths1(3, 2))
    print(solution.uniquePaths2(3, 2))
```