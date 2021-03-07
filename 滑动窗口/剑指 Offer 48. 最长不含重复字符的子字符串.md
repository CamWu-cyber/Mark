# 剑指 Offer 48. 最长不含重复字符的子字符串
请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。


#### 示例 1:

    输入: "abcabcbb"
    输出: 3 
    解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
#### 示例 2:

    输入: "bbbbb"
    输出: 1
    解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
#### 示例 3:

    输入: "pwwkew"
    输出: 3
    解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
         请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。

思路：非常典形的滑动窗口。初始值只包含第一个元素

    class Solution:
        def lengthOfLongestSubstring(self, s):
            if not s:
                return 0
            if len(s) == 1:
                return 1
            # 初始值
            arr = [s[0]]
            cur_len = 1
            max_len = 0
            for j in range(len(s)):
                # 如果j在窗口中出现的话，窗口就先减小再增加
                if s[j] in arr:
                    index = arr.index(s[j])
                    arr = arr[index+1:]
                    arr.append(s[j])
                    cur_len = len(arr)
                # 窗口直接增加
                else:
                    arr.append(s[j])
                    cur_len = len(arr)
                max_len = max(max_len, cur_len)
            return max_len

    if __name__ == '__main__':
        obj = Solution()
        print(obj.lengthOfLongestSubstring("abcabcbb"))
        
#### 运行结果
    3
