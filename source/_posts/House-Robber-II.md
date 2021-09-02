---
title: House Robber II
date: 2021-04-15 13:41:31
tags:
    - algorithm
    - Leetcode
categories:
    - Data structure and algorithm
---

![House-robber](https://github.com/Corner-MVP/hexo-picture/blob/main/house-robber.jpg?raw=true)

# 213. House Robber II
---

**Description**

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle**. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and it **will automatically contact the police if two adjacent houses were broken into on the same night.**

Given an integer array `nums` representing the amount of money of each house, return the maximum amount of money you can rob tonight **without alerting the police.**

**Input and output**

```
Input: nums = [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.
```

**Solution**

It is a classical **dp** question, if all houses are not arranged in a circle(Leetcode 198). Making a list `dp` and `dp[i]` means most money can be achieved in position `i`. From the description, the state transition equation is:

<center>{% mathjax %} dp[i] = max(dp[i-2] + nums[i], dp[i-1]) {% endmathjax %}</center>

and the boundary condition is:

<center>{% mathjax %}
dp[i]=
\begin{cases}
nums[0], i = 1 \\
max(nums[0], nums[1]), i = 2
\end{cases}
{% endmathjax %}</center>

And in order to avoid stolen the first, and the last house at the same time, we can split this question into two conditions. When stealing the first house, the last one cannot be stolen, thus, the range is the first to the last second house. When stealing the last house, the first one cannot be stolen, therefore, the range is the second to the last house.

If the length of array is `n`, the first condition's range is `[0, n-2]` and the other's range is `[1, n-1]`. After determining the ranges, the method mentioned above can be used to get highest stolen value respectively. The maximum value is the maximum total amount that can be stolen in `n` houses


```
class Solution:
    def rob(self, nums: List[int]) -> int:
        if not nums:
            return 0
        elif len(nums) == 1:
            return nums[0]
        return max(self.rob2(nums[1:]), self.rob2(nums[: len(nums) - 1]))
    
    def rob2(self, nums):
        if not nums:
            return 0
        elif len(nums) == 1:
            return nums[0]

        first, second = nums[0], max(nums[0], nums[1])

        for i in range(2, len(nums)):
            first, second = second, max(second, first + nums[i])

        return max(first, second)
```


**Time and space complexity**

Time complexity: `O(n)`, `n` is the length of nums, it need traverse array twice.

Space complexity: `O(1)`
