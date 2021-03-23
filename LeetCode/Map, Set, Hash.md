![image](https://user-images.githubusercontent.com/27000065/112184676-d010f800-8bd5-11eb-9c19-a43f528b6de3.png)
![image](https://user-images.githubusercontent.com/27000065/112184790-f040b700-8bd5-11eb-8b8e-b6d7e2f1569b.png)
Hash: O(1)无序 Tree:O(N)有序
![image](https://user-images.githubusercontent.com/27000065/112184857-0189c380-8bd6-11eb-9292-c30486cf35d0.png)
![image](https://user-images.githubusercontent.com/27000065/112184948-1d8d6500-8bd6-11eb-8dea-4749264deb1c.png)

## 242. Valid Anagram
### Question
### Intuition
Map O(N)
![image](https://user-images.githubusercontent.com/27000065/112207164-2c334680-8bed-11eb-930c-19925f1b41e7.png)
Point:
1. dict.get(key, default): 如果dict里有key返回value，如果没有，加入key，返回default

## 1. Two Sum
### Question
### Intuition
Map (set)
### Solution
```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        h = {}
        
        for i, num in enumerate(nums):
            if target - num not in h:
                h[num] = i
            else:
                return [h[target - num], i]
        # Time: O(N)
```

### 15.3Sum
### Question
### Intuition
![image](https://user-images.githubusercontent.com/27000065/112217715-3bb88c80-8bf9-11eb-9939-e18b00390714.png)
### Solution
2. c = -(a+b) Set O(N^2)
```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        if len(nums) < 3:
            return []
        nums.sort()
        res = set()
        for i, v in enumerate(nums[:-2]):
            if i >= 1 and v == nums[i-1]:
                continue
            d = {}
            for x in nums[i+1:]:
                if x not in d:
                    d[-v-x] = 1
                else:
                    res.add((v, -v-x, x))
        return map(list, res)
```

4. sort+find O(NlogN)
```
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        nums.sort()
        for i in range(len(nums)-2):
            if i > 0 and nums[i] == nums[i-1]:
                continue
            l, r = i+1, len(nums)-1
            while l < r:
                s = nums[i] + nums[l] + nums[r]
                if s < 0:
                    l += 1
                elif s>0:
                    r -= 1
                else:
                    res.append([nums[i], nums[l], nums[r]])
                    while l < r and nums[l] == nums[l+1]:
                        l += 1
                    while l < r and nums[r] == nums[r-1]:
                        r -= 1
                    l += 1; r -= 1
        return res
```
Point:
while l < r and nums[l] == nums[l+1]: 可以查掉所有相同的值；用if只能执行一次

## 18. 4Sum


