---
layout: post
title: Word Break
categories:  [blog ]
tags: [Leetcode ]
comments: true
published: true


---
## Word Break

## Problem

Given a string s and a dictionary of words dict, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

For example, given

- s = "leetcode",
- dict = ["leet", "code"].

Return true because "leetcode" can be segmented as "leet code".

## Analytics

It is a dynamic programming problem. 

To verify whether the string s can be break into subsequence in the word dicts, first break the string s into two parts:

- substring s1
- substring s2

s = s1+s2;

if:

- s1 is in the word dicts.
- s2 can break into subsequence in the word dicts.

example:

s = "leetcode"

word dicts = ['le', 'et', 'code']

s1 = 'code'

s2 = 'leet'

Dynamic Programming will record the state of substring of s.

dp is boolean list used to record the return value.

n = len(s)

dp[n] is used to record the state of s[n-1]

if dp[n] = true, it means that s[0:n-1] can be segmented into a space-separated sequence of one or more dictionary words.

## Code

```python
class Solution(object):
    def wordBreak(self, s, wordDict):
    """
    :type s: str
    :type wordDict: Set[str]
    :rtype: bool
    """
        dp = []
        dp.append(True)
        le = len(s)
        for i in range(1, le+1):
            dp.append(False)
        #print dp
        for i in range(0, le):
            for j in range(i, -1, -1):
                print 'j', j, 'dp[j]', dp[j]
                #print 's', s[j:i-j+1]
                if dp[j] and (s[j:i+1] in wordDict):
                    dp[i+1] = True
                    break
         print dp[le]
         return dp[le]
```