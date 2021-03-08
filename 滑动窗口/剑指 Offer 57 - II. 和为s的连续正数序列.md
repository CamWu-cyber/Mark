# 剑指 Offer 57 - II. 和为s的连续正数序列
输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

#### 示例 1：

    输入：target = 9
    输出：[[2,3,4],[4,5]]
#### 示例 2：

    输入：target = 15
    输出：[[1,2,3,4,5],[4,5,6],[7,8]]


思路：滑动窗口，因为题目要求至少含有两个数，则i从1开始，j从2开始，窗口的和等于target时，保留窗口同时j++；窗口和大于target时，窗口减去i的值，然后i++（整个操作相当于窗口右移）；窗口和小于target时，j++然后窗口加上j的值。

    class Solution:
        def findContinuousSequence(self, target):
            # 滑动窗口
            # i = 1
            # j = 2
            # res = []

            # # 滑动窗口的右边界不能超过target的中值
            # # 比如16的中值是8，最多是8+8，一旦8+9了，就会超过16，永远不可能等于16了
            # while j <= target//2 + 1:
            #     total = sum(list(range(i, j+1)))
            #     if total < target:
            #         j += 1
            #     elif total > target:
            #         i += 1
            #     else:
            #         res.append(list(range(i, j+1)))
            #         # 继续扩大寻找下一个可能的窗口
            #         j += 1
            # return res

            i = 1
            j = 2
            res = []
            while i < j:
                total = sum(list(range(i, j+1)))
                if total == target:
                    res.append(list(range(i, j+1)))
                    j += 1
                elif total > target:
                    i += 1
                    total -= i
                elif total < target:
                    j += 1
                    total += j
            return res

    if __name__ == '__main__':
        obj = Solution()
        print(obj.findContinuousSequence(9))
        
 #### 运行结果
     [[2, 3, 4], [4, 5]]
