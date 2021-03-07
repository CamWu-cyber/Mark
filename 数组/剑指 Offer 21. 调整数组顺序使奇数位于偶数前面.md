# 剑指 Offer 21. 调整数组顺序使奇数位于偶数前面
输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。


#### 示例：

    输入：nums = [1,2,3,4]
    输出：[1,3,2,4] 
    注：[3,1,2,4] 也是正确的答案之一。

思路：i，j从第一个元素开始，i不动，j往后遍历。当j为奇数时，就把i，j交换，同时i++

    class Solution:
        def exchange(self, nums):
            if not nums:
                return []
            i = j = 0
            while j < len(nums):
                if nums[j]%2 != 0:
                    nums[i], nums[j] = nums[j], nums[i]
                    i += 1
                j += 1
            return nums

    if __name__ == '__main__':
        obj = Solution()
        print(obj.exchange([1,2,3,4]))
        
 #### 运行结果
    [1, 3, 2, 4]
