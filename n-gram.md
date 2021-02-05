# N-gram的实现

#### N-Gram 算法具体过程：

1. 过滤掉文本数据中的标点符号和其他特殊字符；

2. 对所有单词执行小写转换，并删除单词之间的空格、换行符等标志位；

3. 使用长度为 N 的窗口对文本内容执行字符级滑动取词，将结果存入有序列表。

        class Solution:
          def textFilter(self, text):
            res = ''
            for c in text:
              if c.isalnum():
                if c.isalpha():
                  c = c.lower()
                  res += c
            return res

          def ngram(self, text, n):
            res = []
            tf = self.textFilter(text)
            for i in range(len(tf)):
              word = tf[i:i+n]
              if len(word)<n:
                break
              res.append(word)
            return res

        if __name__ == '__main__':
          obj = Solution()
          text = 'abcdefghigkLMN*^%$*   \r\n)021'
          print(obj.ngram(text, 5))

##### 运行结果
    ['abcde', 'bcdef', 'cdefg', 'defgh', 'efghi', 'fghig', 'ghigk', 'higkl', 'igklm', 'gklmn']
