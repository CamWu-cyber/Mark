# 剑指 Offer 18. 删除链表的节点
给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

注意：此题对比原题有改动

#### 示例 1:

    输入: head = [4,5,1,9], val = 5
    输出: [4,1,9]
    解释: 给定你链表中值为 5 的第二个节点，那么在调用了你的函数之后，该链表应变为 4 -> 1 -> 9.
#### 示例 2:

    输入: head = [4,5,1,9], val = 1
    输出: [4,5,9]
    解释: 给定你链表中值为 1 的第三个节点，那么在调用了你的函数之后，该链表应变为 4 -> 5 -> 9.

# 首先在头节点之前构建一个空节点，pre在前，cur在后，当碰到val时，令pre下一次指向空，cur的next。

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

        def deleteNode(self, head, val):
            # 首先在头节点之前构建一个空节点
            tmp = LinkNode(None)
            tmp.next = head
            # pre在前，cur在后
            h = cur = tmp
            pre = head
            while pre:
                # 当碰到val时，令pre下一次指向空，cur的next
                if pre.val == val:
                    cur.next = pre.next
                    pre.next = None
                pre = pre.next
                cur = cur.next
            return h.next

        def showLink(self, head):
            res = []
            while head:
                res.append(head.val)
                head = head.next
            return res

    if __name__ == '__main__':
        obj = Solution()
        head = obj.createLink([4,5,1,9])
        head_1 = obj.deleteNode(head, 5)
        print(obj.showLink(head_1))

####运行结果
    [4, 1, 9]
