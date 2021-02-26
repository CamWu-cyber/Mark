# 剑指 Offer 53 - I. 在排序数组中查找数字 I
统计一个数字在排序数组中出现的次数。

#### 示例1
    输入: nums = [5,7,7,8,8,10], target = 8
    输出: 2
    
#### 示例2
    输入: nums = [5,7,7,8,8,10], target = 6
    输出: 0
    
思路：因为是有序数组，可以用二分法，找到左右边界，左右边界之差就是出现次数了。

    #!/usr/bin/python
    class Solution:
      def search(self, nums, target):
        if target not in nums:
          return 0
        left = self.left_bound(nums, target)
        right = self.right_bound(nums, target)
        return right-left+1

      def left_bound(self, nums, target):
        left = 0
        right = len(nums)-1
        while left <= right:
          mid = (left+right) // 2
          if nums[mid] == target:
            right = mid - 1
          elif nums[mid] > target:
            right = mid - 1
          else:
            left = mid + 1
        if left >= len(nums) or nums[left] != target:
          return -1
        else:
          return left

      def right_bound(self, nums, target):
        left = 0
        right = len(nums)-1
        while left <= right:
          mid = (left+right) // 2
          if nums[mid] == target:
            left = mid + 1
          elif nums[mid] > target:
            right = mid - 1
          else:
            left = mid + 1
        if right < 0 or nums[right] != target:
          return -1
        else:
          return right

    if __name__ == '__main__':
      obj = Solution()
      print(obj.search([5,7,7,8,8,10], 8))
      
#### 运行结果
    2
