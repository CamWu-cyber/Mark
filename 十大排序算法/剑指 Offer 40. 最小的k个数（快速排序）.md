# 剑指 Offer 40. 最小的k个数
输入整数数组 arr ，找出其中最小的 k 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。


#### 示例 1：

    输入：arr = [3,2,1], k = 2
    输出：[1,2] 或者 [2,1]
#### 示例 2：

    输入：arr = [0,1,2,1], k = 1
    输出：[0]

思路：快排

    class Solution:
        def getLeastNumbers(self, arr, k):
            def quick(arr, left, right):
                if left >= right:
                    return None
                i = left
                j = right
                pivot = left
                while i < j:
                    while i < j and arr[j] > arr[pivot]:
                        j -= 1
                    while i < j and arr[i] <= arr[pivot]:
                        i += 1
                    arr[i], arr[j] = arr[j], arr[i]
                arr[pivot], arr[j] = arr[j], arr[pivot]
                quick(arr, left, j-1)
                quick(arr, j+1, right)
                return arr
            res = quick(arr, 0, len(arr)-1)
            return res[:k]

    if __name__ == '__main__':
        obj = Solution()
        print(obj.getLeastNumbers([3,2,1], 2))
        
 #### 运行结果
    [1, 2]
