---
title: 1. 两数之和【哈希表】
date: 2021-05-28
tags:
 -  哈希表
categories:
 -  algo
sidebar: 'auto'
---

> ## 题目描述
> ```
> 给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
> 你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。
> 示例:
> 
> 给定 nums = [2, 7, 11, 15], target = 9
> 
> 因为 nums[0] + nums[1] = 2 + 7 = 9
> 所以返回 [0, 1]
> 
> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com/problems/two-sum
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
> ```


## 方法一：哈希表
### 解题思路
对每一个出现的 num 判断其另一半 target - num 是否也出现在数组中， 可以用哈希表记录所有已经遍历过的数字，判断 target - num 是否出现时，直接查表即可。
**哈希表是非常常用的时间换空间的方式**

### 代码

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    //哈希
    let myMap = new Map();
    nums.forEach((item,index) => {
        myMap.set(item,index)
    })
    for(let i = 0; i<nums.length; i++){
        let j = myMap.get(target-nums[i])
        if(j && j!=i ){
            return[i,j]
        }
    }
};
```
### 复杂度分析
时间复杂度：O(N)
空间复杂度：O(N)

## 方法二：动态哈希表
### 解题思路
这题之前做过一次所以一下子能想起来用哈希表，但是只是笨拙的想到了先一口气把nums里的数字存进去，再遍历匹配。
看了别人的答案，发现可以一边判断一边存放，节约时间和空间。

### 代码

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    let myMap = new Map();
    for(let i=0; i<nums.length; i++){
        const tar = target - nums[i];
        //判断哈希表里是否已经有了与现在这个值加起来是目标值的数
        if(myMap.has(tar)){
            return [myMap.get(tar), i]
        }else{
        //没有的话存放入哈希表
            myMap.set(nums[i],i)
        }
    }
};
```
### 复杂度分析
时间复杂度：O(N)
空间复杂度：O(N)
