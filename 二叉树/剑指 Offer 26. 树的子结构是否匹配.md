# 剑指 Offer 26. 树的子结构
输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:
         3
        / \
       4   5
      / \
     1   2
给定的树 B：
       4 
      /
     1
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

思路：这是一种新的题型，二叉树之间的匹配问题。总体思路是先找到根节点，再比较子节点，最后返回结果。

    #!/usr/bin/python
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

      def isSubStructure(self, A, B):
        # 根节点相同后再比较子结构
        res = False
        if not A or not B:
          return False
        # 值相同了，就进入helper函数中比较子节点
            # 值相同时，先不要返回结果，因为答案可能在后面，，此处先把结果保存在res中
        if A.val == B.val:
          res = self.helper(A, B)
        # 如果值不同，就在A的左子树和B，或者A的右子树和B中寻找答案
        return res or self.isSubStructure(A.left, B) or self.isSubStructure(A.right, B)

      def helper(self, a, b):
        # 此处必须先b后a
        # b都遍历完了，还没发现不一样的，说明那就一样了
        if not b:
          return True
        # 压根就没有a，当然不行
        if not a:
          return False
        if a.val != b.val:
          return False
        # 如果值相同，就继续比较a.left\b.left和a.right和b.right
        return self.helper(a.left, b.left) and self.helper(a.right, b.right)

    if __name__ == '__main__':
      obj = Solution()
      A = obj.createTree([3,4,5,1,2], None, 0)
      B = obj.createTree([4,1], None, 0)
      print(obj.isSubStructure(A, B))
      
#### 运行结果
    True
