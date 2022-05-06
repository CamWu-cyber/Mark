# 剑指 Offer 11. 旋转数组的最小数字
把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。  

##### 示例1
    输入：[3,4,5,1,2]
    输出：1
    
##### 示例2
    输入：[2,2,2,0,1]
    输出：0
    
思路：二分法，每次跟右指针比较，想象[3,4,5,1,2]，因为5>2，所以最小值在右区间，令left=mid+1；想象[4,5,1,2,3]，因为1<3，所以最小值在左区间，但是可能最小值就在边界上，所以令right=mid。还有一种特殊情况是nums[mid]==nums[right]，想象[1,1,1,1,1]，令right-=1，缩小检测范围即可。所有情况下都是left先指向的最小值，所以返回nums[left]即可。

    class Solution:
        def minArray(self, numbers):
            if not numbers:
                return None
            left = 0
            right = len(numbers)-1
            while left <= right:
                mid = (left+right)//2
                # 全部都跟nums[right]作比较，因为此题本质上是在寻找 右排序数组 的首个元素，即旋转点。
                if numbers[mid] > numbers[right]:
                    left = mid+1
                elif numbers[mid] < numbers[right]:
                    right = mid
                else:
                    right -= 1
            return numbers[left]

    if __name__ == '__main__':
      obj = Solution()
      print(obj.minArray([3,4,5,1,2]))
  
 #### 运行结果
    1

### C++

    #include<iostream>
    #include<vector>
    using namespace std;


    class Solution {
    public:
        int minArray(vector<int>& nums) {
            if (nums.empty()) {
                return 0;
            }
            int left = 0;
            int right = nums.size() - 1;
            while (left <= right) {
                int mid = (left + right) / 2;
                if (nums[mid] < nums[right]) {
                    right = mid;
                }
                else if (nums[mid] > nums[right]) {
                    left = mid + 1;
                }
                else {
                    right -= 1;
                }
            }
            return nums[left];
        }
    };

    int main() {
        vector<int> nums = { 3,4,5,1,2 };
        Solution obj;
        cout << obj.minArray(nums) << endl;
        system("pause");
        return 0;
    }
    
    运行结果：1
