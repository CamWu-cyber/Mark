# 剑指 Offer 39. 数组中出现次数超过一半的数字
数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

#### 示例 1:

    输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
    输出: 2

思路：构建counter()字典，再依次比较即可。

    import collections
    class Solution:
        def majorityElement(self, nums):
            counter = collections.Counter(nums)
            n = len(nums)
            res = float('inf')
            for k, v in counter.items():
                if v > n//2:
                    res = k
                    break
            return  res

    if __name__ == '__main__':
        obj = Solution()
        print(obj.majorityElement([1, 2, 3, 2, 2, 2, 5, 4, 2]))
    
#### 运行结果
    2
