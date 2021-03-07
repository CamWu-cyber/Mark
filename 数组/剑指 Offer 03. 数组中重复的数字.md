# 剑指 Offer 03. 数组中重复的数字
找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

#### 示例 1：

    输入：
    [2, 3, 1, 0, 2, 5, 3]
    输出：2 或 3 

思路：数组排序之后，从第二个元素开始，依次遍历，每次与前面一个元素比较，如果相同，就代表是重复的元素。

    class Solution:
        def findRepeatNumber(self, nums):
            nums.sort()
            temp = -1
            for num in nums:
                if num == temp:
                    return num
                else:
                    temp = num

    if __name__ == '__main__':
        obj = Solution()
        print(obj.findRepeatNumber([2, 3, 1, 0, 2, 5, 3]))
        
#### 运行结果
    2
