1. extend等list内置函数，对list做动作，函数返回的是None，因此不能直接a=b.extend(c)，此时a是None。https://www.runoob.com/python/python-lists.html
2. 初始化 list方法：res=\[\[1]\*(i+1)for i in range(numRows)]（[118. Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/)）
3. Class (类),Object（实例）,Attributes（属性）
实例的属性通过self绑定，类的属性在class中直接定义
https://www.liaoxuefeng.com/wiki/1016959663602400/1017594591051072
4. [True Value Testing](https://docs.python.org/3/library/stdtypes.html#truth-value-testing)
Any object can be tested for truth value, for use in an if or while condition or as operand of the Boolean operations below.

By default, an object is considered true unless its class defines either a __bool__() method that returns False or a __len__() method that returns zero, when called with the object. 1 Here are most of the built-in objects considered false:

constants defined to be false: None and False.

zero of any numeric type: 0, 0.0, 0j, Decimal(0), Fraction(0, 1)

empty sequences and collections: '', (), [], {}, set(), range(0)

Operations and built-in functions that have a Boolean result always return 0 or False for false and 1 or True for true, unless otherwise stated. (Important exception: the Boolean operations or and and always return one of their operands.)

### 392. Is Subsequence
#### My Solution

```
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        sl = list(s)
        tl = list(t)
        for sub in sl:
            if sub not in tl:
                return False
            else:
                tl = tl[tl.index(sub)+1:]
        return True
 ```
#### Best Solution

```class Solution:
    def isSubsequence(self, s, target):
        iter_target = iter(target) #生成迭代器
        return all(char in iter_target for char in s) #all()判断所有S里的都是在T里，返回True
        ```
        

### Find Numbers with Even Number of Digits

#### My Solution

```
import numpy

class Solution:
    def findNumbers(self, nums: List[int]) -> int:
        count = 0
        log10 = numpy.log10(nums)
        digits = [floor(x) + 1 for x in log10]
        for digit in digits:
            if digit % 2 == 0:
                count +=1
        return count
 ```
#### Best Solution

```class Solution:
    def findNumbers(self, nums: List[int]) -> int:
        return sum([int(log10(num)) %2 for num in nums])```
        


### 88. Merge Sorted Array

#### My Solution

```
class Solution:
    def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        
       
        for i in range(n):
            nums1[m+i] = nums2[i]
         
        return nums1.sort()
 ```
#### Best Solution

```tot = m+n
        i1 = m-1
        i2 = n-1
        target = tot-1
        while i2>=0:
            if i1 >= 0 and nums1[i1] > nums2[i2]:
                nums1[target] = nums1[i1]
                i1-=1
            else:
                nums1[target] = nums2[i2]
                i2-=1
            target-=1
```

        
        
        
