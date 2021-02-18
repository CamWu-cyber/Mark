# 剑指 Offer 19. 正则表达式匹配
请实现一个函数用来匹配包含'. '和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但与"aa.a"和"ab*a"均不匹配。

#### 示例1
    输入:
    s = "aa"
    p = "a"
    输出: false
    解释: "a" 无法匹配 "aa" 整个字符串。
    
#### 示例2
    输入:
    s = "aa"
    p = "a*"
    输出: true
    解释: 因为 '*' 代表可以匹配零个或多个前面的那一个元素, 在这里前面的元素就是 'a'。因此，字符串 "aa" 可被视为 'a' 重复了一次。

思路：二维dp，行为s，列为p，开头是空字符串。此题的重点是分清楚哪些情况是匹配的，那么其他的情况就都是不匹配的了。 这一题真TM难，代码里面还有坑

![8](https://github.com/CamWu-cyber/leetcode/blob/master/%E5%8A%A8%E6%80%81%E8%A7%84%E5%88%92/8.JPG)

1. dp[i][j]表示s[:i]和p[:j]是否匹配的情况

2. 状态转移，见上图，前三种为True，最后一种为False

3. base case：矩阵第一行中dp[0][0] = True，因为空字符串肯定匹配空字符串，后面是否匹配与偶数位上的字符串有关系，如果偶数位上的字符串为#，则匹配（即让 p 的奇数位出现 0 次，保持 p 是空字符串）。因此，循环遍历字符串 p ，步长为 2（即只看偶数位）。

        #!/usr/bin/python
        class Solution:
            def isMatch(self, s, p):
                if not s or not p:
                    return False
                m = len(s)+1
                n = len(p)+1
                dp = [[False for _ in range(n)] for _ in range(m)]
                dp[0][0] = True
                # base case
                for j in range(2, n, 2):
                    dp[0][j] = dp[0][j-2] and p[j-1] == '*'
                # 状态转移
                for i in range(1, m):
                    for j in range(1, n):
                        if s[i-1] == p[j-1] or p[j-1] == '.':
                            dp[i][j] = dp[i-1][j-1]
                        elif p[j-1] == '*':
                            # 此处必须用这个if else写，不许交换条件，否则报错
                            if s[i-1] == p[j-2] or p[j-2] == '.':
                                dp[i][j] = dp[i][j-2] or dp[i-1][j]
                            else:
                                dp[i][j] = dp[i][j-2]
                        else:
                            dp[i][j] = False
                return dp[-1][-1]

        if __name__ == '__main__':
            obj = Solution()
            print(obj.isMatch('aa', 'a'))
            print(obj.isMatch('aa', 'a*'))

#### 运行结果
    False
    True
