# 剑指 Offer 38. 字符串的排列
输入一个字符串，打印出该字符串中字符的所有排列。


你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。


#### 示例:

    输入：s = "abc"
    输出：["abc","acb","bac","bca","cab","cba"]

**同47. 全排列 II，但有些许不同**

思路：1. 同47. 全排列 II，但是在条件判断的部分，改成啥啥啥''.join(s)就不行了。逻辑上没有问题，但是结果会不同。所以此题需要先按照list的方式处理，得到最终的list后，再把其转换为字符串形式。

2. 当然了，有官方答案。

        class Solution:
            def permutation(self, s):
                # if not s:
                #     return []
                # n = len(s)
                # def backtrack(path, s):
                #     if len(path) == n and path not in res:
                #         # 如果不用ans，aab时就是正确的，太奇怪了
                #         ans = ''.join(path)
                #         res.append(ans)
                #         return None
                #     for i in range(len(s)):
                #         path.append(s[i])
                #         backtrack(path, s[:i]+s[i+1:])
                #         path.pop()
                # path = []
                # res = []
                # backtrack(path, s)
                # return res

            s = sorted(list(s))

            res = []
            def dfs(s,road):
                if s == []:
                    res.append(''.join(road))
                for i in range(len(s)):
                    if i>0 and s[i] == s[i-1]:continue
                    dfs(s[:i]+s[i+1:], road+[s[i]])
            dfs(s,[])
            return(res)

    if __name__ == '__main__':
        obj = Solution()
        print(obj.permutation("abc"))
        
#### 运行结果
    ['abc', 'acb', 'bac', 'bca', 'cab', 'cba']
