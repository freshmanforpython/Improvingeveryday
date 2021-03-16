## Priority Queue：有条件的Queue，非fifo或lifo
![image](https://user-images.githubusercontent.com/27000065/111044694-20d76280-8418-11eb-99bb-ad60cbfb01f0.png)
![image](https://user-images.githubusercontent.com/27000065/111044703-28970700-8418-11eb-83ce-f5d30717912a.png)
需要了解实现机制：1. 堆heap（ Min Heap, Max Heap) 2. 二叉搜索树
![image](https://user-images.githubusercontent.com/27000065/111044740-62680d80-8418-11eb-8a0c-511904fbe693.png)

### 703. Kth Largest Element in a Stream
#### Question
Design a class to find the kth largest element in a stream. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Implement KthLargest class:

KthLargest(int k, int[] nums) Initializes the object with the integer k and the stream of integers nums.
int add(int val) Returns the element representing the kth largest element in the stream.
 

Example 1:

Input
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
Output
[null, 4, 5, 5, 8, 8]

Explanation
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8

#### Solution
```
def __init__(self, k: int, nums: List[int]):
    self.k = k
    self.nums = nums
    heapq.heapify(self.nums)
    while len(self.nums) > self.k:
        heapq.heappop(self.nums)

def add(self, val: int):
    if len(self.nums) < self.k:
        heapq.heappush(self.nums, val)
    elif val > self.nums[0]:
        heapq.heapreplace(self.nums, val)
    return self.nums[0]
```
Points:
1. Module [** heapy**](https://docs.python.org/zh-cn/3/library/heapq.html)

### 1792. Maximum Average Pass Ratio
#### Question
There is a school that has classes of students and each class will be having a final exam. You are given a 2D integer array classes, where classes[i] = [passi, totali]. You know beforehand that in the ith class, there are totali total students, but only passi number of students will pass the exam.

You are also given an integer extraStudents. There are another extraStudents brilliant students that are guaranteed to pass the exam of any class they are assigned to. You want to assign each of the extraStudents students to a class in a way that maximizes the average pass ratio across all the classes.

The pass ratio of a class is equal to the number of students of the class that will pass the exam divided by the total number of students of the class. The average pass ratio is the sum of pass ratios of all the classes divided by the number of the classes.

Return the maximum possible average pass ratio after assigning the extraStudents students. Answers within 10-5 of the actual answer will be accepted.

 

Example 1:

Input: classes = [[1,2],[3,5],[2,2]], extraStudents = 2
Output: 0.78333
Explanation: You can assign the two extra students to the first class. The average pass ratio will be equal to (3/4 + 3/5 + 2/2) / 3 = 0.78333.
Example 2:

Input: classes = [[2,4],[3,9],[4,5],[2,10]], extraStudents = 4
Output: 0.53485
 

Constraints:

1 <= classes.length <= 105
classes[i].length == 2
1 <= passi <= totali <= 105
1 <= extraStudents <= 105
#### Intuition
For each class, the delta is decreasing when we add extra students.
The best local option is always the best.
It's a loss if we don't take it.

#### Solution 
```
def maxAverageRatio(self, A, k):
        h = [(a / b - (a + 1) / (b + 1), a, b) for a, b in A]
        heapify(h)
        while k:
            v, a, b = heapq.heappop(h)
            a, b = a + 1, b + 1
            heapq.heappush(h, (-(a + 1) / (b + 1) + a / b, a, b))
            k -= 1
        return sum(a / b for v, a, b in h) / len(h)
```

### 
#### Question
You are given an array of integers nums, there is a sliding window of size k which is moving from the very left of the array to the very right. You can only see the k numbers in the window. Each time the sliding window moves right by one position.

Return the max sliding window.

 

Example 1:

Input: nums = [1,3,-1,-3,5,3,6,7], k = 3
Output: [3,3,5,5,6,7]
Explanation: 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       3
 1 [3  -1  -3] 5  3  6  7       3
 1  3 [-1  -3  5] 3  6  7       5
 1  3  -1 [-3  5  3] 6  7       5
 1  3  -1  -3 [5  3  6] 7       6
 1  3  -1  -3  5 [3  6  7]      7
Example 2:

Input: nums = [1], k = 1
Output: [1]
Example 3:

Input: nums = [1,-1], k = 1
Output: [1,-1]
Example 4:

Input: nums = [9,11], k = 2
Output: [11]
Example 5:

Input: nums = [4,-2], k = 2
Output: [4]

#### Intuition
#### Solution
```
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        n = len(nums)
        if n * k == 0:
            return []
        window, res = [], []
        for i, x in enumerate(nums):
            if i >= k and window[0] <= i - k:
                window.pop(0)
            while window and nums[window[-1]] <=x:
                window.pop()
            window.append(i)
            if i >= k - 1:
                res.append(nums[window[0]])
        return res
        # Time: O(NK) Space: O(1)
```        
Point: Double-End Queue (Dequeue)
