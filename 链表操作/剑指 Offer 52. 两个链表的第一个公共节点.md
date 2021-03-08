# 剑指 Offer 52. 两个链表的第一个公共节点
输入两个链表，找出它们的第一个公共节点。

#### 示例1
![1](https://github.com/CamWu-cyber/leetcode/blob/master/%E9%93%BE%E8%A1%A8%E6%93%8D%E4%BD%9C/1.JPG)

    输入：intersectVal = 8, listA = [4,1,8,4,5], listB = [5,0,1,8,4,5], skipA = 2, skipB = 3
    输出：Reference of the node with value = 8
    输入解释：相交节点的值为 8 （注意，如果两个列表相交则不能为 0）。从各自的表头开始算起，链表 A 为 [4,1,8,4,5]，链表 B 为 [5,0,1,8,4,5]。在 A 中，相交节点前有 2 个节点；在 B 中，相交节点前有 3 个节点。

思路：1.两个指针 node1，node2 分别指向两个链表 headA，headB 的头结点，然后同时分别逐结点遍历，当 node1 到达链表 headA 的末尾时，重新定位到链表 headB 的头结点；当 node2 到达链表 headB 的末尾时，重新定位到链表 headA 的头结点。

2.没有交点的话，第二次他们会同时指向A和B的最后一个节点的next，而最后一个节点的next都是null，此时相等，返回null

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

        # 构造相交的两个链表
        def combineLink(self, headA, headB, tmp):
            A = headA
            B = headB
            while A.next:
                A = A.next
            while B.next:
                B = B.next
            A.next = B.next = tmp
            return headA, headB

        def getIntersectionNode(self, headA, headB):
            # 两个指针 node1，node2 分别指向两个链表 headA，headB 的头结点，然后同时分别逐结点遍历，当 node1 到达链表 headA 的末尾时，重新定位到链表 headB 的头结点；当 node2 到达链表 headB 的末尾时，重新定位到链表 headA 的头结点。
            # 没有交点的话，第二次他们会同时指向A和B的最后一个节点的next，而最后一个节点的next都是null，此时相等，返回null
            node1 = headA
            node2 = headB
            while node1 != node2:
                if node1:
                    node1 = node1.next
                else:
                    node1 = headB

                if node2:
                    node2 = node2.next
                else:
                    node2 = headA
            # 返回node1和node2都可以
            return node1.val if node1 else None


    if __name__ == '__main__':
        obj = Solution()
        headA = obj.createLink([4,1])
        headB = obj.createLink([5,0,1])
        tmp = obj.createLink([8,4,5])
        headA_1, headB_1 = obj.combineLink(headA, headB, tmp)
        print(obj.getIntersectionNode(headA, headB))
        
#### 运行结果
    8
