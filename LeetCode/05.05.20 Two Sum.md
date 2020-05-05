## Question
Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

## Thinking


## My First Solution
```
#暴力求解，从后往前相加
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            if i>0:
                
                for j in range(0,i):
                    if nums[i]+nums[j] == target:
                        return i,j
```

## Best Solution

```
#Hash Table
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        seen = {} #Hash Table
        for i, item in enumerate(nums): #enumerate for iterable
            second_val = target - item
            if second_val in seen:
                return [seen[second_val], i]
            seen[item] = i
        return []
 ```
 

## Learning Section
[Hash Table](https://blog.csdn.net/v_JULY_v/article/details/6256463)
