# 剑指 Offer 51. 数组中的逆序对
在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

#### 示例1
    输入: [7,5,6,4]
    输出: 5
    
思路：暴力法会超时。采用改进的归并排序，在两数组比较的过程中，如果left[i] > right[j]则出现了逆序对，需要计算一次cnt = mid-i+1，表示i以及i后面的数跟right中的那个数都能组成逆序对。

通常的归并排序不需要start, end, mid等参数，最后的结果是放到新的数组中的，但是此题最后返回的是逆序对数而不是排序的数组，所以每次排序后，都要把排好的数组放到nums中，如此一来就需要引入start, end, mid等参数，导致整个归并排序的写法有较大的变化，这也是此题比较困难的原因吧。

    class Solution:
        def reversePairs(self, nums):
            cnt = 0

            def merge(nums, start, mid, end, temp):
                nonlocal cnt
                i, j = start, mid + 1
                while i <= mid and j <= end:
                    if nums[i] <= nums[j]:
                        temp.append(nums[i])
                        i += 1
                    else:
                        cnt += mid - i + 1
                        temp.append(nums[j])
                        j += 1
                while i <= mid:
                    temp.append(nums[i])
                    i += 1
                while j <= end:
                    temp.append(nums[j])
                    j += 1

                # 把排好的结果赋值给原数组nums上面，这样就不需要返回temp了，要不然根本写不出来
                # 为了赋值需要引入start，所以整个归并排序的写法加了很多参数start, end, mid，跟原始的归并排序写法不一样
                # 所以才是难题，原理很简单但是写出来很难
                for i in range(len(temp)):
                    nums[start + i] = temp[i]
                temp.clear()

            def mergeSort(nums, start, end, temp):
                if start >= end:
                    return None
                mid = (start + end) // 2
                mergeSort(nums, start, mid, temp)
                mergeSort(nums, mid + 1, end, temp)
                merge(nums, start, mid, end, temp)

            start = 0
            end = len(nums)-1
            temp = []
            mergeSort(nums, start, end, temp)
            return cnt


    if __name__ == '__main__':
        obj = Solution()
        print(obj.reversePairs([7,5,6,4]))
        
#### 运行结果
    5
