# 剑指 Offer 46. 把数字翻译成字符串
给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

#### 示例 1:

    输入: 12258
    输出: 5
    解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"

思路：没有必要把数字真的转换成它要求的字母，只要得出有多少种分割方法就行了。

1. dp[i]:到第i位元素为止，总共的分割方法

2. 状态转移：通过找规律可得dp[i] = dp[i-1] + dp[i-2] 或者 dp[i-1]

3. base case: dp[0]=1 ,dp[1]=2 or 1

    class Solution:
        def translateNum(self, num):
            s = str(num)
            if len(s) < 2:
                return 1
            dp = [0] * len(s)
            dp[0] = 1
            dp[1] = 2 if int(s[0] + s[1]) < 26 else 1
            for i in range(2, len(s)):
                dp[i] = dp[i - 1] + dp[i - 2] if int(s[i - 1] + s[i]) < 26 and s[i - 1] != '0' else dp[i - 1]
            return dp[-1]

    if __name__ == '__main__':
        obj = Solution()
        print(obj.translateNum(12258))
        
#### 运行结果
    5
