---
title: 【leetcode】3. 无重复字符的最长子串
url: 375.html
id: 375
categories:
  - leetcode
date: 2019-05-18 21:47:03
tags:
toc: true
---

题目描述：
-----

> 给定一个字符串，请你找出其中不含有重复字符的 最长子串 的长度。

本人题解：
-----

    int lengthOfLongestSubstring(string s) 
        {
            unordered_map<char, int> storeIndex;
            queue<char> charlist;
            int maxSize = 0;
            for (int i = 0; i < s.size(); ++i)
            {
                if (storeIndex.count(s[i]) == 0) // map中不存在该元素
                {
                    storeIndex[s[i]] = 1;
                    charlist.push(s[i]);
                }
                else
                {
                    while(charlist.front() != s[i])
                    {
                        maxSize = maxSize>storeIndex.size()?maxSize:storeIndex.size();
                        storeIndex.erase(charlist.front());
                        charlist.pop();
                    }
                    charlist.pop();
                    charlist.push(s[i]);
                }
            }
            return maxSize>storeIndex.size()?maxSize:storeIndex.size();
        }
    

dalao题解：
--------

> 这道题主要用到思路是：滑动窗口 什么是滑动窗口？ 其实就是一个队列,比如例题中的 abcabcbb，进入这个队列（窗口）为 abc 满足题目要求，当再进入 a，队列变成了 abca，这时候不满足要求。所以，我们要移动这个队列！ 如何移动？ 我们只要把队列的左边的元素移出就行了，直到满足题目要求！ 一直维持这样的队列，找出队列出现最长的长度时候，求出解！ 时间复杂度：O(n)

    int lengthOfLongestSubstring(string s) 
    {
        if(s.size() == 0) return 0;
        unordered_set<char> lookup;
        int maxStr = 0;
        int left = 0;
        for(int i = 0; i < s.size(); i++)
        {
            while (lookup.find(s[i]) != lookup.end())
            {
                lookup.erase(s[left]);
                left ++;
            }
            maxStr = max(maxStr,i-left+1);
            lookup.insert(s[i]);
        }
        return maxStr;
    }