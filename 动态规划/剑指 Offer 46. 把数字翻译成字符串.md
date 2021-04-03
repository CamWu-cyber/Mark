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


**增加一个递归到动态规划的方法**

        #!/usr/bin/python
        class Solution:
            def translateNum1(self, num):
                def process(num, index):
                    # 找到一个答案，返回1
                    if index == len(num):
                        return 1
                    # 碰到0，返回0
                    if num[index] == '0':
                        return 0
                    # 碰到1，要么1单独处理，要么1和后面一个数一起处理
                    if num[index] == '1':
                        res = process(num, index + 1)
                        if index + 1 < len(num):
                            res += process(num, index + 2)
                        return res
                    # 碰到2，要么2单独处理，要么2和后面一个数一起处理，但是后面一位得在0到6之间
                    if num[index] == '2':
                        res = process(num, index + 1)
                        if index + 1 < len(num) and '0' <= num[index + 1] <= '6':
                            res += process(num, index + 2)
                        return res
                    # 碰到3到9，只能单独处理，无法与后面的数结合
                    return process(num, index + 1)

                res = process(num, 0)
                return res
            
            # 根据递归，参数只有i一个，所以是一个一位的dp，i的范围是从0到len(num)+1
            # base case：dp[n] = 1，返回值是递归的入口，即dp[0]，所以遍历的过程就是从右往左遍历
            # 观察发现，dp[i]的值只与dp[i+1]和dp[i+2]有关
            # 递归中的res就是dp[i]，不需要管题意，挨个改就完了。
            def translateNum2(self, num):
                if len(num) < 2:
                    return 1
                n = len(num)
                dp = [0] * (n + 1)
                dp[n] = 1
                for i in range(n - 1, -1, -1):
                    if num[i] == '0':
                        dp[i] = 0
                    elif num[i] == '1':
                        dp[i] = dp[i + 1]
                        if i + 1 < n:
                            dp[i] += dp[i + 2]
                    elif num[i] == '2':
                        dp[i] = dp[i + 1]
                        if i + 1 < n and '0' <= num[i + 1] <= '6':
                            dp[i] += dp[i + 2]
                    else:
                        dp[i] = dp[i + 1]
                return dp[0]



        if __name__ == '__main__':
            obj = Solution()
            print(obj.translateNum1('12258'))
            print(obj.translateNum2('12258'))
            
#### 运行结果
    5
    5
