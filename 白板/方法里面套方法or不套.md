# 方法里面套方法or不套方法
在leetcode题解当中，时常会出现方法里面再写一个方法的情况，然而我们自己写代码时，如果有另一个方法的话，一般是重新起一个def的，而不会套用。两种写法都能达到目的，主要区别在于套用方法里面的那个方法不需要写self，且递归调用时也不需要写self; 而不套用的话需要写self, 且递归调用时需要写self。下面用一个例子来说明，两种代码都能运行成功。

##### 套用方法

    #!/usr/bin/python
    class TreeNode:
        def __init__(self, val):
            self.val = val
            self.left = None
            self.right = None


    class Solution:
        def inittree(self, list, root, i):
            if i < len(list):
                root = TreeNode(list[i])
                root.left = self.inittree(list, root.left, 2 * i + 1)
                root.right = self.inittree(list, root.right, 2 * i + 2)
            return root

        def isSymmetric(self, root):
            if not root:
                return True
            left = root.left
            right = root.right
            # 方法里面套方法，也可以把方法写在外面
            def isMirror(left, right):
                if not left and not right:
                    return True 
                if not left or not right:
                    return False
                if left.val != right.val:
                    return False
                return isMirror(left.left, right.right) and isMirror(left.right, right.left)
            return isMirror(root.left, root.right)

        def inorder(self, root):
            if not root:
                return []
            return self.inorder(root.left) + [root.val] + self.inorder(root.right)

    if __name__ == '__main__':
        a = [1, 2, 2, None, 3, None, 3]
        obj = Solution()
        root = obj.inittree(a, None, 0)
        print(obj.inorder(root))
        print(obj.isSymmetric(root))
