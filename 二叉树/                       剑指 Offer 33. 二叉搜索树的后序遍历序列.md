# 剑指 Offer 33. 二叉搜索树的后序遍历序列
输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 true，否则返回 false。假设输入的数组的任意两个数字都互不相同。

参考以下这颗二叉搜索树：

         5
        / \
       2   6
      / \
     1   3

#### 示例1
    输入: [1,6,3,2,5]
    输出: false
    
#### 示例2
    输入: [1,3,2,6,5]
    输出: true

思路：想象[1,3,2,6,5]这个数组。5是根节点，6是右子树，最前面的1，3，2是左子树。规律就很明显了，首先找到根节点（数组的最后一个元素），然后找到第一个大于根节点的元素6，6就是左右子树的分解点，之后按照此规律递归就行。判断的条件是从6开始，后面的节点应该都大于根节点5，如果不是就返回False。

因为需要不断递归左右子树的，所以是一个内嵌结构。

    #!/usr/bin/python
    class TreeNode:
      def __init__(self, val):
        self.val = val
        self.left = None
        self.right = None

    class Solution:
      def verifyPostorder(self, postorder):
        if not postorder:
          return False
        def helper(left, right):
          # 没有节点，或者只有一个节点
          if left >= right:
            return True
          i = left
          root = postorder[right] # 最后一个元素就是根节点
          # 第一个大于根节点的数就是左右子树的边界
          while postorder[i] < root:
            i += 1
          # 找到6了 左子树[i:mid] 右子树[mid:j+1]
          mid = i
          # 后面的数应该都大于根节点，否则的话就不是搜搜二叉树了
          while postorder[i] > root:
            i += 1
          # 看是否遍历到了最后一个节点
          if i == right:
            res = True
          else:
            res = False
          # 继续递归左右子树，注意边界条件
          return res and helper(left, mid-1) and helper(mid, right-1)
        left = 0
        right = len(postorder)-1
        return helper(left, right)

    if __name__ == '__main__':
      obj = Solution()
      print(obj.verifyPostorder([1,3,2,6,5]))
      print(obj.verifyPostorder([1,6,3,2,5]))

#### 运行结果
    True
    False
