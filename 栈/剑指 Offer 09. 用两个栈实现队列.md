# 剑指 Offer 09. 用两个栈实现队列
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )


#### 示例 1：

    输入：
    ["CQueue","appendTail","deleteHead","deleteHead"]
    [[],[3],[],[]]
    输出：[null,null,3,-1]
#### 示例 2：

    输入：
    ["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
    [[],[],[5],[2],[],[]]
    输出：[null,-1,null,null,5,2]

思路：添加元素时，直往A中添加元素；弹出元素时，

1. 如果B还有元素的话，直接返回B的栈顶元素；
2. 如果A为空，说明队列里没有元素了，返回-1；
3. 如果A不为空，把A的元素都装入B中，再弹出B的栈顶元素。

    class CQueue:

        def __init__(self):
            self.A = []
            self.B = []


        def appendTail(self, value: int) -> None:
            # 直往A中添加元素
            self.A.append(value)


        def deleteHead(self) -> int:
            # 如果B还有元素的话，直接返回B的栈顶元素
            if self.B:
                return self.B.pop()
            # 如果A为空，说明队列里没有元素了，返回-1
            if not self.A:
                return -1
            # 弹出时，如果A不为空，把A的元素都装入B中，再弹出B的栈顶元素
            while self.A:
                self.B.append(self.A.pop())
            return self.B.pop()


        if __name__ == '__main__':
            obj = CQueue()
            obj.appendTail(3)    # 压入3
            ans_1 = obj.deleteHead()  # 弹出3
            ans_2 = obj.deleteHead()  # 为空，弹出-1
            print(ans_1)
            print(ans_2)
        
#### 运行结果
    3
    -1
