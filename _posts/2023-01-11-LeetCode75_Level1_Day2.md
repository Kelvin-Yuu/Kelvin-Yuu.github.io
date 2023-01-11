---
layout: post
title: LeetCode 75 Level 1 Day2
date: 2023-1-11
categories: blog
tags: [LeetCode,哈希表,字符串,双指针,动态规划]
description: 文章金句。
subtitle: 谋求出路Day2
---

## 205. 同构字符串
给定两个字符串 s 和 t ，判断它们是否是同构的。

如果 s 中的字符可以按某种映射关系替换得到 t ，那么这两个字符串是同构的。

每个出现的字符都应当映射到另一个字符，同时不改变字符的顺序。不同字符不能映射到同一个字符上，相同字符只能映射到同一个字符上，字符可以映射到自己本身。

**示例1：**
```
输入：s = "egg", t = "add"
输出：true
```
**示例 2：**
```
输入：s = "foo", t = "bar"
输出：false
```
**示例 3：**
```
输入：s = "paper", t = "title"
输出：true
```
来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/isomorphic-strings

**解法**

解法1：C++哈希表映射法
```
本题是基于集合论的一个概念【映射】。

	- 单射：对于任意 x ，都有唯一的 y 与之对应。

	- 满射：对于任意 y ，至少存在一个 x 与之对应。

	- 双射：既是单射又是满射，又称为一一对应。
```
<p><img src="https://github.com/Kelvin-Yuu/Kelvin-Yuu.github.io/blob/master/image/blog/2023-01-11-LeetCode75_Level1_Day2/2.jpeg?raw=true" alt="> 图1" class="img-responsive"></p>

```
本题很明显，需要字符串s和t是双射关系。

如图，一开始先新建哈希表s2t，t2s用于存储字符串s与t的映射关系。

s2t为s映射t，t2s为t映射s。

这里用示例2演示步骤~

	开始遍历字符串：
	①	s[0] = "f"检索s2t，不存在此键值对, t[0] = "b"检索t2s，不存在该键值对。
		将此键值对添加进哈希表：s2t["f"] = "b", t2s["b"] = "f"；
		
	②	s[1] = "o"检索s2t，不存在此键值对, t[1] = "a"检索t2s，不存在该键值对。
		将此键值对添加进哈希表：s2t["o"] = "a", t2s["a"] = "o"；
		
	③	s[2] = "o"检索s2t，存在键"o"
		∵ s2t["o"] = "a"，而t[2] = "r"，s2t["o"] != t[2]；
		∴ 映射不同(o → a ≠ o → r) 存在一对多关系，不是双射，返回false。
	
```
		
<p><img src="https://github.com/Kelvin-Yuu/Kelvin-Yuu.github.io/blob/master/image/blog/2023-01-11-LeetCode75_Level1_Day2/1.jpg?raw=true" alt="> 图2" class="img-responsive"></p>

```cpp
class Solution 
{
public:
    bool isIsomorphic(string s, string t) 
	{
        int slen = s.size();
        int tlen = t.size();
        if (slen != tlen)
        {
            return false;
        }
        unordered_map<char, char> s2t, t2s;
        for (int i = 0; i < slen; ++i)
        {
            char a = s[i], b = t[i];
            if ((s2t.count(a) && s2t[a] != b) ||
                (t2s.count(b) && t2s[b] != a))
            {
                return false;
            }
            s2t[a] = b;
            t2s[b] = a;
        }
        return true;
    }
};
```

## 392. 判断子序列
给定字符串 s 和 t ，判断 s 是否为 t 的子序列。

字符串的一个子序列是原始字符串删除一些（也可以不删除）字符而不改变剩余字符相对位置形成的新字符串。（例如，"ace"是"abcde"的一个子序列，而"aec"不是）。


**示例1：**
```
输入：s = "abc", t = "ahbgdc"
输出：true
```
**示例2：**
```
输入：s = "axc", t = "ahbgdc"
输出：false
```
来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/is-subsequence

**解法**
C++：
```cpp
class Solution 
{
public:
    bool isSubsequence(string s, string t) 
	{
        int slen = s.size();
        int tlen = t.size();
        int i = 0, j = 0;
        while (i < slen && j < tlen)
        {
            if (s[i] == t[j])
            {
                ++i;
            }
            ++j;
        }
        return i == slen;
    }
};
```