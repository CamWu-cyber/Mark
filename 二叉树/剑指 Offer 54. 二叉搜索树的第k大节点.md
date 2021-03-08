# 剑指 Offer 54. 二叉搜索树的第k大节点
给定一棵二叉搜索树，请找出其中第k大的节点。

 

#### 示例 1:

    输入: root = [3,1,4,null,2], k = 1
       3
      / \
     1   4
      \
       2
    输出: 4
#### 示例 2:

    输入: root = [5,3,6,2,4,null,null,1], k = 3
           5
          / \
         3   6
        / \
       2   4
      /
     1
    输出: 4

思路：中序遍历一定是升序的，返回第k大的节点即可

    class TreeNode:
        def __init__(self, val):
            self.val = val
            self.left = None
            self.right = None

    class Solution:
        def createTree(self, list, root, i):
            if i < len(list):
                root = TreeNode(list[i])
                if root.val == None:
                    return None
                root.left = self.createTree(list, root.left, i*2+1)
                root.right = self.createTree(list, root.right, i*2+2)
            return root

        # 中序遍历一定是升序的，返回第k大的节点即可
        def kthLargest(self, root, k):
            if not root or not k:
                return None
            def helper(node):
                if not node:
                    return None
                helper(node.right)
                res.append(node.val)
                helper(node.left)
            res = []
            helper(root)
            return res[k-1]

    if __name__ == '__main__':
        obj = Solution()
        root = obj.createTree([3,1,4,None,2], None, 0)
        print(obj.kthLargest(root, 1))
        
#### 运行结果
    4
