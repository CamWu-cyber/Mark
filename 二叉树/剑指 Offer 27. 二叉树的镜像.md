# 剑指 Offer 27. 二叉树的镜像
请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

         4
       /   \
      2     7
     / \   / \
    1   3 6   9
镜像输出：

         4
       /   \
      7     2
     / \   / \
    9   6 3   1

思路：此题表面上同110.平衡二叉树，实际上简单的多。别想太复杂了。

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

      def mirrorTree(self, root):
        if not root:
          return None
        if not root.left and not root.right:
          return root
        # 节点的交换就是这么朴实无华，别想太复杂
        root.left, root.right = root.right, root.left
        self.mirrorTree(root.left)
        self.mirrorTree(root.right)
        return root

      def inOrder(self, root):
        if not root:
          return []
        return self.inOrder(root.left)+[root.val]+self.inOrder(root.right)

    if __name__ == '__main__':
      obj = Solution()
      root = obj.createTree([4,2,7,1,3,6,9], None, 0)
      root_1 = obj.mirrorTree(root)
      print(obj.inOrder(root_1))
      
#### 运行结果
    [9, 7, 6, 4, 3, 2, 1]

#### C++

         #include<iostream>
         #include<vector>
         #include<stack>
         using namespace std;

         struct TreeNode {
                  int val;
                  TreeNode* left;
                  TreeNode* right;
                  TreeNode(int x) :val(x), left(NULL), right(NULL) {};
         };

         class Solution {
         public:
                  TreeNode* createTree(int* list, int len, int i) {
                           if (list[i] == '#') {
                                    return NULL;
                           }
                           TreeNode* root = new TreeNode(list[i]);
                           int lnode = i * 2 + 1;
                           int rnode = i * 2 + 2;
                           root->left = lnode <= len - 1 ? createTree(list, len, lnode) : NULL;
                           root->right = rnode <= len - 1 ? createTree(list, len, rnode) : NULL;
                           return root;
                  }

                  TreeNode* mirrorTree(TreeNode* root) {
                           if (root == NULL)return NULL;
                           swap(root->left, root->right);
                           mirrorTree(root->left);
                           mirrorTree(root->right);
                           return root;
                  }

                  // 中序遍历
                  vector<int> midTraversal_1(TreeNode* root) {
                           if (root == NULL) {
                                    return {};
                           }
                           vector<int>res;
                           stack<TreeNode*>st;
                           TreeNode* cur = root;
                           while (cur != NULL || !st.empty()) {
                                    if (cur != NULL) {
                                             st.push(cur);   // 压入栈，继续找左子树
                                             cur = cur->left;
                                    }
                                    else {
                                             cur = st.top();
                                             st.pop();
                                             res.push_back(cur->val);
                                             cur = cur->right;
                                    }
                           }
                           return res;
                  }
         };

         int main() {
                  Solution obj;
                  int list[] = { 4,2,7,1,3,6,9 };
                  TreeNode* root = obj.createTree(list, sizeof(list) / sizeof(list[0]), 0);
                  TreeNode* node = obj.mirrorTree(root);
                  vector<int> res = obj.midTraversal_1(node);
                  for (int i = 0; i < res.size(); i++) {
                           if (i == 0) {
                                    cout << "[" << res[i] << ",";
                           }
                           else if (i == res.size() - 1) {
                                    cout << res[i] << "]";
                           }
                           else {
                                    cout << res[i] << ",";
                           }
                  }
         }
         
 #### 运行结果
         [9,7,6,4,3,2,1]
