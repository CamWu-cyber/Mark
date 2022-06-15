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

### C++

* 首先扩充数组到每个空格替换成"%20"之后的大小。
* i指向新长度的末尾，j指向旧长度的末尾。
* 如果j没有碰到空格，就赋值到i处
* 如果j碰到了空格，i处就插入“%20”，i-=2


        #include<iostream>
        #include<string>
        using namespace std;

        class Solution {
        public:
            string replaceSpace(string s) {
                string result;
                for (auto c : s) {
                    if (c == ' ') {
                        result.push_back('%');
                        result.push_back('2');
                        result.push_back('0');
                    }
                    else {
                        result.push_back(c);
                    }
                }
                return result;
            }

            // 正规解法
            string replaceSpace_1(string s) {
                int count = 0; // 统计空格的个数
                int sOldSize = s.size();
                for (int i = 0; i < s.size(); i++) {
                    if (s[i] == ' ') {
                        count++;
                    }
                }
                // 扩充字符串s的大小，也就是每个空格替换成"%20"之后的大小
                s.resize(s.size() + count * 2);
                int sNewSize = s.size();
                // 从后先前将空格替换为"%20"
                for (int i = sNewSize - 1, j = sOldSize - 1; j < i; i--, j--) {
                    if (s[j] != ' ') {
                        s[i] = s[j];
                    }
                    else {
                        s[i] = '0';
                        s[i - 1] = '2';
                        s[i - 2] = '%';
                        i -= 2;
                    }
                }
                return s;
            }
        };

        int main() {
            Solution obj;
            string res = obj.replaceSpace_1("We are happy.");
            cout << res;
        }
#### 运行结果
    We%20are%20happy.
