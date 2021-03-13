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
