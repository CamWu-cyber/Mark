# q16_哪三个数最接近target
给定一个包括 n 个整数的数组 nums 和 一个目标值 target。找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。假定每组输入只存在唯一答案。
##### 示例
    输入：nums = [-1,2,1,-4], target = 1
    输出：2
    解释：与 target 最接近的和是 2 (-1 + 2 + 1 = 2) 。
# 思路
第一步：准备三个指针，i，left和right，其中left = i+1, right = len(nums)-1，left和right从两端向中间移动。

第二步：若三数之和==target，则返回target；若三数之和>target，则right--，同时记录下三树之和跟target的差值，每次取更小的那个，并记录下对应的三数之和，否则直接right--；若三数之和<target，则left++，同时记录下三数之和跟target的差值，每次取更小的那个，并记录下对应的三数之和，否则直接left++。
# 解题
    class Solution:
        def threeSumClosest(self, nums: List[int], target: int) -> int:
            if nums is None or len(nums)<3:
                return None

            com = res = float("inf")
            nums = sorted(nums)
            for i in range(len(nums)):
                left = i+1
                right = len(nums)-1
                while left<right:
                    total = nums[i]+nums[left]+nums[right]
                    if total-target == 0:
                        return target
                    elif total-target > 0:
                        if com > total-target:
                            com = total-target
                            res = total
                        right -= 1
                    else:
                        if com > target-total:
                            com = target-total
                            res = total
                        left += 1
            return res
# 关键词
i, left, right 三个指针
