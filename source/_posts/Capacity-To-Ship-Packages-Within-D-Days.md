---
title: Capacity To Ship Packages Within D Days
date: 2021-04-26 22:04:53
tags:
    - algorithm
    - Leetcode
categories:
    - Data structure and algorithm
---

![delivery](https://raw.githubusercontent.com/Corner-MVP/hexo-picture/main/delivery.jpg)

# 1011. Capacity To Ship Packages Within D Days
---

**Description**

A conveyor belt has packages that must be shipped from one port to another within `D` days.

The {% mathjax %}i^{th}{% endmathjax %} package on the conveyor belt has a weight of `weights[i]`. Each day, we load the ship with packages on the conveyor belt (in the order given by `weights`). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within `D` days.

**Input and output**

```
Input: weights = [1,2,3,4,5,6,7,8,9,10], D = 5
Output: 15
Explanation: A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:
1st day: 1, 2, 3, 4, 5
2nd day: 6, 7
3rd day: 8
4th day: 9
5th day: 10

Note that the cargo must be shipped in the order given, so using a ship of capacity 14 and splitting the packages into parts like (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) is not allowed.
```

```
Input: weights = [3,2,2,4,1,4], D = 3
Output: 6
Explanation: A ship capacity of 6 is the minimum to ship all the packages in 3 days like this:
1st day: 3, 2
2nd day: 2, 4
3rd day: 1, 4
```

**Solution**

There exists a lower limit {% mathjax %}x_{res}{% endmathjax %} that when {% mathjax %}x \geq x_{res}{% endmathjax %}, we can deliver packages in `D` days and vice versa. At the same time, {% mathjax %}x_{res}{% endmathjax %} is the result. Therefore, this is a binary search problem. The left boundary is maximum of weights, and the right boundary is total weights. During binary search, we need to judge whether current capacity meets to the day requirement. And we can solve it by greedy algorithm.

```
class Solution:
    def shipWithinDays(self, weights, D):
        
        left, right = max(weights), sum(weights)
        
        while left < right:
            
            mid = left + (right - left) // 2
            
            days, curr = 1, 0
            for weight in weights:
                
                if curr + weight > mid:
                    curr = 0
                    days += 1
                
                curr += weight
            
            if days > D:
                left = mid + 1
            else:
                right = mid
        
        return left
```

# Time and space complexity

Time complexity {% mathjax %}O(nlog\sum w){% endmathjax %}, `n` is the length of array weights. {% mathjax %}\sum w{% endmathjax %} is sum of elements in array weights. The number of times the binary search needs to be performed is {% mathjax %}O(log(\sum w){% endmathjax %}. In every binary search, array need to be traversed and time is `O(n)`. So the total time is {% mathjax %}O(nlog\sum w){% endmathjax %}

Space complexity `O(n)`
