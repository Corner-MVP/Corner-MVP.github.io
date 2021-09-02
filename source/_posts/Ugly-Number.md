---
title: Ugly Number
date: 2021-04-10 10:12:43
tags: 
    - algorithm
    - Leetcode
categories:
    - Data structure and algorithm
---

# Definition
---

**Ugly number** is a positive number whose prime factors only include 2, 3, and/or 5.

# Leetcode

## 263. Ugly Number
---

**Description**

Given an integer `n`, return true if `n` is an ugly number.

**Input and output**

```
Input: n = 6
Output: true
Explanation: 6 = 2 × 3
```

**Solution**

From the ugly number definition, we can know that the ugly number is combined with at most three factors that are 2, 3 and/or 5. Therefore, every ugly number `n` can be rewritten as {% mathjax %}n = 2^a + 3^b + 5^c {% endmathjax %}and {% mathjax %}a \geq 0, b \geq 0, c \geq 0 {% endmathjax %}.

In order to judge whether target number is ugly number. We  can divisor 2, 3 and 5 until the number cannot be divisor by 2, 3 and 5. If the remaining number equals to 1, it indicates that the target number is ugly number and vice versa.

```
class Solution:
    def isUgly(self, n: int) -> bool:

        if n <= 0: return False

        factors = [2, 3, 5]

        for factor in factors:
            while n % factor == 0:
                n //= factor
        
        return n == 1
```

## 264. Ugly Number II
---

**Description**

Given an integer `n`, return the $n^{th}$ **ugly number**.

**Input and output**

```
Input: n = 10
Output: 12
Explanation: [1, 2, 3, 4, 5, 6, 8, 9, 10, 12] is the sequence of the first 10 ugly numbers.
```

**Solution**

The factors of ugly number are 2, 3 and/or 5, therefore, every ugly number comes from former ugly number multiply by 2, 3 and/or 5. For example, 1 is the first ugly number and 2, 3 and 5 have qualification to be multiplied by 1. Taking the mines one, that is 2 and put 2 into ugly number sequence. 2 lose the qualification to be multiplied by 1 and 2 has qualification to be multiplied by 2. Therefore, 3 and 5 has qualification to be multiplied by 1 and 2 can be multiplied by 2 and then continue to take mines number and so on.

```
class Solution:
    def nthUglyNumber(self, n):

        dp = [0] * (n+1)
        dp[1] = 1
        p2, p3, p5 = 1, 1, 1

        for i in range(2, n+1):

            target = min(dp[p2] * 2, dp[p3] * 3, dp[p5] * 5)
            dp[i] = target
            if target == dp[p2] * 2: p2 += 1
            if target == dp[p3] * 3: p3 += 1
            if target == dp[p5] * 5: p5 += 1

        return dp[n]
```

## 313. Super Ugly Number
---

**Description**

Given an integer `n` and an array of integers primes, return the {% mathjax %} n ^ {th} {% endmathjax %} **super ugly number**.

**Super ugly number** is a positive number whose all prime factors are in the array `primes`.

The {% mathjax %} n ^ {th} {% endmathjax %} **super ugly number** is **guaranteed** to fit in a **32-bit** signed integer.

**Input and output**

```
Input: n = 12, primes = [2,7,13,19]
Output: 32
Explanation: [1,2,4,7,8,13,14,16,19,26,28,32] is the sequence of the first 12 super ugly numbers given primes == [2,7,13,19].
```

**Solution**

The solution is similar with the former one. The only difference is that the factors are not 2, 3 and/or 5, but given primes.

```
class Solution:
    def nthSuperUglyNumber(self, n, primes):

        nums = [1]
        k = len(primse)
        i_index = [0] * k
        for i in range(1, n):
            ugly = min([primes[j] * nums[i_index[j]] for j in range(k)])
            nums.append(ugly)
            for j in range(k):
                if ugly == primes[j] * nums[i_index[j]]:
                    i_index[j] += 1
                
        return nums[n - 1]
``` 
