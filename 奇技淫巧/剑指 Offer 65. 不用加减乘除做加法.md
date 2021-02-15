# 剑指 Offer 65. 不用加减乘除做加法
观察发现，无进位和 与 异或运算 规律相同，进位 和 与运算 规律相同（并需左移一位）。

    #!/usr/bin/python
    class Solution:
      def add(self, a, b):
        x = 0xffffffff
        # 如果a,b为负数，需要先获取它们的补码
        a = a & x
        b = b & x
        while b != 0:
          # 异或运算，相同为0，不同为1
          # 与运算，都是1才为1
          a, b = (a ^ b), (a & b) << 1 & x
        # 如果a是正数直接返回，如果a是负数，需要将补码还原至 Python 的存储格式
        if a  <= 0x7fffffff:
          return a
        else:
          return ~(a ^ x)

    if __name__ == '__main__':
      obj = Solution()
      print(obj.add(1,2))

#### 运算结果
    3
