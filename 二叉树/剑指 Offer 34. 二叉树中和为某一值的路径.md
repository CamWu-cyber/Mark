# 剑指 Offer 34. 二叉树中和为某一值的路径
输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。

#### 示例:
给定如下二叉树，以及目标和 sum = 22，

              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
返回:

    [
       [5,4,11,2],
       [5,8,4,5]
    ]

思路：此题同112.路径总和。唯一增加的要求是需要返回路径上的值，所以dfs和bfs的时候，还需要加入一个参数list来保存路径上的值。

**此题涉及到二叉树的回溯，可以总结框架，日后再详细讨论**

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
                root.left = self.createTree(list, root.left, i * 2 + 1)
                root.right = self.createTree(list, root.right, i * 2 + 2)
            return root

        def pathSum(self, root, sum):
            if not root:
                return []
            # 增加了一个[root.val]来记录节点的值
            queue = [(root, root.val, [root.val])]
            res = []
            while queue:
                node, total, tmp = queue.pop(0)
                if not node.left and not node.right and total == sum:
                    res.append(tmp)
                if node.left:
                    queue.append((node.left, total + node.left.val, tmp + [node.left.val]))
                if node.right:
                    queue.append((node.right, total + node.right.val, tmp + [node.right.val]))
            return res

        # 回溯
        def pathSum_1(self, root, sum):
            if not root:
                return []

            def backtrack(node, sum):
                # 递归出口：解决子问题
                if not node:
                    return None
                path.append(node.val)
                sum -= node.val
                # 如果节点为叶子节点，并且 sum == 0
                if not node.left and not node.right and sum == 0:
                    res.append(path[:])
                backtrack(node.left, sum)  # 递归处理左边
                backtrack(node.right, sum)  # 递归处理右边
                path.pop()  # 处理完一个节点后，恢复初始状态

            res = []
            path = []
            backtrack(root, sum)
            return res


    if __name__ == '__main__':
        obj = Solution()
        root = obj.createTree([5, 4, 8, 11, None, 13, 4, 7, 2, None, None, None, None, 5, 1], None, 0)
        print(obj.pathSum(root, 22))
        print(obj.pathSum_1(root, 22))
      
#### 运行结果
    [[5, 4, 11, 2], [5, 8, 4, 5]]
    [[5, 4, 11, 2], [5, 8, 4, 5]]
