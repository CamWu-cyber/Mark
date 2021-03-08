# 剑指 Offer 53 - II. 0～n-1中缺失的数字
一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

#### 示例 1:

    输入: [0,1,3]
    输出: 2
#### 示例 2:

    输入: [0,1,2,3,4,5,6,7,9]
    输出: 8

思路：如果将缺失数字放回，则是连续n个数字求和，求和作差，缺失即为不存在的数字。

    class Solution:
        def missingNumber(self, nums):
            # 数学题
            # 如果将缺失数字放回，则是连续n个数字求和，求和作差，缺失即为不存在的数字
            n = len(nums)
            maxSum = (1+n)*n//2 # 高斯求和
            curSum = sum(nums)
            return maxSum - curSum


    if __name__ == '__main__':
        obj = Solution()
        print(obj.missingNumber([0,1,3]))
        
#### 运行结果
    2
