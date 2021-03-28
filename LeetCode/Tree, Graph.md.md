## 树 Tree
![image](https://user-images.githubusercontent.com/27000065/112231837-dc18ac00-8c0d-11eb-823d-56f423c945a0.png)
![image](https://user-images.githubusercontent.com/27000065/112231877-f05ca900-8c0d-11eb-9e3a-50b58d515ae9.png)
![image](https://user-images.githubusercontent.com/27000065/112231938-12eec200-8c0e-11eb-9420-371688e81e8e.png)
![image](https://user-images.githubusercontent.com/27000065/112232038-492c4180-8c0e-11eb-9a72-616d34187052.png)
不光是左/右儿子
![image](https://user-images.githubusercontent.com/27000065/110733377-d1185180-81f3-11eb-9e92-1684b0f6c29f.png)
![image](https://user-images.githubusercontent.com/27000065/110733428-f1481080-81f3-11eb-9c6a-e0d29831d97a.png)
左树上的所有节点小于节点，右树上的node都大于节点。查找时间短一半lgn。
![image](https://user-images.githubusercontent.com/27000065/110733657-526fe400-81f4-11eb-81a6-4d0caae975f8.png)

### 98. Validate Binary Search Tree
#### Solution1 Inorder Traversal
中序遍历：左中右
```
def inValidBST(self, root):

    inorder = self = self.inorder(root)
    return inorder == list(sorted(set(inorder)))

def inorder(self, root):
    if root is None:
    return []
    return self.inorder(root.left) + [root.val] + self.inorder(root.right)
    # Time: O(N) Space: O(h)
```

```
def inValidBST(self, root):
    self.prev = None
    return self.helper(root)
def helper(self, root):
    if root is None:
        return True
    if not self.helper(root.left):
        return False
    if self.prev and self.prev.val >= root.val:
        return False
    self.prev = root
    return self.helper(root.right)
    # Time: O(N) Space: O(h)
```    
### Solution2 Recruision
```
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        
        
        def validate(node, low=-math.inf, high=math.inf):
            
            if not node:
                return True
            if nod.val <=low or node.val>=high:
                return False
            
            return (validate(node.right, nod.val, high) and validate(node.left, low, nod.val))
        
        return validate(root)
        
        # Time: O(N) Space: O(1)
```

### 236. Lowest Common Ancestor of a Binary Search Tree 二叉树的最近公共祖先
### Solution: Recursion
![image](https://user-images.githubusercontent.com/27000065/112536078-66365100-8d83-11eb-9b08-cbf983285a5f.png)
```
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if root is None or root == p or root == q:
            return root
        
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        
        if left is None:
            return right
        elif right is None:
            return left
        else:
            return root
```        

### 235. Lowest Common Ancestor of a Binary Search Tree 二叉搜索树的最近公共祖先
### Solution：利用二叉搜索树的大小关系
```
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        
        if root.val > p.val and root.val > q.val:
            return self.lowestCommonAncestor(root.left, p, q)
        if root.val < p.val and root.val < q.val:
            return self.lowestCommonAncestor(root.right, p, q)
        return root
```        






### 160. Intersection of Two Linked Lists
#### Solution 1 Hash Table
![image](https://user-images.githubusercontent.com/27000065/110005350-5d9fad00-7ce6-11eb-955f-bb08aabf5f7b.png)

```
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        nodes_in_B = set()

        while headB is not None:
            nodes_in_B.add(headB)
            headB = headB.next

        while headA is not None:
            # if we find the node pointed to by headA,
            # in our set containing nodes of B, then return the node
            if headA in nodes_in_B:
                return headA
            headA = headA.next

        return None
  ````
  #### Solution 2 Two Pointers
  ![image](https://user-images.githubusercontent.com/27000065/110005431-7740f480-7ce6-11eb-9910-0a12d1dcbf75.png)
```
class Solution:
    def getIntersectionNode(self, headA: ListNode, headB: ListNode) -> ListNode:
        pA = headA
        pB = headB

        while pA != pB:
            pA = headB if pA is None else pA.next
            pB = headA if pB is None else pB.next

        return pA
        # Note: In the case lists do not intersect, the pointers for A and B
        # will still line up in the 2nd iteration, just that here won't be
        # a common node down the list and both will reach their respective ends
        # at the same time. So pA will be NULL in that case.
  ```
  
## 二叉树遍历
Pre-order, In-order, Post-order 前中后序遍历（实际很少用），一般用广度优先等
![image](https://user-images.githubusercontent.com/27000065/112543110-b6191600-8d8b-11eb-9568-1d2e342ebe30.png)
![image](https://user-images.githubusercontent.com/27000065/112544164-16f51e00-8d8d-11eb-8e8a-5fd6f57bd62e.png)

## 递归（Recursion）分治（divide & Conquer）
递归
![image](https://user-images.githubusercontent.com/27000065/112545577-c1ba0c00-8d8e-11eb-994b-0d28c60c774c.png)
![image](https://user-images.githubusercontent.com/27000065/112546059-54f34180-8d8f-11eb-857a-518bad6033ed.png)
![image](https://user-images.githubusercontent.com/27000065/112546106-650b2100-8d8f-11eb-9649-5a0719d9e97a.png)
可以分成子问题，并行，不适合重复计算的
![image](https://user-images.githubusercontent.com/27000065/112546241-9388fc00-8d8f-11eb-91ee-ea806b41b276.png)

### 50. Pow(x,n)
### Intuition
### Solution1 递归，分治
```
        if not n:
            return 1
        if n < 0:
            return 1 / self.myPow(x, -n)
        if n % 2:
            return x * self.myPow(x, n-1)
        return self.myPow(x*x, n/2)
```
### Solution2 非递归，借助位运算
```
        if n < 0:
            x = 1 / x
            n = -n
            
        pow = 1
        while n:
            if n & 1: # 按位与，判断是否为偶数
                pow *= x
            x *= x
            n >>= 1 # 二进制左移一位
        return pow
```
Points: 1. 边界条件
2. 位运算




