---
title: Sliding window
date: 2021-04-08 09:12:39
tags:
    - algorithm
    - Leetcode
categories:
    - Data structure and algorithm
---

# Sliding Window Algorithm
---

Sliding window algorithm is a kind of two pointers. This algorithm mostly used in string match.

## template
---

```
def slidingWindow(s, t):
    need, window, valid = {}, {}, 0

    left, right = 0, 0
    while right < len(s):
        node = s[right]
        right += 1

        // update date
        ...

        while (window needs shrink):
            deleteNode = s[left]
            left += 1

            // update data
            ...

```


## Notice
---

There are 4 questions need to be thought in sliding window algorithm

1. When move `right` to expand window indicating add characters, which data need to update?

2. Under what conditions, the window should pause to expand, and start to move `left` to shrink the window?

3. When move `left`, which means delete characters, which data need to update?

4. Should the result we want be updated when the window is enlarged or when the window is reduced?


## Example
---

### leetcode 76 Minimum Window Substring (hard)

#### Description
Given two strings `s` and `t`, return the minimum window in `s` which will contain all the characters in `t`. If there is no such window in `s` that covers all characters in `t`, return the empty string `"".`

**Note** that If there is such a window, it is guaranteed that there will always be only one unique minimum window in `s`.

#### Example
```
Input: s = "ADOBECODEBANC", t = "ABC"
Output: "BANC"
```

#### Code
```
def minWindow(self, s, t):
    need, window, valid, length = {}, {}, 0, float('inf')

    for node in t:
        if node not in need:
            need[node] = 1
        else:
            need[node] += 1

    left, right = 0, 0

    while right < len(s):

        node = s[right]
        right += 1

        if node in need.keys():
            if node not in window:
                window[node] = 1
            else:
                window[node] += 1

            if window[node] == need[node]:
                valid += 1

        while valid == len(need):
            if right - left < length:
                start = left
                length = right - left

            deleteNode = s[left]
            left += 1

            if deleteNode in need.keys():
                if window[deleteNode] == need[deleteNode]:
                    valid -= 1
                window[deleteNode] -= 1

    return '' if length == float('inf') else s[start: start+length]
```

### leetcode 567 Permutation in String (Medium)

#### Description:
Given two strings **s1** and **s2**, write a function to return true if **s2** contains the permutation of **s1**. In other words, one of the first string's permutations is the **substring** of the second string.

#### Example

```
Input: s1 = "ab" s2 = "eidbaooo"
Output: True
Explanation: s2 contains one permutation of s1 ("ba").
```

#### Code
```

def checkInclusion(self, s1, s2):
    need, window, valid, = {}, {}, 0

    for node in s1:
        if node not in need:
            need[node] = 1
        else:
            need[node] += 1

    left, right = 0, 0

    while right < len(s2):
        node = s2[right]
        right += 1

        if node in need.keys():
            if node not in window:
                window[node] = 1
            else:
                window[node] += 1

            if window[node] == need[node]:
                valid += 1

        while right - left >= len(s1):
            if valid == len(need):
                return True

            deleteNode = s2[left]
            left += 1
            if deleteNode in need.keys():
                if window[deleteNode] == need[deleteNode]:
                    valid -= 1
                window[deleteNode] -= 1

    return False
```


### leetcode 438 Find All Anagrams in a String (Medium)

#### Description:
Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

#### Example

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

#### Code
```
def findAnagrams(self, s, p):

    need, window, valid, res = {}, {}, 0, []

    for node in p:
        if node not in need:
            need[node] = 1
        else:
            need[node] += 1

    left, right = 0, 0

    while right < len(s):
        node = s[right]
        right += 1

        if node in need.keys():
            if node not in window:
                window[node] = 1
            else:
                window[node] += 1

            if window[node] == need[node]:
                valid += 1

        while right - left >= len(p):
            if valid == len(need):
                res.append(left)

            deleteNode = s[left]
            left += 1
            if deleteNode in need.keys():
                if window[deleteNode] == need[deleteNode]:
                    valid -= 1
                window[deleteNode] -= 1

    return res

```

### leetcode 3 Longest Substring Without Repeating Characters (Medium)

#### Description:
Given a string s, find the length of the longest substring without repeating characters.

#### Example

```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

#### Code
```
def lengthOfLongestSubstring(self, s):
    if not s: return 0

    left, right, res, window = 0, 0, 0, {}

    while right < len(s):
        node = s[right]
        right += 1

        if node not in window:
            window[node] = 1
        else:
            window[node] += 1

        while window[node] > 1:
            deleteNode = s[left]
            left += 1

            window[deleteNode] -= 1

        res = max(res, right - left)

    return res
```
