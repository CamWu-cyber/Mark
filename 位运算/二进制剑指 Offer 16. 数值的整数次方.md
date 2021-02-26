# 剑指 Offer 16. 数值的整数次方
实现函数double Power(double base, int exponent)，求base的exponent次方。不得使用库函数，同时不需要考虑大数问题。

#### 示例1
    输入: 2.00000, 10
    输出: 1024.00000
   
#### 示例2
    输入: 2.10000, 3
    输出: 9.26100
    
#### 示例3
    输入: 2.00000, -2
    输出: 0.25000
    解释: 2-2 = 1/22 = 1/4 = 0.25
    
思路：二进制。分n为奇数、偶数的情况，当n为奇数时，需要在偶数的基础上多乘上一个x. **n & 1 相当于 n % 2 == 1；n >>= 1 相当于 n //= 2**

    #!/usr/bin/python
    class Solution:
        def myPow(self, x: float, n: int) -> float:
            if x == 0:
                return 0
            # 示例3的情况
            if n < 0:
                n = -n
                x = 1/x
            res = 1
            while n:
                # 当n为奇数时，会多出一个x，就用res接住
                if n & 1:  # 相当于n%2 == 1
                    res *= x
                x *= x
                n >>= 1   # 相当于n//=2
            return res

    if __name__ == '__main__':
      obj = Solution()
      print(obj.myPow(2.00000, 10))
      print(obj.myPow(2.10000, 3))

#### 运行结果
    1024.0
    9.261000000000001
