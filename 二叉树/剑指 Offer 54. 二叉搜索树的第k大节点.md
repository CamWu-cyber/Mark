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

### c++

    // 求二叉搜索树第 k大的节点” 可转化为求 “二叉搜索树的中序遍历倒序的第k 个节点”
    // 1、按照右->根->左的顺序（中序遍历倒序）遍历二叉树
    // 2、我们每次遍历一个节点的时候就让k--，当k减为0时，我们就找到了第k大的节点。

    #include<iostream>
    #include<stack>
    using namespace std;

    struct TreeNode {
        int val;
        TreeNode* left;
        TreeNode* right;
    };

    class Solution {
    public:
        TreeNode* createTree(int* list, int len, int i) {
            if (list[i] == 0) {
                return NULL;
            }
            TreeNode* root = new TreeNode;
            root->val = list[i];
            int lnode = i * 2 + 1;
            int rnode = i * 2 + 2;
            root->left = lnode <= len - 1 ? createTree(list, len, lnode) : NULL;
            root->right = rnode <= len - 1 ? createTree(list, len, rnode) : NULL;
            return root;
        }

        // 递归
        int kthLargest(TreeNode* root, int k) {
            if (root == NULL || k <= 0) {
                return 0;
            }
            int res;
            traversal(root, res, k);
            return res;
        }
        void traversal(TreeNode* root, int &res, int &k) {
            if (root == NULL) {
                return;
            }
            traversal(root->right, res, k);
            if (!--k) {
                res = root->val;
            }
            traversal(root->left, res, k);
        }

        // 迭代 中序遍历模板基础上，把左右子树交换一下顺序
        int kthLargest_1(TreeNode* root, int k) {
            if (root == NULL || k <= 0) {
                return 0;
            }
            stack<TreeNode*> st;
            TreeNode* cur = root;
            while (cur != NULL || !st.empty()) {
                if (cur != NULL) {
                    st.push(cur);    // 如果栈不为空，就往继续右子树找
                    cur = cur->right;
                }
                else {
                    cur = st.top();
                    st.pop();
                    if (!--k) {     // 找到了，直接return
                        return cur->val;
                    }
                    cur = cur->left;
                }
            }
        }
    };

    int main() {
        Solution obj;
        int list[] = { 5,3,6,2,4,NULL,NULL,1 };
        int k = 3;
        TreeNode* root = obj.createTree(list, sizeof(list) / sizeof(list[0]), 0);
        int res = obj.kthLargest(root, k);
        cout << res << endl;

        int res_1 = obj.kthLargest_1(root, k);
        cout << res_1 << endl;
    }
        
#### 运行结果
    4
    4
