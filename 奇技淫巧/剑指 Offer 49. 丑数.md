# 剑指 Offer 49. 丑数
我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

#### 示例:

    输入: n = 10
    输出: 12
    解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。

思路：一个丑数乘以 2， 3， 5 之后， 一定还是一个丑数。

    class Solution:
        def nthUglyNumber(self, n):
            # 一个丑数乘以 2， 3， 5 之后， 一定还是一个丑数。
            # 构造三个数组num2, num3, num5
            # nums2 = {1*2, 2*2, 3*2, 4*2, 5*2, 6*2, 8*2...}
            # nums3 = {1*3, 2*3, 3*3, 4*3, 5*3, 6*3, 8*3...}
            # nums5 = {1*5, 2*5, 3*5, 4*5, 5*5, 6*5, 8*5...}
            # 注意 7 不是丑数.
            # 2, 3, 5 这前 3 个丑数一定要乘以其它的丑数， 所得的结果才是新的丑数， 所以上例中没有出现 7*2, 7*3, 7*5
            # 最终的丑数序列实际上就是这 3 个有序序列对的合并结果
            res = [1]*n
            a = b = c = 0
            for i in range(1, n):
                nums2 = res[a]*2
                nums3 = res[b]*3
                nums5 = res[c]*5
                # 三个数计算出来，挑出最小的那个，相当于边计算边合并，太巧妙了~
                res[i] = min(nums2, nums3, nums5)
                if res[i] == nums2:
                    a += 1
                if res[i] == nums3:
                    b += 1
                if res[i] == nums5:
                    c += 1
            return res[-1]

    if __name__ == '__main__':
        obj = Solution()
        print(obj.nthUglyNumber(10))
        
#### 运行结果
    12
