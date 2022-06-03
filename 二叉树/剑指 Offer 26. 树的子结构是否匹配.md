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

                  TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
                           if (t1 == NULL) return t2; // 如果t1为空，合并之后就应该是t2
                           if (t2 == NULL) return t1; // 如果t2为空，合并之后就应该是t1
                           // 修改了t1的数值和结构
                           t1->val += t2->val;                             // 中
                           t1->left = mergeTrees(t1->left, t2->left);      // 左
                           t1->right = mergeTrees(t1->right, t2->right);   // 右
                           return t1;
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
                  int list_1[] = { 1,3,2,5 };
                  TreeNode* root_1 = obj.createTree(list_1, sizeof(list_1) / sizeof(list_1[0]), 0);
                  int list_2[] = { 2,1,3,'#',4,'#',7};
                  TreeNode* root_2 = obj.createTree(list_2, sizeof(list_2) / sizeof(list_2[0]), 0);
                  TreeNode* node = obj.mergeTrees(root_1, root_2);
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
         true
