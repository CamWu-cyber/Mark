# 剑指 Offer 05. 替换空格
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。


#### 示例 1：

    输入：s = "We are happy."
    输出："We%20are%20happy."

思路：遍历。

    class Solution:
        def replaceSpace(self, s):
            res = []
            for c in s:
                if c == ' ':
                    res.append("%20")
                else:
                    res.append(c)
            return "".join(res)

    if __name__ == '__main__':
        obj = Solution()
        print(obj.replaceSpace("We are happy."))

# 运行结果
    We%20are%20happy.
