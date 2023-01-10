---
layout: post
title: LeetCode 75 Level 1 Day1
date: 2023-1-10
categories: blog
tags: [LeetCode,数组,前缀和]
description: 文章金句。
subtitle: 谋求出路Day1
---

## 1480. 一维数组的动态和
给你一个数组 nums 。数组「动态和」的计算公式为：runningSum[i] = sum(nums[0]…nums[i]) 。

请返回 nums 的动态和。

**示例1：**
```
输入：nums = [1,2,3,4]
输出：[1,3,6,10]
解释：动态和计算过程为 [1, 1+2, 1+2+3, 1+2+3+4] 。
```
**示例 2：**
```
输入：nums = [1,1,1,1,1]
输出：[1,2,3,4,5]
解释：动态和计算过程为 [1, 1+1, 1+1+1, 1+1+1+1, 1+1+1+1+1] 。
```
**示例 3：**
```
输入：nums = [3,1,2,10,1]
输出：[3,4,6,16,17]
```
来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/running-sum-of-1d-array

**解法：**
C++：
```cpp
class Solution {
public:
    vector<int> runningSum(vector<int>& nums) {
        int len = nums.size();
        for (int i = 1; i < len; ++i)
        {
            nums[i] = nums[i - 1] + nums[i];
        }
        return nums;
    }
};
```


## 724. 寻找数组的中心下标
给你一个整数数组 nums ，请计算数组的 中心下标 。

数组 中心下标 是数组的一个下标，其左侧所有元素相加的和等于右侧所有元素相加的和。

如果中心下标位于数组最左端，那么左侧数之和视为 0 ，因为在下标的左侧不存在元素。这一点对于中心下标位于数组最右端同样适用。

如果数组有多个中心下标，应该返回 最靠近左边 的那一个。如果数组不存在中心下标，返回 -1 。

**示例1：**
```
输入：nums = [1, 7, 3, 6, 5, 6]
输出：3
解释：
中心下标是 3 。
左侧数之和 sum = nums[0] + nums[1] + nums[2] = 1 + 7 + 3 = 11 ，
右侧数之和 sum = nums[4] + nums[5] = 5 + 6 = 11 ，二者相等。
```
**示例2：**
```
输入：nums = [1, 2, 3]
输出：-1
解释：
数组中不存在满足此条件的中心下标。
```
**示例3：**
```
输入：nums = [2, 1, -1]
输出：0
解释：
中心下标是 0 。
左侧数之和 sum = 0 ，（下标 0 左侧不存在元素），
右侧数之和 sum = nums[1] + nums[2] = 1 + -1 = 0 。
```
来源：力扣（LeetCode）
链接：https://leetcode.cn/problems/find-pivot-index

**解法：**
C++：
```cpp
class Solution {
public:
    int pivotIndex(vector<int>& nums) {
        int len = nums.size();
        int total = accumulate(nums.begin(), nums.end(), 0);
        int sum = 0;
        for (int i = 0; i < len; ++i)
        {
            if (2 * sum + nums[i] == total)
            {
                return i;
            }
            sum += nums[i];
        }
        return -1;
    }
};
```