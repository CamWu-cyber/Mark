# q6_Z字形变换
将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 "LEETCODEISHIRING" 行数为 3 时，排列如下：
    L   C   I   R
    E T O E S I I G
    E   D   H   N
之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如："LCIRETOESIIGEDHN"。

请你实现这个将字符串进行指定行数变换的函数：
    string convert(string s, int numRows);
##### 示例1
    输入: s = "LEETCODEISHIRING", numRows = 3
    输出: "LCIRETOESIIGEDHN"
##### 示例2
    输入: s = "LEETCODEISHIRING", numRows = 4
    输出: "LDREOEIIECIHNTSG"
    解释:

    L     D     R
    E   O E   I I
    E C   I H   N
    T     S     G
# 思路
第一步：有几行res里面就建立几个空字符串，设立一个flag=-1, 每当到达第一行或者最后一行是flag = -flag, 控制向上移动还是向下移动。

第二步：遍历字符串，依次输入进res, 最后输出res就是按行输出的
