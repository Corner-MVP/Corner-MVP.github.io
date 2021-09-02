---
title: 881. Boats to Save People.md
date: 2021-08-26 22:56:28
tags:
    - algorithm
    - Leetcode
    - two-pointers
    - greedy-algorithm
categories:
    - Data structure and algorithm
---

## Description
You are given an array `people` where `people[i]` is the weight of the `ith` person, and an **infinite number of boats** where each boat can carry a maximum weight of `limit`. Each boat carries at most two people at the same time, provided the sum of the weight of those people is at most `limit`.

Return *the minimum number of boats to carry every given person*.

## Examples
### example 1
```
Input: people = [1,2], limit = 3
Output: 1
Explanation: 1 boat (1, 2)
```

### example 2
```
Input: people = [3,2,2,1], limit = 3
Output: 3
Explanation: 3 boats (1, 2), (2) and (3)
```

### example 3
```
Input: people = [3,5,3,4], limit = 5
Output: 4
Explanation: 4 boats (3), (3), (4), (5)
```

### constraints
- {% mathjax %}1 <= people.length <= 5 * 10^4{% endmathjax %}
- {% mathjax %}1 <= people[i] <= limit <= 3 * 10^4{% endmathjax %}

## Idea
In order to take all people with less boats, it must let more boats to take two people.

`n` is the length of array `people`, `res` is the final answer and {% mathjax %}f(){% endmathjax %} is the function to solve this problem. To consider people with lightest weight.
- if the lightest weight people cannot take boat with heaviest people, it indicates that the heaviest cannot take the same boats with other people and he(she) need take boat alone. And the following question is to consider how many boats that `n-1` people need. Therefore, we can know that {% mathjax %}res += 1 + f(n-1){% endmathjax %};
- if the total weight of lightest and heaviest people is less than `limit`, it means they can take boat together, namely, `res += 1` and the follwing question is to consider how many boats that `n-2` people need. And {% mathjax %}res += 1 + f(n-2){% endmathjax %}.

## Code
### Python
```
class Solution:
    def numRescueBoats(self, people, limit):
        res = 0
        people.sort()
        light, heavy = 0, len(people) - 1

        while light <= heavy:
            if people[light] + people[heavy] > limit:
                heavy -= 1
            else:
                light += 1
                heavy -= 1
            res += 1
        
        return res
```

### JavaScript
```
/**
 * @param {number[]} people
 * @param {number} limit
 * @return {number}
 */
var numRescueBoats = function(people, limit) {
  let res = 0;
  people.sort((a, b) => a - b)
  let light = 0, heavy = people.length - 1
  while (light <= heavy) {
      if (people[light] + people[heavy] > limit) {
          heavy -= 1
      } else {
          heavy -= 1
          light += 1
      }
      res += 1
  }
  return res
};
```

## Time and space complexity
- time complexity: {% mathjax %}O(nlog(n)){% endmathjax %}, `n` is the length of array `people`, sort array `people` need {% mathjax %}O(nlog(n)){% endmathjax %};
- space complexity: {% mathjax %}O(log(n)){% endmathjax %}, sorting need {% mathjax %}O(log(n)){% endmathjax %} extra space.
