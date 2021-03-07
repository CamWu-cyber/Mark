# 剑指 Offer 45. 把数组排成最小的数
输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

#### 示例 1:

    输入: [10,2]
    输出: "102"
#### 示例 2:

    输入: [3,30,34,5,9]
    输出: "3033459"

思路：回溯法超时，但是简单的例子还是可以用的。

    class Solution:
    def minNumber(self, nums):
        #根据题目的要求,两个数字m和n能拼接成数字mn和nm,如果mn < nm那么现在他们的相对位置是正确的,如果mn > nm,那么就需要将n移到m的前面,根据这样的特性我们能将整个数组进行排列,得到最终的结果.
        if not nums:
            return None
        for i in range(len(nums)):
            nums[i] = str(nums[i])
        for i in range(len(nums)):
            for j in range(i+1, len(nums)):
                if (nums[i] + nums[j]) > (nums[j] + nums[i]):
                    nums[i], nums[j] = nums[j], nums[i]
        return ''.join(nums)

        # 回溯法超时
        # def backtrack(path, nums):
        #     if len(path) == n and path not in res:
        #         res.append(path[:])
        #         return None
        #     for i in range(len(nums)):
        #         path.append(nums[i])
        #         backtrack(path, nums[:i] + nums[i + 1:])
        #         path.pop()
        #
        # path = []
        # res = []
        # n = len(nums)
        # backtrack(path, nums)
        # ans = float('inf')
        # for item in res:
        #     tmp = ''
        #     for num in item:
        #         tmp += str(num)
        #     ans = min(ans, int(tmp))
        # return str(ans)

    if __name__ == '__main__':
        obj = Solution()
        print(obj.minNumber([10, 2]))
        print(obj.minNumber([3,30,34,5,9]))
        
#### 运行结果
    102
    3033459
