# 剑指 Offer 30. 包含min函数的栈
定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

 

#### 示例:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.min();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.min();   --> 返回 -2.

思路：详见注释

    class MinStack:

        def __init__(self):
            """
            initialize your data structure here.
            """
            self.A = []
            self.B = []

        def push(self, x: int) -> None:
            # A直接压入，B只压入比栈顶小的元素
            self.A.append(x)
            if not self.B or self.B[-1] >= x:
                self.B.append(x)

        def pop(self) -> None:
            # A直接pop，如果Apop的值等于B栈顶的元素，B才pop
            ans = self.A.pop()
            if ans == self.B[-1]:
                self.B.pop()

        def top(self) -> int:
            return self.A[-1]


        def min(self) -> int:
            return self.B[-1]


    if __name__ == '__main__':
        obj = MinStack()
        # 压入-2，0，-3
        obj.push(-2)
        obj.push(0)
        obj.push(-3)
        # 打印此时的最小值
        print(obj.min())
        # 弹出元素
        obj.pop()
        # 打印栈顶元素
        print(obj.top())
        # 打印此时的最小值
        print(obj.min())
        
#### 运行结果
    -3
    0
    -2
