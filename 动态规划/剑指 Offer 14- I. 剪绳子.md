# 剑指 Offer 14- I. 剪绳子
给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

#### 示例1
    输入: 2
    输出: 1
    解释: 2 = 1 + 1, 1 × 1 = 1
   
#### 示例2
    输入: 10
    输出: 36
    解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36
    
思路：切割点为j，j遍历1到i

1. 状态定义：dp[i]表示长度为i的绳子的最大乘积值(也就表示了肯定至少切割过一次)

2. 转移方程 dp[i] = max(j段绳子最大值*剩下i-j段绳子最大值)，其中j段绳子最大值可以分为切还是不切：max(j,dp[j])，同理有剩下i-j段绳子最大值：max(i-j,dp[i-j])

3. base case：dp[1] = 1 只有一米绳子的时候，最大乘积为1.

        #!/usr/bin/python
        class Solution:
            def cuttingRope(self, n: int) -> int:
                # 状态定义：dp[i]表示长度为i的绳子的最大乘积值(也就表示了肯定至少切割过一次)
                # 切割点为j，j遍历1到i
                # 则有转移方程 dp[i] = max(j段绳子最大值*剩下i-j段绳子最大值)
                # 其中j段绳子最大值可以分为切还是不切：max(j,dp[j])
                # 同理有剩下i-j段绳子最大值：max(i-j,dp[i-j])
                dp = [0]*(n+1)
                dp[1] = 1
                for i in range(n+1):
                    for j in range(1, i+1):
                        # dp[i]表示保留初始值，即0
                        dp[i] = max(dp[i], max(j, dp[j])*max(i-j, dp[i-j]))
                return dp[-1]

        if __name__ == '__main__':
          obj = Solution()
          print(obj.cuttingRope(10))
      
#### 运行结果
    36
