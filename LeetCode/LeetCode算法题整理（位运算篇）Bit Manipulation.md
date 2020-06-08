## 231. Power of Two
### Key Point: 
* 1. n&(n-1) 一个数n和n-1的与运算操作，相当于去掉了最右面的1
For example:
1.n = 100000, then n - 1 = 011111 and n & (n-1) = 000000, so if it is power of two, result is zero
2.n = 101110, then n - 1 = 101101 and n & (n-1) = 101100, number is not power of two and result is not zero.
* 2. <<= Performs bitwise left shift and assigns value to the left operand.
For example:
mask <<= 1
### Solution:
'''
return n > 0 and not (n & n-1) #判断n为正数以及 n&(n-1) result is zero
'''
