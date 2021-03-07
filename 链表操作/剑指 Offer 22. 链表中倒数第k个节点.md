# 剑指 Offer 22. 链表中倒数第k个节点
输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

#### 示例：

    给定一个链表: 1->2->3->4->5, 和 k = 2.

    返回链表 4->5.

思路：首先得到链表的总长度，遍历到倒数第k个节点，返回即可。

    class LinkNode:
        def __init__(self, val):
            self.val = val
            self.next = None

    class Solution:
        def createLink(self, list):
            h = head = LinkNode(list[0])
            for i in range(1, len(list)):
                head.next = LinkNode(list[i])
                head = head.next
            return h

        def getKthFromEnd(self, head, k):
            total = 1
            h = head
            # 得到链表的总长度
            while head:
                head = head.next
                total += 1
            if k == total:
                return h
            head = h
            # 遍历到倒数第k个节点
            for i in range(1, total-k):
                head = head.next
            return head

        def showLink(self, head):
            res = []
            while head:
                res.append(head.val)
                head = head.next
            return res

    if __name__ == '__main__':
        obj = Solution()
        head = obj.createLink([1,2,3,4,5])
        head_1 = obj.getKthFromEnd(head, 2)
        print(obj.showLink(head_1))

#### 运行结果
    [4, 5]
